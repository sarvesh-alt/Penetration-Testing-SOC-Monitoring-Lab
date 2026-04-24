# 🔐 Penetration Testing & SOC Monitoring Lab


![Kali](https://img.shields.io/badge/Kali_Linux-2025.3-557C94?logo=kali-linux&logoColor=white)
![Metasploit](https://img.shields.io/badge/Metasploit-Framework-2596CD?logo=metasploit)
![Security Onion](https://img.shields.io/badge/Security_Onion-3.0-blue)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

End-to-end penetration test simulating a real-world attack lifecycle — from 
reconnaissance to full SYSTEM compromise — with live SOC detection in Security Onion 3.0.

---

## 🖥 Lab Environment

<img width="719" height="376" alt="Diagram drawio" src="https://github.com/user-attachments/assets/dd1d1b50-d676-4f05-9c23-ba1c202f6f04" />


| Component | Details |
|-----------|---------|
| Attacker | Kali Linux 2025.3 — 192.168.109.131 |
| Target | Metasploitable3 Windows Server 2008 R2 — 192.168.109.135 |
| Monitor | Security Onion 3.0 — 10.0.0.99 |
| Network | VMware VMnet1 Host-Only — 192.168.109.0/24 |

---

## 📋 Attack Phases

### 1️⃣ Reconnaissance
- ARP host discovery with `netdiscover -r 192.168.109.0/24`
- Service enumeration with `nmap -sV -sC -Pn -A -T4 192.168.109.135`
- Identified: FTP (21), IIS (80), SMB (445), MySQL (3306), RDP (3389)

### 2️⃣ Social Engineering & Payload Delivery
- Generated Meterpreter reverse TCP payload via SET (LHOST: 192.168.109.131, LPORT: 1234)
- Renamed to `securitypatch.exe` — disguised as Windows KB patch
- Delivered via phishing email impersonating IT Security

### 3️⃣ Exploitation
- Established Meterpreter session on target
- Escalated to `NT AUTHORITY\SYSTEM` via Named Pipe Impersonation
- Migrated into `notepad.exe` (PID 1128) for stealth persistence

### 4️⃣ SOC Detection
- Security Onion generated **10 Suricata IDS alerts**
- Detected: Meterpreter C2, PE/EXE download, Kali attacker fingerprint
- Kibana logged **221,644+ events** with full attack timeline

---

## 🛠 Tools Used
`Kali Linux` `Metasploit` `SET` `Nmap` `Netdiscover` `Security Onion 3.0`  
`Suricata` `Zeek` `Elasticsearch` `Kibana` `VMware` `Vagrant`

---

## 📄 Full Report
See [`/report/PenTest&SOC.pdf)

---

## ⚠️ Disclaimer
This lab was conducted in a fully isolated, controlled environment for educational 
purposes only. All techniques demonstrated are for ethical security research and 
academic assessment. Do not replicate outside a legal lab environment.
