# 05 — Firewall Configuration for Microsoft 365

Production-grade egress filtering: locking down a Linux workstation
so it can ONLY reach Microsoft 365 endpoints, with everything else blocked.

## What I did
- Researched **official Microsoft 365 IP address ranges** published by Microsoft
  (the same lists used by enterprise network teams for SD-WAN/proxy bypass rules)
- Set UFW default policy to `deny incoming` AND `deny outgoing` —
  full lockdown by default
- Created **explicit allow rules** for the M365 IP ranges on the required ports:
  - **TCP/587** — SMTP submission (Outlook outbound mail)
  - **TCP/443** — HTTPS (everything else: Teams, OneDrive, SharePoint, Exchange Web)
- Allowed inbound SSH only from the local LAN `192.168.10.0/24`
- Enabled UFW logging at `high` verbosity to capture every blocked attempt
- Verified that `curl http://google.com` is blocked (no response) while
  M365 endpoints remain reachable
- Tailed `/var/log/ufw.log` in real time to observe `[UFW BLOCK]` and
  `[UFW AUDIT]` events as they happened

## Key screenshots
- `statusufwverbose.jpg` — `ufw status verbose` showing 20+ explicit allow rules
  for Microsoft IP ranges on ports 587 and 443
- `testblokujacy.jpg` — `curl http://google.com` blocked (hangs and is killed)
- `analizalogow.jpg` — Live `tail -f /var/log/ufw.log` showing UFW decisions

## Takeaway
Egress filtering is one of the most underrated security controls.
Most malware needs to call home — blocking arbitrary outbound destinations
breaks the kill chain even if initial compromise succeeds.
This exercise also showed me why enterprise firewall rules are tedious:
maintaining accurate IP allowlists for SaaS services is real, ongoing work.
