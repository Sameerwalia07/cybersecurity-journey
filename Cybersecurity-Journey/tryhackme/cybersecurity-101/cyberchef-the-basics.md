# TryHackMe — CyberChef: The Basics

**Path:** Cyber Security 101
**Date completed:** [19/06/2026]
**Room link:** https://tryhackme.com/room/cyberchefbasics

---

## 🎯 What I Learned

- What CyberChef is and why it's described as a "Swiss Army knife for data"
- The four main areas of the CyberChef interface
- The recipe-based workflow (chaining operations together)
- A structured thought process for approaching an unknown/encoded string
- A practical worked example applying that process

## 🧠 In My Own Words

**CyberChef** is a simple, intuitive **web-based application** for
performing various "cyber" operations directly in the browser. It's often
described as a **Swiss Army knife for data** — a toolbox full of individual
tools, each designed for a specific task. These tasks range from simple
encodings like **XOR** or **Base64**, all the way to more complex
operations like **AES encryption** or **RSA decryption**.

CyberChef works using **recipes** — a series of operations chained together
and executed in order, transforming the input step by step until you reach
the output you're after.

### The Four Interface Areas

1. **Operations** — a searchable list of every available tool/function
   (e.g. `Base64 Decode`, `ROT13`, `From Hex`). This is where you browse or
   search for the specific transformation you want to apply.
   *Example: searching "base64" instantly filters to every Base64-related
   operation available.*

2. **Recipe** — where you drag operations from the Operations list to build
   your actual processing chain. Operations run **top to bottom**, so
   order matters — the output of one operation becomes the input of the
   next.
   *Example: a recipe of `From Base64` → `From Hex` first decodes Base64,
   then treats that result as hex and decodes it again — two layers of
   encoding undone in sequence.*

3. **Input** — where you paste or upload the raw data you're investigating
   (e.g. a suspicious string found during an investigation).
   *Example: pasting a gibberish string copied from a phishing email's
   source code.*

4. **Output** — shows the result after your recipe has been applied to the
   input. This updates live as you add/adjust operations.
   *Example: after applying `From Base64`, the Output pane instantly shows
   the decoded plaintext.*

### Thought Process for Using CyberChef

1. **Set a clear objective** — define specifically what you're trying to
   accomplish. This answers "What do I want to achieve?" and gives
   direction to the whole process.
   *Example objective: "During a security investigation, I found a
   gibberish string — I want to know if it contains a hidden message."*

2. **Put your data into the Input area** — paste or upload the actual data
   you're working with (e.g. the gibberish string from the example above).

3. **Select the Operations to try** — this step can be tricky without prior
   knowledge of what you're dealing with. If research suggests the data
   might involve encoding/encryption, you'd try relevant operations under
   the Encryption/Encoding category — things like `ROT13`, `Base64`,
   `Base85`, or `ROT47` — since there are many possible operations to test.

4. **Check the Output** — ask "Have I achieved my objective?" If the output
   makes sense (e.g. the gibberish successfully decoded into readable
   text), the objective is met. If not, repeat the process with a
   different operation or combination.

### Worked Example

**Objective:** Decode a suspicious string found during an investigation to
see if it hides a readable message.

**Input:** `SGVsbG8gV29ybGQh`

**Process:**
1. The string's character set (letters, numbers, `=` padding) looks like
   classic **Base64**
2. Added the `From Base64` operation to the Recipe
3. **Output:** `Hello World!`
4. Objective achieved — the string decoded cleanly into plaintext on the
   first attempt, confirming it was simple Base64 encoding with no
   additional layers

This is a simple case, but in a real investigation the same process would
apply to a more obfuscated string — potentially requiring multiple chained
operations (e.g. Base64 → XOR → Hex) before reaching readable output.

## 🛠️ Key Terms Introduced

- Recipe (chained operations)
- Operations, Input, Output panes
- Base64, ROT13, ROT47, Base85 (common encoding operations)
- XOR, AES, RSA (mentioned as more advanced operation examples)

## ❓ Questions I Had / Things to Revisit

- Want to practice with a multi-layered encoded string (e.g. Base64 wrapped
  in hex, or XOR'd data) to get comfortable chaining several operations
- Curious about CyberChef's **"Magic" operation** — I believe it can
  auto-detect likely encodings, which would speed up step 3 significantly
- Want to try this on a real malware string sample (from a safe, public
  source) to connect this directly to malware analysis work

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I understand
the interface, the recipe-based workflow, and can walk through the
four-step thought process with a working example.

---

*This feels like a genuinely practical everyday tool for SOC/analyst work —
decoding suspicious strings, obfuscated PowerShell commands, or phishing
payloads is a common real task, and CyberChef seems built exactly for that.
Want to keep a running list of "encoding fingerprints" (what different
encoded formats look like) as I get more practice recognising them on
sight.*
