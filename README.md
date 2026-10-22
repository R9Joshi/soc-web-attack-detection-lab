# soc-web-attack-detection-lab
Blue Team SOC Detection Lab using OWASP Juice Shop, ModSecurity WAF, OWASP CRS, Wazuh SIEM, Burp Suite and MITRE ATT&amp;CK.
# SOC Detection Lab
### Web Attack Detection using ModSecurity + Wazuh SIEM

---

## Overview

This project demonstrates a complete Blue Team detection pipeline where real web attacks are generated against OWASP Juice Shop, detected by ModSecurity (OWASP CRS), forwarded to Wazuh SIEM, and mapped to MITRE ATT&CK.

Instead of only exploiting a vulnerable application, this project focuses on the SOC analyst perspective:

- Detecting attacks
- Collecting forensic evidence
- Writing custom Wazuh detection rules
- Mapping detections to MITRE ATT&CK
- Validating alerts inside Wazuh Dashboard

---

# Architecture

![Architecture](architecture/screenshot1.png)

---

# Detection Pipeline

```
Attacker
    │
    ▼
Burp Suite
    │
    ▼
Apache Reverse Proxy
    │
    ▼
ModSecurity WAF
    │
    ▼
OWASP CRS
    │
    ▼
modsec_audit.log
    │
    ▼
Wazuh Agent
    │
    ▼
Wazuh Manager
    │
    ▼
OpenSearch Dashboard
```

---

# Lab Environment

| Component | Version |
|-----------|---------|
| Windows 11 | Host OS |
| Apache | 2.4.58 |
| ModSecurity | 2.9.6 |
| OWASP CRS | 3.3.5 |
| Wazuh | 4.x |
| Docker | Latest |
| Juice Shop | Latest |
| Burp Suite Community | 2026 |
| OpenSearch Dashboard | Included |

---

# Attack Scenarios

## SQL Injection (Login Bypass)

Payload

```json
{
 "email":"' OR 1=1--",
 "password":"x"
}
```

Detected by

- CRS 942100
- Wazuh Rule 100501

MITRE

T1190

---

## UNION SQL Injection

Payload

```
apple' UNION SELECT ...
```

Detected by

- CRS 942260
- Wazuh Rule 100502

MITRE

T1190

---

## Cross Site Scripting (XSS)

Payload

```
<script>alert(1)</script>
```

Detected by

- CRS 941110
- CRS 941160
- Wazuh Rule 100500

---

# Custom Wazuh Rules

| Rule ID | Description |
|----------|-------------|
|100500|ModSecurity XSS Detection|
|100501|SQL Injection Detection|
|100502|UNION SQL Injection Detection|

---

# Screenshots

## Lab Setup

![Screenshot](screenshots/screenshot1.png)

---

## SQL Injection Detection

![Screenshot](screenshots/screenshot2.png)

---

## UNION SQLi Detection

![Screenshot](screenshots/screenshot3.png)

---

## XSS Detection

![Screenshot](screenshots/screenshot4.png)

---

## Wazuh Dashboard

![Screenshot](screenshots/screenshot5.png)

---

# Project Structure

```
soc-detection-lab-modsecurity-wazuh
│
├── README.md
│
├── screenshots
│   ├── screenshot1.png
│   ├── screenshot2.png
│   ├── screenshot3.png
│   ├── screenshot4.png
│   └── screenshot5.png
│
├── configs
│   ├── apache
│   ├── modsecurity
│   └── wazuh-agent
│
├── wazuh
│   ├── local_decoder.xml
│   └── local_rules.xml
│
├── attacks
│   ├── login-bypass.md
│   ├── union-sqli.md
│   └── xss.md
│
├── evidence
│   └── sample-modsec-audit.json
│
└── docs
    └── challenges.md
```

---

# MITRE ATT&CK Mapping

| Technique | ID |
|------------|-----|
| Exploit Public Facing Application | T1190 |
| JavaScript | T1059.007 |

---

# Key Skills Demonstrated

- Web Application Security
- ModSecurity
- OWASP CRS
- Wazuh SIEM
- Detection Engineering
- JSON Log Parsing
- Custom Rule Development
- MITRE ATT&CK Mapping
- SOC Investigation
- Burp Suite
- Apache Reverse Proxy
- Docker

---

# Future Improvements

- LFI Detection
- RCE Detection
- Command Injection Detection
- Saved Wazuh Dashboards
- Sigma Rules
- Detection Tuning
- False Positive Analysis

---

# Author

**Rishabh Joshi**

MCA Student

SOC Analyst

GitHub

https://github.com/R9Joshi
