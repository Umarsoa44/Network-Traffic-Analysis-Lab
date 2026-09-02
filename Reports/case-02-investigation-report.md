# SOC Incident Investigation Report: Case 02

| Parameter | Details |
| :--- | :--- |
| **Incident ID** | INC-2026-002 |
| **Severity** | High |
| **Investigator** | Umar Farooq |
| **Status** | Closed (Mitigated) |
| **Dataset Source** | Router Credential Harvesting / Exploit Probe Dataset |

---

## 1. Executive Summary
During threat hunting operations, high-frequency HTTP POST traffic was detected targeting internal web management endpoints. External source host `185.125.171.55` executed unencrypted HTTP form submissions targeting the `/boaform/admin/formLogin` endpoint on target server `162.0.237.236`. Transmitting login attempts and form parameters in clear-text over HTTP exposes administrative credentials to Man-in-the-Middle (MitM) interception and automated credential harvesting.

---

## 2. Investigation Details

### Host & Network Identifiers
- **Source Host (Attacker IP):** `185.125.171.55`
- **Target Host (Destination IP):** `162.0.237.236`
- **Target Endpoint:** `/boaform/admin/formLogin`
- **Protocol:** HTTP (TCP Port 80)
- **Content-Type:** `application/x-www-form-urlencoded`

### Wireshark Filtering Methodology
1. Applied display filter to isolate HTTP form submissions:
   ```text
   http.request.method == "POST"

   ---

## 3. Indicators of Compromise (IOCs)
- **Target Endpoint:** `http://162.0.237.236/boaform/admin/formLogin`
- **HTTP Method:** POST
- **Primary Scanning IP:** `185.125.171.55`
- **Secondary Scanning IPs:** `85.31.46.179`, `45.61.185.76`
- **Protocol:** Unencrypted HTTP (TCP Port 80)

---

## 5. Risk & Impact Assessment
Automated bots regularly target unencrypted router management interfaces (`/boaform/admin/formLogin`) to perform brute-force credential stuffing or execute command-injection exploits. Transmitting administrative authentication credentials over unencrypted HTTP allows attackers monitoring network paths to harvest plain-text login parameters.

---

## 6. Recommendations & Mitigation
1. **Disable Clear-Text HTTP:** Disable HTTP access on management interfaces and enforce HTTPS/TLS 1.3 with HSTS.
2. **Access Control:** Restrict administrative access (`/boaform/admin/*`) to trusted management subnets via firewall Access Control Lists (ACLs).
3. **Perimeter Blocking:** Add scanning IP `185.125.171.55` to the perimeter firewall drop list and implement rate limiting on authentication endpoints.