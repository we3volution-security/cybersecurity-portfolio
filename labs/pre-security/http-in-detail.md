# HTTP in Detail

**Platform:** TryHackMe
**Path / Module:** Pre Security — How The Web Works
**Environment:** Browser / interactive web environment
**Completed:** ✅

## Objective

Understand what actually travels between a browser and a web server — the structure of requests and responses, rather than just the page that results from them.

## What I did

- Made HTTP requests and inspected the full request and response structure
- Worked through the different request methods and what each is for
- Read response headers and interpreted what the server was disclosing
- Triggered and interpreted different status code classes
- Followed how cookies are set and returned to maintain state across requests

## Concepts applied

**Methods** — `GET` retrieves, `POST` submits, and the rest (`PUT`, `DELETE`, `HEAD`) each carry an intent the server chooses whether to honour.

**Status codes**, as classes rather than individual numbers:

| Class | Meaning | Why it matters |
|---|---|---|
| `2xx` | Success | The request did what it asked |
| `3xx` | Redirection | Where the client gets sent next |
| `4xx` | Client error | `403` vs `404` leaks whether a resource *exists* |
| `5xx` | Server error | Often the most informative to an attacker — errors disclose internals |

**Headers** — the metadata that does most of the real work. `Host`, `User-Agent`, `Content-Type`, `Set-Cookie`, and the server/version headers that quietly tell you what software you're talking to.

**Statelessness and cookies** — HTTP doesn't remember you between requests, so state has to be reconstructed each time, usually with a cookie. That single fact explains most of how web authentication works, and where it breaks.

## Security relevance

Effectively all web attacks operate at this layer:

- Session hijacking is possible because session state rides in a cookie
- Verbose headers and error responses disclose server software and versions, which is reconnaissance
- The difference between `403` and `404` is information disclosure — it confirms a resource exists
- Manipulating requests directly, rather than through the browser UI, is the basis of web application testing

This also connected back to my own build work. The [security review of my beta platform](../../projects/security-review-beta-code.md) found that I'd been returning specific internal error messages to the client — the exact disclosure problem this lab describes, in code I'd written myself.

## Takeaway

The browser stopped being the thing I was using and became a client making structured requests I could read and reason about. Statelessness was the key idea: once you understand the server doesn't remember you, every authentication mechanism becomes an answer to "so how does it know?" — and every one of those answers is attackable.

## Next step

Intercepting and modifying requests with a proxy, so I'm manipulating traffic rather than just reading it.

---

*Excludes flags, answers and credentials in line with TryHackMe's terms.*
