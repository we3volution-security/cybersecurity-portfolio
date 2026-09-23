# Security Review: My Own Production Code

A retrospective security review of the first production build of the we3volution platform — roughly 1,100 lines of JavaScript/Velo that I wrote, shipped and ran live before I had any security training.

**Code reviewed:** [web3-literacy-program-beta](https://github.com/we3volution-security/web3-literacy-program-beta)
**Status:** Decommissioned. The referral and tracking system described here has been removed from the [live platform](https://we3volution.com).
**Reviewer:** me, reviewing my own work with the benefit of subsequent training.

---

## Why this exists

I built this system with no development background. It handled member signups, referral attribution, subscription status checks, a points and rewards tier system, and automated data retention. It worked. It ran in production.

Going back through it after starting formal security training, I can see problems I had no framework for recognising at the time. Writing those up properly — with severity, impact and remediation, the way a real finding would be documented — is more useful than pretending the code was fine, and it's a better demonstration of what I've learned than any lab completion.

The code is preserved unchanged. I'd rather show the work and the correction than quietly delete it.

---

## Findings

### 1. Client-side database writes with authorisation suppressed

**Severity:** High
**Location:** `frontend/growYourVisionPage.js`, `frontend/piCodeLookup.js`, `frontend/rankAndRewardPage.js`

Frontend scripts wrote directly to the database using `suppressAuth: true`, which bypasses the platform's permission checks:

```javascript
await wixData.update("MemberData", {
    _id: user._id,
    subscriptionStatus: user.subscriptionStatus || 'Inactive',
    totalReferrals: user.totalReferrals || 0,
    // ...
}, { suppressAuth: true });
```

There are more than a dozen occurrences of this pattern across the frontend files.

**Impact.** Frontend code executes in the user's browser, where the user controls it entirely. Anything the page can do, a user with the developer console open can do deliberately — and with authorisation suppressed, the database had no independent check. In practice this meant a user could have modified their own `subscriptionStatus` to `Active`, inflated `totalReferrals` and `monthlyPlansSold`, or altered another member's record by supplying a different `_id`. The subscription gate elsewhere in the system was enforceable only as long as nobody looked at the client code.

**The underlying mistake.** I treated the browser as part of my system. It isn't — it's the boundary of it. I reached for `suppressAuth: true` because permission errors were blocking me during development, which made it a fix that resolved a symptom and created a vulnerability.

**Remediation.** Every write moves to a backend module (`.web.js`), where it runs server-side and out of the user's reach. The backend re-derives the acting user from the session rather than trusting an identifier sent by the client, and validates that the requested change is one that user is permitted to make. The frontend calls the backend function; it never touches the database.

---

### 2. Internal error detail returned to the client

**Severity:** Low–Medium
**Location:** `backend/referrerData.web.js`

Error responses returned specific internal state to the browser:

```javascript
if (userData.items.length === 0) {
    return { error: 'No MemberData record found.' };
}
```

The same pattern appears in client-side logging elsewhere, where collection names, user IDs and email addresses were written to the browser console.

**Impact.** This is information disclosure. `No MemberData record found` names an internal collection and confirms the query structure — it tells anyone probing the application how the database is organised, which is exactly the reconnaissance an attacker wants before attempting injection or enumeration. Differentiated error messages also allow account enumeration: if "no record found" and "not subscribed" produce distinguishable responses, the error itself answers questions about who exists.

**The underlying mistake.** These messages were debugging aids. They were genuinely useful to me and I never considered that the audience for them wasn't only me.

**Remediation.** Generic messages to the client (`An error occurred, please try again`), with full technical detail written to server-side logs where the developer can reach it and the user cannot. Console logging of user identifiers and emails removed from frontend code entirely.

---

### 3. Insufficient input validation on referral URLs

**Severity:** Medium
**Location:** `frontend/referralLandingPage.js`, `frontend/learnMorePage.js`

URL validation used unanchored substring matching:

```javascript
if (!referralLink || !referralLink.includes('we3volution.com/referral/')) {
    // reject
}
```

**Impact.** `.includes()` asks only whether a string appears *somewhere* in the input. It does not check position, structure or domain ownership. A URL such as `https://malicious-site.example/we3volution.com/referral/abc` contains the required substring and passes the check — so a validator written specifically to stop users being redirected to fraudulent links would have approved one.

This matters more than usual given the platform's subject. A referral link is exactly the delivery mechanism a scammer would target, and the audience is people being taught to avoid precisely this.

**Remediation.** Parse the input with the `URL` API and compare the `hostname` property against an allowlist, rather than pattern-matching the raw string. Anchored regular expressions for the code format itself, validating structure and character set rather than presence.

---

## What held up

Reviewing honestly means noting what was already right:

- **`backend/referrerData.web.js`** authenticates properly. It calls `currentMember.getMember()` to establish identity server-side and scopes the query with `.eq("_owner", userId)` — the correct pattern, deriving the user from the session rather than trusting the client. It's the model the other files should have followed, which suggests I had the right instinct without having generalised it.
- **Server-side subscription verification.** `piCode.web.js` checks subscription status on the backend and halts on failure rather than returning data for the frontend to filter.
- **Automated data retention.** `jobs.js` and `jobs.config` ran a scheduled monthly job deleting tracking data older than six months. I wrote that for database performance, but it implements data minimisation and storage limitation — GDPR principles I hadn't read at the time.

---

## What I take from this

The most useful thing this review taught me is that **the vulnerabilities came from reasonable decisions made without the right model.** I wasn't careless. `suppressAuth: true` unblocked me, detailed errors helped me debug, and `.includes()` looked like validation. Each was a sensible local choice made without understanding the trust boundary it crossed.

That's a more valuable lesson than memorising a vulnerability class, and it's changed how I read other people's code: the question isn't "did they make a mistake" but "what did they not have a reason to think about?"

It also gave the training concrete anchors. The information-disclosure material in [HTTP in Detail](../labs/pre-security/http-in-detail.md) and the input-validation content in [Database SQL Basics](../labs/pre-security/database-sql-basics.md) landed differently because I had already made both mistakes in code that ran in production.

## Next step

A structured second pass against the OWASP Top 10 rather than the three issues that were most obvious to me, and reviewing the current platform's configuration with the same scrutiny.

---

*Reviewing my own decommissioned code. No live system is described and no vulnerability disclosed here affects the current platform.*
