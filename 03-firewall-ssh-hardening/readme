# 03 — Firewall & SSH Hardening

Progressive SSH hardening across four difficulty tiers: from basic service
verification to active intrusion prevention with custom log monitoring.

## What I did
**Junior:** Installed and verified OpenSSH service; observed live brute-force
attempts from Kali in `systemctl status ssh` output (`Failed password for
invalid user admin from 192.168.10.102`).

**Medium:** Configured password complexity via `pam_pwquality.so`
(minimum length, character classes, retry limit). Tested rejection
of weak passwords in real time.

**Senior:** Implemented password aging with `chage`:
- Minimum age: 7 days (`-m 7`)
- Maximum age: 90 days (`-M 90`)
- Warning period: 14 days (`-W 14`)

**Expert:** Combined three production-grade defenses:
- **UFW firewall** — SSH moved from port 22 to 2222, telnet (23) explicitly denied,
  HTTP restricted to local subnet `192.168.10.0/24`
- **fail2ban** — automated banning of repeat offenders with status verification
  via `systemctl status fail2ban`
- **Custom monitoring script** — bash script parsing `/var/log/auth.log` and
  aggregating failed logins by attacking IP and targeted username (mini-SIEM logic)
- **cron** — scheduled tasks for `apt update` and `debsums` integrity checks

## Key screenshots
- `serverSSHinstalacja.jpg` — SSH service status with visible brute-force attempts
- `nowapolitykahaseltest.jpg` — `chage -l` showing applied password aging
  and `passwd` rejecting weak password
- `fail2ban.jpg` — fail2ban service running and configured
- `zmianaportu.jpg` — UFW status showing custom SSH port and locked-down rules
- `cron.jpg` — Crontab with scheduled security tasks
- `monitorblednychlogow.jpg` — Custom log monitor: "Top attacking IPs",
  "Top targeted accounts" — manual implementation of SIEM aggregation logic

## Takeaway
SSH hardening is not a single setting — it's a defense-in-depth stack:
non-default port + key auth + rate limiting + log monitoring + automated banning.
Each layer alone is insufficient; together they make brute force economically pointless.
