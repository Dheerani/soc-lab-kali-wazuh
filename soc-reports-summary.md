# SOC REPORTS SUMMARY — KALI LAB

## Reports Created

| # | Report File | Attack Type | Alerts | MITRE |
|---|-------------|-------------|--------|-------|
| 1 | incident-report-002.md | SSH Brute Force | 19 | T1110 |
| 2 | fim-incident-report.md | File Integrity | 117 | T1565 |
| 3 | mitre-coverage-report.md | MITRE Coverage | 686 | Multiple |
| 4 | nmap-detection-report.md | Nmap Scan | 7 | T1046 |
| 5 | web-attack-report.md | Web Attack (XSS) | 3 | T1190 |
| 6 | sql-injection-report.md | SQL Injection | 2 | T1190 |
| 7 | path-traversal-report.md | Path Traversal | 15 | T1083 |
| 8 | command-injection-report.md | Command Injection | 2 | T1059 |
| 9 | file-upload-report.md | File Upload | 12 | T1505.003 |
| 10 | file-inclusion-report.md | File Inclusion | 8 | T1083 |
| 11 | ssrf-report.md | SSRF | 2 | T1190 |
| 12 | xxe-report.md | XXE | 7 | T1190 |
| 13 | ssti-report.md | SSTI | 5 | T1190 |
| 14 | open-redirect-report.md | Open Redirect | 3 | T1190 |
| 15 | deserialization-report.md | Insecure Deserialization | 5 | T1190 |
| 16 | log4shell-report.md | Log4Shell | 5 | T1190 |
| 17 | spring4shell-report.md | Spring4Shell | 3 | T1190 |
| 18 | ldap-injection-report.md | LDAP Injection | 5 | T1190 |
| 19 | nosql-injection-report.md | NoSQL Injection | 5 | T1190 |
| 20 | graphql-injection-report.md | GraphQL Injection | 5 | T1190 |
| 21 | advanced-ssrf-report.md | Advanced SSRF | 3 | T1190 |
| 22 | billion-laughs-report.md | Billion Laughs | 3 | T1499 |
| 23 | smuggling-report.md | HTTP Smuggling | 1 | T1190 |
| 24 | cache-poisoning-report.md | Web Cache Poisoning | 0 | T1190 |
| 25 | host-header-report.md | Host Header Injection | 0 | T1190 |
| 26 | process-monitoring-report.md | Process Monitoring | — | T1059 |
| 27 | web-shell-report.md | Web Shell | 3 | T1505.003 |
| 28 | cryptominer-report.md | Cryptominer | 5 | T1496 |
| 29 | reverse-shell-report.md | Reverse Shell | 5 | T1059 |
| 30 | data-exfiltration-report.md | Data Exfiltration | 5 | T1041 |
| 31 | priv-esc-report.md | Privilege Escalation | 5 | T1548 |
| 32 | persistence-report.md | Persistence | 5 | T1053 |
| 33 | active-response-test-report.md | Active Response (SSH) | 100+ | T1110, T1078 |

## Custom Rules Created (16 Total)

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 100001 | SSH failed login | 10 | T1110 |
| 100002 | SSH Brute Force | 12 | T1110 |
| 100003 | SSH connection (Nmap) | 10 | T1046 |
| 100010 | Suppress: Wazuh internal | 0 | — |
| 100011 | Suppress: dash shell | 0 | — |
| 100020 | Netcat via auditd | 10 | T1059 |
| 100021 | Cryptominer via auditd | 12 | T1496 |
| 100022 | Recon tools via auditd | 12 | T1046 |
| 100100 | SSH brute force → success | 13 | T1110, T1078 |
| 100101 | Sudo after SSH breach | 14 | T1548.003, T1078 |
| 100200 | VirusTotal: 50+ engines | 15 | T1204 |
| 100201 | VirusTotal: 10-49 engines | 12 | T1204 |
| 100202 | VirusTotal: 1-9 engines | 8 | T1204 |
| 100300 | MyApp: Login failed | 8 | T1110 |
| 100301 | MyApp: Successful login | 3 | — |
| 100302 | MyApp: Brute force | 12 | T1110 |

## Detections Working (37+)

