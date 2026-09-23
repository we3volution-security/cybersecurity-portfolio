# Windows Basics

**Platform:** TryHackMe
**Path / Module:** Pre Security — Operating Systems Basics
**Environment:** Windows virtual machine
**Completed:** ✅

## Objective

Work directly with a Windows system: its filesystem layout, built-in administrative tooling, user accounts and security settings.

## What I did

- Explored the Windows filesystem and the purpose of the core directories
- Used built-in system tools to inspect running processes and system state
- Reviewed user accounts and the difference between standard and administrator accounts
- Examined the security settings exposed through the Windows interface
- Investigated how the system surfaces information about itself to an operator

## Concepts applied

| Concept | Why it mattered |
|---|---|
| Filesystem layout | `C:\Windows`, `Program Files` and user profile directories each hold predictable things — useful for both administration and investigation |
| User Account Control | The prompt is a privilege boundary, not an annoyance — it marks the point where a process requests elevation |
| Standard vs administrator accounts | The Windows expression of least privilege |
| Built-in tooling | Task Manager, Computer Management and the system information tools expose most of what you need without extra software |
| Security settings | Where the OS lets you see and change its own protections |

The useful realisation was that Windows exposes a lot about itself through tools that ship with it. You don't need third-party software to find out what's running, who's logged in, or what a machine is configured to do.

## Security relevance

Windows dominates corporate environments, which makes it the environment most security work actually happens in:

- IT support and systems administration are overwhelmingly Windows-facing
- Endpoint investigation during an incident starts with built-in tooling, because it's what's guaranteed to be present
- Understanding UAC and account separation is the basis for understanding Windows privilege escalation later

## Takeaway

I'd used Windows for years without understanding it. The difference after this lab was knowing *where to look* — that questions like "what is this machine running?" or "which accounts exist here?" have specific, findable answers in specific places.

UAC was the concept that shifted most. Reframing it from an interruption into a visible privilege boundary made the account model make sense.

## Next step

The Windows Registry, event logs, and doing the same investigation from the command line rather than the GUI.

---

*Excludes flags, answers and credentials in line with TryHackMe's terms.*
