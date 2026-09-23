# we3volution

**Live:** [we3volution.com](https://we3volution.com)
**Status:** 🔵 Live, actively developed
**Role:** Sole designer, developer, researcher and writer

A free public platform teaching digital literacy, wallet security and scam recognition — with no products to sell, no referral scheme and no financial advice.

---

## What it is

Three free course tracks, a public safety hub and ongoing security writing:

| Section | Content |
|---|---|
| **[Academy](https://we3volution.com/academy)** | Commercial Web3 fundamentals; the UK Digital Pound; the Digital Euro. Wallets, transactions, key protection and safe test-network practice |
| **[Stay Safe](https://we3volution.com/stay-safe)** | A public threat hub — the shared pattern behind scams, a directory of currently active tactics (delivery texts, parking codes, "new number" messages, clone sites, wallet approvals), and a structured verification process |
| **[Insights](https://we3volution.com/blog)** | Security writing, including analysis of AI-assisted phishing, QR-code attacks and account-drainage techniques |
| **[Sovereign Roadmaps](https://we3volution.com/sovereign-roadmaps)** | Tracking CBDC development and its privacy design |

All practical exercises run on zero-value test networks. The platform holds no funds, issues nothing and gives no financial advice.

---

## The decision that defines it

The first version was a commercial product. It had a referral system, subscription gating, a points and rewards tier structure, and an income model built on users recruiting other users. I built the whole thing and ran it in production — around 1,100 lines of JavaScript, backend event handlers, database logic and automated maintenance jobs.

Then I removed it.

The problem was structural rather than technical: a referral-driven monetisation model sitting underneath educational content about avoiding referral-driven schemes. The mechanism I'd built to generate income was recognisably the mechanism the content was warning people about. Teaching scam recognition while running a recruitment incentive doesn't work, however careful the implementation.

So the tracking, referral and gamification layers came out, and what remains is a straightforward, free, jargon-free literacy resource. The original codebase is [preserved, not deleted](https://github.com/we3volution-security/web3-literacy-program-beta) — it's the record of what I built and what I learned, including [three security findings I've since documented against my own code](security-review-beta-code.md).

I'd rather show a decision I got right after getting the framing wrong than present a clean history.

---

## Why this is security work

The subject matter is security:

- **Social engineering.** The Stay Safe hub is built around the observation that losses usually begin with a message, call or listing that pressures someone to act before verifying — not with broken technology. Documenting that pattern means analysing attacker methodology.
- **Phishing and its evolution.** Tracking live tactics as they change, including AI-generated lures and QR-code delivery, and writing them up for a non-technical audience.
- **Key and wallet security.** Explaining self-custody accurately requires understanding public-key cryptography properly — the [Cryptography Concepts](../labs/pre-security/cryptography-concepts.md) lab fed directly into this.
- **Verification practice.** The "check first" process is threat-modelling translated into steps an ordinary person can follow under pressure.

The constraint that makes it useful to me: **I can't teach something I only half understand.** Writing for people without technical background means every explanation has to be correct at the mechanism level, not just at the analogy level. That exposes gaps in my own knowledge faster than any exercise, and I've repeatedly had to go and learn something properly because a draft explanation didn't hold up.

---

## Skills this demonstrates

| | |
|---|---|
| **Threat research** | Tracking live attack tactics and documenting them accurately |
| **Security communication** | Translating technical risk for non-technical audiences — a core requirement in most security roles |
| **Development** | Designed, built, debugged and operated a production system with database logic, event handlers and scheduled jobs |
| **Secure code review** | [Three documented findings](security-review-beta-code.md) against my own production code |
| **Independent delivery** | Specified, built, launched and maintained the whole thing solo |
| **Ethical judgement** | Removed a working revenue model because it conflicted with the platform's purpose |

---

## Direction

The longer-term aim is an interactive sandbox where people practise recognising malicious behaviour — wallet approvals, phishing flows, suspicious contract interactions — against simulated targets rather than learning from real losses. Safe failure is how security training works everywhere else; it should apply to public education too.

As the cybersecurity training progresses, the Stay Safe hub gets more technically grounded. The two sides feed each other: [labs](../labs/) build the understanding, the platform forces me to be able to explain it, and explaining it exposes what I don't actually know yet.
