# 13 — Zero Trust Architecture

Theoretical and architectural exercise: designing a Zero Trust security model
for a hypothetical organization, including all required components and
their interactions.

## What I did
- Designed a complete Zero Trust Architecture diagram showing the relationships
  between core components:
  - **Policy Engine (PE)** — makes the access decision (allow/deny) based on
    policy rules and contextual signals
  - **Policy Administrator (PA)** — implements the decision by establishing
    or terminating connections
  - **Policy Enforcement Point (PEP)** — the actual gateway that brokers
    each connection request between subject and resource
  - **Identity Provider (IdP)** — authenticates users (federated SSO, MFA)
  - **SIEM** — provides continuous monitoring signals to the Policy Engine
  - **Network Access Control (NAC)** — verifies device posture before granting
    network access
- Applied Zero Trust principles:
  - **Never trust, always verify** — every request is authenticated and
    authorized, regardless of network location
  - **Least privilege per session** — access scoped to specific resources,
    re-evaluated continuously (e.g., every N hours or on signal change)
  - **Assume breach** — design assumes attackers may already be inside;
    segment everything (VLANs, microsegmentation)
  - **Conditional access** — decisions consider context: user identity,
    device health, location, time of day, behavioral anomalies
- Mapped the architecture to **NIST SP 800-207** (the official US standard
  for Zero Trust Architecture)

## Files
- `Architektura_Zero_Trust.pdf` — written assignment with full architecture
  description, principles, and mapping to organizational requirements
- `architekturazerotrust.jpg` — architecture diagram showing all components
  and their data flows

## Takeaway
Zero Trust is **a security model, not a product**. Vendors will sell you
"Zero Trust solutions," but the architecture itself is a mindset shift:

- **Old model (perimeter security):** Trust everything inside the corporate
  network, verify only at the edge. Once a VPN connection is established,
  the user is implicitly trusted.
- **New model (Zero Trust):** Trust nothing. Every connection — even between
  two internal microservices — goes through authentication, authorization,
  and continuous validation.

For a SOC analyst, Zero Trust changes the detection landscape:
- More authentication events to analyze (every resource access logs)
- More signal sources feeding the SIEM (NAC, device posture, behavioral analytics)
- Faster detection of compromised accounts (because anomalies trigger
  conditional access policies in near real-time)

**Real-world examples** I studied while doing this exercise:
- **Google BeyondCorp** — the original production Zero Trust implementation
- **Microsoft Conditional Access** — entry point for Microsoft 365 environments
- **Cloudflare Zero Trust** — vendor-managed access broker

This isn't a "future" architecture — it's already standard practice in
mature security organizations.
