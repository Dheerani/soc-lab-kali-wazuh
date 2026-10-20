# FILE UPLOAD ATTACK DETECTION REPORT

## Executive Summary
- Detection Type: Malicious File Upload
- Agent: kali (192.168.1.109)
- Web Server: Apache2
- Target: /var/www/html/upload.php
- Total Alerts: 12
- Time Period: 2026-10-09 18:39:28 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 31514 | Simple shell.php command execution | 6 | T1505.003 |
| 31106 | Web attack returned code 200 | 6 | T1190 |

## Attack Payloads Detected

1. **PHP Shell Upload:**
   POST /upload.php with shell.php

2. **Reverse Shell Script:**
   POST /upload.php with rev.sh

3. **PHP Info File:**
   POST /upload.php with info.php

4. **.htaccess Upload:**
   POST /upload.php with .htaccess

5. **Double Extension:**
   POST /upload.php with shell.php.jpg

## MITRE ATT&CK Mapping
- **T1190** - Exploit Public-Facing Application
- **T1505.003** - Web Shell
- **Tactic:** Initial Access, Persistence

## Key Findings
1. Wazuh detected file upload attempts
2. 5 different upload techniques tested
3. Web shell execution detected (Rule 31514)
4. All attacks logged in Apache access.log

## Analysis
- File Upload allows arbitrary file placement
- Attacker can upload web shells, backdoors
- Real SOC: block IP, validate file types, disable execution
- Lab: authorized test

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block source IP
3. **Real SOC:** Validate file extensions
4. **Real SOC:** Store uploads outside webroot
5. **Improvement:** Add file upload rules
6. **Improvement:** Integrate Suricata

## Status
**CLOSED** - Lab simulation

## Analyst Notes
File Upload is a critical vulnerability.
It allows:
- Web shell upload
- Backdoor placement
- Server compromise
- Persistent access

Detection relies on:
- HTTP POST monitoring
- File extension analysis
- Response code monitoring
- Wazuh built-in rules (31100-31199)
