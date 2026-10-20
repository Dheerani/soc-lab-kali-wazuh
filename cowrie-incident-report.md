# Incident Report: Cowrie Honeypot Login

## Incident Overview
- **Date:** Oct 20, 2026
- **Attack Type:** SSH Honeypot Interaction
- **Target:** Cowrie Honeypot (Docker, Port 2222)
- **Source IP:** 172.17.0.1
- **Destination IP:** 172.17.0.2

## Alert Details
- **Rule ID:** 100500
- **Rule Level:** 8
- **Description:** Cowrie Honeypot: Successful login from 172.17.0.1 using root/234234
- **MITRE ATT&CK:** T1078 (Valid Accounts)

## Log Evidence (Raw JSON)
```json
{"session":"bf97f31c15b0","protocol":"ssh","src_ip":"172.17.0.1","username":"root","password":"234234","eventid":"cowrie.login.success","timestamp":"2026-10-20T18:25:15.904399Z","message":"login attempt [root/234234] succeeded"}
