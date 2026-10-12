# INSECURE DESERIALIZATION DETECTION REPORT

## Executive Summary
- Detection Type: Insecure Deserialization
- Agent: kali (192.168.1.109)
- Web Server: Apache2
- Target: /var/www/html/deserialize.php
- Total Alerts: 5
- Time Period: 2026-10-10 14:58:11 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 31122 | Web server 500 error code (Internal Error) | 5 | T1190 |

## Attack Payloads Detected

1. **Basic Deserialization:**
   GET /deserialize.php?data=O:8:"stdClass":1:{s:4:"test";s:5:"hello";}

2. **Command Injection:**
   GET /deserialize.php?data=O:4:"Exec":1:{s:3:"cmd";s:6:"whoami";}

3. **File Read:**
   GET /deserialize.php?data=O:4:"Read":1:{s:4:"file";s:11:"/etc/passwd";}

4. **Array Injection:**
   GET /deserialize.php?data=a:1:{i:0;s:4:"test";}

## MITRE ATT&CK Mapping
- **T1190** - Exploit Public-Facing Application
- **T1059** - Command and Scripting Interpreter
- **Tactic:** Initial Access, Execution

## Key Findings
1. Wazuh detected deserialization attempts
2. Insecure deserialization allows code execution
3. Real SOC: block IP, avoid unserialize()
4. Lab: authorized test

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block source IP
3. **Real SOC:** Avoid unserialize() on user input
4. **Real SOC:** Use JSON instead
5. **Improvement:** Add deserialization rules
6. **Improvement:** Integrate Suricata

## Status
**CLOSED** - Lab simulation

## Analyst Notes
Insecure Deserialization is a critical web vulnerability.
It allows:
- Arbitrary code execution
- File system access
- Reverse shells
- Full server compromise

Detection relies on:
- Serialized data pattern detection (O:, a:)
- Response code monitoring (500 errors)
- Wazuh built-in rules (31100-31199)
