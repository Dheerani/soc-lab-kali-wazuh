# OPEN REDIRECT DETECTION REPORT

## Executive Summary
- Detection Type: Open Redirect
- Agent: kali (192.168.1.109)
- Web Server: Apache2
- Target: /var/www/html/redirect.php
- Total Alerts: 3
- Time Period: 2026-10-10 14:58:11 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 31105 | XSS attempt | 6 | T1190 |

## Attack Payloads Detected

1. **Basic Open Redirect:**
   GET /redirect.php?url=http://evil.com

2. **HTTPS Redirect:**
   GET /redirect.php?url=https://evil.com

3. **Protocol-Relative:**
   GET /redirect.php?url=//evil.com

4. **Data URI Redirect:**
   GET /redirect.php?url=data:text/html,<script>alert(1)</script>

## MITRE ATT&CK Mapping
- **T1190** - Exploit Public-Facing Application
- **Tactic:** Initial Access

## Key Findings
1. Wazuh detected redirect attempts
2. Open redirect allows phishing
3. Data URI redirect allows XSS
4. Real SOC: block IP, whitelist domains
5. Lab: authorized test

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block source IP
3. **Real SOC:** Whitelist allowed domains
4. **Real SOC:** Validate redirect URLs
5. **Improvement:** Add redirect rules
6. **Improvement:** Integrate Suricata

## Status
**CLOSED** - Lab simulation

## Analyst Notes
Open Redirect is a common web vulnerability.
It allows:
- Phishing attacks
- Credential theft
- XSS via data URIs

Detection relies on:
- Redirect parameter analysis
- Location header monitoring
- XSS pattern detection
- Wazuh built-in rules (31100-31199)
