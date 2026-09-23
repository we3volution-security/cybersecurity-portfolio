# Operating System Security

**Platform:** TryHackMe
**Path / Module:** Pre Security — Operating Systems Basics
**Environment:** Linux machine accessed over SSH
**Completed:** ✅

## Objective

Connect to a remote Linux system securely, and understand how the operating system decides who a user is and what they are allowed to do.

## What I did

- Connected to a remote machine over SSH using supplied credentials
- Confirmed the account context I was operating in after connecting
- Examined how user accounts are recorded on the system
- Looked at file permissions and how they are changed
- Used elevated privileges to perform actions the standard user could not

## Commands and concepts

```bash
ssh user@10.10.x.x    # authenticated remote shell over an encrypted channel
whoami                # confirm which account the session is running as
ls -l                 # read the permission string on files
chmod                 # change file permissions
sudo <command>        # run a single command with elevated privileges
cat /etc/passwd       # user account records — readable by design
```

Three concepts did the work here:

**Authentication vs authorisation.** SSH proves *who* you are. Permissions and `sudo` decide *what that identity may do*. They're separate mechanisms and conflating them is where a lot of access-control mistakes come from.

**The permission model.** Read / write / execute, applied across owner / group / other. Once that clicked, `-rw-r--r--` became a sentence rather than a symbol, and `chmod` became a deliberate act rather than a fix to make something work.

**Least privilege in practice.** `sudo` per-command, rather than operating as root, is the principle made concrete. It was also the first time I understood *why* running as root routinely is a problem: everything you execute inherits that authority, including anything you executed by mistake.

`/etc/passwd` being world-readable while password hashes live separately in `/etc/shadow` was a useful illustration that "readable" and "sensitive" are decisions a system makes deliberately, not accidents.

## Security relevance

This is the access-control layer that most real-world compromises interact with:

- SSH is the standard remote-access route for Linux infrastructure — and a standard target for credential attacks
- Overly permissive file permissions are a routine privilege-escalation path
- `sudo` misconfiguration is one of the most common Linux privilege-escalation findings in real assessments

Understanding how these are *meant* to work is a prerequisite for recognising when they're wrong.

## Takeaway

Access control stopped being a policy idea and became a mechanism I could inspect. A user is an entry in a file; a permission is three bits repeated three times; elevation is a specific, logged action. Being able to look at each of those directly makes the abstract principle ("least privilege") something I can actually check on a system.

## Next step

SSH key-based authentication over passwords, and learning to read `sudo -l` output — the first thing to check for escalation paths on a system you've landed on.

---

*Excludes flags, answers and credentials in line with TryHackMe's terms.*
