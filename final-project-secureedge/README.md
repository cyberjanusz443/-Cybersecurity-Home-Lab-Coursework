# Final Project — SecureEdge Solutions Security Audit

**A 69-page comprehensive security assessment** for a fictional SaaS company,
representing the capstone of the Practima Cybersecurity Specialist program.
This is the single largest and most polished deliverable in this portfolio.

---

## Project Overview

**Target organization (fictional):** SecureEdge Solutions Sp. z o.o.
- **Industry:** SaaS provider for SMB customers
- **Size:** 100 employees across multiple departments
- **Infrastructure:** AWS-based cloud deployment with hybrid office connectivity
- **Customer base:** ~500 SMB clients with sensitive operational data

**Project objective:** Conduct a full security audit, identify control gaps,
quantify risks, and deliver a prioritized remediation roadmap with cost
estimates and timeline.

## What I Delivered

### 1. Organizational profile & threat landscape
- Mapped the organization's data flows, critical assets, and trust boundaries
- Identified the threat actors relevant to a SaaS provider (cybercriminals,
  hacktivists, nation-states, malicious insiders, competitors)
- Documented compliance scope (GDPR/RODO, contractual SLAs with customers)

### 2. Current state assessment
- Inventoried existing security controls against **CIS Controls v8** framework
- Used a maturity model (Implementation Group IG1 / IG2 / IG3) to determine
  appropriate baseline for the organization's size and risk profile
- Identified **16 distinct control gaps** across the following CIS Controls:
  - CIS 1: Inventory and Control of Enterprise Assets
  - CIS 3: Data Protection
  - CIS 5: Account Management
  - CIS 6: Access Control Management
  - CIS 8: Audit Log Management
  - CIS 10: Malware Defenses
  - CIS 11: Data Recovery (Backup)
  - CIS 14: Security Awareness and Skills Training
  - CIS 16: Application Software Security
  - CIS 17: Incident Response Management

### 3. Risk assessment
- Selected the **7 most critical risks** from the gap analysis
- Applied a **3x3 risk matrix** (Likelihood × Impact)
- For each risk:
  - Threat scenario narrative
  - Likelihood justification (frequency data, threat actor capability)
  - Impact analysis (financial, operational, reputational, regulatory)
  - Current control effectiveness
  - Recommended treatment

### 4. Remediation roadmap with timeline
Prioritized findings into three implementation tiers:

**🔴 IMMEDIATE (within 30 days)** — items where the cost of inaction
exceeds the cost of action:
- Enable MFA for all administrative accounts
- Implement AWS GuardDuty for threat detection
- Configure CloudTrail logging with S3 immutability
- Patch critical vulnerabilities flagged by AWS Inspector

**🟡 SHORT-TERM (0–3 months)** — controls requiring planning but
strong ROI:
- Deploy centralized SIEM (Wazuh or commercial alternative)
- Implement formal incident response procedures
- Roll out security awareness training program
- Establish backup strategy with AWS Backup + Object Lock

**🟢 MEDIUM-TERM (3–6 months)** — controls requiring more substantial
investment or organizational change:
- Implement Zero Trust network architecture
- Establish vulnerability management program with SLAs
- Build threat intelligence integration
- Achieve ISO 27001 certification readiness

### 5. AWS-specific technical recommendations
Because the organization runs on AWS, included concrete service-level
recommendations:
- **GuardDuty** for threat detection
- **Inspector** for vulnerability assessment
- **Config** for compliance monitoring
- **CloudTrail + S3 Object Lock** for tamper-evident audit logging
- **Backup with cross-region replication** for disaster recovery
- **Security Hub** as the central security findings aggregator
- **IAM Access Analyzer** for permission boundary review
- **Macie** for sensitive data discovery in S3

### 6. Cost estimation
Approximate budgets for each remediation tier:
- Tools and AWS service costs
- Internal effort (FTE-months)
- External consulting/audit costs
- Training and certification investments

### 7. Presentation deck (HTML)
Also delivered a stakeholder presentation summarizing findings for
executive audience — focusing on business risk language rather than
technical detail.

## Files
- `PROFIL_ORGANIZACJI_-_SecureEdge_Solutions_Sp.pdf` — full 69-page
  audit report
- `prezentacja_secureedge.html` — interactive executive presentation deck

## Why This Project Matters

This was the **first time I produced a deliverable that resembles real
consulting work** — not an exercise with a known answer, but an open-ended
problem requiring synthesis across everything I'd learned in the program:

- **Linux and Windows hardening** (from the OS exercises)
- **SIEM operations** (from the Wazuh deployment)
- **Network architecture** (from the firewall and VPN exercises)
- **Identity and access management** (from the MFA exercise)
- **Cryptography and data protection** (from the encryption exercises)
- **Web application security** (from the OWASP and Juice Shop work)
- **OSINT and reconnaissance** (from the Shodan exercise)
- **GRC** (from the ISMS policy and audit plan exercises)
- **Incident response** (from the playbook exercise)

The 69 pages aren't padding — each section is rooted in a control I
either implemented hands-on or studied in depth during the program.

## What I Learned About the Profession

1. **Security audit work is mostly writing.** Technical knowledge is the
   prerequisite, but the actual deliverable is documentation that a
   non-technical executive will read, a board member will approve, and
   an auditor will verify. **The ability to translate technical findings
   into business language is the differentiator.**

2. **Prioritization is harder than identification.** Finding 16 control
   gaps was the easy part. Convincing fictional management which 5 to
   fix first required understanding their business context — revenue
   model, customer commitments, regulatory exposure, organizational
   risk appetite.

3. **Mapping to standards multiplies value.** Every finding I mapped to
   CIS Controls v8 became simultaneously a finding mappable to ISO 27001,
   NIST CSF, and SOC 2. Once you understand one framework deeply, the
   others fall into place quickly because they all describe the same
   underlying security concepts.

4. **Real consulting work needs cost estimates.** Recommendations without
   budget context are useless to decision-makers. Even rough estimates
   (which I included for AWS service costs, FTE effort, and external
   audit fees) transform a recommendation from "should do this" into
   "here's the business case."

5. **This is the kind of work I want to grow into.** Starting in SOC L1
   gives me operational depth. After 2-3 years, the natural progression
   for someone who enjoys synthesis and writing is into security
   consulting, audit, or GRC — and this final project showed me I have
   the foundation for that trajectory.

## A Note for Reviewers

This document was a course assignment for SecureEdge Solutions — a
**fictional company**. Any resemblance to actual organizations, AWS
configurations, or specific vulnerabilities is coincidental. The document
is presented here as evidence of analytical methodology and depth of
synthesis, not as an authentic third-party audit.

If you're a hiring manager reviewing this portfolio: **this is the
deliverable I'd point to as my best work** from the program. It demonstrates
that I can take a brief, structure a comprehensive analysis, and produce
a deliverable suitable for executive consumption. That skill set — applied
at smaller scale to incident reports, vulnerability findings, or audit
responses — is what I'll bring to a Junior SOC Analyst role from day one.
