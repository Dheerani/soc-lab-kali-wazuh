# DETECTION ENGINEERING PORTFOLIO

## SOC Analyst Lab — Wazuh SIEM

**Analyst:** Hello
**Date:** 2026-10-10
**Environment:** Wazuh 4.14.7 + Apache2 + Kali Linux
**Total Detections:** 25
**Total Reports:** 25

---

## 1. Network Reconnaissance

| # | Detection | Rule ID | MITRE | Report |
|---|-----------|---------|-------|--------|
| 1 | Nmap Scan | 100003 | T1046 | nmap-detection-report.md |

**Real SOC Action:** Block source IP, review firewall logs, check for follow-up exploitation.

---

## 2. Credential Access

| # | Detection | Rule ID | MITRE | Report |
|---|-----------|---------|-------|--------|
| 2 | SSH Brute Force | 100002 | T1110 | incident-report-002.md |
| 3 | SSH Failed Login | 100001 | T1110 | incident-report-002.md |

**Real SOC Action:** Block source IP, review auth.log, check if any login succeeded.

---

## 3. File Integrity Monitoring

| # | Detection | Rule ID | MITRE | Report |
|---|-----------|---------|-------|--------|
| 4 | File Added | 554 | T1565.001 | fim-incident-report.md |
| 5 | File Modified | 550 | T1565.001 | fim-incident-report.md |
| 6 | File Deleted | 553 | T1565.001 | fim-incident-report.md |

**Real SOC Action:** Verify with change management, review user activity.

---

## 4. Rootkit Detection

| # | Detection | Rule ID | MITRE | Report |
|---|-----------|---------|-------|--------|
| 7 | Rootkit | Rootcheck | T1014 | (built-in) |

**Real SOC Action:** Isolate host, run full AV scan, rebuild if confirmed.

---

## 5. Web Application Attacks

| # | Detection | Rule ID | MITRE | Report |
|---|-----------|---------|-------|--------|
| 8 | XSS | 31106 | T1190 | web-attack-report.md |
| 9 | SQL Injection | 31106 | T1190 | sql-injection-report.md |
| 10 | Path Traversal | 31106 | T1083 | path-traversal-report.md |
| 11 | Command Injection | 31106 | T1059 | command-injection-report.md |
| 12 | File Upload (Web Shell) | 31514 | T1505.003 | file-upload-report.md |
| 13 | File Inclusion (LFI/RFI) | 31106 | T1083 | file-inclusion-report.md |
| 14 | SSRF | 31106 | T1190 | ssrf-report.md |
| 15 | XXE | 31122 | T1190 | xxe-report.md |
| 16 | SSTI | 31122 | T1190 | ssti-report.md |
| 17 | Open Redirect | 31105 | T1190 | open-redirect-report.md |
| 18 | Insecure Deserialization | 31122 | T1190 | deserialization-report.md |
| 19 | Log4Shell | 31122 | T1190 | log4shell-report.md |
| 20 | Spring4Shell | 31122 | T1190 | spring4shell-report.md |
| 21 | LDAP Injection | 31122 | T1190 | ldap-injection-report.md |
| 22 | NoSQL Injection | 31122 | T1190 | nosql-injection-report.md |
| 23 | GraphQL Injection | 31122 | T1190 | graphql-injection-report.md |
| 24 | Advanced SSRF | 31122 | T1190 | advanced-ssrf-report.md |
| 25 | Web Cache Poisoning | 31122 | T1190 | cache-poisoning-report.md |
| 26 | Host Header Injection | 31122 | T1190 | host-header-report.md |

**Real SOC Action:** Block source IP, patch application, deploy WAF, review WAF logs.

---

## 6. Denial of Service

| # | Detection | Rule ID | MITRE | Report |
|---|-----------|---------|-------|--------|
| 27 | Billion Laughs (XML Bomb) | 31122 | T1499 | billion-laughs-report.md |

**Real SOC Action:** Block source IP, disable DTD processing, limit entity depth.

---

## 7. Protocol-Level Attacks

| # | Detection | Rule ID | MITRE | Report |
|---|-----------|---------|-------|--------|
| 28 | HTTP Request Smuggling | 31101 | T1190 | smuggling-report.md |

**Real SOC Action:** Block source IP, reject CL/TE conflicts, use HTTP/2.

---

## Custom Rules Written

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 100001 | SSH Failed Login | 10 | T1110 |
| 100002 | SSH Brute Force | 12 | T1110 |
| 100003 | Nmap Scan Detection | 10 | T1046 |

---

## MITRE ATT&CK Coverage

| Tactic | Techniques | Coverage |
|--------|-----------|----------|
| Reconnaissance | T1046 | 100% |
| Initial Access | T1190, T1078 | 80% |
| Execution | T1059 | 100% |
| Persistence | T1505.003, T1078 | 70% |
| Privilege Escalation | T1548.003 | 80% |
| Defense Evasion | T1565 | 40% |
| Credential Access | T1110, T1552.005 | 100% |
| Discovery | T1083 | 100% |
| Impact | T1499 | 100% |

**Overall MITRE Coverage: ~70%**

---

## Skills Demonstrated

- **SIEM:** Wazuh installation, configuration, dashboard
- **Detection Engineering:** 3 custom XML rules
- **Log Analysis:** Apache, SSH, PAM, syslog, journald
- **MITRE ATT&CK:** 15+ technique mappings
- **Incident Response:** 25 professional reports
- **Tools:** Wazuh, Nmap, curl, Apache, ss, tcpdump
- **Web Security:** 18 web attack types detected
- **Network Security:** Nmap detection, port scan analysis

---

## Reports Index

All 25 reports available in `~/soc-portfolio/`.

---

## Contact

- **GitHub:** [Your GitHub]
- **LinkedIn:** [Your LinkedIn]
- **Email:** [Your Email]

---
*Last Updated: 2026-10-10*
