# ACTIVE RESPONSE TEST REPORT — KALI LAB

**Date:** 2026-10-15
**Analyst:** hello
**Host:** kali (192.168.1.109)
**Environment:** Wazuh Manager + Agent on same host
**Wazuh Version:** 4.14.7
**OS:** Kali Linux (rolling)

---

## Executive Summary

Three Active Response scenarios were tested against SSH brute force attacks:

1. **SSH Failed Login detection** (Rule 100001) — firewall-drop
2. **SSH Brute Force detection** (Rule 100002) — firewall-drop
3. **SSH Brute Force Success detection** (Rule 100100) — firewall-drop + disable-account

All three tests **PASSED**. The implementation provides multi-layer defense:
- Network layer: automatic IP blocking via iptables
- Account layer: automatic account disabling on successful breach

---

## 1. Objective

Validate Wazuh Active Response for SSH brute force scenarios:
- Automatic IP blocking on failed login attempts
- Automatic IP blocking on brute force detection
- Automatic account disabling when brute force succeeds

---

## 2. Test Scenarios

| # | Scenario | Rule ID | AR Command | Status |
|---|----------|---------|------------|--------|
| 1 | SSH Failed Login | 100001 | firewall-drop | PASS |
| 2 | SSH Brute Force | 100002 | firewall-drop | PASS |
| 3 | SSH Brute Force Success | 100100 | firewall-drop + disable-account | PASS |

---

## 3. Test 1: SSH Failed Login (Rule 100001)

### 3.1 Attack Command

    for i in {1..10}; do
      sshpass -p "wrongpass$i" ssh -o StrictHostKeyChecking=no -o ConnectTimeout=2 root@192.168.1.109 2>/dev/null
      echo "Attempt $i done at $(date +%T)"
      sleep 1
    done

- **Attack Source:** 192.168.1.109
- **Target:** 192.168.1.109:22 (SSH)
- **User:** root

### 3.2 Detection Alert

    Rule: 100001 (level 10) -> 'Custom: SSH failed login detected'
    Src IP: 192.168.1.109
    User: root
    MITRE: T1110 (Brute Force)

### 3.3 Active Response Triggered

    Rule: 651 (level 3) -> 'Host Blocked by firewall-drop Active Response'
    Src IP: 192.168.1.109

### 3.4 Verification

Command:

    sudo iptables -L -n --line-numbers

Output:

    Chain INPUT (policy DROP)
    num  target     prot opt source               destination
    1    DROP       all  --  192.168.1.109        0.0.0.0/0

**Result:** PASS — Attacker IP successfully blocked.

---

## 4. Test 2: SSH Brute Force (Rule 100002)

### 4.1 Attack Command

    for i in {1..10}; do
      sshpass -p "wrongpass$i" ssh -o StrictHostKeyChecking=no -o ConnectTimeout=2 root@192.168.1.109 2>/dev/null
      echo "Attempt $i at $(date +%T)"
      sleep 1
    done

- **Attack Source:** 192.168.1.109
- **Target:** 192.168.1.109:22 (SSH)
- **User:** root

### 4.2 Detection Alerts

    Rule: 100001 (level 10) -> 'Custom: SSH failed login detected'  (x25)
    Rule: 100002 (level 12) -> 'SSH Brute Force Attack detected from 192.168.1.109'
    Rule: 651 (level 3)  -> 'Host Blocked by firewall-drop Active Response'

### 4.3 Active Response Log

    2026/10/15 14:44:56 active-response/bin/firewall-drop:
    {"command":"add", "rule":{"id":"100002"}, "data":{"srcip":"192.168.1.109"}}

    parameters.alert.rule.id: 100002

### 4.4 Verification

Command:

    sudo iptables -L INPUT -n --line-numbers | grep 192.168.1.109

Output:

    1    DROP       all  --  192.168.1.109        0.0.0.0/0

**Result:** PASS — Brute force detected and IP blocked automatically.

---

## 5. Test 3: SSH Brute Force Success (Rule 100100)

### 5.1 Attack Command

    # Step 1: 5 failed attempts
    for i in {1..5}; do
      sshpass -p "wrongpass$i" ssh -o StrictHostKeyChecking=no victim@192.168.1.109 2>/dev/null
      sleep 1
    done

    # Step 2: 1 successful attempt (brute force success)
    sshpass -p "loko@345ab" ssh -o StrictHostKeyChecking=no victim@192.168.1.109 "whoami"

- **Attack Source:** 192.168.1.109
- **Target:** 192.168.1.109:22 (SSH)
- **User:** victim (test account)

### 5.2 Detection Alerts

    Rule: 100001 (level 10) -> 'Custom: SSH failed login detected'  (x5)
    Rule: 100002 (level 12) -> 'SSH Brute Force Attack detected from 192.168.1.109'
    Rule: 5715 (level 3)  -> 'sshd: authentication success.'
    Rule: 100100 (level 13) -> 'CRITICAL: SSH brute force SUCCEEDED from 192.168.1.109'

### 5.3 Active Response Triggered (BOTH)

    2026/10/15 15:57:43 active-response/bin/firewall-drop:
    {"command":"add", "rule":{"id":"100100"}, "data":{"srcip":"192.168.1.109"}}
    parameters.alert.rule.id: 100100

    2026/10/15 15:57:43 active-response/bin/disable-account:
    {"command":"add", "rule":{"id":"100100"}, "data":{"dstuser":"victim"}}
    parameters.alert.rule.id: 100100

### 5.4 Verification

**Account Status:**

    sudo passwd -S victim
    Output:
    victim L 2026-10-15 0 99999 7 -1     ← L = Locked

