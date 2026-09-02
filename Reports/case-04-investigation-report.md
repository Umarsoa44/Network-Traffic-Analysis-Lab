# 🚨 SOC Incident Investigation Report: Case 04

| **Parameter** | **Details** |
| :--- | :--- |
| **Incident ID** | `INC-2026-004` |
| **Severity** | 🔴 <mark style="background-color: #fee2e2; color: #dc2626; padding: 2px 6px; border-radius: 4px; font-weight: bold;">Critical</mark> |
| **Investigator** | **Umar Farooq** |
| **Status** | 🔒 <mark style="background-color: #e0f2fe; color: #0284c7; padding: 2px 6px; border-radius: 4px; font-weight: bold;">Closed (Mitigated)</mark> |
| **Dataset Source** | Cobalt Strike C2 Traffic Capture |

---

## 1. Executive Summary
> **Incident Overview:** Command and Control (C2) beaconing activity was detected originating from internal enterprise endpoints.

- **Primary Source:** Internal victim host `10.0.0.150` established periodic HTTP beaconing channels to external C2 server `192.168.1.50`.
- **Core Risk:** <mark style="background-color: #e0f2fe; color: #0369a1; padding: 2px 4px; border-radius: 3px;">Active C2 channels permit remote adversary execution, privilege escalation, lateral movement, and data exfiltration.</mark>

---

## 2. Investigation Details

### 📌 Host & Network Identifiers
- **Victim Host (Source IP):** `10.0.0.150`
- **C2 Server (Destination IP):** `192.168.1.50`
- **C2 Communication Protocol:** HTTP (`TCP Port 80`) / HTTPS (`TCP Port 443`)
- **Observed Beacon URI:** `/jquery-3.3.1.min.js`

### 🔍 Wireshark Filtering Methodology
1. Filtered network capture for outbound HTTP requests:
   ```text
   http.request

   Analyzed timing intervals and HTTP headers (User-Agent, Cookie, Host) to identify malleable C2 profile signatures.

3. Indicators of Compromise (IOCs)
Victim IP: 10.0.0.150

C2 Infrastructure IP: 192.168.1.50

Beacon URIs: /jquery-3.3.1.min.js

Threat Vector: Cobalt Strike Red Team / Adversary Framework

4. Evidence
Figure 1: Wireshark packet analysis revealing HTTP beaconing requests sent to external C2 server infrastructure.

5. Risk & Impact Assessment
Cobalt Strike beacons provide threat actors with full post-exploitation access over compromised hosts. Immediate risks include credential dumping, kerberoasting, internal network enumeration, and deployment of secondary payloads such as ransomware.

6. Recommendations & Mitigation
☣️ Endpoint Containment: Instantly isolate victim host 10.0.0.150 from the network via EDR agent to halt C2 communications.

🛡️ Perimeter Blocking: Add C2 server IP 192.168.1.50 and associated malicious domain names to firewalls, proxy blocklists, and DNS sinkholes.

🔬 Forensic Analysis: Perform memory analysis and triage artifact collection (LSASS dumps, persistent scheduled tasks) on the victim host.