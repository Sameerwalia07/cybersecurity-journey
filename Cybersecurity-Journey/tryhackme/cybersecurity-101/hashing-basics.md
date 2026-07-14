# TryHackMe — Hashing Basics

**Path:** Cyber Security 101
**Date completed:** [09/06/2026]
**Room link:** https://tryhackme.com/room/hashingbasics

---

## 🎯 What I Learned

- What a hash value is and how a hash function produces it
- The key properties that make hashing useful and secure
- What a hash collision is, and why the "pigeonhole effect" makes collisions
  mathematically unavoidable (but rare with good algorithms)
- Insecure password storage practices and how attacks like rainbow tables
  exploit weak hashing
- Real-world use cases: password storage, integrity checking, HMACs

## 🧠 In My Own Words

A **hash value** is a fixed-size string of characters produced by a **hash
function**. The hash function takes an input of **any/arbitrary size** and
always produces an output of a **fixed length** — essentially a summary or
"digest" of that data.

Key properties of a good hash function:
- **One-way:** it should be practically impossible to reverse the process —
  going from the output back to the original input shouldn't be feasible
- **Fixed output size:** no matter how large or small the input is, the
  output length stays the same
- **Avalanche effect:** even a single bit changed in the input completely
  changes the output — this is what makes hashing useful for detecting even
  the smallest tampering
- **Purpose:** hashing is used to ensure **data integrity** (confirming data
  hasn't been altered) and **password confidentiality** (storing passwords
  without keeping the actual plaintext)

**Hash collisions** happen when two different inputs produce the exact same
output. This connects to the **pigeonhole effect**: since hash outputs are a
fixed, limited size, but inputs can be infinitely many different sizes and
values, there are always more possible inputs than possible outputs. Given
enough inputs, some of them are mathematically guaranteed to produce the
same output eventually — like having more pigeons than pigeonholes, meaning
some pigeons *must* share a hole. A **good hash function** doesn't eliminate
collisions entirely, but makes the probability of one happening in practice
**negligible**.

**Insecure password storage practices** covered:
1. Storing passwords in **plaintext** — the worst practice, since anyone
   with database access sees the real password directly
2. Storing passwords using a **deprecated encryption** method — outdated
   algorithms that are no longer considered safe
3. Storing passwords using an **insecure hashing algorithm** — weak or old
   hash functions that are easier to crack or reverse

A **Rainbow Table** is a precomputed lookup table mapping hashes back to
their original plaintext values. If a system uses a weak/unsalted hash,
attackers can use a rainbow table to instantly look up what password
produced a given hash, without needing to actually crack anything.

The room also touched on how **Linux and Windows/MS Word** store passwords
differently, and covered practical password cracking using tools like
**Hashcat** and lookup services like **CrackStation** — tested in a VM
environment.

Finally, hashing is also used for **integrity checking** (verifying a file
or message hasn't been tampered with by comparing hashes) and **HMACs**
(Hash-based Message Authentication Codes), which combine a hash function
with a secret key to verify both integrity *and* authenticity of a message.

## 🛠️ Key Terms Introduced

- Hash value / hash function
- Avalanche effect
- Hash collision
- Pigeonhole effect
- Rainbow table
- Hashcat, CrackStation
- HMAC (Hash-based Message Authentication Code)

## ❓ Questions I Had / Things to Revisit

- Want to actually run Hashcat against a sample hash in a lab to see the
  cracking process hands-on rather than just knowing it exists
- Want to understand **salting** in more depth — I know it defends against
  rainbow tables, but want to see exactly how a salt gets combined with a
  password before hashing
- Curious about the specific difference between how Linux (`/etc/shadow`)
  and Windows store password hashes

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I understand
hash properties, collisions, the pigeonhole effect, and why weak
password-hashing practices are dangerous. Salting is the one area I'd want
to firm up before teaching it confidently.

---

*This connects directly back to Operating System Security from Pre Security
— weak passwords were flagged there as a major OS-level risk, and this room
showed me exactly why: weak hashing + no salting is what makes those weak
passwords crackable at scale in the first place.*
