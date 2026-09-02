# SOC Incident Investigation Report: Case 01

| Parameter | Details |
| :--- | :--- |
| **Incident ID** | INC-2026-001 |
| **Severity** | High |
| **Investigator** | Umar Farooq |
| **Status** | Closed (Mitigated) |
| **Dataset Source** | DarkGate Malware Activity (2023-10-25) |

---

## 1. Executive Summary
During threat hunting operations within network traffic captures, high-frequency anomalous DNS queries were observed originating from an internal workstation. Analysis confirmed that host `10.10.25.101` was infected with DarkGate malware, which repeatedly queried suspicious domain names to resolve command and control (C2) infrastructure.

---

## 2. Investigation Details

### Host & Network Identifiers
- **Source Host (Victim IP):** `10.10.25.101`
- **DNS Server / Gateway IP:** `10.10.25.1`
- **Protocol:** DNS (UDP Port 53)

### Wireshark Filtering Methodology
1. Applied display filter to isolate outbound DNS requests:
   ```text
   dns.flags.response == 0
   ---

## 3. Indicators of Compromise (IOCs)
- **Threat Vector:** DarkGate Malware Campaign
- **Protocol:** DNS (UDP Port 53)
- **Suspicious Domain / C2 Query:** Host resolution queries linked to malicious external infrastructure.

---

## 5. Risk & Impact Assessment
DNS queries associated with known malware families like DarkGate indicate active command-and-control (C2) communication or initial payload retrieval attempts. Unfiltered DNS resolution allows infected internal hosts to maintain persistent remote communication with attacker infrastructure.

---

## 6. Recommendations & Mitigation
1. **DNS Sinkholing:** Add identified malicious domains to internal DNS sinkholes and secure DNS resolvers (e.g., Quad9, Cloudflare Teams).
2. **Host Quarantine:** Isolate the originating internal host machine from the network to conduct full endpoint detection and response (EDR) remediation.
3. **Egress Filtering:** Block outbound DNS traffic that bypasses designated internal enterprise DNS servers.