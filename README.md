
🔍 Advanced Nmap Network Reconnaissance & Security Analysis

📌 Overview

This project demonstrates a comprehensive network reconnaissance and security analysis conducted using Nmap against an authorized target (scanme.nmap.org).

The objective is not just to scan ports, but to:

- Identify and analyze exposed services
- Detect potential vulnerabilities
- Map realistic attack paths from an attacker’s perspective

---

🎯 Objectives

- Perform stealth (SYN) network scanning
- Identify open, filtered, and closed ports
- Detect running services and versions
- Analyze NSE script outputs
- Conduct OS fingerprinting
- Map CVEs and potential exploits
- Model the attack surface

---

⚙️ Commands Used

nmap -sS -sV -O -sC scanme.nmap.org
nmap --script vuln scanme.nmap.org

---

📊 Full Nmap Scan Output (RAW)

Starting Nmap 7.95 ( https://nmap.org ) at 2026-04-19 08:29 EDT

Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.21s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f

Not shown: 995 closed tcp ports (reset)

PORT      STATE    SERVICE    VERSION
22/tcp    open     ssh        OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   1024 ac:00:a0:1a:82:ff:cc:55:99:dc:67:2b:34:97:6b:75 (DSA)
|   2048 20:3d:2d:44:62:2a:b0:5a:9d:b5:b3:05:14:c2:a6:b2 (RSA)
|   256 96:02:bb:5e:57:54:1c:4e:45:2f:56:4c:4a:24:b2:57 (ECDSA)
|_  256 33:fa:91:0f:e0:e1:7b:1f:6d:05:a2:b0:f1:54:41:56 (ED25519)

25/tcp    filtered smtp

80/tcp    open     http       Apache httpd 2.4.7 ((Ubuntu))
|_http-server-header: Apache/2.4.7 (Ubuntu)
|_http-title: Go ahead and ScanMe!
|_http-favicon: Nmap Project

9929/tcp  open     nping-echo

31337/tcp open     tcpwrapped

Aggressive OS guesses:
  Linux 4.19 - 5.15 (97%)
  Linux 4.15 (94%)
  Linux 5.4 (93%)

No exact OS matches for host (test conditions non-ideal).

Network Distance: 24 hops

Service Info: OS: Linux

Nmap done: 1 IP address (1 host up) scanned in XX.XX seconds

---

📊 Scan Summary

Port| State| Service| Version
22| open| SSH| OpenSSH 6.6.1
25| filtered| SMTP| -
80| open| HTTP| Apache 2.4.7
9929| open| nping-echo| -
31337| open| tcpwrapped| -

---

🔍 Technical Analysis

🖥️ Host & Network Context

- Host is up (0.21s latency)
- Dual-stack (IPv4 & IPv6)
- Network distance: 24 hops
- OS guess: Linux (kernel 4.x – 5.x)

👉 Insight: Likely hosted in a cloud infrastructure environment.

---

🔐 Port & Service Analysis

🔹 22/tcp — SSH

Service: OpenSSH 6.6.1 (Ubuntu)

🧠 Analysis

- Outdated SSH version
- Remote access enabled

🚨 Potential Vulnerabilities

- User enumeration
- Brute-force attacks
- Weak cryptographic configurations

🔎 Relevant CVEs

- CVE-2015-5600
- CVE-2016-6210

🎯 Attacker Perspective

- Hydra brute-force attempts
- Credential stuffing
- SSH banner fingerprinting

---

🔹 25/tcp — SMTP (Filtered)

🧠 Analysis

- Service exists but filtered
- Likely protected by firewall

🔐 Security Insight

- Indicates network-level defense
- Possible internal exposure

---

🔹 80/tcp — HTTP

Service: Apache 2.4.7

🧠 Analysis

- Public web server
- Outdated software

🚨 Potential Vulnerabilities

- Directory traversal
- Misconfiguration
- Information disclosure

🔎 Relevant CVEs

- CVE-2017-15715
- CVE-2019-0211

---

🌐 Web Enumeration

gobuster dir -u http://scanme.nmap.org -w /usr/share/wordlists/dirb/common.txt
nikto -h http://scanme.nmap.org
whatweb http://scanme.nmap.org

---

🔹 9929/tcp — Nping Echo

🧠 Analysis

- Debug/testing service
- Uncommon in production

🚨 Risk

- Information leakage
- Network probing abuse

---

🔹 31337/tcp — tcpwrapped

🧠 Analysis

- Access-controlled service
- Possibly hidden backend

---

🧠 OS Detection Analysis

- Linux (4.x – 5.x)
- No exact match

❗ Reason

- Filtering & latency impact fingerprinting

---

🧪 NSE Vulnerability Scan

nmap --script vuln scanme.nmap.org

---

⚔️ Attack Scenario (Attack Path)

1. Web reconnaissance
2. Directory brute-force
3. Apache vulnerability research
4. SSH attack attempts
5. Internal service probing

---

🛡️ Mitigation Recommendations

SSH

- Disable root login
- Use key-based authentication
- Enable Fail2Ban

HTTP

- Update Apache
- Harden configuration
- Add security headers

Network

- Close unnecessary ports
- Restrict access via firewall

---

📊 Risk Assessment

Service| Risk Level
SSH| 🔴 High
HTTP| 🔴 High
SMTP| 🟡 Medium
9929| 🟡 Medium
31337| 🟡 Medium

---

🎯 Attack Surface Summary

- SSH → access vector
- HTTP → primary attack surface
- Outdated services → exploit potential

---

🧠 Key Takeaways

- Enumeration is critical
- Version detection enables vulnerability mapping
- Analysis > raw scanning

---

⚠️ Legal Disclaimer

This analysis was conducted only on an authorized target (scanme.nmap.org) for educational purposes.

---

🚀 Skills Demonstrated

- Network Scanning
- Service Enumeration
- Vulnerability Analysis
- CVE Mapping
- Attack Surface Modeling

---

⭐ Conclusion

This project demonstrates a structured, real-world approach to network reconnaissance and security assessment, focusing on both technical accuracy and attacker mindset.
