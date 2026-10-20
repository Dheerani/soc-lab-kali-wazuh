# INCIDENT REPORT: Multi-Stage Web Attack & Exfiltration

## 1. Executive Summary
On [Aaj ki Date], a simulated multi-stage cyber attack was executed against a Kali Linux web server. The Wazuh SIEM successfully detected the entire attack chain, from initial reconnaissance to data exfiltration, mapping the events to the MITRE ATT&CK framework.

## 2. Attack Timeline (Kill Chain)

| Time | Attack Phase | MITRE ID | Wazuh Rule | Detection Details |
|------|--------------|----------|------------|-------------------|
| T+0m | Reconnaissance (Nmap) | T1046 | 100022 | Nmap scan detected via auditd process monitoring |
| T+2m | Web Attack (SQLi) | T1190 | 31164 | SQL injection attempt detected in Apache access logs |
| T+5m | Backdoor Upload | T1505.003 | 554 | New PHP file (shell.php) created in `/var/www/html` |
| T+10m| Privilege Escalation | T1548 | Auditd | Suspicious `sudo -l` command executed |
| T+15m| Data Exfiltration | T1041 | 100020 | Netcat (nc) used to transfer `/etc/secret.txt` |

## 3. Evidence (Screenshots)
*[Yahan aap apne Slack alerts ke screenshots laga sakte hain]*

## 4. Detection Engineering Insights
- **FIM Optimization:** Added `/var/www/html` with `realtime="yes"` to catch web shells immediately. The configuration was validated and the Wazuh manager was successfully restarted.
- **Correlation:** Wazuh successfully mapped the source IP (127.0.0.1) across multiple rules, providing a clear attack narrative.
- **VirusTotal Integration:** The uploaded files were automatically hashed and checked against VirusTotal.

## 5. Recommendations (Blue Team Actions)
- Block the source IP using Active Response.
- Review Apache logs for further anomalous payloads.
- Quarantine and delete the uploaded web shell (`/var/www/html/shell.php`).
- Investigate the `sudo` usage to ensure no further privilege escalation occurred.

## 6. Lessons Learned
- The attack chain proved that Wazuh is capable of not just isolating alerts, but correlating them to tell a complete attack story.
- FIM required specific directory monitoring (`/var/www/html`), which was successfully tuned during this incident.
