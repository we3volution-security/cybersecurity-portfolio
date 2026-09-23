# Database SQL Basics

**Platform:** TryHackMe
**Path / Module:** Pre Security — Software Basics
**Environment:** SQL environment
**Completed:** ✅

## Objective

Understand how structured data is stored and queried, and write SQL against a real database rather than reading about it.

## What I did

- Explored how data is organised into tables, rows and columns
- Wrote queries to retrieve specific data rather than whole tables
- Filtered results against conditions
- Inserted and modified records
- Observed how a query is constructed and interpreted by the database

## Commands and concepts

```sql
SELECT * FROM users;                          -- retrieve everything
SELECT username FROM users;                   -- retrieve specific columns
SELECT * FROM users WHERE id = 1;             -- filter by condition
INSERT INTO users VALUES (...);               -- add a record
UPDATE users SET column = value WHERE ...;    -- modify existing records
```
<!-- CHECK: adjust the statements above to match what you actually ran in the room -->

The structural idea that mattered: a query is a *sentence* assembled from parts — what to retrieve, where from, under what condition. The database parses that sentence and acts on it.

That framing is what makes SQL injection comprehensible rather than magic. If user input is concatenated into the sentence instead of being treated as a value, the user gets to write part of the query.

## Security relevance

- Databases hold what attackers are usually after — credentials, personal data, payment records
- SQL injection remains one of the highest-impact web vulnerabilities, and it's a direct consequence of how queries are constructed
- `WHERE` clause logic is exactly what injection manipulates
- Understanding legitimate queries is a prerequisite for recognising malicious ones in logs

This connects directly to my own code. My [beta platform](../../projects/security-review-beta-code.md) used `.includes()` for input checking rather than strict validation — the review of that is where this lab's content stopped being theoretical.

## Takeaway

Seeing a query as an assembled instruction rather than a fixed command was the useful shift. It makes both sides legible: how applications legitimately retrieve data, and why unsanitised input is dangerous at precisely the point where value and instruction get mixed.

## Next step

`JOIN` operations across tables, and practising SQL injection in a deliberately vulnerable application to see the theory execute.

---

*Excludes flags, answers and credentials in line with TryHackMe's terms.*
