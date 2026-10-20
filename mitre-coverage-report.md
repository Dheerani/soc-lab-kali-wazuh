# MITRE ATT&CK COVERAGE REPORT

## Executive Summary
- Report Type: MITRE ATT&CK Coverage Analysis
- Agent: kali (192.168.1.109)
- Total Alerts Analyzed: 686
- Time Period: 2026-10-07 to 2026-10-08
- Data Source: Wazuh Dashboard MITRE ATT&CK module

## Tactics Detected

| Tactic | Alerts | Description |
|--------|--------|-------------|
| Defense Evasion | ~250 | File manipulation, log tampering |
| Privilege Escalation | ~200 | Sudo abuse |
| Credential Access | ~150 | Brute force, password guessing |
| Initial Access | ~100 | Valid accounts |
| Persistence | ~100 | Login sessions |

## Top Techniques Detected

| Technique | Name | Tactic |
|-----------|------|--------|
| Password Guessing | T1110.001 | Credential Access |
| Sudo and Sudo Caching | T1548.003 | Privilege Escalation |
| Valid Accounts | T1078 | Initial Access, Persistence |
| Stored Data Manipulation | T1565.001 | Defense Evasion |
| SSH | T1021.004 | Lateral Movement |

## Detection Rules Mapping

| Rule ID | Description | MITRE Technique | Level |
|---------|-------------|-----------------|-------|
| 100002 | SSH Brute Force Attack | T1110 | 12 |
| 5760 | sshd: authentication failed | T1110 | 5 |
| 5551 | PAM: Multiple failed logins | T1110 | 10 |
| 5501 | PAM: Login session opened | T1078 | 3 |
| 5502 | PAM: Login session closed | T1078 | 3 |
| 5402 | Successful sudo to ROOT | T1548.003 | 3 |
| 554 | File added to the system | T1565.001 | 5 |
| 550 | Integrity checksum changed | T1565.001 | 7 |
| 553 | File deleted | T1565.001 | 7 |

## Coverage Analysis

### Strengths (Covered)
- ✅ Credential Access — T1110 (Brute Force)
- ✅ Privilege Escalation — T1548.003 (Sudo)
- ✅ Defense Evasion — T1565 (Data Manipulation)
- ✅ Initial Access — T1078 (Valid Accounts)
- ✅ Persistence — T1078

### Gaps (Not Covered)
- ❌ Reconnaissance — T1046 (Nmap scans)
- ❌ Lateral Movement — T1021 (partially)
- ❌ Exfiltration — T1041
- ❌ Command & Control — T1071
- ❌ Impact — T1486

## Recommendations

### Immediate
1. Add Nmap scan detection (T1046)
2. Enable rootkit detection
3. Add web attack detection

### Short-Term
1. Deploy agents on multiple VMs
2. Enable vulnerability detection
3. Add Suricata for network detection

### Long-Term
1. Threat intelligence feeds
2. SOC playbooks per technique
3. Automated response actions

## Coverage Score

| Category | Coverage |
|----------|----------|
| Credential Access | 100% |
| Privilege Escalation | 80% |
| Defense Evasion | 40% |
| Initial Access | 60% |
| Persistence | 50% |
| Reconnaissance | 0% |
| Lateral Movement | 20% |
| Exfiltration | 0% |
| Command & Control | 0% |
| Impact | 0% |

**Overall Coverage: ~35%**

## Status
**ANALYZED** — Lab environment

## Analyst Notes
MITRE ATT&CK mapping helps SOC analysts:
- Understand attacker behavior patterns
- Prioritize detection efforts
- Build defense strategies
- Communicate with management

Lab covers most common attack vectors. Next: expand to network-based detections.
