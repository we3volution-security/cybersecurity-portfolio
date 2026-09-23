# Python: Simple Demo

**Platform:** TryHackMe
**Path / Module:** Pre Security — Software Basics
**Environment:** Python environment
**Completed:** ✅

## Objective

Write and run Python, and understand the control-flow building blocks that all scripting rests on.

## What I did

- Ran Python scripts from the command line with `python3`
- Worked with variables and data types
- Used conditional logic to branch on a condition
- Used loops to repeat operations over data
- Traced why a script behaved the way it did when it didn't do what I expected

## Commands and concepts

```bash
python3 script.py     # execute a script
python3               # interactive interpreter for testing single expressions
```

```python
variable = value      # storing and reusing data
if / else             # branching on a condition
for / while           # repetition over a range or collection
```

Coming to this with existing JavaScript experience from [building my own platform](../../projects/we3volution.md) made the transition mostly syntactic — the logic (conditions, iteration, state) was already familiar. What was new was Python's readability and how directly it maps to shell-style automation.

## Security relevance

Python is the default language of security tooling:

- Most offensive and defensive tools are written in or extensible with Python
- Automating repetitive tasks — parsing output, processing wordlists, handling data — is what separates efficient work from manual work
- Reading a tool's source to understand what it actually does requires being able to read Python
- Exploit proof-of-concepts are overwhelmingly published as Python scripts

## Takeaway

The value here wasn't learning to program — it was adding the language that security tooling is written in. Being able to read a script before running it is a security practice in itself.

## Next step

Scripting something genuinely useful rather than exercises: file parsing, or automating a repetitive step in a lab workflow.

---

*Excludes flags, answers and credentials in line with TryHackMe's terms.*
