# 14 — Information Security Management System (ISMS) Policy

GRC-focused exercise: drafted a full Information Security Management System
policy document for a fictional Polish company ("Januszex").
This is the kind of document that auditors (ISO 27001, SOC 2) ask for first.

## What I did
- Wrote a comprehensive ISMS policy covering:
  - **Scope** — which systems, data, and personnel are covered
  - **Roles & responsibilities** — Information Security Officer, Data Protection
    Officer, asset owners, system administrators, all employees
  - **Risk management framework** — methodology for identifying, assessing,
    treating, and monitoring information security risks
  - **Asset classification** — public / internal / confidential / strictly
    confidential, with handling rules for each tier
  - **Access control policy** — least privilege, segregation of duties,
    privileged account management, access review cadence
  - **Acceptable use policy** — what employees can and cannot do with company
    IT resources (devices, internet, email, cloud storage)
  - **Incident response procedures** — reporting channels, classification,
    escalation paths, communication with regulators (UODO under GDPR)
  - **Cryptography policy** — approved algorithms, key management,
    encryption-at-rest and in-transit requirements
  - **Physical security** — server room access, clean desk policy,
    device theft response
  - **Business continuity & disaster recovery** — RPO/RTO targets, backup
    strategy, regular DR testing
  - **Training & awareness** — onboarding, annual refresh, phishing simulations
  - **Compliance audits** — internal and external audit schedule
- Aligned the document with **ISO/IEC 27001:2022** Annex A controls

## Files
- `Zasady_Bezpieczenstwa_Systemow_Informatycznych_Januszex-POL.pdf` —
  full ISMS policy document (in Polish)

## Takeaway
A SOC analyst's day-to-day work happens in the context of these policies.
When you flag an incident, the policy defines:
- **Severity classification** — is this a minor event or a reportable breach?
- **Communication paths** — who gets notified and when?
- **External obligations** — does this trigger a GDPR 72-hour reporting clock?
- **Forensic preservation** — how must evidence be handled?

**Without a written policy, every incident becomes ad-hoc improvisation.**
Mature organizations have these policies precisely so that response is
predictable, defensible, and auditable.

For me as someone entering the field: understanding that the **technical
work** of cybersecurity sits inside a **governance framework** changed how
I think about every other exercise in this course. SIEM rules exist to
detect violations of policy. Firewall rules exist to enforce policy.
Incident playbooks exist to operationalize policy.

The policy is the source code; everything else is the runtime.
