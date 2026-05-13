# 15 — Banking IT Security (SWIFT CSP & KNF Recommendation D)

Domain-specific compliance exercise: documented the security requirements
for connecting a Polish bank's IT systems to the **SWIFT network** —
the global financial messaging system that processes ~$5 trillion in
transactions daily.

## What I did
- Studied and documented compliance with two key frameworks:

### SWIFT Customer Security Programme (CSP)
SWIFT mandates a **Customer Security Controls Framework** for every
institution connecting to its network. Documented requirements across:
- **Restrict Internet Access** — SWIFT environment isolated from general
  internet, no direct routing
- **Segregate Critical Systems** — SWIFT infrastructure in dedicated VLANs,
  separate from corporate network
- **Reduce Attack Surface** — minimum services, no unnecessary software,
  patched within SLA
- **Physically Secure Environment** — locked racks, controlled access,
  no shared workstations
- **Prevent Compromise of Credentials** — MFA mandatory for all SWIFT users,
  no shared accounts
- **Manage Identities and Separate Privileges** — role-based access control,
  segregation of duties between operators and administrators
- **Detect Anomalous Activity** — SIEM integration, logging of every SWIFT
  transaction, alerting on out-of-pattern activity
- **Plan for Incident Response and Information Sharing** — incident playbook
  specifically for SWIFT-related events, mandatory reporting to SWIFT

### KNF Recommendation D (Polish Financial Supervision Authority)
The Polish regulator's IT security framework for banks, covering:
- IT governance structure and Board responsibilities
- Risk management for IT systems
- Outsourcing and cloud computing requirements
- Cybersecurity incident reporting obligations
- Business continuity and disaster recovery requirements

## Files
- `Podlaczenie_Bankowosci_Do_SWIFT.pdf` — full assignment document covering
  both SWIFT CSP and KNF Recommendation D requirements, including
  network architecture diagram for SWIFT integration

## Takeaway
The financial sector operates under some of the **strictest cybersecurity
regulations in the world**. Every control I learned in other exercises
(firewalls, SIEM, MFA, segmentation, IR playbooks) becomes a **regulatory
mandate** in banking — not optional, not best-practice, but legally required.

**Why this exercise matters for my career:**
- Polish banks (BNP Paribas, mBank, ING, Santander, PKO BP) are major
  employers of SOC analysts in Warsaw
- Their job postings frequently mention "knowledge of KNF Rec. D" or
  "SWIFT CSP experience" — having even theoretical exposure is a
  differentiator
- Compliance work pays well and is recession-resistant: banks **must**
  comply regardless of market conditions

**Real-world incident:** The 2016 Bangladesh Bank heist ($81M stolen via
SWIFT) is the case study that drove SWIFT CSP into existence. The attackers
used legitimate SWIFT credentials obtained via malware — exactly the
scenario these controls are designed to prevent.

Compliance is not paperwork. It's hardened operations encoded as
contractual obligations.
