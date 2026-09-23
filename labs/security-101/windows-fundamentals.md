# Windows Fundamentals

**Platform:** TryHackMe
**Path / Module:** Cyber Security 101 — Windows Fundamentals
**Environment:** Windows virtual machine
**Completed:** ✅

## Objective

Understand Windows as an operating system to be secured and investigated — its filesystem, permission model, built-in security features and administrative tooling.

## What I did

- Examined the NTFS filesystem and how permissions are applied to files and folders
- Worked through User Account Control and what the elevation prompt actually represents
- Reviewed user accounts, groups and the privileges attached to them
- Used built-in system tools to inspect processes, services and system configuration
- Examined the security features shipped with Windows and what each protects against
- Reviewed system and security event logging

## Concepts applied

| Area | What I took from it |
|---|---|
| **NTFS permissions** | More granular than Linux's owner/group/other — an access control list per object, with inheritance down the tree |
| **User Account Control** | A privilege boundary made visible. Even an administrator account runs with reduced privileges until elevation is requested |
| **Accounts and groups** | Group membership, not the account itself, is what usually carries privilege — which is why group membership is what attackers target |
| **Computer Management** | Central console for users, services, storage and event logs |
| **Windows Defender & firewall** | The built-in control set, and what each is actually watching |
| **Event logs** | The Windows evidence trail — structured, indexed, and the starting point for endpoint investigation |

The NTFS comparison was the most useful. Linux gives you three permission sets; NTFS gives you an access control list with inheritance. More expressive, and correspondingly easier to get wrong — inherited permissions mean a mistake high in a directory tree propagates a long way down.

UAC was the other. Reading it as a boundary rather than a prompt explains a whole category of Windows attacks: UAC bypasses exist because that boundary is exactly what an attacker needs to cross.

## Security relevance

Windows is where most enterprise security work happens:

- Corporate endpoints and servers are overwhelmingly Windows, making it the primary target environment
- Event logs are the main evidence source for endpoint incident response
- NTFS permission misconfiguration is a recognised privilege-escalation path
- UAC bypass is a well-documented technique class — understanding the control is a prerequisite to understanding the bypass
- Knowing the default security posture is what lets you recognise a weakened one

## Takeaway

Windows went from familiar-but-opaque to a system with an inspectable security model. The most valuable outcome was being able to compare it against Linux — two different answers to the same problems of identity, privilege and access. Seeing both makes the underlying principles clearer than either does alone.

## Next step

Windows privilege escalation techniques, PowerShell for administration and enumeration, and reading event logs with enough fluency to reconstruct a sequence of events.

---

*Excludes flags, answers and credentials in line with TryHackMe's terms.*
