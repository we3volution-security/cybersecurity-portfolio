# Linux Fundamentals (Parts 1–3)

**Platform:** TryHackMe
**Path / Module:** Cyber Security 101 — Linux Fundamentals
**Environment:** Browser-based Linux machine, then deployed VMs accessed over SSH
**Completed:** ✅

## Objective

Move from basic Linux navigation to operating a Linux system properly — remote access, permissions, processes, services, scheduled tasks and logs.

The three parts progress deliberately: an interactive machine in the browser, then a remote machine over SSH, then system administration on a deployed VM.

## What I did

**Part 1 — interacting with the system**
- Navigated the filesystem and inspected files and directories
- Searched for files by name and searched within file contents
- Created directory structures

**Part 2 — remote access and permissions**
- Connected to a remote Linux machine over SSH
- Read and interpreted permission strings, and changed them
- Worked with users, groups and ownership
- Used `sudo` for privileged operations and understood the elevation boundary

**Part 3 — running systems**
- Inspected running processes and the state of the system
- Managed services and examined what starts automatically
- Set up and examined scheduled tasks with cron
- Served files over HTTP with a one-line Python web server
- Checked disk usage and reviewed system and application logs

## Commands and concepts

```bash
# Navigation and investigation
pwd                            # where am I
ls -al                         # full listing including hidden files
cd                             # move around the filesystem
cat /etc/...                   # read configuration
mkdir                          # create directory structure
df                             # disk usage — how full is the filesystem

# Searching
find / -name "*.conf"          # locate files by name across the system
sudo find / -perm -4000        # find SUID binaries — a classic escalation check
grep "pattern" file            # search within file contents

# Remote access and permissions
ssh user@10.10.x.x             # authenticated encrypted remote shell
whoami                         # confirm current account context
chmod                          # change read/write/execute permissions
sudo <command>                 # elevate for a single command

# Processes, services and automation
systemctl status <service>     # inspect a service's state
systemctl start/stop/enable    # control services and boot behaviour
crontab -e                     # schedule recurring tasks
python3 -m http.server          # serve the current directory over HTTP
```

Three things stood out.

**`sudo find / -perm -4000`.** This was the first command I ran that was unambiguously a *security* command rather than an administrative one. SUID binaries run with the file owner's privileges rather than the caller's, so enumerating them is a standard privilege-escalation check. It was the moment `find` stopped being a utility and became a technique.

**`systemctl` and cron together.** Services and scheduled tasks are how a Linux system does things without a human present — which makes them exactly where persistence hides. A malicious cron job or a modified service unit survives reboots and looks unremarkable.

**`python3 -m http.server`.** One line turns any directory into a web server. Enormously useful for moving files between machines, and a clear illustration that "a server" is a process, not a category of computer.

Having built and debugged a live platform previously meant the *concept* of a service, a scheduled job and a log was already familiar from the [beta system I ran](../../projects/security-review-beta-code.md) — which used exactly this pattern, with a scheduled monthly job clearing tracking data older than six months. What was new was doing it at the operating-system level rather than inside a hosted platform.

## Security relevance

This is the working knowledge underneath most practical Linux security:

| Skill | Applied to |
|---|---|
| SUID enumeration | Privilege escalation — both finding and remediating |
| Permissions and ownership | The most common misconfiguration class on Linux |
| Process and service inspection | Identifying unexpected or malicious processes during IR |
| Cron and scheduled tasks | A primary persistence mechanism |
| Log review | The evidence base for incident response |
| SSH | The standard remote-access route, and a standard target |

## Takeaway

Part 1 was navigation; by Part 3 I was administering a system. The step that mattered was realising that an operating system is a set of running processes and scheduled work that you can inspect, control and — if you have the right permissions — subvert.

`sudo find / -perm -4000` was the hinge. Up to that point I'd been learning to use Linux. That command was the first time I was looking at a system for a way in, using the same tools an administrator uses. It made the overlap between administration and offensive security concrete rather than theoretical.

## Next step

Working through a full Linux privilege-escalation methodology on a vulnerable machine — enumerating systematically and finding the path unaided, rather than being pointed at the check.

---

*Excludes flags, answers and credentials in line with TryHackMe's terms.*
