# 22 — Risk Assessment Case Studies (Practical Scenarios)

Five real-world risk assessment scenarios applying the **3x3 risk matrix
methodology** (Likelihood × Impact) to everyday situations.
This exercise translated abstract risk management concepts into concrete,
relatable scenarios — the kind of risk thinking that should be second
nature for any security professional.

## What I did
For each scenario, performed a full risk assessment cycle:
1. **Identify threats** — what could go wrong?
2. **Assess risk** — what's the likelihood and impact?
3. **Plot on 3x3 matrix** — derive the risk level (Low / Medium / High)
4. **Choose treatment strategy** — Avoid / Mitigate / Transfer / Accept
5. **Define concrete mitigation steps** — specific technical and procedural controls
6. **Reassess residual risk** — what's left after controls are applied?

### Scenario 1: Guest on home network
- **Threats:** unauthorized access to NAS backups, malware spreading to local
  devices, network traffic sniffing
- **Initial risk:** Medium likelihood × High impact = **HIGH**
- **Strategy:** Mitigation via **Guest Network with AP Isolation**
  (separate SSID, WPA2/WPA3 password, "disable access to local network")
- **Alternative:** mobile phone hotspot if router doesn't support guest network
- **Residual risk:** reduced to **Medium/Low**

### Scenario 2: Critical EoL router vulnerability (CVSS 10.0 RCE)
- **Context:** publicly disclosed unpatched vulnerability with maximum severity
- **Initial risk:** High likelihood × High impact = **CRITICAL**
- **Strategy:** Defense-in-depth mitigation since no patch exists
- **Mitigation layers:**
  - Disable ICMP responses on WAN interface
  - Disable remote management
  - Configure aggressive WAN-side firewall rules
  - Plan device replacement within defined timeline
- **Long-term:** **transfer** the risk by replacing the EoL device

### Scenario 3: Cloud backup vs. local-only backup
- **Threat analysis:** ransomware, hardware failure, theft, fire/flood
- **Risk comparison:** local-only backup has Low likelihood × Critical impact
  (single point of failure)
- **Strategy:** Implement **3-2-1 backup rule** (3 copies, 2 media types,
  1 offsite)
- **Tools considered:** cloud storage with versioning, encrypted offsite
  drives, immutable cloud backups

### Scenario 4: Buying a used laptop
- **Threats:** pre-installed malware, hidden hardware modifications,
  drive remnants of previous owner's data
- **Mitigation:** factory reset → secure wipe of drive (multi-pass) →
  fresh OS install from known-good media → verify BIOS/firmware integrity →
  check for hardware tampering

### Scenario 5: Public TV display in restaurant
- **Threats:** display showing inappropriate content (compromised TV/source),
  network attack via smart TV, customer device compromise via shared WiFi
- **Mitigation:** isolated VLAN for public displays, restricted internet
  access, separate guest WiFi network with content filtering, regular
  firmware updates on TV/streaming devices

## Files
- `Zadanie_16.pdf` — full 20-page risk assessment document covering all
  5 scenarios with matrices, decision trees, and step-by-step mitigation
  procedures

## Takeaway
**Risk assessment is a transferable skill across every cybersecurity role.**
Whether I'm a SOC analyst (assessing alert severity), a GRC analyst
(evaluating organizational controls), or eventually a security manager
(prioritizing budget), the same 3x3 framework applies.

What this exercise reinforced:

1. **Risk = Likelihood × Impact.** This is the central equation. Either
   factor being low (or eliminated) reduces the overall risk.
   You can attack risk from two angles, not one.

2. **Mitigation strategies have a hierarchy:**
   - **Avoid** — eliminate the activity creating the risk (best when feasible)
   - **Mitigate** — reduce likelihood or impact through controls (most common)
   - **Transfer** — pay someone else to bear the risk (insurance, outsourcing)
   - **Accept** — explicit decision to live with the risk (when controls
     would cost more than the impact)

3. **Residual risk is real.** No mitigation reduces risk to zero. The
   question is always "is the residual risk acceptable to the
   risk owner?" — and that decision must be **documented**.

4. **Risk assessments must be revisited.** Yesterday's "low likelihood"
   becomes today's "high likelihood" when threat landscape changes
   (e.g., a CVE goes from theoretical to mass-exploited).

5. **The scenarios that feel mundane are the highest-value training.**
   Anyone can theoretically discuss "advanced persistent threats."
   Far fewer people can clearly explain to a non-technical family member
   **why a guest network matters** — that's the communication skill
   security professionals get paid for.

This exercise was my first real attempt to **think in risk-management
terms** rather than just technical terms. That mental shift is what
separates a technician from a security professional.
