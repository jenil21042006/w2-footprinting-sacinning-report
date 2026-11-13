
# 🛡️ Week 2 – Footprinting & Network Discovery (W2-PM-FINAL)

![Kali Linux](https://img.shields.io/badge/Kali-Linux-557C94?logo=kalilinux&logoColor=white)
![WHOIS](https://img.shields.io/badge/WHOIS-Reconnaissance-blue)
![DNSRecon](https://img.shields.io/badge/DNSRecon-DNS%20Enumeration-informational)
![Phase](https://img.shields.io/badge/Phase-1-red)
![Purpose](https://img.shields.io/badge/Purpose-Education%20Only-green)

**Author:** Jenil Patel  
**Program:** Cybersecurity Program at Networkwalks | **Week:** 02  
**Date:** 13 November 2026  
**Module:** W2-PM1 – Multiple Kali Tools

---

## 📑 Table of Contents

1. [Disclaimer](#-disclaimer)
2. [Overview](#-overview)
3. [Lab Setup](#-lab-setup)
4. [Tools Used](#-tools-used)
5. [Footprinting & Reconnaissance](#-footprinting--reconnaissance)
6. [Network Topology Evidence](#-network-topology-evidence)
7. [Summary of Findings](#-summary-of-findings)
8. [Risk Analysis](#-risk-analysis)
9. [Recommendations](#-recommendations)
10. [Key Learnings](#-key-learnings)
11. [Repository Structure](#-repository-structure)
12. [How to Upload This Project to GitHub](#-how-to-upload-this-project-to-github)
13. [Author](#-author)

---

## ⚠️ Disclaimer

This project documents educational reconnaissance and network-discovery activities.

Testing must only be performed on systems that you own or for which you have explicit authorization. The material is intended for education and research purposes only. Unauthorized access to computer systems is illegal in most countries. Every action performed is the responsibility of the person carrying it out.

---

## 📖 Overview

This project documents Week 2 practical activities from my Cybersecurity Program at Networkwalks.

The project focuses on gathering publicly available information about a domain using multiple Kali Linux tools and reviewing the supplied network topology evidence.

| Phase | Goal | Tools |
|-------|------|-------|
| 🔍 Phase 1 – Reconnaissance & Footprinting | Collect information about networkwalks.com | WHOIS, WhatWeb, Nslookup, Curl, Wafw00f, DNSRecon |
| 🗺️ Network Topology Review | Review the supplied network topology | Network topology diagram |

> ℹ️ No exploitation or vulnerability validation was demonstrated in the supplied evidence. The activities documented here focus on information gathering and topology review.

---

## 🧪 Lab Setup

| Item | Details |
|------|---------|
| 🐉 Operating System | Kali Linux |
| 💻 Virtual Environment | Kali Linux terminal environment |
| 🎯 Target Domain | networkwalks.com |
| 🗺️ Network Evidence | 192.168.56.1 connected to localhost |
| 📚 Program | Cybersecurity Program at Networkwalks |
| 📅 Week | 02 |

The target and scope reflect the supplied practical report. Authorization must be confirmed before performing further testing.

---

## 🧰 Tools Used

| Tool | Purpose |
|------|---------|
| 🐉 Kali Linux | Operating environment |
| `whois` | Retrieve domain registration details |
| `whatweb` | Identify website technologies, server and CMS |
| `nslookup` | Resolve domain names into IP addresses |
| `curl -I` | Retrieve HTTP response headers |
| `wafw00f` | Detect Web Application Firewall technology |
| `dnsrecon` | Enumerate DNS records |
| Network Topology Diagram | Visualize the supplied network relationship |

---

# 🔍 Footprinting & Reconnaissance

The following activities were performed using Kali Linux tools against networkwalks.com.

## 1️⃣ WHOIS – Domain Registration Information

```bash
whois networkwalks.com
```

**What it does:**

Retrieves public domain registration information, including registrar, creation date, expiry date and name servers.

**What I found:**

| Field | Value |
|-------|-------|
| Registrar | GoDaddy.com, LLC |
| Creation Date | 2019-11-06 |
| Expiry Date | 2027-11-06 |
| Name Servers | NS6135.HOSTGATOR.COM, NS6136.HOSTGATOR.COM |
| DNSSEC | Unsigned |
| Domain Status | Client transfer, update, renew and delete prohibitions |

💡 **Why it matters:** WHOIS information helps identify domain registration details and name-server infrastructure.

---

## 2️⃣ WhatWeb – Web Technology Fingerprinting

```bash
whatweb networkwalks.com
```

**What it does:**

Identifies technologies used by a website, including web servers, CMS platforms, plugins and scripts.

**What I found:**

- HTTP redirected with 301 Moved Permanently to HTTPS.
- HTTPS returned 200 OK.
- Web Server: Apache.
- CMS: WordPress 7.1.4.
- Plugin: WordPress Download Manager 3.3.76.
- jQuery 3.7.1.
- HTML5 and Google Tag Manager.
- Website Title: Networkwalks Academy.
- Email: info@networkwalks.com.
- Server IP: 192.232.216.135.

💡 **Why it matters:** Technology fingerprinting helps identify publicly exposed software and components that may require security updates.

---

## 3️⃣ Nslookup – DNS Resolution

```bash
nslookup networkwalks.com
```

**What it does:**

Queries DNS to resolve a domain name into its corresponding IP address.

**What I found:**

| Field | Value |
|-------|-------|
| DNS Server | 10.149.143.69 |
| Answer Type | Non-authoritative |
| Domain | networkwalks.com |
| IPv4 Address | 192.232.216.135 |

💡 **Why it matters:** DNS resolution helps identify the IP address associated with a domain.

---

## 4️⃣ Curl – HTTP Response Headers

```bash
curl -I https://networkwalks.com
```

**What it does:**

Retrieves HTTP response headers without downloading the complete webpage.

**What I found:**

- HTTP Response: 200 OK.
- Server: Apache.
- WordPress REST API link visible.
- Set-Cookie header.
- Referrer-Policy header.
- X-Endurance-Cache-Level header.
- X-nginx-cache header.
- Content-Type header.

**Security headers not visible in the displayed output:**

- Strict-Transport-Security
- X-Frame-Options
- X-Content-Type-Options
- Content-Security-Policy

💡 **Why it matters:** HTTP headers provide information about server configuration and browser security policies.

---

## 5️⃣ Wafw00f – Web Application Firewall Detection

```bash
wafw00f networkwalks.com
```

**What it does:**

Identifies whether a website is protected by a Web Application Firewall.

**What I found:**

> The website networkwalks.com is behind ModSecurity (SpiderLabs) WAF.

Number of requests: 2.

💡 **Why it matters:** WAF identification helps understand which defensive technology is detected in front of a web application.

---

## 6️⃣ DNSRecon – DNS Enumeration

```bash
dnsrecon -d networkwalks.com
```

**What it does:**

Enumerates DNS information, including NS, MX, TXT, SPF and SRV records.

**What I found:**

| Record | Result |
|--------|--------|
| DNSSEC | No answer to DNSSEC query |
| SOA | SOA-related lookup issue |
| NS | ns6135.hostgator.com |
| NS | ns6136.hostgator.com |
| BIND Version | 9.16.23-RH |
| MX | mail.networkwalks.com |
| MX IP | 192.232.216.135 |
| TXT | Google site-verification record |
| SPF | SPF TXT record |
| SRV | Multiple autodiscover records pointing to cPanel email-discovery hosts |

The enumeration continued despite the DNSSEC and SOA-related errors.

💡 **Why it matters:** DNS enumeration helps understand publicly visible DNS and email infrastructure.

---

# 🗺️ Network Topology Evidence

The supplied network topology image contains two visible nodes:

- 🟢 192.168.56.1
- ⚫ localhost

Both nodes are connected by a dotted line.

**Observation:**

The topology diagram provides a visual representation of the relationship between the two displayed labels.

**Evidence limitation:**

The supplied topology image does not include the associated scan command, scan profile, subnet range, host count, port results or MAC-address details.

Therefore, this report documents only the information visible in the supplied topology image and does not claim a completed Zenmap scan.

---

# 📊 Summary of Findings

| # | Tool | Key Result |
|---|------|------------|
| 1 | WHOIS | GoDaddy registrar and HostGator name servers |
| 2 | WhatWeb | Apache, WordPress 7.1.4 and WP Download Manager 3.3.76 |
| 3 | Nslookup | 192.232.216.135 |
| 4 | Curl | WordPress REST API and HTTP response headers |
| 5 | Wafw00f | ModSecurity (SpiderLabs) WAF |
| 6 | DNSRecon | BIND version, MX, SPF, TXT and SRV records |
| 7 | Network Topology | 192.168.56.1 connected to localhost |

---

# ⚖️ Risk Analysis

The following findings are potential information-exposure observations, not confirmed vulnerabilities.

| # | Finding | Evidence | Potential Impact | Risk |
|---|---------|----------|------------------|------|
| 1 | Web technology information exposed | WordPress and plugin versions | Helps identify technologies for security review | 🟠 Medium |
| 2 | Server IP identifiable | 192.232.216.135 | Reveals public hosting endpoint | 🟡 Low |
| 3 | HTTP information visible | REST API and caching headers | Helps technology fingerprinting | 🟡 Low |
| 4 | WAF technology identifiable | ModSecurity | Reveals defensive technology | 🟡 Low |
| 5 | DNS infrastructure exposed | BIND, MX, SPF and SRV records | Helps build infrastructure profile | 🟠 Medium |
| 6 | Topology labels visible | 192.168.56.1 and localhost | Provides limited topology information | Informational |

**Risk Level Key:**

- 🔴 Critical
- 🟠 Medium
- 🟡 Low

The risk levels are indicative observations. A technology version, IP address, DNS record or WAF name does not automatically mean a system is vulnerable.

---

# ✅ Recommendations

1. 🔎 Review publicly exposed technology information.
2. 🔄 Keep WordPress, plugins and server software updated.
3. 🧾 Review HTTP response headers and appropriate security headers.
4. 🌐 Review DNS records regularly.
5. 🛡️ Maintain and monitor the Web Application Firewall.
6. 🗺️ Maintain updated network topology documentation.
7. 📝 Retain complete scan commands, timestamps and output for future network-discovery activities.
8. 🔐 Perform reconnaissance and security testing only with authorization.

---

# 🎓 Key Learnings

- WHOIS provides domain registration information.
- WhatWeb identifies website technologies.
- Nslookup helps resolve domain names into IP addresses.
- Curl helps inspect HTTP response headers.
- Wafw00f identifies reported Web Application Firewall technologies.
- DNSRecon helps enumerate DNS records.
- Network topology diagrams help visualize network relationships.
- Technical observations should not be treated as confirmed vulnerabilities without validation.
- Ethical hacking must always be performed within an authorized scope.

---

# 📁 Repository Structure

Suggested GitHub repository structure:

```text
W2-PM-FINAL-Jenil-Patel/
│
├── README.md
│
├── Jenil_Patel_Week_2_Penetration_Testing_Report_Final.docx
│
└── screenshots/
    ├── 1_whois.png
    ├── 2_whatweb.png
    ├── 3_nslookup.png
    ├── 4_curl_headers.png
    ├── 5_wafw00f.png
    ├── 6_dnsrecon.png
    └── 7_network_topology.png
```

Use your actual screenshot filenames when uploading the evidence.

---

# 🚀 How to Upload This Project to GitHub

### Step 1: Create a project folder

```bash
mkdir W2-PM-FINAL-Jenil-Patel
cd W2-PM-FINAL-Jenil-Patel
```

### Step 2: Initialize Git

```bash
git init
```

### Step 3: Add all project files

```bash
git add .
```

### Step 4: Commit the project

```bash
git commit -m "Add Week 2 Footprinting and Network Discovery Report"
```

### Step 5: Connect your GitHub repository

```bash
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repository>.git
```

### Step 6: Push the project

```bash
git push -u origin main
```

You can also upload everything through GitHub:

1. Open your GitHub repository.
2. Click **Add file**.
3. Select **Upload files**.
4. Upload README.md, the report and screenshots.
5. Click **Commit changes**.

---

## 👤 Author

**Jenil Patel**  
Cybersecurity Student  
Cybersecurity Program at Networkwalks

🔗 **LinkedIn:**  
https://lnkd.in/p/gdXR4SJb

📌 **Project Information:**  
Program: Cybersecurity Program at Networkwalks  
Week: 02  
Project: W2-PM-FINAL  
Topic: Footprinting & Network Discovery

---

⭐ Made for learning – Always Hack Ethically! 🛡️
