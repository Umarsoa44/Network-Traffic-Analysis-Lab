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