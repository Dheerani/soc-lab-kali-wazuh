# BILLION LAUGHS DETECTION REPORT

## Executive Summary
- Detection Type: Billion Laughs (XML Entity Expansion DoS)
- Agent: kali (192.168.1.109)
- Web Server: Apache2
- Target: /var/www/html/billionlaughs.php
- Total Alerts: 3
- Time Period: 2026-10-10 16:53:32 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 31122 | Web server 500 error code (Internal Error) | 5 | T1190 |

## Attack Payloads Detected

1. **Small Billion Laughs:**
   POST /billionlaughs.php with 4-level entity expansion

2. **Medium Attack:**
   POST /billionlaughs.php with 6-level entity expansion

3. **Massive Attack:**
   POST /billionlaughs.php with 8-level entity expansion

## MITRE ATT&CK Mapping
- **T1499** - Endpoint Denial of Service
- **T1499.002** - Service Exhaustion Flood
- **Tactic:** Impact

## Key Findings
1. Wazuh detected XML entity expansion attempts
2. PHP rejected entity expansion (safe by default)
3. Server returned 500 error on malicious XML
4. Real SOC: block IP, disable entity expansion
5. Lab: authorized test

## Analysis
- Billion Laughs is a DoS attack via XML entity expansion
- Attacker sends small XML that expands to GB in memory
- PHP's DOMDocument blocks this by default
- Real SOC: block IP, limit XML entity depth

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block source IP
3. **Real SOC:** Disable DTD processing
4. **Real SOC:** Limit entity expansion depth
5. **Improvement:** Add Billion Laughs rules
6. **Improvement:** Integrate Suricata

## Status
**CLOSED** - Lab simulation

## Analyst Notes
Billion Laughs (also known as XML Bomb) is a classic DoS attack.
It allows:
- Memory exhaustion
- CPU exhaustion
- Service crash
- Denial of Service

**Note:** PHP's `DOMDocument` blocks entity expansion by default.
To make this attack work, `LIBXML_NOENT` must be enabled.

Detection relies on:
- XML body inspection
- ENTITY pattern detection
- Response code monitoring (500 errors, timeouts)
- Wazuh built-in rules (31100-31199)
