# 10 — Cryptography & Password Cracking

Hands-on cryptanalysis exercise demonstrating WHY password storage matters,
WHY salt matters, and WHY low-entropy data should never be hashed without salt.

## What I did

### Junior tier — Caesar cipher
- Wrote a **Python brute-force script** against a Caesar-shifted ciphertext
  using the full Polish alphabet (35 characters including ą, ć, ę, ł, ń, ó, ś, ź, ż)
- Iterated through all 35 possible shift values, output candidate plaintexts
- Identified the correct shift visually (the only readable Polish output)

### Medium tier — MD5 cracking with hashcat
- Generated test hashes from a small password list
- Ran `hashcat -m 0 md5.txt /usr/share/wordlists/rockyou.txt` (MD5, dictionary attack)
- **Result: 3 out of 3 hashes cracked in 2 seconds**
- Recovered passwords:
  - `monkey1120` (animal + numbers — common pattern)
  - `lemonkingsle` (concatenated dictionary words)
  - `donttellany1` (passphrase + number)
- Throughput: 4.66 GH/s on lab hardware — even faster on a GPU

### Senior tier — SHA-256 cracking of Polish PESEL numbers
This was the **scariest** part of the exercise.
- Hashed Polish PESEL numbers (11-digit national IDs) with raw SHA-256, no salt
- Ran `hashcat -m 1400 pesel.txt ?d?d?d?d?d?d?d?d?d?d?d` (brute force, 11 digits)
- Cracked PESEL numbers `74062086425` and `79092765647`
- Why this worked: PESEL has **only ~10^11 possible values**, with date-of-birth
  structure further constraining the space. Modern GPUs brute force this in minutes.

### Expert tier — John the Ripper comparison
- Ran the same workload through John the Ripper for comparison
- Documented the differences in approach (incremental mode, mask attacks,
  rule-based mutation) — hashcat is faster on GPUs, John has more flexibility

## Key screenshots
- `juniorAlfabetPolski.jpg` — Caesar cipher brute force script and output
- `mediumLamanieHasel_MD5_Hashcat.jpg` — hashcat cracking 3/3 MD5 hashes
  in 2 seconds using rockyou.txt
- `seniorWynikLamaniaPesel.jpg` — `hashcat --show` revealing cracked
  SHA-256 hashes of Polish PESEL numbers

## Takeaway
**Three lessons that change how you think about password storage:**

1. **MD5 is dead.** A 14-million-password wordlist + commodity hardware =
   instant compromise of any unsalted MD5 hash. SHA-1 is dying too.

2. **SHA-256 without salt is also dead for low-entropy data.** PESEL numbers,
   credit card numbers, phone numbers, license plates — anything with bounded
   structure can be brute-forced by exhausting the keyspace, regardless of
   the underlying hash function's cryptographic strength.

3. **The right answer is `bcrypt` / `argon2id`** — deliberately slow,
   memory-hard algorithms with built-in salting. The "slow" part is the feature:
   it costs the attacker billions of times more compute per guess.

**Practical implication:** If you ever inherit a system that stores
unsalted MD5/SHA-256 hashes of any user-identifying data,
that's a critical finding. Document it, escalate it, plan the migration.
