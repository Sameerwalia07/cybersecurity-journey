# Cryptography Cheat Sheet — Hashing, Encryption, Encoding

Quick-comparison reference for three commonly confused concepts, plus
hash algorithm details.

## The Three Concepts — At a Glance

| | Reversible? | Purpose | Example |
|---|---|---|---|
| **Encoding** | Yes (no key needed) | Format conversion for storage/transmission | Base64, URL encoding |
| **Encryption** | Yes (with correct key) | Confidentiality | AES, RSA |
| **Hashing** | No (one-way) | Integrity / password storage | MD5, SHA-256 |

**Rule of thumb:** if you need to get the original data back, it's
encoding or encryption. If you only need to verify data hasn't changed
(or verify a password without storing it), it's hashing.

## Hash Algorithms Comparison

| Algorithm | Output Size | Status |
|---|---|---|
| MD5 | 128-bit | ❌ Broken — collisions found, not secure |
| SHA-1 | 160-bit | ❌ Deprecated by NIST (2011), banned for signatures (2013) |
| SHA-256 (SHA-2 family) | 256-bit | ✅ Current recommended standard |

## Encryption Types

**Symmetric** — same key encrypts and decrypts
- Fast, but key distribution is the challenge
- Example: AES

**Asymmetric** — public/private key pair
- Public key encrypts (or verifies), private key decrypts (or signs)
- Slower, but solves the key distribution problem
- Example: RSA
- Powers: HTTPS, SSH keys, digital signatures

## Key Terms

- **Avalanche effect** — a single bit change in input completely changes
  the hash output
- **Collision** — two different inputs producing the same hash output
  (rare with good algorithms, but mathematically inevitable — pigeonhole
  effect)
- **Rainbow table** — precomputed hash-to-plaintext lookup table, used to
  crack weak/unsalted hashes quickly
- **Salting** — adding random data to a password before hashing, so
  identical passwords produce different hashes (defeats rainbow tables)
- **HMAC** — combines a hash function with a secret key, verifying both
  integrity AND authenticity

## Insecure Password Storage Practices (avoid these)

1. Storing passwords in plaintext
2. Storing passwords with deprecated encryption
3. Storing passwords with a weak/unsalted hash (e.g. raw MD5)

**Correct approach:** salted hash using a slow, modern algorithm (e.g.
bcrypt, Argon2) — not covered in depth yet, but the direction to research
further.

## Quick Example

*Why hashing, not encryption, for passwords:* if a password database is
breached and passwords were properly hashed (salted, modern algorithm),
attackers can't recover the originals directly — they'd need to crack
each hash individually. If passwords were "encrypted" instead, and the
encryption key is also compromised, every password is instantly
recoverable.

---
*Ties directly to Hashing Basics writeup — this file is the fast-reference
version for whenever a term needs a quick refresh.*
