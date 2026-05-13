# 17 — OWASP Top 10 (2025) Analysis

Comprehensive analysis of the OWASP Top 10 — the industry-standard list of
the most critical web application security risks. This exercise combined
theoretical coverage with practical HTTPS traffic interception.

## What I did

### Theoretical coverage — all 10 categories
For each OWASP Top 10 (2025 edition) category, documented:
- **What it is** — definition and typical attack pattern
- **Why it happens** — common root causes in code and architecture
- **How to prevent it** — secure coding practices, framework-level mitigations
- **How to detect it** — testing approaches, monitoring signals

Categories covered:
- **A01: Broken Access Control** — IDOR, forced browsing, missing function-level auth
- **A02: Cryptographic Failures** — weak algorithms, missing TLS, exposed credentials
- **A03: Injection** — SQL, NoSQL, command, LDAP, XSS as code injection
- **A04: Insecure Design** — threat modeling gaps, missing security requirements
- **A05: Security Misconfiguration** — default passwords, verbose errors, unpatched systems
- **A06: Vulnerable and Outdated Components** — supply chain risks, dependency management
- **A07: Identification and Authentication Failures** — weak passwords, no MFA, session bugs
- **A08: Software and Data Integrity Failures** — unsigned updates, insecure deserialization
- **A09: Security Logging and Monitoring Failures** — missing logs, ignored alerts
- **A10: Server-Side Request Forgery (SSRF)** — internal network exposure via user-supplied URLs

### Deep-dive on A06 (Vulnerable and Outdated Components)
- Special focus document on A06 because this category was significantly
  re-ranked in the 2025 edition
- Documented the supply chain risk: a single malicious or vulnerable
  dependency can compromise the entire application
- Real-world examples studied: log4shell (CVE-2021-44228), event-stream NPM
  attack, SolarWinds Orion

### Practical — HTTPS traffic interception with Burp Suite
- Configured **Burp Suite Community Edition** as a proxy
- Generated Burp's CA certificate and imported it into Firefox's trust store
  (so the browser trusts Burp's man-in-the-middle for testing)
- Intercepted live HTTPS traffic to `example.com`:
  - Examined HTTP/2 request structure (headers, method, URL, body)
  - Reviewed response details (status code, server, cache, content-type)
  - Inspected modern security headers (Sec-Fetch-*, Upgrade-Insecure-Requests)
- This is the **standard setup for web application pentesting**

## Key screenshots
- `senior_Firefox_https.jpg` — Firefox showing trusted HTTPS connection
  via Burp's MITM certificate
- `senior_Przechwycony_Ruch.jpg` — Burp Suite intercepting and decrypting
  HTTPS traffic, showing full request/response cycle

## Files
- `opis_OWASP_TOP_10.pdf` — complete OWASP Top 10 analysis document
- `NIEBEZPIECZNY_PROJEKT_A06_2025.pdf` — deep-dive on A06 category

## Takeaway
The OWASP Top 10 is not a "checklist" — it's a **frequency-weighted threat
landscape** for web applications. Knowing it cold is table stakes for
anyone doing AppSec, but it's also valuable for SOC analysts because:

1. **Most external attacks target these vectors** — when you see a
   suspicious HTTP request in logs, recognizing it as "looks like SQLi"
   or "looks like SSRF" speeds up triage by orders of magnitude.

2. **Detection signals map to these categories** — your SIEM rules
   should fire on patterns characteristic of each category (e.g., 
   `SELECT * FROM` in POST data → likely SQLi attempt).

3. **Compensating controls fall out naturally** — WAF rules, RASP,
   API gateways exist specifically to block these categories at the
   network edge.

**Why this exercise matters:** Burp Suite is THE tool for hands-on web app
security work. Even as a Blue Team analyst, understanding what Red Team
sees in Burp helps me write better detection rules and recognize
real attacks faster.
