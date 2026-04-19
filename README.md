
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

👉 Insight: Likely hosted in a cloud-based infrastructure.

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

- CVE-2015-5600 → brute-force mitigation bypass
- CVE-2016-6210 → user enumeration

🎯 Attacker Perspective

- Password brute-force using Hydra
- Credential stuffing
- Banner grabbing for fingerprinting

---

🔹 25/tcp — SMTP (Filtered)

🧠 Analysis

- Service exists but is filtered by firewall
- External access restricted

🔐 Security Insight

- Indicates defensive filtering
- Internal relay or misconfiguration may still exist

---

🔹 80/tcp — HTTP

Service: Apache 2.4.7

🧠 Analysis

- Public-facing web server
- Outdated version

🚨 Potential Vulnerabilities

- Directory traversal
- Misconfiguration issues
- Information disclosure

🔎 Relevant CVEs

- CVE-2017-15715
- CVE-2019-0211 (privilege escalation)

---

🌐 Web Enumeration

Tools Used:

gobuster dir -u http://scanme.nmap.org -w /usr/share/wordlists/dirb/common.txt
nikto -h http://scanme.nmap.org
whatweb http://scanme.nmap.org

🎯 Purpose:

- Discover hidden directories
- Identify technologies
- Detect known vulnerabilities

---

🔹 9929/tcp — Nping Echo

🧠 Analysis

- Debugging/testing service
- Rarely used in production

🚨 Risk

- Information leakage
- Network mapping opportunities

---

🔹 31337/tcp — tcpwrapped

🧠 Analysis

- Access is restricted or filtered
- Service likely protected by access control

🎯 Possibilities

- Administrative service
- Internal tool
- Hidden backend service

---

🧠 OS Detection Analysis

- Linux kernel range: 4.x – 5.x
- No exact match found

❗ Reasons

- Firewall interference
- Network latency
- Packet filtering

👉 This is normal in real-world scenarios.

---

🧪 NSE Vulnerability Scan

nmap --script vuln scanme.nmap.org

🎯 Purpose:

- Automated vulnerability detection
- Service-specific security checks

---

⚔️ Attack Scenario (Attack Path)

1. Perform HTTP reconnaissance
2. Enumerate directories
3. Identify Apache vulnerabilities
4. Attempt SSH brute-force or credential attacks
5. Probe internal/hidden services (9929, 31337)

👉 This reflects a realistic penetration testing workflow.

---

🛡️ Mitigation Recommendations

SSH

- Disable root login
- Enforce key-based authentication
- Implement Fail2Ban

HTTP

- Update Apache to latest version
- Add security headers
- Disable directory listing

Network

- Close unnecessary ports
- Harden firewall rules

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

- SSH → remote access vector
- HTTP → primary attack surface
- Outdated services → exploit opportunities

---

🧠 Key Takeaways

- Nmap output alone is not sufficient
- Service versions are critical for vulnerability mapping
- Enumeration is the most important phase of pentesting
- Analysis is more valuable than raw data

---

⚠️ Legal Disclaimer

This analysis was conducted strictly on an authorized target (scanme.nmap.org) for educational purposes only.
No unauthorized access or exploitation was performed.

---

🚀 Skills Demonstrated

- Network Scanning
- Service Enumeration
- Vulnerability Analysis
- CVE Mapping
- Attack Surface Modeling
- Threat-Oriented Thinking

---

⭐ Conclusion

This project goes beyond simple scanning by answering key questions:

- How can this system be attacked?
- Where are the weakest points?
- How can it be secured?

It reflects a practical and analytical approach to real-world network security assessment.
