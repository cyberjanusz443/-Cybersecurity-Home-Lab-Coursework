# 11 — VeraCrypt Encrypted & Hidden Volumes

Practical disk encryption exercise covering both standard encrypted containers
and the more sophisticated **hidden volume** mechanism that provides
plausible deniability.

## What I did

### Junior tier — Standard encrypted container
- Created a VeraCrypt container using AES encryption
- Mounted the container as a virtual drive (`J:`) under Windows
- Verified that files written to the mounted volume are accessible
  while mounted but completely inaccessible (no file headers, no metadata)
  when the volume is unmounted — the entire container appears as random bytes

### Medium tier — Volume verification
- Used `df -h` and disk management tools to verify volume properties
- Confirmed the mounted container behaves as a normal filesystem
- Practiced mount/unmount workflow including password verification

### Senior tier — Hidden volume (plausible deniability)
- Created a **hidden volume nested inside a standard container** —
  the same file holds two independent encrypted volumes with different passwords
- **Outer volume password** → opens decoy data (e.g., personal documents)
- **Inner (hidden) volume password** → opens the real sensitive data
- Without knowing the second password, it is **cryptographically impossible**
  to prove that a hidden volume exists at all — the free space looks like
  random padding either way

## Key screenshots
- `junior_Test_Pliku_wDysku.jpg` — File visible when volume mounted (`J:`)
- `junior_Test_Pliku_Unmounted.jpg` — Same volume after unmount: drive gone
- `medium_Wynik_Dysk_dfh.jpg` — `df -h` showing mounted encrypted volume
- `senior_Dysk_Ukryty.jpg` — VeraCrypt UI showing `Type: Hidden` on drive `K:`
  with AES encryption, 49.9 MiB — proof of working hidden volume

## Takeaway
**Disk encryption alone is not enough** in adversarial scenarios where you
might be **compelled** to reveal a password (legal coercion, physical threat).
Hidden volumes solve this by making it impossible to prove sensitive data exists.

This is not theoretical — it's a documented use case for journalists,
activists, and people crossing borders with sensitive material.
The cryptography works because random data and encrypted data are
indistinguishable.

**Operational caveat:** hidden volumes only work if you don't write to
the outer volume after creating the inner one — otherwise you risk
overwriting your hidden data. This is a real-world tradeoff that
demonstrates how security tools require **operational discipline**,
not just technical knowledge.
