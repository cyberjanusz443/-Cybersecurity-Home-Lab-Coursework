# 07 — Windows Hardening with AppLocker

Multi-tier Windows hardening exercise covering Group Policy Objects,
AppLocker application control, and — importantly — a demonstration
of how policies can be bypassed when configured incorrectly.

## What I did

### Junior tier — User account policies
- Configured the `Non-Administrators Policy` via Microsoft Management Console
  (`mmc.exe` → Group Policy Object Editor) targeting only non-admin users
- Verified User Configuration settings were applied selectively

### Medium tier — Application execution control
- Configured **Local Security Policy** (`secpol.msc`) with restrictions
  on which applications standard users can launch
- Applied Software Restriction Policies for legacy compatibility

### Senior tier — AppLocker Publisher-based rules
- Configured **AppLocker** with Executable Rules:
  - Default Allow rules for `Program Files` and `Windows` directories
  - **Deny rules** specifically for `windowspro\junior_user`:
    - `CMD.EXE` (Publisher condition, version 10.0.26100.7309+)
    - `POWERSHELL.EXE` (Publisher condition)
- Why Publisher condition matters: it survives file path changes and
  works on signed Microsoft binaries reliably

### Expert tier — Bypass demonstration (red team perspective)
- Logged in as `junior_user` with full AppLocker policy active
- `cmd.exe` and `powershell.exe` correctly blocked
- **BUT** — successfully launched **PowerShell ISE**, which is a separate
  binary not covered by my rules
- Inside PowerShell ISE: executed `whoami` and `ipconfig` as `junior_user`,
  proving that blocklisting specific executables is insufficient

## Key screenshots
- `MediumPolitykaUzytkownikow.jpg` — MMC console with Non-Administrators Policy
- `SeniorBlokadaDlaJuniorUserCMDPowerShell.jpg` — AppLocker rules showing
  Publisher-based Deny for CMD.EXE and POWERSHELL.EXE
- `ExpertObejsciePowerShell.jpg` — PowerShell ISE running as `junior_user`
  with `whoami` and `ipconfig` working — the bypass

## Takeaway
**Application control by blocklist is fundamentally fragile.**
Even with Publisher-based rules — which are stronger than path-based —
Windows ships with so many script interpreters (PowerShell ISE, `wscript.exe`,
`mshta.exe`, Office macros, `.NET` host binaries) that enumerating them
exhaustively is impossible.

The right approach is **allowlisting**: deny everything except known-good binaries.
But that's operationally expensive, which is why organizations often
end up with the weaker blocklist approach this exercise demonstrated.

**For Blue Team:** understanding bypass techniques is a prerequisite to
defending against them. You cannot detect what you don't understand.
