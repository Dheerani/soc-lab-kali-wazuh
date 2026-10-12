# SSRF DETECTION REPORT

## Executive Summary
- Detection Type: Server-Side Request Forgery (SSRF)
- Agent: kali (192.168.1.109)
- Web Server: Apache2
- Target: /var/www/html/fetch.php
- Total Alerts: 2
- Time Period: 2026-10-09 23:43:33 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 31106 | Web attack returned code 200 | 6 | T1190 |

## Attack Payloads Detected

1. **Basic SSRF:**
   GET /fetch.php?url=http://localhost/

2. **Cloud Metadata:**
   GET /fetch.php?url=http://169.254.169.254/latest/meta-data/

3. **Port Scan (SSH):**
   GET /fetch.php?url=http://127.0.0.1:22

4. **File Protocol:**
   GET /fetch.php?url=file:///etc/passwd

5. **Gopher Protocol:**
   GET /fetch.php?url=gopher://127.0.0.1:6379/_INFO

6. **Dict Protocol:**
   GET /fetch.php?url=dict://127.0.0.1:11211/stat

7. **Internal Admin:**
   GET /fetch.php?url=http://127.0.0.1/admin

8. **AWS Metadata:**
   GET /fetch.php?url=http://169.254.169.254/latest/user-data/

## MITRE ATT&CK Mapping
- **T1190** - Exploit Public-Facing Application
- **T1090** - Proxy
- **Tactic:** Initial Access, Command and Control

## Key Findings
1. Wazuh detected SSRF payloads
2. 8 different SSRF techniques tested
3. Server made requests to internal resources
4. Cloud metadata endpoint accessible

## Analysis
- SSRF allows server to make requests on attacker's behalf
- Attacker can scan internal network
- Attacker can access cloud metadata (credentials!)
- Real SOC: block IP, validate URLs, use allowlist

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block source IP
3. **Real SOC:** Validate URL inputs
4. **Real SOC:** Use URL allowlist
5. **Improvement:** Add SSRF rules
6. **Improvement:** Integrate Suricata

## Status
**CLOSED** - Lab simulation

## Analyst Notes
SSRF is one of the most critical web vulnerabilities.
It allows:
- Internal network scanning
- Cloud metadata access (AWS keys!)
- Bypass firewalls
- Access internal services

Detection relies on:
- URL parameter analysis
- Internal IP detection (127.0.0.1, 169.254.x.x)
- Protocol analysis (file://, gopher://, dict://)
- Response code monitoring
- Wazuh built-in rules (31100-31199)
