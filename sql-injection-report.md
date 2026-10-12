# SQL INJECTION DETECTION REPORT

## Executive Summary
- Detection Type: SQL Injection Attack
- Agent: kali (192.168.1.109)
- Web Server: Apache2
- Target: /var/www/html/login.php
- Total SQLi Alerts: 2
- Time Period: 2026-10-09 15:27:33 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 31106 | Web attack returned code 200 | 6 | T1190 |
| 31101 | Web server 400 error code | 5 | T1190 |

## Attack Payloads Detected

1. **Basic SQLi:**
   GET /login.php?username=admin'&password=anything

2. **OR 1=1 Bypass:**
   GET /login.php?username=admin' OR '1'='1&password=anything

3. **UNION-based:**
   GET /login.php?username=1' UNION SELECT 1,2,3--&password=x

4. **Comment-based:**
   GET /login.php?username=admin'--&password=x

5. **Time-based Blind:**
   GET /login.php?username=1' AND SLEEP(5)--&password=x

## MITRE ATT&CK Mapping
- **T1190** - Exploit Public-Facing Application
- **Tactic:** Initial Access

## Key Findings
1. Wazuh detected SQL injection payloads in URL parameters
2. Multiple injection techniques tested
3. All attacks logged in Apache access.log
4. Wazuh rules fired correctly

## Analysis
- SQL Injection = #1 in OWASP Top 10
- Attacker can bypass authentication
- Attacker can extract database contents
- Real SOC: block IP, patch application, deploy WAF

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block source IP
3. **Real SOC:** Deploy WAF (ModSecurity)
4. **Real SOC:** Use parameterized queries
5. **Improvement:** Add more SQLi rules
6. **Improvement:** Integrate Suricata

## Status
**CLOSED** - Lab simulation

## Analyst Notes
SQL Injection is one of the most dangerous web attacks.
Detection relies on:
- URL parameter analysis
- Response code monitoring
- Apache access log parsing
- Wazuh built-in rules (31100-31199)
