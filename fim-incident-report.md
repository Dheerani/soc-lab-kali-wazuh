# FIM INCIDENT REPORT #001

## Executive Summary
- Detection Type: File Integrity Monitoring (FIM)
- Agent: kali (192.168.1.109)
- Total FIM Alerts: 117
- Time Period: 2026-10-07 19:20 to 19:27 PKT
- Frequency: 60 seconds (lab setting)

## Alert Breakdown

| Rule ID | Description | Level | Count |
|---------|-------------|-------|-------|
| 554 | File added to the system | 5 | 39 |
| 550 | Integrity checksum changed | 7 | 39 |
| 553 | File deleted | 7 | 39 |
| **Total** | | | **117** |

## MITRE ATT&CK Mapping
- **T1565** — Data Manipulation (file modification)
- **T1070** — Indicator Removal on Host (file deletion)
- **T1105** — Ingress Tool Transfer (file creation)

## Key Findings
1. FIM detected 117 file operations in 7 minutes
2. Detection time: Within 60 seconds of file change
3. All three Wazuh rules fired correctly (554, 550, 553)
4. Balanced distribution: 39 add, 39 modify, 39 delete
5. No false positives observed

## Analysis
- FIM monitoring working as designed in Wazuh
- `/etc/` directory changes trigger immediate alerts
- Rule 550 (modify) = Level 7 (higher severity)
- Rule 553 (delete) = Level 7 (higher severity)
- Rule 554 (add) = Level 5 (lower severity)

### Real SOC Context
If this was a production system:
- **Who changed the files?** — Check user, process
- **Was it authorized?** — Compare against change management
- **What was the content?** — Use `auditd` for full details
- **Is it a sign of attack?** — Check for TTPs (T1070, T1565)

## Recommended Actions
1. **Immediate:** No escalation (lab activity)
2. **Production:** Verify file change with change management
3. **Production:** Review user activity for the change
4. **Improvement:** Enable `realtime="yes"` for critical files
5. **Improvement:** Add high-priority monitoring for:
   - `/etc/passwd`
   - `/etc/shadow`
   - `/etc/sudoers`
   - `/etc/ssh/sshd_config`
6. **Improvement:** Integrate with `auditd` for full command context

## Status
**CLOSED** — Lab test, FIM working correctly

## Analyst Notes
FIM is one of the most important Wazuh features for SOC work. It detects:
- Unauthorized file changes
- Attacker persistence mechanisms
- Data exfiltration preparation
- Malware drops

This lab validated FIM detection capability with 117 successful detections.
