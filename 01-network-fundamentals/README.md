# 01 — Network Fundamentals

Initial lab setup: three virtual machines (Kali Linux, Ubuntu Server, Windows 11 Pro)
running on VMware Workstation, configured to communicate over an isolated lab network.

## What I did
- Configured network interfaces on Linux (`ip addr show`) and Windows (`ipconfig`)
- Verified connectivity between VMs (ICMP, gateway reachability)
- Tested external DNS resolution and ICMP latency to public hosts (8.8.8.8, google.com)
- Confirmed isolated subnet `192.168.234.0/24` with each VM having a unique address

## Key screenshots
- `linux.jpg` — Kali network configuration and connectivity tests
- `ubuntu.jpg` — Ubuntu Server with system summary and routing checks
- `windows.jpg` — Windows 11 PowerShell with `ipconfig` and ping tests

## Takeaway
A proper lab environment is the foundation for everything else.
Three VMs on the same isolated subnet let me simulate attacker-target-defender
scenarios used in later exercises.
