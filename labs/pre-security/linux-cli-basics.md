# Linux CLI Basics

**Platform:** TryHackMe
**Path / Module:** Pre Security — Operating Systems Basics
**Environment:** Linux terminal (browser-based machine)
**Completed:** ✅

## Objective

Work a Linux system entirely from the command line — locate myself in the filesystem, move around it, read files and find information without a graphical interface.

## What I did

- Established where I was and who I was on the system before doing anything else
- Navigated the filesystem using both absolute and relative paths
- Listed directory contents including hidden files and permission data
- Read file contents directly from the terminal
- Searched the filesystem for files by name, and searched inside files for specific content
- Investigated `/etc` to see where system and service configuration lives

## Commands and concepts

```bash
pwd              # print working directory — confirm where I am before acting
whoami           # which user account I'm operating as
uname            # kernel name
uname -a         # full system info: kernel version, architecture, hostname

ls               # list directory contents
ls -l            # long format — permissions, owner, group, size, modified date
ls -al           # as above, plus hidden dotfiles

cd /etc          # absolute path
cd ..            # relative — move up one level
cat file.txt     # read a file straight to the terminal

find / -name "filename"   # locate a file by name across the filesystem
grep "string" file        # search for a pattern inside a file
```

The three that changed how I work were `ls -al`, `find` and `grep`. `ls -l` was the point the permission string (`-rw-r--r--`) stopped being noise and started being information — owner, group and other, read/write/execute. Hidden files only appearing under `-a` was a small thing with an obvious security implication: what isn't shown by default is still there.

`/etc` was the other one. Seeing that configuration for users, services and the system sits in readable text files in one predictable place reframed the OS as something inspectable rather than opaque.

## Security relevance

CLI comfort on Linux is a baseline requirement rather than a specialism. Most security tooling is terminal-driven, most servers have no desktop, and remote access gives you a shell and nothing else.

Specifically, this is the foundation for:

- **Enumeration** — `find` and `grep` are how you locate credentials, config files and misconfigurations on a system you've gained access to
- **Incident response and forensics** — reading logs and config without altering the system
- **Server administration** — the environment most production systems actually run in

## Takeaway

The shift was treating the terminal as the primary interface rather than a fallback. Once `pwd`, `ls -al` and `cd` became automatic, the filesystem stopped being abstract — I could form a question ("where is the config for this?") and answer it directly.

The bigger realisation was that `find` and `grep` are the same tool for an administrator and an attacker. The intent differs; the command doesn't.

## Next step

Piping and redirection (`|`, `>`, `>>`), and combining `find` with `grep` to search across many files at once — which is where this becomes genuinely useful for enumeration rather than navigation.

---

*Excludes flags, answers and credentials in line with TryHackMe's terms.*
