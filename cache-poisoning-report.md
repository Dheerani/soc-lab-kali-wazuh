# WEB CACHE POISONING DETECTION REPORT

## Executive Summary
- Detection Type: Web Cache Poisoning
- Agent: kali (192.168.1.109)
- Web Server: Apache2
- Target: /var/www/html/cache.php
- Total Alerts: 0 (detected via logs)
- Time Period: 2026-10-10 20:14:03 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| N/A | Detected via Apache access log | N/A | T1190 |

## Attack Payloads Detected

1. **Basic Cache Poisoning:**
   GET /cache.php with X-Forwarded-Host: evil.com

2. **Cache Key Manipulation:**
   GET /cache.php with X-Forwarded-Host: evil.com, X-Cache-Key: /cache.php?cb=1

3. **Unkeyed Header Injection:**
   GET /cache.php with X-Forwarded-Scheme: nothttps

4. **Cache Deception:**
   GET /cache.php/nonexistent.css

5. **Parameter Cloaking:**
   GET /cache.php?utm_content=x%26callback=evil

## MITRE ATT&CK Mapping
- **T1190** - Exploit Public-Facing Application
- **Tactic:** Initial Access

## Key Findings
1. Cache poisoning attempts detected in logs
2. X-Forwarded-Host header manipulable
3. Server accepts unkeyed headers
4. Real SOC: block IP, validate headers
5. Lab: authorized test

## Analysis
- Web Cache Poisoning exploits cache behavior
- Attacker can serve malicious content to other users
- Real SOC: block IP, sanitize headers, use cache keys
- Lab: authorized test

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block source IP
3. **Real SOC:** Validate X-Forwarded-* headers
4. **Real SOC:** Use cache keys with all headers
5. **Improvement:** Add cache poisoning rules
6. **Improvement:** Integrate Suricata

## Status
**CLOSED** - Lab simulation

## Analyst Notes
Web Cache Poisoning is an advanced web vulnerability.
It allows:
- Serving malicious content to all users
- XSS via cached responses
- Credential theft
- Denial of Service

Detection relies on:
- HTTP header analysis (X-Forwarded-Host, X-Forwarded-Scheme)
- Cache key manipulation patterns
- Response code monitoring
- Wazuh built-in rules (31100-31199)
