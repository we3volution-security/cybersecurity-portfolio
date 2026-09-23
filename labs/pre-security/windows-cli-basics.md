# Windows CLI Basics

**Platform:** TryHackMe
**Path / Module:** Pre Security — Operating Systems Basics
**Environment:** Windows command prompt
**Completed:** ✅

## Objective

Interact with Windows through the command line rather than the graphical interface, and understand where it differs from the Linux shell.

## What I did

- Opened and worked in the Windows command prompt
- Navigated the Windows filesystem from the CLI
- Listed directory contents and interpreted the output
- Compared the Windows command set against the Linux equivalents I'd just learned

## Commands and concepts

```batch
dir              :: list directory contents  (Linux equivalent: ls)
cd               :: change directory         (same verb, different path syntax)
cd ..            :: move up one level
```

The comparison was the most useful part of this lab. The *concepts* transfer directly — working directory, absolute vs relative paths, listing contents — while the syntax doesn't:

| Task | Linux | Windows |
|---|---|---|
| List contents | `ls` | `dir` |
| Change directory | `cd` | `cd` |
| Path separator | `/` | `\` |
| Root | `/` | `C:\` |

Recognising that the mental model is portable even when the commands aren't made the second operating system much faster to pick up than the first.

## Security relevance

- Remote access to Windows systems frequently lands you in a command shell rather than a desktop
- Command-line activity is a primary source of detection signal in defensive security — knowing what normal looks like is a prerequisite for spotting abnormal
- Scripted administration and automation on Windows are CLI-driven

## Takeaway

This was short but clarifying: the command line is a general interface pattern, not a Linux feature. The transferable skill is knowing what you want the system to tell you — the syntax is lookup.

## Next step

PowerShell, which is where real Windows command-line capability lives, and where most modern Windows administration and offensive tooling operates.

---

*Excludes flags, answers and credentials in line with TryHackMe's terms.*
