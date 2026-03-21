# 🛡️ Cloudflare Infrastructure OSINT Analysis

This project performs a **passive reconnaissance** analysis of Cloudflare's infrastructure, utilizing data collection tools and Python automation scripts for asset consolidation.

## 🚀 Technologies & Toolstack
* **Reconnaissance:** Sublist3r, WhatWeb, HTTPX.
* **Processing:** Python 3.x (Regex, OS).
* **Data Visualization:** CSVKit (csvlook).

## 📂 Project Structure
* `evidencia/`: Contains raw logs obtained from scanning tools.
* `scripts/`: Python scripts for data filtering and normalization (ETL).
* `reportes/`: Final CSV master report with unique identified assets.

## 🛠️ How to Run the Processor
To generate the master report from the collected evidence, execute:
```bash
python3 scripts/procesar_evidencia.py
```

---

## ⚠️ Disclaimer

**This project is for educational and passive auditing purposes only.**

No intrusion attacks, active scanning, or denial-of-service tests 
were performed against Cloudflare's infrastructure. 

The author (Sic4ri0) is not responsible for any misuse 
of this information or the tools provided in this repository. 

Always ensure you have explicit permission before 
conducting any security assessment.

---

## 🔍 Infrastructure & OSINT Analysis

During the reconnaissance phase, an automated analysis was performed on the domain's infrastructure. The following evidence was extracted and analyzed from the `evidencia/whois/whois_filtered.txt` logs.

### 1. Domain Governance & Lifecycle
| Parameter | Technical Data | Analysis |
| :--- | :--- | :--- |
| **Creation Date** | 2009-02-17 | **Established Reputation:** 15+ years of continuous history. |
| **Registry Expiry** | 2033-02-17 | **Anti-Hijacking:** Long-term protection strategy (24-year span). |
| **Last Update** | 2024-01-15 | **Active Maintenance:** Consistent record audits by the IT team. |

### 2. DNS Resilience & Edge Infrastructure
The domain utilizes a high-redundancy Anycast network through **Cloudflare**, distributed across five dedicated Name Servers:
* `NS3.CLOUDFLARE.COM`
* `NS4.CLOUDFLARE.COM`
* `NS5.CLOUDFLARE.COM`
* `NS6.CLOUDFLARE.COM`
* `NS7.CLOUDFLARE.COM`

> **Key Insight:** This configuration ensures **99.99% uptime** and provides a robust defense layer against volumetric DDoS attacks targeting the DNS protocol.

### 3. Evidence Log (WHOIS Raw)
```bash
# Snapshot of the filtered evidence processed by the script
   Updated Date: 2024-01-09T16:45:28Z
   Creation Date: 2009-02-17T22:07:54Z
   Registry Expiry Date: 2033-02-17T22:07:54Z
   Name Server: NS3.CLOUDFLARE.COM
   ... [truncated]

### 3. DNSSEC & Cryptographic Integrity
The infrastructure implements **DNSSEC Extensions**, providing a layer of trust by signing DNS records.
* **Signature Verified:** Detected `RRSIG` records using **Algorithm 13 (ECDSA P-256)**.
* **Protocol Protection:** This setup effectively mitigates **DNS Spoofing** and **Man-in-the-Middle (MitM)** attacks during the resolution phase.
* **Dual-Stack Capability:** Full support for both **IPv4 (A records)** and **IPv6 (AAAA records)**, ensuring global reachability and modern networking standards.

> **Technical Evidence (`dnsdig.txt`):**
> Valid RRSIG signatures detected with expiration dates set for March 2026, confirming real-time cryptographic maintenance.
