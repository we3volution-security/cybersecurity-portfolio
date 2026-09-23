# Active Directory Basics

**Platform:** TryHackMe
**Path / Module:** Cyber Security 101 — Active Directory Basics
**Environment:** Windows domain environment
**Completed:** ✅

## Objective

Understand how identity and access are managed centrally across an organisation, rather than per-machine — and why that centralisation is the defining feature of enterprise attack paths.

## What I did

- Examined the structure of an Active Directory domain and its objects
- Reviewed users, groups, computers and organisational units, and how they relate
- Looked at how Group Policy distributes configuration across the domain
- Examined the privileged groups and what membership of each confers
- Worked through how domain authentication differs from local authentication

## Concepts applied

| Object | Role |
|---|---|
| **Domain** | The boundary of a single administrative authority |
| **Domain Controller** | The server holding the directory and handling authentication — the highest-value target in the environment |
| **Organisational Unit (OU)** | Structural grouping used to apply policy to sets of objects |
| **Users and groups** | Identity, and the permissions attached to it via group membership |
| **Group Policy (GPO)** | Centrally enforced configuration, pushed to every machine in scope |
| **Privileged groups** | Domain Admins and equivalents — effectively total control of the environment |

The central idea: AD trades per-machine independence for centralised control. One credential works across the estate, policy is applied once, and administration scales.

The security consequence follows immediately. **Centralised identity means centralised compromise.** A single set of domain credentials is valid everywhere in scope, and compromising a domain controller is compromising the organisation. That's why privilege escalation and lateral movement in enterprise environments are almost always AD problems rather than individual-machine problems.

Group Policy was the other piece worth sitting with: configuration that applies automatically to every machine is powerful administratively and equally powerful as a distribution mechanism if an attacker can modify it.

## Security relevance

- Active Directory runs identity in the overwhelming majority of corporate environments
- Enterprise attack paths — lateral movement, privilege escalation, persistence — are largely AD attack paths
- Kerberoasting, pass-the-hash, golden tickets and similar techniques all target AD authentication specifically
- On the defensive side, AD is a primary monitoring surface: authentication events, group membership changes and GPO modifications are high-value signals
- AD knowledge is close to a hard requirement for penetration testing roles

## Takeaway

This was the first lab that made enterprise scale concrete. Everything before it concerned one machine. AD introduced the reality that organisations run thousands, tied together by a single identity system — and that the interesting attack surface is the relationships between machines, not the machines themselves.

It also reframed privilege. On a standalone system, escalation means reaching root or administrator. In a domain, it means reaching Domain Admin — and the route there typically runs through misconfigured group membership and delegation rather than through a software exploit.

## Next step

Practical AD enumeration — using BloodHound to map attack paths, and working through the common attack techniques in a lab domain rather than only understanding the structure.

---

*Excludes flags, answers and credentials in line with TryHackMe's terms.*
