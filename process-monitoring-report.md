# PROCESS MONITORING DETECTION REPORT

## Executive Summary
- Detection Type: Process Monitoring (Auditd)
- Agent: kali (192.168.1.109)
- Total Alerts: [YOUR NUMBER]
- Time Period: 2026-10-11 00:10:54 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 100005 | Process execution detected via auditd | 10 | T1059 |

## Suspicious Processes Detected

1. **Cryptominer:**
   /tmp/miner.sh (CPU loop)

2. **Reverse Shell:**
   nc -lvnp 4444

3. **Data Exfiltration:**
   tar czf /tmp/data.tar.gz /etc/passwd

## MITRE ATT&CK Mapping
- **T1059** - Command and Scripting Interpreter
- **T1041** - Exfiltration Over C2 Channel
- **T1496** - Resource Hijacking
- **Tactic:** Execution, Exfiltration, Impact

## Key Findings
1. Auditd + Wazuh detects process execution
2. Suspicious processes detected via audit key
3. Real SOC: isolate host, kill process, investigate
4. Lab: authorized test

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Isolate host
3. **Real SOC:** Kill suspicious process
4. **Real SOC:** Check for persistence
5. **Improvement:** Add process-specific rules

## Status
**CLOSED** - Lab simulation

## Analyst Notes
Process monitoring via Auditd detects:
- Reverse shells
- Cryptominers
- Data exfiltration tools
- Suspicious binaries

Detection relies on:
- Auditd execve syscall monitoring
- Wazuh audit decoder
- Custom rule 100005
- MITRE T1059 mapping
