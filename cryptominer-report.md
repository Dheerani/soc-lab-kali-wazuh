# CRYPTOMINER DETECTION REPORT

## Executive Summary
- Detection Type: Cryptominer (Resource Hijacking)
- Agent: kali (192.168.1.109)
- Total Alerts: 5
- Time Period: 2026-10-11 11:29:48 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 100005 | Process execution detected via auditd | 10 | T1059 |
| 100006 | Suspicious process detected | 10 | T1496 |

## Suspicious Processes Detected

1. **Cryptominer:**
   /tmp/miner.sh (CPU loop)

2. **High CPU Usage:**
   Process consuming 100% CPU

## MITRE ATT&CK Mapping
- **T1496** - Resource Hijacking
- **T1059** - Command and Scripting Interpreter
- **Tactic:** Impact, Execution

## Key Findings
1. Cryptominer process detected
2. High CPU usage observed
3. Auditd + Wazuh detected execution
4. Real SOC: kill process, isolate host, investigate

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Kill suspicious process
3. **Real SOC:** Isolate host
4. **Real SOC:** Check for persistence
5. **Improvement:** Add cryptominer rules

## Status
**CLOSED** - Lab simulation

## Analyst Notes
Cryptominer is a common malware type.
It allows:
- CPU/GPU resource theft
- Financial loss (cloud costs)
- System slowdown
- Persistence

Detection relies on:
- Process monitoring (Auditd)
- CPU usage analysis
- Process signatures
- Custom rules (100005, 100006)
