# SEC560 Penetration Testing Labs — Personal Walkthrough & Theory Notes

## Overview
Tài liệu này tổng hợp toàn bộ quá trình thực hành SEC560 từ:
- Password attacks
- Initial access
- Command & Control (C2)
- Privilege Escalation
- Active Directory attacks
- Persistence
- Credential dumping
- Post-exploitation
- Extra vulnerable machine labs

Mục tiêu:
- Biến lab thành playbook thực chiến
- Ghi lại command quan trọng
- Hiểu bản chất từng kỹ thuật thay vì chỉ chạy lệnh

---

# Lab Environment
## Core Machines
- DC / Domain Controller: `10.130.10.10`
- Linux Slingshot: `10.130.10.18`
- Windows Slingshot: `10.130.10.25`

## Default Credentials
- Linux: `sec560 | sec560`
- Windows:
  - `sec560 | M@nh19012004`
  - `Clark | Password1`

---

# 1. Password Attacks
## Techniques Covered
### Password Guessing
- Hydra SMB / SSH brute force
- Seasonal password patterns
- Username list + single password
- Password list attacks

### Password Spraying
- One password → many users
- Lower lockout risk
- Useful in AD environments

### Breached Credential Stuffing
- Testing leaked username:password combos
- Hydra `-C`

## Key Lessons
- Threading matters (`-t`)
- SMB often easier than SSH
- Internal network brute force is faster
- Valid credentials ≠ Admin rights

---

# 2. Initial Access & Exploitation
## Metasploit + Meterpreter
### Focus:
- Icecast exploit
- Reverse TCP payload
- Session management
- Shell upgrade
- Keylogging
- Backdoor user creation

### Core Concepts:
- In-memory payloads
- Reverse shells
- Session migration
- OPSEC considerations

---

# 3. Command & Control Frameworks
## Sliver
- Multiplayer server
- Operator accounts
- HTTPS / mTLS payloads
- Implant generation
- Payload staging

## Empire
- Listener
- Stager
- Agent deployment
- PowerShell modules
- PowerDump
- UAC bypass

---

# 4. Enumeration & Situational Awareness
## Tools
### Seatbelt
- TCP connections
- Autoruns
- Processes
- Local users

### beRoot
- Misconfig discovery
- Service path abuse
- Weak permissions

---

# 5. Privilege Escalation
## Windows
### Unquoted Service Path
- Missing quotes in service binary path
- Path hijacking
- Local admin creation

### PowerUp
- AbuseFunction
- Service exploitation

### UAC Bypass
- Elevation through user deception or config abuse

## Linux
### SUID Abuse
- GTFOBins techniques
- Root via misconfigured binaries

---

# 6. Persistence
## Methods
### Registry Run Keys
- HKCU persistence
- User-level stealth

### WMI Event Filters
- Trigger on failed logons
- Event-based persistence

### Sliver Services
- Service-based high privilege persistence

---

# 7. Credential Access
## Hash Dumping
- smart_hashdump
- hashdump
- Mimikatz / Kiwi

## Captured Data
- NTLM
- SHA1
- Kerberos tickets
- WDigest

## External Capture
### Responder
- LLMNR / NBT-NS poisoning
- NTLMv2 capture

### Pcredz
- PCAP credential extraction

---

# 8. Lateral Movement
## Tools
### PsExec
- SMB + Service creation

### WMIC
- Remote process creation

### Impacket
- wmiexec.py
- smbexec.py
- smbclient.py
- lookupsid.py

---

# 9. Active Directory Attacks
## Kerberoasting
- SPN enumeration
- TGS extraction
- Offline cracking

## Pass-the-Hash
- NTLM hash authentication
- No plaintext required

## NTDS.dit Extraction
- Full domain hash dump
- VSS shadow copy

## Silver Ticket
- Service-specific forged ticket

## Golden Ticket
- Full domain persistence via `krbtgt`

---

# 10. Password Cracking
## John the Ripper
- LM
- NTLM
- Shadow files

## Hashcat
- Wordlists
- Rules
- Masks
- GPU acceleration

---

# 11. Payload Development
## MSFVenom
- EXE
- MSI
- VBS
- ISO

## MSBuild
- XML payload execution
- App whitelisting bypass

---

# 12. Extra Practice (DC-1)
## Skills Applied
- Nmap
- Drupal exploit
- Database extraction
- Config credential harvesting
- MySQL pivoting
- SUID privesc

---

# Core Theory Summary
## Authentication Attacks
- Password Guessing
- Password Spraying
- Credential Stuffing

## Post Exploitation
- C2
- Persistence
- Privilege Escalation
- Credential Dumping

## AD Domination
- Kerberoast
- PtH
- Silver Ticket
- Golden Ticket

---

# OPSEC Notes
- Avoid noisy service creation when possible
- Prefer WMI over SMBExec when stealth needed
- Session migration reduces crashes
- Persistence cleanup matters
- Hashes can be more valuable than passwords

---

# Personal Takeaways
- Enumeration decides everything
- Misconfig > Exploit in many real systems
- AD is often won through credential abuse
- Persistence is easier than re-entry
- Tool mastery matters less than understanding attack chain

---

# Disclaimer
For authorized lab, educational, and defensive security purposes only.

---
