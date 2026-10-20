# HOST HEADER INJECTION DETECTION REPORT

## Executive Summary
- Detection Type: Host Header Injection
- Agent: kali (192.168.1.109)
- Web Server: Apache2
- Target: /var/www/html/host.php
- Total Alerts: 0 (detected via logs)
- Time Period: 2026-10-10 20:14:03 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| N/A | Detected via Apache access log | N/A | T1190 |

## Attack Payloads Detected

1. **Basic Host Injection:**
   Host: evil.com

2. **X-Forwarded-Host:**
   X-Forwarded-Host: evil.com

3. **Multiple Host Headers:**
   Host: localhost, Host: evil.com

4. **Absolute URL:**
   Request-Target: http://evil.com/host.php

5. **Port Injection:**
   Host: evil.com:8080

6. **Newline Injection:**
   Host: localhost%0d%0aX-Injected: evil

## MITRE ATT&CK Mapping
- **T1190** - Exploit Public-Facing Application
- **Tactic:** Initial Access

## Key Findings
1. Host header injection detected in logs
2. Server accepts arbitrary Host headers
3. Password reset link manipulable
4. Real SOC: block IP, validate Host header
5. Lab: authorized test

## Analysis
- Host Header Injection allows password reset poisoning
- Attacker can redirect users to malicious site
- Real SOC: block IP, whitelist Host headers
- Lab: authorized test

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block source IP
3. **Real SOC:** Whitelist allowed Host headers
4. **Real SOC:** Use absolute URLs in emails
5. **Improvement:** Add host header rules
6. **Improvement:** Integrate Suricata

## Status
**CLOSED** - Lab simulation

## Analyst Notes
Host Header Injection is a web vulnerability.
It allows:
- Password reset poisoning
- Cache poisoning
- Bypass access controls
- XSS via host reflection

Detection relies on:
- HTTP Host header analysis
- X-Forwarded-Host patterns
- Response code monitoring
- Wazuh built-in rules (31100-31199)

