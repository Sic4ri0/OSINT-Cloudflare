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
```

### 4. DNSSEC & Cryptographic Integrity
The infrastructure implements **DNSSEC Extensions**, providing a layer of trust by signing DNS records.
* **Signature Verified:** Detected `RRSIG` records using **Algorithm 13 (ECDSA P-256)**.
* **Protocol Protection:** This setup effectively mitigates **DNS Spoofing** and **Man-in-the-Middle (MitM)** attacks during the resolution phase.
* **Dual-Stack Capability:** Full support for both **IPv4 (A records)** and **IPv6 (AAAA records)**, ensuring global reachability and modern networking standards.

> **Technical Evidence (`dnsdig.txt`):**
> Valid RRSIG signatures detected with expiration dates set for March 2026, confirming real-time cryptographic maintenance.
´´´
---

## 🌐 HTTP Infrastructure Mapping (httpx)

The final stage of the reconnaissance pipeline involved deep fingerprinting of active services using `httpx`. This mapped the functional architecture of the target, revealing service segmentation and security filters.

### 1. Active Services & Public Gateways (HTTP 200)
These represent the "Front-Door" of the organization—fully accessible and operational services.
* **Developer Tools:** `developers.cloudflare.com`, `workers.cloudflare.com`, `pages.cloudflare.com`.
* **Security & Research:** `radar.cloudflare.com`, `research.cloudflare.com`, `rpki.cloudflare.com`.
* **Dashboards:** `one.dash.cloudflare.com` (Zero Trust entrance).

### 2. Hardened Endpoints (HTTP 403 - Forbidden)
Critical discovery: Several subdomains are behind **Active Challenge/WAF filters**.
* **Evidence:** `dash.cloudflare.com`, `community.cloudflare.com`, `support.cloudflare.com`.
* **Insight:** The presence of titles like *"Just a moment..."* and *"Attention Required!"* indicates that these assets are protected by **Cloudflare Turnstile** and **Bot Management** policies, preventing automated scraping or unauthorized bot access.

### 3. Service Redirection & Lifecycle (HTTP 301/302)
* Significant use of redirects for legacy or specialized tools (e.g., `ai.cloudflare.com` -> `playground.ai.cloudflare.com`).
* **Canonical Enforcement:** Continuous redirection to HTTPS ensuring encrypted-only traffic.

### 📊 Infrastructure Snapshot (`mmapa_infra.txt`)
```bash
# Top-tier findings from the httpx automated mapping
[https://help.one.cloudflare.com](https://help.one.cloudflare.com) [200] [Help tool - Cloudflare Zero Trust]
[https://dash.cloudflare.com](https://dash.cloudflare.com) [403] [Attention Required! | Cloudflare]
[https://challenges.cloudflare.com](https://challenges.cloudflare.com) [200] [Cloudflare Turnstile]
[https://one.dash.cloudflare.com](https://one.dash.cloudflare.com) [200] [Cloudflare One]
