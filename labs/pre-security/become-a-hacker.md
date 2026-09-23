# Become a Hacker

**Platform:** TryHackMe
**Path / Module:** Pre Security — Attacks and Defenses
**Environment:** Deliberately vulnerable web target
**Completed:** ✅

> **Scope:** This is a guided introductory lab. It demonstrates that I've followed an attacker workflow against a live target and understand why each step exists — not that I can conduct an independent assessment. The honest boundary matters, so I've set it out explicitly under *Next step*.

## Objective

Apply the technical foundations from the rest of the pathway against a vulnerable target for the first time — approaching a system as something to be examined for weakness rather than used as intended.

## What I did

- Examined the target's exposed web functionality to establish what was actually there
- Used directory enumeration to discover content that wasn't linked from the visible site
- Reviewed what the discovered paths disclosed about the application's structure
- Identified a weakness in the target based on that information
- Tested the weakness and confirmed the result
- Followed the guided exploitation path through to completion

## Commands and concepts

```bash
dirb <target-url>     # brute-force discovery of directories and files
                      # against a wordlist — finds what isn't linked
```

`dirb` was the tool that made the concept land. A website presents you the pages it wants you to see; the web server will happily serve anything else that exists at a valid path. Enumeration is the gap between those two facts.

The workflow I followed:

```
Understand the target
      ↓
Enumerate what's actually exposed
      ↓
Identify a potential weakness
      ↓
Test it
      ↓
Validate the result
      ↓
Document
```

The step I'd underestimated was the first two. Most of the work is finding out what's there — exploitation is comparatively short, and it only becomes possible because enumeration made it visible.

## Security relevance

- Directory enumeration is a standard early step in real web application assessment
- It demonstrates why "unlinked" is not a security control — obscurity isn't access control
- Forgotten admin panels, backup files and old directories are genuinely common real-world findings
- The same methodology underpins professional penetration testing, just with more depth at every stage

## Takeaway

This was the point where the previous rooms connected. Operating systems, networking, HTTP and web architecture stopped being separate subjects and became a stack with an attack surface. Understanding HTTP was what made the enumeration results readable — I could tell what the responses meant rather than just seeing a list.

The mindset shift was concrete: moving from "what is this system for?" to "what does this system expose, and what did nobody intend to expose?"

## Next step

To make this real capability rather than an introduction, I need to work unguided: enumerate a target without being told what to look for, use a proper toolset (`gobuster`, `ffuf`, Burp Suite), and reach exploitation through my own reasoning rather than a walkthrough. That's what the Cyber Security 101 path and subsequent vulnerable-machine practice are for.

---

*Excludes flags, answers and credentials in line with TryHackMe's terms.*
