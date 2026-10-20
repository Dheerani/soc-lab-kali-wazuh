# XXE DETECTION REPORT

## Executive Summary
- Detection Type: XML External Entity (XXE) Injection
- Agent: kali (192.168.1.109)
- Web Server: Apache2
- Target: /var/www/html/xml.php
- Total Alerts: 7
- Time Period: 2026-10-10 14:37:20 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 31122 | Web server 500 error code (Internal Error) | 5 | T1190 |

## Attack Payloads Detected

1. **Basic XXE:**
   POST /xml.php with `<!ENTITY xxe SYSTEM "file:///etc/passwd">`

2. **Parameter Entity:**
   POST /xml.php with `<!ENTITY % xxe SYSTEM "file:///etc/passwd">`

3. **XXE SSRF:**
   POST /xml.php with `<!ENTITY xxe SYSTEM "http://169.254.169.254/...">`

4. **Billion Laughs (DoS):**
   POST /xml.php with nested entities

5. **PHP Filter:**
   POST /xml.php with `php://filter/convert.base64-encode/resource=/etc/passwd`

## MITRE ATT&CK Mapping
- **T1190** - Exploit Public-Facing Application
- **T1083** - File and Directory Discovery
- **Tactic:** Initial Access, Discovery

## Key Findings
1. Wazuh detected XXE payloads via 500 errors
2. 5 different XXE techniques tested
3. XXE allows reading arbitrary files
4. XXE can also cause SSRF and DoS

## Analysis
- XXE is a critical XML parsing vulnerability
- Attacker can read files, scan internal network, DoS
- Real SOC: block IP, disable external entities
- Lab: authorized test

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block source IP
3. **Real SOC:** Disable XML external entities
4. **Real SOC:** Use safe XML parsers
5. **Improvement:** Add XXE rules
6. **Improvement:** Integrate Suricata

## Status
**CLOSED** - Lab simulation

## Analyst Notes
XXE is one of the OWASP Top 10 vulnerabilities.
It allows:
- Reading local files
- SSRF attacks
- Denial of Service (Billion Laughs)
- Port scanning

Detection relies on:
- XML body inspection
- DOCTYPE/ENTITY pattern matching
- Response code monitoring (500 errors)
- Wazuh built-in rules (31100-31199)