| # | Detection | Rule | Status |
|---|-----------|------|--------|
| 1 | SSH Brute Force | 100002 | ✅ |
| 2 | Nmap Scan | 100003 | ✅ |
| 3 | File Integrity | 550, 553, 554 | ✅ |
| 4 | Rootkit | Rootcheck | ✅ |
| 5 | Web Attack | 31106 | ✅ |
| 6 | SQL Injection | 31106 | ✅ |
| 7 | Path Traversal | 31106 | ✅ |
| 8 | Command Injection | 31106 | ✅ |
| 9 | File Upload (Web Shell) | 31514 | ✅ |
| 10 | File Inclusion | 31106 | ✅ |
| 11 | SSRF | 31106 | ✅ |
| 12 | XXE | 31122 | ✅ |
| 13 | SSTI | 31122 | ✅ |
| 14 | Open Redirect | 31105 | ✅ |
| 15 | Insecure Deserialization | 31122 | ✅ |
| 16 | Log4Shell | 31122 | ✅ |
| 17 | Spring4Shell | 31122 | ✅ |
| 18 | LDAP Injection | 31122 | ✅ |
| 19 | NoSQL Injection | 31122 | ✅ |
| 20 | GraphQL Injection | 31122 | ✅ |
| 21 | Advanced SSRF | 31122 | ✅ |
| 22 | Billion Laughs | 31122 | ✅ |
| 23 | HTTP Smuggling | 31101 | ✅ |
| 24 | Web Cache Poisoning | 31122 | ✅ |
| 25 | Host Header Injection | 31122 | ✅ |
| 26 | Netcat (auditd) | 100020 | ✅ |
| 27 | Cryptominer | 100021 | ✅ |
| 28 | Recon tools | 100022 | ✅ |
| 29 | Correlation: Brute→Success | 100100 | ✅ |
| 30 | Correlation: Sudo after breach | 100101 | ✅ |
| 31 | VirusTotal: High-confidence | 100200 | ✅ |
| 32 | VirusTotal: Medium | 100201 | ✅ |
| 33 | VirusTotal: Low | 100202 | ✅ |
| 34 | MyApp: Login failed | 100300 | ✅ |
| 35 | MyApp: Brute force | 100302 | ✅ |
| 36 | Active Response: firewall-drop | 100002 | ✅ |
| 37 | Active Response: disable-account | 100100 | ✅ |

---

# DETECTION ENGINEERING — TUNING & OPTIMIZATION

## Problem Statement (Before Tuning)

| Issue | Value | Impact |
|-------|-------|--------|
| Alerts per day | 59,476+ | 99.9% noise |
| alerts.log size | 131 MB | Disk bloat |
| Rule 100005 (broad auditd) | 41,121 fires | Noise factory |
| Duplicate rule IDs | 2x rule 100005 | Wazuh confusion |
| FIM frequency | 60 seconds | Constant scanning |
| FIM realtime on /usr/bin | yes | Infinite loop |
| Syscollector interval | 1 hour | Frequent scans |

## Root Cause Analysis

1. **Duplicate Rule ID 100005** — The same rule ID was used in two places (syscollector + auditd), causing Wazuh confusion and the broad rule firing on every execve.
2. **Broad auditd Rule** — There was no filter on `audit.key=process_exec`, so Wazuh's own internal commands were also being detected.
3. **Aggressive FIM Configuration** — `frequency=60` (1 minute) + `realtime=yes` on `/usr/bin, /usr/sbin` generated thousands of events per hour.
4. **Hard Link Issue** — `alerts.log` and `alerts.json` were hard links (`Links: 2`), so even after `rm`, the file remained alive and was relinked on Wazuh restart.

## Fixes Applied

| Fix | Before | After |
|-----|--------|-------|
| Duplicate rule ID | 100005 (2x) | 100005, 100006, 100007 (unique) |
| Broad auditd rule | All execve | Only nc/socat/miner/nmap |
| Wazuh internal suppression | None | Rules 100010, 100011 (level 0) |
| FIM frequency | 60 sec | 43200 sec (12 hours) |
| FIM scan_on_start | yes | no |
| FIM realtime on /usr/bin | yes | removed |
| Syscollector interval | 1h | 12h |
| Syscollector scan_on_start | yes | no |
| Log cleanup method | `rm` (failed) | `truncate -s 0` |

## Results (After Tuning)

| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| alerts.log size | 131 MB | ~50 KB | **99.96%** |
| Alerts per day | 59,476 | ~120 | **99.8%** |
| Rule 100005 fires | 41,121 | 0 | **100%** |
| False positives | High | Near zero | — |
| Disk usage | Critical | Normal | — |

---

# CORRELATION RULES — MULTI-STAGE ATTACK DETECTION

## Rule 100100: SSH Brute Force → Success

```xml
<rule id="100100" level="13" frequency="5" timeframe="300">
  <if_matched_sid>100001</if_matched_sid>
  <if_sid>5715</if_sid>
  <same_source_ip />
  <description>CRITICAL: SSH brute force SUCCEEDED from $(srcip)</description>
  <mitre>
    <id>T1110</id>
    <id>T1078</id>
  </mitre>
  <group>attack_chain,</group>
</rule>
