# PATH TRAVERSAL DETECTION REPORT

## Executive Summary
- Detection Type: Path Traversal Attack
- Agent: kali (192.168.1.109)
- Web Server: Apache2
- Target: /var/www/html/file.php
- Total Alerts: 15
- Time Period: 2026-10-09 15:39:52 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 31106 | Web attack returned code 200 | 6 | T1190 |
| 31101 | Web server 400 error code | 5 | T1190 |

## Attack Payloads Detected

1. **Basic Traversal:**
   GET /file.php?file=../../../../etc/passwd

2. **URL Encoded:**
   GET /file.php?file=..%2F..%2F..%2Fetc%2Fpasswd

3. **Double Encoded:**
   GET /file.php?file=..%252F..%252Fetc%252Fpasswd

4. **Null Byte:**
   GET /file.php?file=../../etc/passwd%00.txt

5. **Windows-style:**
   GET /file.php?file=..\..\..\windows\system32\config\sam

6. **Filter Bypass:**
   GET /file.php?file=....//....//....//etc/passwd

## MITRE ATT&CK Mapping
- **T1083** - File and Directory Discovery
- **T1190** - Exploit Public-Facing Application
- **Tactic:** Discovery, Initial Access

## Key Findings
1. Wazuh detected path traversal payloads
2. Multiple traversal techniques tested
3. All attacks logged in Apache access.log
4. Wazuh rules fired correctly

## Analysis
- Path Traversal allows reading arbitrary files
- Attacker can read /etc/passwd, config files, source code
- Real SOC: block IP, patch application, use WAF
- Lab: authorized test

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block source IP
3. **Real SOC:** Validate file paths
4. **Real SOC:** Use whitelist of allowed files
5. **Improvement:** Add path traversal rules
6. **Improvement:** Integrate Suricata

## Status
**CLOSED** - Lab simulation

## Analyst Notes
Path Traversal is a critical web vulnerability.
Detection relies on:
- URL parameter analysis
- File path pattern matching
- Response code monitoring
- Wazuh built-in rules (31100-31199)

Real impact:
- Sensitive file disclosure
- Source code theft
- Credential harvesting
- Further exploitation
