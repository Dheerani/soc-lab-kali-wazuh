# WEB SHELL DETECTION REPORT

## Executive Summary
- Detection Type: Web Shell Upload & Execution
- Agent: kali (192.168.1.109)
- Web Server: Apache2
- Target: /var/www/html/upload.php
- Total Alerts: 3
- Time Period: 2026-10-11 11:29:48 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 31514 | Simple shell.php command execution | 6 | T1505.003 |

## Attack Payloads Detected

1. **Web Shell Upload:**
   POST /upload.php with shell.php

2. **Command Execution:**
   GET /uploads/shell.php?cmd=whoami
   GET /uploads/shell.php?cmd=id
   GET /uploads/shell.php?cmd=cat /etc/passwd

## MITRE ATT&CK Mapping
- **T1505.003** - Web Shell
- **T1059** - Command and Scripting Interpreter
- **Tactic:** Persistence, Execution

## Key Findings
1. Web shell uploaded successfully
2. Commands executed as `www-data` user
3. Wazuh Rule 31514 detected execution
4. Real SOC: remove shell, patch upload, investigate

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Remove web shell
3. **Real SOC:** Patch file upload validation
4. **Real SOC:** Check for other shells
5. **Improvement:** Add web shell rules

## Status
**CLOSED** - Lab simulation

## Analyst Notes
Web Shell is a critical web vulnerability.
It allows:
- Remote command execution
- File system access
- Persistence
- Full server compromise

Detection relies on:
- File upload monitoring
- Command execution patterns
- Response code analysis
- Wazuh built-in rules (31100-31599)
