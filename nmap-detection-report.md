# NMAP DETECTION REPORT

## Executive Summary
- Detection Type: Network Service Discovery (T1046)
- Agent: kali (192.168.1.109)
- Total Nmap Alerts: 7
- Time Period: 2026-10-08 16:41 to 16:43 PKT
- Attack Source: ::1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 100003 | SSH connection detected from ::1 | 10 | T1046 |

## MITRE ATT&CK Mapping
- **T1046** — Network Service Discovery
- **Tactic:** Reconnaissance

## Key Findings
1. Nmap scan detected via SSH connection attempts
2. 7 alerts fired in 2 minutes
3. Source IP: ::1 (IPv6 localhost)
4. Custom rule 100003 working as designed

## Analysis
- Nmap SYN scan detected through SSH probe correlation
- Port scanning = first phase of attack chain
- Real SOC: block source IP, investigate intent
- Lab: authorized activity

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block source IP
3. **Real SOC:** Review firewall logs
4. **Improvement:** Add UFW iptables monitoring for better coverage

## Status
**CLOSED** — Lab simulation

## Analyst Notes
Nmap scan detection is critical for SOC work. It catches:
- Reconnaissance phase of attacks
- Automated vulnerability scanners
- Network mapping attempts
- Pre-attack intelligence gathering

Rule 100003 successfully detects SSH-based port scanning.

