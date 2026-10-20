# GRAPHQL INJECTION DETECTION REPORT

## Executive Summary
- Detection Type: GraphQL Injection
- Agent: kali (192.168.1.109)
- Web Server: Apache2
- Target: /var/www/html/graphql.php
- Total Alerts: 5
- Time Period: 2026-10-10 16:44:47 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 31122 | Web server 500 error code (Internal Error) | 5 | T1190 |

## Attack Payloads Detected

1. **Introspection Query:**
   GET /graphql.php?query={__schema{types{name}}}

2. **Basic Query:**
   GET /graphql.php?query={users{id,name,email}}

3. **Injection Query:**
   GET /graphql.php?query={users(id:"1\" OR 1=1--"){name}}

4. **Sensitive Fields:**
   GET /graphql.php?query={users{id,name,email,password}}

5. **Batching Attack:**
   GET /graphql.php?query=[{users{id}},{users{id}},{users{id}}]

## MITRE ATT&CK Mapping
- **T1190** - Exploit Public-Facing Application
- **Tactic:** Initial Access

## Key Findings
1. Wazuh detected GraphQL injection payloads via 500 errors
2. 5 different GraphQL techniques tested
3. Introspection query reveals schema
4. Real SOC: block IP, disable introspection
5. Lab: authorized test

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block source IP
3. **Real SOC:** Disable introspection in production
4. **Real SOC:** Add query depth limiting
5. **Improvement:** Add GraphQL rules
6. **Improvement:** Integrate Suricata

## Status
**CLOSED** - Lab simulation

## Analyst Notes
GraphQL Injection is a modern web vulnerability.
It allows:
- Schema disclosure (introspection)
- Data exfiltration
- DoS via deep queries
- Bypass rate limiting via batching

Detection relies on:
- GraphQL query pattern detection (__schema, users)
- Introspection query detection
- Response code monitoring (500 errors)
- Wazuh built-in rules (31100-31199)
