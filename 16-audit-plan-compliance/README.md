# 16 — Network Audit Plan & Compliance Framework

Two-document deliverable: a structured audit plan for assessing a corporate
network's security posture, and a complementary compliance framework
mapping organizational practices to regulatory requirements.

## What I did

### Network Audit Plan
Prepared a comprehensive audit plan document covering:
- **Audit scope** — which network segments, systems, and processes
  are within scope (and explicitly out of scope)
- **Audit objectives** — what the audit is intended to verify (e.g.,
  effectiveness of access controls, integrity of network segmentation,
  completeness of logging)
- **Methodology** — combination of:
  - **Document review** — policies, procedures, architecture diagrams,
    previous audit findings
  - **Technical testing** — vulnerability scanning, configuration review,
    log sampling
  - **Interviews** — discussions with system administrators, security
    operations, business owners
- **Timeline & resource plan** — auditor allocation, scheduled meetings,
  evidence collection milestones
- **Reporting structure** — executive summary, detailed findings,
  recommendations with priority ranking, management responses

### Compliance Framework Plan
Mapped organizational security practices to applicable frameworks:
- **ISO/IEC 27001** — Annex A controls relevant to the organization's
  scope statement
- **NIST Cybersecurity Framework** — Identify / Protect / Detect / Respond /
  Recover function mapping
- **GDPR** (RODO in Polish) — Article 32 technical and organizational
  measures for data protection
- **CIS Controls v8** — Implementation Group (IG1/IG2/IG3) prioritization
- **3 Lines of Defense model**:
  - **Line 1:** Operational management (system admins, developers)
    own day-to-day controls
  - **Line 2:** Risk management and compliance functions oversee Line 1
  - **Line 3:** Internal audit provides independent assurance to the Board

## Files
- `Plan_Audytu_Sieci_Komputerowej.pdf` — full network audit plan
- `Plan_Compliance.pdf` — compliance framework with mapping tables

## Takeaway
**Audit and compliance work is the "feedback loop" of a security program.**
Without it, you can implement all the controls in the world and never know
whether they actually work.

What I internalized through this exercise:

1. **An audit plan is a contract** — between the auditor and the audited
   party. The scope, methodology, and deliverables must be agreed
   upfront so there are no surprises.

2. **Findings need owners** — every recommendation must have a named
   accountable person and a target remediation date. Otherwise nothing
   gets fixed.

3. **Compliance frameworks overlap heavily** — ISO 27001 control A.5.7
   (threat intelligence) maps to NIST CSF DE.AE-7, which also satisfies
   CIS Control 17. One properly designed control can satisfy multiple
   frameworks simultaneously. Smart organizations design once, certify
   many times.

4. **The 3 Lines of Defense model** is why audit independence matters —
   the auditor cannot be the same person who designed and operates the
   controls. Independence is built into the org chart.

For my career path: many SOC analyst roles in regulated industries
involve preparing evidence for audits (showing investigation reports,
log retention proof, MTTR metrics). Understanding the audit perspective
makes this work meaningful instead of bureaucratic.
