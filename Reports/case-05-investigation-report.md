# 🚨 SOC Incident Investigation Report: Case 05

| **Parameter** | **Details** |
| :--- | :--- |
| **Incident ID** | `INC-2026-005` |
| **Severity** | 🔴 <mark style="background-color: #fee2e2; color: #dc2626; padding: 2px 6px; border-radius: 4px; font-weight: bold;">High</mark> |
| **Investigator** | **Umar Farooq** |
| **Status** | 🔒 <mark style="background-color: #e0f2fe; color: #0284c7; padding: 2px 6px; border-radius: 4px; font-weight: bold;">Closed (Mitigated)</mark> |
| **Dataset Source** | AgentTesla Data Exfiltration Traffic (FTP) |

---

## 1. Executive Summary
> **Incident Overview:** Cleartext data exfiltration via FTP was identified originating from internal workstation `10.1.31.101` infected with AgentTesla spyware.

- **Primary Source:** Internal host `10.1.31.101` initiated unencrypted FTP sessions to external adversary server `93.89.225.40` using compromised account `pgizemM6`.
- **Core Risk:** <mark style="background-color: #e0f2fe; color: #0369a1; padding: 2px 4px; border-radius: 3px;">Cleartext transmission of harvested credentials and sensitive browser data (`PW_david.miller-...html`) to external threat infrastructure.</mark>

---

## 2. Investigation Details

### 📌 Host & Network Identifiers
- **Victim Workstation (Source IP):** `10.1.31.101`
- **Exfiltration FTP Server (Destination IP):** `93.89.225.40`
- **Compromised FTP User:** `pgizemM6`
- **Observed Exfiltrated File:** `PW_david.miller-DESKTOP-WE9H2FM_2025_01_31_20_24_25.html`

### 🔍 Wireshark Filtering Methodology
1. Filtered traffic stream for File Transfer Protocol:
   ```text
   ftp

   Analyzed authentication packets (USER, PASS) and identified active payload transfer commands (STOR).

3. Indicators of Compromise (IOCs)
Victim Internal IP: 10.1.31.101

Adversary FTP Infrastructure: 93.89.225.40

Malicious Storage Command: STOR PW_david.miller-DESKTOP-WE9H2FM_2025_01_31_20_24_25.html

Threat Malware Family: AgentTesla Spyware

4. Evidence
Figure 1: Wireshark packet capture displaying AgentTesla outbound FTP file upload (STOR) commands to 93.89.225.40.

5. Risk & Impact Assessment
AgentTesla keyloggers extract stored browser credentials, desktop telemetry, and system passwords. Cleartext FTP transmission allows external eavesdropping and grants threat actors direct access to user account david.miller and associated enterprise assets.

6. Recommendations & Mitigation
☣️ Endpoint Containment: Instantly isolate host 10.1.31.101 via EDR to terminate ongoing FTP exfiltration sessions.

🛡️ Perimeter Blocking: Block destination IP 93.89.225.40 and restrict outbound unencrypted FTP (Port 21) across network firewalls.

🔑 Credential Revocation: Force password resets and revoke active OAuth tokens for host user david.miller.