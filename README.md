# 🛡️ SOC Incident Investigation & Network Traffic Analysis Lab

<br>

> **Professional Portfolio:** Standardized SOC incident response reports, packet analysis artifacts (`.pcap`), and threat evidence compiled from real-world network traffic captures.

<br>

---

<br>
## 📌 Executive Portfolio Summary

This repository serves as a hands-on **SOC Incident Investigation & DFIR Portfolio**, demonstrating end-to-end network traffic analysis across **5 distinct threat vectors**:

- **DNS Malware Beaconing** (*DarkGate Analysis*)
- **Cleartext Credential Harvesting** (*HTTP POST Inspection*)
- **Network Reconnaissance** (*TCP SYN Port Scanning Sweeps*)
- **Adversary Command & Control** (*Cobalt Strike Malleable HTTP C2*)
- **Data Exfiltration** (*AgentTesla Keylogger Exfiltration over Cleartext FTP*)

Each case includes raw packet captures (`.pcap`), detailed investigation reports following a structured 6-phase Incident Response framework, actionable Indicators of Compromise (IOCs), visual Wireshark evidence, and highlighted enterprise mitigation strategies.


## 👤 Author & Analyst Profile

<br>

- **Lead Analyst:** Umar Farooq
- **Focus Areas:** SOC Triage, Network Threat Hunting, Packet Analysis, DFIR
- **Primary Toolkit:** Wireshark, Tshark, VS Code, Git / GitHub Desktop

<br>

---

<br>

## 📂 Project Architecture

<br>

```text
├── Reports/         # Comprehensive Markdown Incident Reports (Cases 01–05)
│
├── Pcaps/           # Packet Capture Evidence Files (.pcap)
│
├── Screenshots/     # High-Resolution Packet Analysis Screenshots
│
└── README.md        # Portfolio Index & IR Framework Overview


📑 Completed Incident CasesCase #Incident ScenarioProtocol & VectorKey Indicator / ArtifactThreat SeverityIncident Report01DarkGate DNS ActivityDNS Malware BeaconingEncoded DNS query patterns🟠 HighView Report02HTTP Credential HarvestingUnencrypted HTTPPlaintext POST payload credentials🔴 CriticalView Report03TCP SYN ReconnaissanceTCP Port Scanningtcp.flags.syn == 1 && tcp.flags.ack == 0🟡 MediumView Report04Cobalt Strike C2 TrafficHTTP Malleable C2Host: tsdassociates.co.sz / /w0ks/🔴 CriticalView Report05AgentTesla ExfiltrationUnencrypted FTPSTOR PW_david.miller...html🔴 CriticalView Report

🔬 Investigation Methodology

All investigations in this portfolio follow a structured 6-phase Incident Response lifecycle:

Traffic Capture Analysis

Filtering raw .pcap files using specific protocol expressions in Wireshark.

Metadata & Signature Extraction

Isolating victim IPs, destination C2 infrastructure, URI paths, and HTTP/FTP payload signatures.

IOC Compilation

Formulating actionable Indicators of Compromise for firewalls and SIEM detection rules.

Visual Evidence Archival

Documenting expanded packet byte details and protocol trees for verification.

Risk & Impact Assessment

Evaluating scope of compromise, data exfiltration risk, and lateral movement potential.

Mitigation & Remediation

Prescribing tactical recommendations (containment, blocking, credential resets).

🚀 How to Navigate This Repository

📄 Read the Reports: Browse the Reports/ directory for full incident documentation.

🧪 Examine Raw PCAPs: Open files in Pcaps/ directly inside Wireshark to verify packet streams.

📸 View Screenshot Evidence: Inspect raw visual proof inside Screenshots/.