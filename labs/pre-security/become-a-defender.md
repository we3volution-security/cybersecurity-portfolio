# Become a Defender

**Platform:** TryHackMe
**Path / Module:** Pre Security — Attacks and Defenses
**Environment:** Defensive security tooling environment
**Completed:** ✅

> **Scope:** Guided introductory lab. It establishes the defensive perspective and vocabulary rather than operational SOC capability.

## Objective

Look at the same systems from the defensive side — how activity is detected, how alerts are investigated, and what defenders are actually working with.

## What I did

- Reviewed security alerts and worked out what each was reporting
- Investigated the activity behind an alert to determine whether it was malicious
- Followed a triage process from alert through to a decision
- Examined the controls that generate detection signal in the first place

## Concepts applied

| Concept | What it means in practice |
|---|---|
| Detection | Attacks leave traces; the question is whether anything is recording them |
| Alert triage | Most alerts are not incidents — the skill is deciding which are |
| Log analysis | Logs are the primary evidence source for reconstructing what happened |
| Security controls | Preventive, detective and corrective controls do different jobs |
| Defence in depth | Layered controls, because any single one will eventually fail |

The idea that reframed things: **defence is an evidence problem.** The defender doesn't see the attack — they see whatever the system happened to record, after the fact, mixed in with enormous volumes of normal activity.

That's what makes the offensive side directly relevant. Having just used `dirb` in [Become a Hacker](become-a-hacker.md), it was obvious that enumeration produces a distinctive pattern in web server logs — a burst of `404`s from one source. Doing the attack first made the detection logic self-evident.

## Security relevance

- Alert triage is the core daily activity of a SOC analyst, and a common entry route into the industry
- Log analysis underpins incident response and digital forensics
- Understanding what defenders can see is directly relevant to offensive work — it's the basis of operational security and of purple teaming
- Knowing which controls detect which behaviours is how you evaluate whether a security posture is actually coherent

## Takeaway

The useful outcome was seeing both sides of the same event. An attack technique and its detection signature are one thing described from two positions. I'd rather understand both than pick a side early — an attacker who doesn't know what generates alerts is loud, and a defender who doesn't know how attacks work is guessing at what matters.

## Next step

Hands-on log analysis with real data volume, and learning a SIEM properly — where the difference between "an alert fired" and "here's what actually happened" gets decided.

---

*Excludes flags, answers and credentials in line with TryHackMe's terms.*
