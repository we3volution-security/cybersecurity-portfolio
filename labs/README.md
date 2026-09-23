# Hands-On Labs

Practical work, documented by what I actually ran and understood rather than by rooms completed.

Each writeup records the environment, the objective, the commands and tools used, and what I took away from it. Flags, answers, credentials and full walkthroughs are deliberately excluded.

---

## TryHackMe — Cyber Security 101 🔄 In progress

| Lab | Environment | Tools & commands | Writeup |
|---|---|---|---|
| Linux Fundamentals 1–3 | Linux VM, browser terminal, remote SSH | `ssh` `find` `sudo find` `chmod` `grep` `systemctl` `cron` `python3` `df` | [→](security-101/linux-fundamentals.md) |
| Windows Fundamentals | Windows VM | NTFS permissions, UAC, Computer Management, Defender | [→](security-101/windows-fundamentals.md) |
| Active Directory Basics | Windows domain environment | Domains, OUs, GPOs, users & groups | [→](security-101/active-directory-basics.md) |

## TryHackMe — Pre Security ✅ Completed · SEC0 certified

| Lab | Environment | Tools & commands | Writeup |
|---|---|---|---|
| Linux CLI Basics | Linux terminal | `pwd` `ls` `ls -l` `ls -al` `cd` `cat` `find` `grep` `whoami` `uname -a` | [→](pre-security/linux-cli-basics.md) |
| Operating System Security | Linux / SSH | `ssh` `sudo` `chmod` `whoami`, `/etc/passwd` | [→](pre-security/operating-system-security.md) |
| Windows Basics | Windows VM | System tools, user accounts, security settings | [→](pre-security/windows-basics.md) |
| Windows CLI Basics | Windows command prompt | `dir` `cd` | [→](pre-security/windows-cli-basics.md) |
| HTTP in Detail | Browser / web environment | Methods, headers, status codes, cookies | [→](pre-security/http-in-detail.md) |
| Database SQL Basics | SQL environment | `SELECT` `WHERE` `INSERT` `UPDATE` | [→](pre-security/database-sql-basics.md) |
| Python: Simple Demo | Python environment | `python3`, variables, conditionals, loops | [→](pre-security/python-simple-demo.md) |
| Cryptography Concepts | Interactive lab | Symmetric/asymmetric encryption, hashing | [→](pre-security/cryptography-concepts.md) |
| Become a Hacker | Vulnerable web target | `dirb`, directory enumeration | [→](pre-security/become-a-hacker.md) |
| Become a Defender | Security tooling environment | Log review, alert triage | [→](pre-security/become-a-defender.md) |

---

## Documentation standard

Every writeup follows the same structure — see [TEMPLATE.md](TEMPLATE.md):

**Environment → Objective → What I did → Commands & concepts → Security relevance → Takeaway → Next step**

## What this excludes

No flags, answers, passwords, private keys, tokens, personal information or complete room solutions. Commands and methodology are included because they demonstrate capability without reproducing the training material.
