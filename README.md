# SOC Analyst Portfolio — Wazuh Lab

## About Me
Aspiring SOC Analyst with hands-on experience in Wazuh SIEM, custom detection rules, MITRE ATT&CK mapping, and incident response.

## Lab Environment
- **SIEM:** Wazuh 4.14.7
- **Attacker:** Kali Linux
- **Target:** Kali (localhost)
- **Web Server:** Apache2
- **Period:** 6 days

## Detections Implemented

| # | Detection | Rule ID | MITRE | Status |
|---|-----------|---------|-------|--------|
| 1 | SSH Brute Force | 100002 | T1110 | ✅ |
| 2 | Nmap Scan | 100003 | T1046 | ✅ |
| 3 | File Integrity | 550, 553, 554 | T1565 | ✅ |
| 4 | Rootkit | Rootcheck | T1014 | ✅ |
| 5 | Web Attack (XSS) | 31106 | T1190 | ✅ |
| 6 | SQL Injection | 31106 | T1190 | ✅ |
| 7 | Path Traversal | 31106 | T1083 | ✅ |

## Reports

| # | Report | Attack Type | Alerts |
|---|--------|-------------|--------|
| 1 | [SSH Brute Force](incident-report-002.md) | Brute Force | 19 |
| 2 | [File Integrity](fim-incident-report.md) | FIM | 117 |
| 3 | [MITRE Coverage](mitre-coverage-report.md) | Analysis | 686 |
| 4 | [Nmap Detection](nmap-detection-report.md) | Recon | 7 |
| 5 | [Web Attack (XSS)](web-attack-report.md) | XSS | 3 |
| 6 | [SQL Injection](sql-injection-report.md) | SQLi | 2 |
| 7 | [Path Traversal](path-traversal-report.md) | Traversal | 15 |

## Skills Demonstrated

- Wazuh installation & configuration
- Custom XML rule writing
- FIM (File Integrity Monitoring)
- MITRE ATT&CK mapping
- Dashboard (OpenSearch) usage
- DQL query syntax
- Incident report writing
- Web attack detection

## Contact
- GitHub: [Your GitHub]
- LinkedIn: [Your LinkedIn]

---
*Last Updated: 2026-10-09*
