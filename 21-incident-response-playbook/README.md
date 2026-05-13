# 21 — Incident Response Playbook (NIST SP 800-61)

GRC + operational exercise: authored a complete Incident Response Playbook
following the official **NIST SP 800-61 Rev. 2** ("Computer Security
Incident Handling Guide") framework. This is the standard reference that
US federal agencies — and most large enterprises globally — base their
IR programs on.

## What I did
Wrote a comprehensive Incident Response Playbook structured around the
NIST four-phase incident lifecycle:

### Phase 1: Preparation
- **Team structure** — defined roles: Incident Commander, Lead Investigator,
  Communications Lead, Legal/Compliance Liaison, IT Operations
- **Tools and resources** — SIEM access, forensic imaging tools,
  out-of-band communication channels, evidence storage requirements
- **Documentation templates** — incident report template, evidence log,
  communications log, lessons-learned template
- **Training requirements** — annual tabletop exercises, quarterly
  technical drills, on-call rotation

### Phase 2: Detection and Analysis
- **Alert sources** — SIEM (Wazuh in our case), EDR, user reports,
  external notifications (CERT, law enforcement, third parties)
- **Initial triage** — severity classification matrix (Critical / High /
  Medium / Low) based on:
  - Affected asset criticality
  - Data sensitivity
  - Scope (single system / department / enterprise-wide)
  - Active threat status
- **Investigation procedures** — log collection, timeline reconstruction,
  IoC (Indicators of Compromise) extraction
- **Documentation requirements** — every action timestamped, every
  artifact hashed and stored with chain of custody

### Phase 3: Containment, Eradication, and Recovery
- **Short-term containment** — isolate affected systems from network
  (firewall rules, switch port shutdown) while preserving evidence
- **System backup** — forensic images of affected systems before
  any remediation
- **Long-term containment** — applying temporary fixes that allow
  business operations to resume while permanent remediation is planned
- **Eradication** — remove malware, close vulnerabilities, rotate
  compromised credentials, revoke certificates
- **Recovery** — restore systems from clean backups, monitor for
  reinfection, gradual production reintegration

### Phase 4: Post-Incident Activity (Lessons Learned)
- **Post-incident meeting** — held within 1-2 weeks of incident closure,
  with all stakeholders
- **Lessons-learned documentation** — what worked, what didn't, what
  needs to improve
- **Playbook updates** — every incident should improve the playbook
  for next time
- **Metrics** — Mean Time to Detect (MTTD), Mean Time to Contain (MTTC),
  Mean Time to Recover (MTTR) tracked over time

### Specific runbook: Lost mobile device
As a concrete example, documented a step-by-step runbook for the most
common incident type: a corporate-owned phone reported as lost or stolen.
- Immediate actions (within 1 hour): remote wipe via MDM, revoke
  device certificates, disable SSO sessions
- Short-term (within 24 hours): notify affected user, IT, compliance
- Investigation: determine if device was encrypted, whether sensitive
  data was accessed before wipe, whether GDPR notification thresholds
  were triggered
- Reporting: internal management, potentially UODO (Polish data
  protection authority) within 72 hours under GDPR Article 33

## Files
- `Incident_response_playbook.pdf` — full IR playbook document with
  all four NIST phases, escalation matrices, and specific runbooks

## Takeaway
**Incident response is the moment everything either pays off or falls
apart.** Every other control I built throughout this course — firewalls,
SIEM, MFA, backups, segmentation — exists to either prevent incidents
or make them survivable.

What I learned from writing this playbook:

1. **The playbook itself is the deliverable** — when an incident is
   actually happening, nobody has time to think clearly. The playbook
   makes the right action obvious, in writing, before adrenaline takes
   over.

2. **Communication is harder than the technical work.** Knowing how to
   isolate an infected host is hours of work. Knowing who to call, what
   to tell them, what to NOT tell them (do you call the FBI? Do you tell
   the press? Do you tell customers immediately?) is days of work —
   and you must decide those questions BEFORE the incident.

3. **Legal and regulatory clocks start the moment detection begins.**
   GDPR's 72-hour notification window starts when you're "aware" of a
   breach. Banking regulators have different windows. Some industries
   require notification within 24 hours. The playbook must encode all
   these clocks.

4. **The post-mortem is where organizations actually learn.** Most
   incidents recur because the same root cause was never addressed.
   A well-run post-mortem produces three things: a corrected playbook,
   a list of new controls to implement, and metrics to track over time.

5. **Tabletop exercises are non-negotiable.** Running a simulated
   ransomware scenario in a conference room exposes every gap in the
   playbook — gaps that would otherwise only surface in the middle of
   a real crisis.

**For my SOC career:** L1 analysts are the **first responders** in the
NIST model. They don't make executive decisions, but they DO execute
the first steps of the playbook. Knowing the framework intimately
means knowing exactly what the senior on call expects of me when an
alert fires at 3 AM.

This document is the kind of deliverable a SOC team lead would write —
authoring it gave me a useful glimpse into the role I'd eventually
want to grow into.
