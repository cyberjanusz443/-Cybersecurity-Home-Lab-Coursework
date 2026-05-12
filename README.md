# -Cybersecurity-Home-Lab-Coursework
Hands-on cybersecurity work completed during the **"Cybersecurity Specialist"** program 
at Practima and the **"Web Application Attack & Defense"** course at Niebezpiecznik.pl 
(Poland's leading cybersecurity training organization).
This repository documents 26 lab exercises and a 69-page final security audit project,  completed across Junior → Medium → Senior → Expert difficulty levels.

## 🎯 Career Focus

**Target role:** SOC Analyst L1 / Junior Security Analyst / Junior IT Security Administrator  
**Specialization interest:** Blue Team, Linux server administration, OT/ICS security  
**Location:** Warsaw, Łódź, Poland (open to hybrid / remote)

---

## 🔧 Tech Stack & Tools (Hands-On Experience)

### SIEM & Detection
- **Wazuh** — manager + agent deployment, threat hunting, vulnerability detection (CVE tracking), 
  Security Configuration Assessment (CIS Ubuntu 24.04 LTS Benchmark), 
  rule analysis with MITRE ATT&CK mapping (T1110 Brute Force), 
  compliance correlation (NIST 800-53, PCI DSS, HIPAA, GDPR)

### Network Security & Firewalls
- **UFW** with custom egress filtering (Microsoft 365 IP ranges)
- **iptables** (MASQUERADE, IP forwarding)
- **fail2ban** (automated intrusion prevention)
- Custom log monitoring scripts (SSH brute force aggregation by IP/user)

### VPN & PKI
- **OpenVPN** end-to-end deployment from scratch
- **Easy-RSA** (Certificate Authority, server/client cert signing)
- **OpenSSL** (CSR generation, Subject Alternative Names)
- Diffie-Hellman 2048, TLS-auth preshared keys
- Bash scripting for `.ovpn` config bundling

### Linux Hardening
- **Ubuntu Server 24.04** (production-grade hardening)
- SSH (custom port, key-based auth, configuration hardening)
- **PAM** (pam_unix, pam_pwquality, pam_faillock)
- Password policies (`chage`, complexity rules)
- User/group management with least-privilege ACLs

### Windows Hardening
- **Group Policy Objects** (GPO)
- **AppLocker** (Publisher vs Path conditions, default rules, Deny rules per user)
- Local Security Policy (`secpol.msc`)
- AppLocker bypass demonstration via PowerShell ISE (red team thinking)

### Web Application Security
- **OWASP TOP 10 (2025)** — full coverage of all categories
- **Burp Suite Community** — proxy interception, HTTP/HTTPS history analysis
- **OWASP Juice Shop** — solved challenges:
  - SQL Injection (`' OR 1=1--`)
  - Reflected XSS (`<iframe src="javascript:alert('XSS')">`)
  - Broken Access Control (admin panel via URL manipulation)
  - Business Logic Flaw (chatbot brute force for coupon)
  - Sensitive Data Exposure (FTP directory traversal)
  - Score Board discovery via Burp HTTP history

### Cryptography & Password Cracking
- **hashcat** — MD5 cracking with rockyou.txt (3/3 cracked in 2s), 
  SHA-256 cracking of Polish PESEL hashes (mode 1400)
- **John the Ripper** — alternative wordlist attacks
- **VeraCrypt CLI** — encrypted containers, hidden volumes (plausible deniability)
- **OpenSSL** — symmetric/asymmetric encryption demos
- Custom Python script for Caesar cipher brute force (Polish 35-char alphabet)

### Network Forensics
- **Wireshark** — PCAP analysis, DNS filter for typosquatting detection 
  (caught `google-authenticator.burleson-appliance.net` as malicious domain)
- ARP traffic analysis for MAC address attribution
- Conversations statistics for infected host identification by traffic volume

### OSINT
- **Shodan** queries identifying exposed:
  - Unauthenticated Elasticsearch cluster (7.4M documents, 660 MB)
  - Siemens SIMATIC S7-1500 PLC (Stuxnet-targeted family) on public IP
  - Modbus devices (port 502) tagged as ICS
  - Live IP cameras without authentication
  - Open MongoDB instances and SCADA admin panels
- **Google Dorks** (`filetype:`, `intitle:`, `inurl:`)
- **ExifTool** for metadata extraction (GPS, device model, software version)

### DevOps / Source Control
- **Git** (server-side init, branching, push/pull)
- **GitLab CE** self-hosted via Docker
- **Docker** (container deployment, port mapping, health checks)
- Full GitFlow workflow (branch → merge request → review → merge)
- **Static Application Security Testing (SAST)** of a Flask application 
  identifying critical vulnerabilities (DEBUG mode in production, 
  hardcoded SECRET_KEY, weak SHA-256 password hashing)

### Backup & Disaster Recovery
- **rsync** (mirroring with `--delete`, incremental sync)
- WSL2 as backup target from Windows
- 3-2-1 backup strategy understanding

### Governance, Risk & Compliance (GRC)
- **Risk Assessment** with 3×3 matrix (likelihood × impact)
- **CIS Controls** mapping
- **NIST SP 800-61 Rev. 2** (Incident Response Lifecycle)
- **Polish KNF Recommendation D** (banking IT security)
- **SWIFT Customer Security Programme**
- **Zero Trust Architecture** (Policy Engine, Identity Server, NAC)
- 69-page security audit project for fictional SaaS company (SecureEdge Solutions) — 
  identified 16 control gaps with prioritized remediation timeline

---

## 📂 Repository Structure

```
.
├── README.md                          ← you are here
├── 01-network-fundamentals/           ← VM lab setup, ping, IP configs
├── 02-user-management/                ← Linux & Windows ACLs, least privilege
├── 03-firewall-ssh-hardening/         ← UFW, fail2ban, SSH custom port
├── 04-incident-analysis-pcap/         ← Wireshark PCAP forensics
├── 05-firewall-m365/                  ← Egress filtering for Microsoft 365
├── 06-https-tls-vpn/                  ← OpenSSL, OpenVPN PKI from scratch
├── 07-windows-hardening-applocker/    ← GPO, AppLocker, bypass demo
├── 08-mfa-password-managers/          ← Federation, SSO concepts
├── 09-wazuh-siem/                     ← SIEM deployment, threat hunting, SCA
├── 10-cryptography-hashcat/           ← Password cracking, VeraCrypt
├── 11-veracrypt-hidden-volumes/       ← Plausible deniability volumes
├── 12-backups-rsync-wsl/              ← Cross-OS backup strategies
├── 13-zero-trust-architecture/        ← Architecture diagrams
├── 14-isms-policy-januszex/           ← Information Security Management System
├── 15-bank-swift-compliance/          ← KNF Rec. D, SWIFT CSP
├── 16-audit-plan-compliance/          ← Audit & compliance plans
├── 17-owasp-top-10/                   ← OWASP Top 10 2025 walkthrough
├── 18-juice-shop-pentest/             ← Web app penetration testing
├── 19-gitlab-docker-sast/             ← Self-hosted GitLab + SAST report
├── 20-osint-shodan-exiftool/          ← OSINT investigations
├── 21-incident-response-playbook/     ← NIST 800-61 IR runbook
└── final-project-secureedge/          ← 69-page security audit (anonymized)
```

> **Note on screenshots:** All screenshots have been redacted to remove any 
> third-party identifying information (real IPs, domain names, exposed asset details). 
> Course-internal IPs and hostnames are intentionally preserved.

---

## 🏆 Most Notable Exercises

### Wazuh Threat Hunting & MITRE ATT&CK Mapping
Configured Wazuh manager with multiple agents (Ubuntu 24.04, Windows 11). 
Generated SSH brute-force traffic from a Kali VM and observed 
real-time alert generation with full framework mapping: 
**T1110 (Brute Force) → Credential Access → NIST/PCI DSS/HIPAA/GDPR controls**.

### CIS Ubuntu 24.04 LTS Benchmark Compliance Assessment
Ran Wazuh SCA against my Ubuntu server: 279 checks evaluated, 
127 passed, 117 failed, score 52%. Documented remediation steps 
for failed checks in the kernel module mounting category.

### OpenVPN Deployment from Zero
Built complete VPN infrastructure: own CA, server/client certificates, 
Diffie-Hellman parameters, TLS-auth preshared key. 
Verified clean TLS 1.3 handshake with AES-256-GCM cipher 
between Kali client and Ubuntu server.

### Network Forensics — Typosquatting Detection
Analyzed PCAP file in Wireshark using DNS filter (`dns.qry.name contains "authenticator"`). 
Identified `google-authenticator.burleson-appliance.net` as a typosquatting 
domain used in a phishing campaign within the lab scenario.

### SecureEdge Solutions Security Audit (Final Project)
69-page security audit of a fictional 100-person SaaS company. 
Mapped findings to CIS Controls v8, performed risk assessment 
with 3×3 matrix for 7 critical risks, delivered prioritized 
remediation roadmap (Immediate / 0-3 months / 3-6 months) 
with cost estimates and AWS-specific recommendations 
(GuardDuty, Inspector, Config, Backup, Object Lock).

---

## 🎓 Certifications & Education

- **Practima** — Cybersecurity Specialist (graduating May 2026)
- **Niebezpiecznik.pl** — Web Application Attack & Defense (graduating May 2026)
- **CompTIA Security+** — In progress (target: August 2026)
- Technical Secondary School — Mechatronics Technician

---

## 📫 Contact

[Your Name]  
LinkedIn: [your URL]  
Email: [your email]

---

*Last updated: May 2026*
