# 🚨 SOC Incident Investigation Report: Case 03

| **Parameter** | **Details** |
| :--- | :--- |
| **Incident ID** | `INC-2026-003` |
| **Severity** | 🟠 **Medium** |
| **Investigator** | **Umar Farooq** |
| **Status** | 🔒 **Closed (Mitigated)** |
| **Dataset Source** | Network Reconnaissance & Port Scanning Capture |

---

## 1. Executive Summary
> **Incident Overview:** Automated **TCP SYN port scanning activity** was detected targeting enterprise endpoints.

- **Primary Source:** External IP `93.174.93.12` executed high-frequency TCP SYN probes against host `203.161.44.208`.
- **Core Risk:** Active port scanning and host discovery permit malicious actors to map running services and identify vulnerable entry points prior to targeted exploitation.

---

## 2. Investigation Details

### 📌 Host & Network Identifiers
- **Attacker Host (Source IP):** `93.174.93.12`
- **Target Host (Destination IP):** `203.161.44.208`
- **Targeted Ports:** TCP Ports **80, 9627, 9875, 19149, 13761, 18964, 44386, 9090**
- **Scan Type:** TCP SYN Stealth Scan (`-sS`)

### 🔍 Wireshark Filtering Methodology
1. Applied display filter to isolate half-open connection attempts *(SYN requests without ACK)*:
   ```text
   tcp.flags.syn == 1 && tcp.flags.ack == 0

   Inspected packet frame #1 and expanded the Transmission Control Protocol flag structure to confirm initial SYN sequence initialization (Syn: Set (1)).

3. Indicators of Compromise (IOCs)
Scanning Host IP: 93.174.93.12

Target Endpoint IP: 203.161.44.208

Probed Protocols: HTTP (80), custom TCP high ports

4. Evidence
Figure 1: Wireshark packet capture displaying automated TCP SYN probes targeting multiple destination ports.

5. Risk & Impact Assessment
Reconnaissance activity allows threat actors to map exposed network services, identify operating systems, and isolate unpatched host applications. Automated SYN sweeps typically act as a direct precursor to targeted vulnerability exploitation.

6. Recommendations & Mitigation
🛡️ Perimeter Blocking: Drop incoming traffic from scanning IP 93.174.93.12 at the perimeter firewall.

⚙️ IDS Threshold Tuning: Configure IDS/IPS rules (e.g., Snort/Suricata) to automatically trigger alerts and temporarily drop connections exceeding high-frequency TCP SYN thresholds from single external IPs.

🔐 Minimize Attack Surface: Enforce firewall rules to restrict public accessibility of non-essential open TCP ports. 