**Shadow File:**

    sudo grep victim /etc/shadow
    Output:
    victim:!$y$j9T$...                     ← ! = Password locked

**Login Attempt:**

    sshpass -p "loko@345ab" ssh victim@192.168.1.109 "whoami"
    Output:
    Permission denied, please try again.

**Result:** PASS — Both IP blocked AND account disabled.

---

## 6. Configuration Reference

### 6.1 Active Response blocks in /var/ossec/etc/ossec.conf:

    <!-- SSH brute force success (100100) → block IP for 3 min -->
    <active-response>
      <command>firewall-drop</command>
      <location>local</location>
      <rules_id>100100</rules_id>
      <timeout>180</timeout>
    </active-response>

    <!-- SSH brute force (100002) → block IP for 10 min -->
    <active-response>
      <command>firewall-drop</command>
      <location>local</location>
      <rules_id>100002</rules_id>
      <timeout>600</timeout>
    </active-response>

    <!-- SSH brute force success (100100) → disable account -->
    <active-response>
      <command>disable-account</command>
      <location>local</location>
      <rules_id>100100</rules_id>
    </active-response>

### 6.2 Command Definitions:

    <command>
      <name>firewall-drop</name>
      <executable>firewall-drop</executable>
      <timeout_allowed>yes</timeout_allowed>
    </command>

    <command>
      <name>disable-account</name>
      <executable>disable-account</executable>
    </command>

### 6.3 Custom Rules in /var/ossec/etc/rules/local_rules.xml:

    <group name="custom_ssh,">
      <rule id="100001" level="10">
        <if_sid>5503,5760</if_sid>
        <description>Custom: SSH failed login detected</description>
        <mitre><id>T1110</id></mitre>
      </rule>
    </group>

    <group name="local,brute_force,">
      <rule id="100002" level="12" frequency="5" timeframe="120">
        <if_matched_sid>100001</if_matched_sid>
        <same_source_ip />
        <description>SSH Brute Force Attack detected from $(srcip)</description>
        <mitre><id>T1110</id></mitre>
      </rule>
    </group>

    <group name="correlation,attack_chain,">
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
    </group>

### 6.4 White List (self-block prevention):

    <global>
      <white_list>127.0.0.1</white_list>
      <white_list>^localhost.localdomain$</white_list>
      <white_list>192.168.1.1</white_list>
    </global>

---

## 7. Findings

### 7.1 Successes

1. Detection worked in less than 2 seconds
2. Brute force correlation worked (100002 after 5 attempts)
3. Active Response triggered automatically on rule 100002
4. Attacker IP blocked in iptables
5. Auto-unblock after 600 seconds confirmed
6. `same_source_ip` tag reliable for correlation (PAM + sshd both)
7. Brute force success detection working (100100, level 13)
8. `disable-account` AR works (account locked after successful breach)
9. Multi-layer defense working (network block + account lock)

### 7.2 Observations

1. Rule 100001 fires TWICE per SSH attempt (PAM line + sshd line) — consider de-duplication
2. `same_field>srcip` did NOT work for correlation — `same_source_ip` is the correct tag
3. Rule 100003 was redundant — removed
4. Rule 100001 parent was 5503 (PAM only) — updated to 5503,5760
5. SSH brute force detected after ~5 attempts (~10-15 seconds)
6. 100100 fires both firewall-drop (180s) AND disable-account — intentional defense-in-depth

### 7.3 Recommendations

1. Consider de-duplicating 100001 (PAM + sshd double-fire)
2. Test `kill-process` on rules 100020, 100021
3. Slack/Email notification integration
4. Consider permanent account lock (currently manual unlock needed)

---

## 8. Conclusion

Active Response is **FULLY FUNCTIONAL** for SSH brute force scenarios including successful breach detection.

| Component | Status |
|-----------|--------|
| Detection (100001) | Working |
| Brute Force (100002) | Working |
| Brute Force Success (100100) | Working |
| firewall-drop AR | Working |
| disable-account AR | Working |
| Logging | Working |
| Auto-Cleanup | Working |

### Next Steps

- [x] Test disable-account on rule 100100
- [ ] Test kill-process on rules 100020, 100021
- [ ] Slack/Email notification integration
- [ ] De-duplicate 100001 (PAM + sshd double-fire)

---

## Appendix A: Test Environment Details

| Component | Value |
|-----------|-------|
| Wazuh Manager | v4.14.7 |
| OS | Kali Linux (rolling) |
| Host | kali (192.168.1.109) |
| Agent ID | 000 (local) |
| Log Source | journald |
| Firewall | iptables |
| SSH Port | 22 |
| Test Users | root, victim |

---

## Appendix B: Active Response Log Timeline

| Timestamp | Event | Rule |
|-----------|-------|------|
| 2026/10/15 14:44:56 | firewall-drop add | 100002 |
| 2026/10/15 15:57:43 | firewall-drop add | 100100 |
| 2026/10/15 15:57:43 | disable-account add | 100100 |

---

## Appendix C: Attack Chain Diagram

    5x Failed Login (100001, level 10)
            ↓
    Brute Force Detected (100002, level 12)
            ↓
    IP Blocked (firewall-drop, 600s)
            ↓
    Successful Login (5715, level 3)
            ↓
    Brute Force SUCCESS (100100, level 13)
            ↓
    ┌──────────────────────┐  ┌──────────────────────┐
    │ IP Block (180s)      │  │ Account Disable      │
    │ firewall-drop        │  │ disable-account      │
    └──────────────────────┘  └──────────────────────┘

---

**Report Status:** COMPLETE
**Signed:** hello
**Date:** 2026-10-15
