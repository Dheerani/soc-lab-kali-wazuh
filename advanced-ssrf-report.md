# ADVANCED SSRF DETECTION REPORT

## Executive Summary
- Detection Type: Advanced Server-Side Request Forgery (SSRF)
- Agent: kali (192.168.1.109)
- Web Server: Apache2
- Target: /var/www/html/ssrf2.php
- Total Alerts: 3
- Time Period: 2026-10-10 16:49:19 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 31122 | Web server 500 error code (Internal Error) | 5 | T1190 |

## Attack Payloads Detected

1. **AWS Metadata:**
   GET /ssrf2.php?url=http://169.254.169.254/latest/meta-data/iam/security-credentials/

2. **GCP Metadata:**
   GET /ssrf2.php?url=http://metadata.google.internal/computeMetadata/v1/

3. **Azure Metadata:**
   GET /ssrf2.php?url=http://169.254.169.254/metadata/instance?api-version=2021-02-01

4. **File Read via SSRF:**
   GET /ssrf2.php?url=file:///etc/passwd

5. **Bypass Localhost Filter:**
   GET /ssrf2.php?url=http://0177.0.0.1/

## MITRE ATT&CK Mapping
- **T1190** - Exploit Public-Facing Application
- **T1552.005** - Cloud Instance Metadata API
- **Tactic:** Initial Access, Credential Access

## Key Findings
1. **/etc/passwd successfully read via SSRF** ⚠️
2. Cloud metadata endpoints reachable
3. File protocol allowed (file:///)
4. Real SOC: block IP, restrict URL schemes
5. Lab: authorized test

## Analysis
- SSRF allows server to make requests to internal/external resources
- Attacker can read local files, scan internal network, steal cloud credentials
- **This is a critical vulnerability**
- Real SOC: block IP, validate URLs, use allowlist, restrict protocols

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block source IP
3. **Real SOC:** Whitelist allowed domains
4. **Real SOC:** Disable file://, gopher://, dict:// protocols
5. **Real SOC:** Use IMDSv2 for cloud metadata
6. **Improvement:** Add advanced SSRF rules
7. **Improvement:** Integrate Suricata

## Status
**CLOSED** - Lab simulation

## Analyst Notes
Advanced SSRF is one of the most dangerous web vulnerabilities.
It allows:
- Reading arbitrary files (file://)
- Cloud credential theft (169.254.169.254)
- Internal network scanning
- Bypass firewalls

**Critical finding:** Server read `/etc/passwd` via SSRF.
In production, this could leak SSH keys, config files, credentials.

Detection relies on:
- URL parameter analysis
- Internal IP detection (169.254.x.x, 127.0.0.1)
- Protocol detection (file://, gopher://, dict://)
- Response code monitoring (500 errors)
- Wazuh built-in rules (31100-31199)
