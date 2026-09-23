# Cryptography Concepts

**Platform:** TryHackMe
**Path / Module:** Pre Security — Attacks and Defenses
**Environment:** Interactive lab
**Completed:** ✅

## Objective

Understand what cryptography actually provides — and, as importantly, what it doesn't.

## What I did

- Worked through symmetric encryption and the key-distribution problem it creates
- Worked through asymmetric encryption and how a public/private key pair resolves that problem
- Examined hashing and how it differs from encryption
- Connected each mechanism to the security property it delivers

## Concepts applied

| Mechanism | Property provided |
|---|---|
| Symmetric encryption | Confidentiality — fast, but both parties need the same key |
| Asymmetric encryption | Confidentiality without pre-shared secrets; enables key exchange |
| Hashing | Integrity — one-way, fixed-length, not reversible |
| Digital signatures | Authenticity and non-repudiation |

The distinction that mattered most: **hashing is not encryption**. Encryption is reversible with the right key; hashing is deliberately one-way. Password storage uses hashing precisely *because* it can't be reversed — which is why a breach of hashed passwords is a different (though not harmless) problem to a breach of plaintext ones.

The second was understanding why both symmetric and asymmetric exist. Asymmetric solves key distribution but is slow; symmetric is fast but requires a shared key. Real systems use asymmetric to exchange a symmetric key, then switch. That's TLS in one sentence.

## Security relevance

- Maps directly onto the CIA triad — confidentiality via encryption, integrity via hashing
- HTTPS, SSH and VPNs all depend on the hybrid model above
- Password hashing, salting and cracking all follow from the one-way property
- Cryptographic *misuse* — weak algorithms, reused keys, unsalted hashes — is a common real-world finding

This is also directly applicable to the wallet and key-security material I teach at [we3volution](../../projects/we3volution.md). Public/private key pairs are the mechanism behind self-custody, and explaining "never share your private key" is far more convincing once you can explain *what the key mathematically is*.

## Takeaway

Cryptography moved from a black box to a set of tools with specific jobs. The useful question is no longer "is it encrypted?" but "which property does this provide — confidentiality, integrity, or authenticity?" Most cryptographic failures come from answering that question wrong.

## Next step

Practical hash identification and cracking, and looking at how TLS negotiates a session in detail.

---

*Excludes flags, answers and credentials in line with TryHackMe's terms.*
