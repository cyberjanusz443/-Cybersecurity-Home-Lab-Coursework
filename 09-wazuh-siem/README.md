# 09 — Wazuh SIEM Deployment & Threat Hunting

The cornerstone exercise of this entire program. Deployed a Wazuh
SIEM in a real classroom lab with **25 agents** (mix of Ubuntu 24.04
and Windows 11) reporting to a central manager. Performed threat hunting,
vulnerability detection, and CIS benchmark compliance auditing
on my own agent.

## What I did

### Agent enrollment & infrastructure
- Verified agent status in the Wazuh manager web console:
  25 agents across `default` group, my agent (`cyberjanusz`, ID 025) active
- Wazuh manager version 4.14.2, single-node cluster (`node01`)
- Agent IP `192.168.10.125` reporting to manager `48.209.8.17`

### Threat Hunting
- Investigated SSH authentication events across the time window
  `Jan 28 – Feb 3, 2026` — 26 hits returned
- Correlated event types: `sshd brute force`, `PAM login failures`,
  `successful sudo to ROOT`, `file integrity checksum changes`
- Identified attack patterns: repeat brute force from same source IP,
  attempts against non-existent users (T1110.001 — Password Guessing)

### MITRE ATT&CK & multi-framework compliance mapping
One alert detail panel showed the true power of a properly configured SIEM —
a single SSH brute force detection mapped automatically to:
- **MITRE ATT&CK**: `T1110 Brute Force` / `Credential Access` tactic
- **NIST 800-53**: SI.4, AU.14, AC.7
- **PCI DSS**: 11.4, 10.2.4, 10.2.5
- **HIPAA**: 164.312.b
- **GDPR**: IV_35.7.d, IV_32.2
- **TSC**: CC6.1, CC6.8, CC7.2, CC7.3
- Rule ID 5712, level 10, fired 10 times, frequency 8

### Vulnerability Detection
Live CVE tracking on my agent showed:
- **6 Critical** severity vulnerabilities
- **790 High** severity
- **1,842 Medium** severity
- **52 Low** + **1,241 Pending Evaluation**
- Top CVEs surfaced: CVE-2022-3219, CVE-2025-68972, CVE-2026-24882
- Most-affected packages: `linux-image-6.8.0` (2,024 findings), `curl`/`libcurl`

### Security Configuration Assessment (SCA)
Ran the **CIS Ubuntu Linux 24.04 LTS Benchmark v1.0.0** against my agent:
- **279 total checks** evaluated
- **127 passed** / **117 failed** / **35 not applicable**
- **Compliance score: 52%**
- Reviewed failed check categories: kernel module mounting controls
  (`cramfs`, `freevxfs`, `hfs`, `hfsplus`), file system parameters

## Key screenshots
- `juniorliczbaAgentow.jpg` — Wazuh manager with 25 agents listed
- `juniorThreadHuntingPK.jpg` — Threat hunting dashboard with
  SSH events, sudo escalations, integrity checks
- `juniorVulnerabilityDetection.jpg` — CVE dashboard (6 critical, 790 high)
- `juniorSCA.jpg` — CIS Ubuntu 24.04 LTS benchmark, 279 checks, 52% score
- `mediumRodzajAtaku.jpg` — **The crown jewel**: single alert detail panel
  showing simultaneous mapping to MITRE T1110, NIST, PCI DSS, HIPAA, GDPR

## Takeaway
This is what a real SOC L1 analyst sees daily. A SIEM is not "log search" —
it's a **correlation engine** that turns raw events into structured,
framework-mapped findings ready for compliance reporting.

The mental shift this exercise produced: alerts are not just notifications.
They are **compliance evidence**, automatically tagged with every framework
the organization needs to satisfy. One detection, one investigation,
and the audit report writes itself.

**Real-world equivalent:** Same workflow runs on Splunk, Microsoft Sentinel,
Elastic Security, IBM QRadar. The vendor changes; the analyst's job
(triage → investigate → escalate or close) does not.
