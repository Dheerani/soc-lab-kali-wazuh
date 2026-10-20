# WEB ATTACK DETECTION REPORT

## Executive Summary
- Detection Type: Web Application Attack (XSS)
- Agent: kali (192.168.1.109)
- Web Server: Apache2
- Total Web Alerts: 3
- Time Period: 2026-10-08 22:48 to 22:51 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 31101 | Web server 400 error code | 5 | T1190 |
| 31106 | Web attack returned code 200 | 6 | T1190 |
| 31106 | Web attack returned code 200 | 6 | T1190 |

## Attack Payloads Detected

1. **XSS Attempt:**
   GET /shopadmin.asp?Password=abc&UserName=\"><script>alert(foo)</script> HTTP/1.1

2. **ActiveSync Probe:**
   GET /Microsoft-Server-ActiveSync HTTP/1.1

## MITRE ATT&CK Mapping
- **T1190** - Exploit Public-Facing Application
- **Tactic:** Initial Access

## Key Findings
1. Wazuh detected XSS payload in URL parameters
2. Rule 31106 fired with code 200 (potential successful attack)
3. Rule 31101 fired with code 400 (failed attack)
4. Apache logs monitored successfully
5. No actual compromise (test environment)

## Analysis
- Web attacks are a common initial access vector
- XSS = attacker injects JavaScript into web pages
- Real SOC: block source IP, review WAF logs, patch application
- Lab: authorized test

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block source IP
3. **Real SOC:** Deploy WAF (ModSecurity)
4. **Real SOC:** Patch web application
5. **Improvement:** Add more web attack rules
6. **Improvement:** Integrate Suricata for network detection

## Status
**CLOSED** - Lab simulation

## Analyst Notes
Web attack detection is critical for SOC work. It catches:
- SQL Injection (T1190)
- Cross-Site Scripting (T1059.007)
- Path Traversal
- Command Injection
- File Inclusion

Apache access logs provide rich data for web attack detection.
Wazuh's built-in rules cover most OWASP Top 10 attacks.
