# Cloudflare WAF Hardening Ruleset & Edge Security Blueprint

[![Licence MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Cloudflare WAF](https://img.shields.io/badge/Cloudflare-WAF%20Hardened-F38020.svg?logo=cloudflare)](https://cloudflare.com)
[![Language](https://img.shields.io/badge/Language-English%20(New%20Zealand)-green.svg)](README.md)
[![Diagnostics Suite](https://img.shields.io/badge/TAVARDT-Diagnostics-5b3cf5.svg)](https://tools.tavardt.com/nz/security-headers-check/)

Cloudflare WAF custom ruleset and edge security blueprint aligned with NZISM frameworks and CERT NZ cybersecurity guidance.

Engineered and maintained by the cybersecurity engineering practice at **TAVARDT**.

> [!IMPORTANT]
> **Universal & Stack-Agnostic Architecture:** This repository is **not exclusive to WordPress**. It is built for **REST APIs, microservices, modern web applications (Next.js, React), and backend infrastructure (Node.js, Python, Go, PHP, Java)**. The suppression of legacy CMS probes acts as an **active edge hygiene layer**, dropping background bot scans and exploit payloads at Cloudflare edge data centers (< 1ms) before reaching your origin compute.

***

### Multi-Stack Defence Matrix

| Defence Layer | Mitigated Vectors | Protected Workloads & Environments |
| :- | :- | :- |
| **Confidential Asset Isolation** | Perimeter drop for `.env`, `.git`, `.sql`, `package.json`, `composer.json` | **APIs, Next.js, Node.js, Python, Go, Laravel, React** |
| **Scanner & Exploit Suppression** | Block automated suites (Nikto, SQLMap, Acunetix, Masscan, Nmap) | **Any production web service, microservice, or API** |
| **HTTP Verb Sanitisation** | Boundary rejection of unsafe verbs (`TRACE`, `TRACK`, `DEBUG`) | **Production RESTful APIs and gateways** |
| **Privileged Access Gating** | Automated challenges securing administrative entry (`/admin`, `/login`) | **Corporate management consoles, dashboards, ERPs** |
| **Zero-Noise Edge Hygiene** | Edge drop for blind scans targeting `/xmlrpc.php` and trackbacks | **Complete protection of origin server capacity** |

***

## 1. Perimeter Security Architecture

This repository provides production-grade declarative Cloudflare WAF rules to fortify public web infrastructure against unauthorised reconnaissance, data harvesting, and exploit attempts:

* **Confidential Asset & Environment Protection:** Direct edge dropping of requests for `.env` secrets, `.git` version control data, `.sql` backups, and package manifests (`composer.json`, `package.json`).
* **Reconnaissance & Exploit Scanner Mitigation:** Real-time edge suppression of automated vulnerability discovery suites (Nikto, SQLMap, Acunetix, Masscan, Nmap, Gobuster, DirBuster).
* **CMS Attack Surface Hardening:** Active blocking of amplification and brute-force endpoints including `/xmlrpc.php` and `/wp-trackback.php`.
* **Dangerous HTTP Method Blocking:** Rejection of testing or tracing verbs at the CDN layer (`TRACE`, `TRACK`, `DEBUG`).
* **Managed Challenge on Administrative Access:** Frictionless automated challenges securing privileged administration dashboards (`/wp-login.php`, `/admin`).

***

## 2. Security Diagnostic Suite

Benchmark your domain's TLS handshake and HTTP response headers before executing edge configuration changes:

* **Security Headers & Edge TLS Diagnostic:** **TAVARDT Security Headers Analyzer**
* **Engineering Tools Platform:** **TAVARDT Tools New Zealand**

***

## 3. Rapid Deployment

### Option A: Deployment via Cloudflare API v4

Apply the structured ruleset [`rules/ruleset.json`](rules/ruleset.json):

```bash
curl -X PUT "https://api.cloudflare.com/client/v4/zones/YOUR_ZONE_ID/rulesets/phases/http_request_firewall_custom/entrypoint" \
     -H "Authorization: Bearer YOUR_CLOUDFLARE_API_TOKEN" \
     -H "Content-Type: application/json" \
     -data @rules/ruleset.json
```

### Option B: Declarative Management with Terraform

Utilise the Terraform infrastructure file in [`terraform/main.tf`](terraform/main.tf):

```bash
cd terraform
terraform init
terraform plan -var="zone_id=YOUR_ZONE_ID"
terraform apply -var="zone_id=YOUR_ZONE_ID"
```

***

## 4. Engineering Services & Advisory

For comprehensive edge security assessments, NZISM alignment, or managed security architecture:

* **Corporate Portal:** **TAVARDT**
* **Technical Contact:** [Contact Engineering Team](https://ag.tavardt.com/nz/contact/)

***

## Useful Links

* **Corporate Portal:** https://ag.tavardt.com/nz/
* **Diagnostic Suite:** https://tools.tavardt.com/nz/
* **Technical Contact:** https://ag.tavardt.com/nz/contact/

***

### Licence

Distributed under the open-source MIT Licence. View the [`LICENSE`](LICENSE) file for terms.

***

© 2026 TAVARDT. All rights reserved.
