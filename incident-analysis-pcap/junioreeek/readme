# 04 — Incident Analysis (PCAP Forensics)

Network forensics exercise: given a packet capture from a suspected
malware incident, identify the infected host, the command-and-control
infrastructure, and the malicious domain involved.

## What I did
- Loaded the provided PCAP into **Wireshark** and used the
  **Conversations** statistics view to identify the top-talking host
  by traffic volume — pinpointing `10.1.17.215` as the likely
  infected machine (communicating with ~24 unique external IPs)
- Applied **DNS query filter** (`dns.qry.name contains "authenticator"`)
  to discover a **typosquatting domain** used by the malware:
  `google-authenticator.burleson-appliance.net`
- Inspected **ARP traffic** to confirm the MAC address attribution
  of the infected host (`00:d0:b7:26:4a:74`)
- Cross-referenced infected host's outbound connections to identify
  the C2 server pattern (frequent small connections to many IPs)

## Key screenshots
- `zainfekowanyadresip.jpg` — Wireshark Conversations sorted by packet count,
  revealing the infected host
- `nazwafalszywejdomenygoogle.jpg` — DNS filter exposing typosquatting domain
- `c2.jpg` — Pattern of outbound connections characteristic of C2 beaconing
- `adresmac.jpg` — ARP packets used to confirm MAC-to-IP mapping

## Takeaway
PCAP analysis is pattern recognition. The infected host doesn't announce itself —
it leaves statistical fingerprints: anomalously many destinations, suspicious
DNS queries, beaconing intervals. Wireshark is just the microscope;
the analyst's job is to know what's suspicious.

**Real-world application:** Same workflow runs in SOC L2 daily — only the
toolset is Splunk/Sentinel instead of Wireshark, and the data feeds are
NetFlow/Zeek instead of raw PCAP.
