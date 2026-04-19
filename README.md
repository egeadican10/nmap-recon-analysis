# nmap-recon-analysis

This project demonstrates practical network reconnaissance and analysis skills using Nmap, focusing on real-world interpretation of scan results.

# 🔍 Advanced Nmap Network Reconnaissance Analysis

## 📌 Overview

This project demonstrates a detailed network reconnaissance process using Nmap against an authorized target (`scanme.nmap.org`). The objective is not only to run scans but to **analyze and interpret the results** in order to understand the system’s attack surface.

---

## 🎯 Objectives

* Perform stealth network scanning
* Identify open, filtered, and protected ports
* Detect running services and versions
* Analyze NSE script outputs
* Perform OS fingerprinting
* Evaluate potential security risks

---

## ⚙️ Command Used

```bash
nmap -sS -sV -O -sC scanme.nmap.org
```

---

## 📊 Full Scan Output (Raw)

```
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
|_http-favicon: Nmap Project
|_http-server-header: Apache/2.4.7 (Ubuntu)
|_http-title: Go ahead and ScanMe!

9929/tcp  open     nping-echo

31337/tcp open     tcpwrapped

Aggressive OS guesses: Linux 4.19 - 5.15 (97%), Linux 4.15 (94%), Linux 5.4 (93%)
No exact OS matches for host (test conditions non-ideal).

Network Distance: 24 hops
Service Info: OS: Linux
```

---

# 🔍 Detailed Technical Analysis

---

## 🖥️ Host Availability & Network Context

* **Host Status:** Up and reachable
* **Latency:** 0.21 seconds → moderate network delay
* **IPv6 Address Present:** Indicates dual-stack network support
* **Network Distance:** 24 hops → relatively distant system

👉 Interpretation:
The host is accessible over the network, but not in close proximity, suggesting it is likely hosted remotely (e.g., cloud infrastructure).

---

## 🔐 Port & Service Analysis

---

### 🔹 Port 22 — SSH (Remote Access Service)

```
22/tcp open ssh OpenSSH 6.6.1p1 Ubuntu
```

#### Analysis:

* SSH is exposed → remote login possible
* Version: **OpenSSH 6.6.1 (older release)**
* Multiple host keys detected (DSA, RSA, ECDSA, ED25519)

#### Security Insight:

* Older SSH versions may contain known vulnerabilities
* Possible attack vectors:

  * Brute-force attempts
  * Exploitation of outdated cryptographic implementations

👉 This port represents a **high-value attack surface**

---

### 🔹 Port 25 — SMTP (Filtered)

```
25/tcp filtered smtp
```

#### Analysis:

* SMTP service exists but is **not directly accessible**
* Traffic is being filtered (likely firewall)

#### Security Insight:

* Indicates presence of **network security controls**
* Service may still be reachable internally or under certain conditions

👉 Suggests **defensive configuration is in place**

---

### 🔹 Port 80 — HTTP (Web Server)

```
80/tcp open http Apache httpd 2.4.7 (Ubuntu)
```

#### NSE Output:

* Server header: Apache/2.4.7
* Page title: "Go ahead and ScanMe!"
* Favicon identified

#### Analysis:

* Web server is publicly accessible
* Apache version **2.4.7 is outdated**

#### Security Insight:

* Potential vulnerabilities may exist in older Apache versions
* Possible attack vectors:

  * Directory traversal
  * Misconfiguration exploitation
  * Web application vulnerabilities

👉 This is a **primary attack surface**

---

### 🔹 Port 9929 — Nping Echo Service

```
9929/tcp open nping-echo
```

#### Analysis:

* Uncommon service
* Used for network testing/debugging

#### Security Insight:

* Rarely used in production
* Could indicate:

  * Testing environment
  * Misconfiguration

👉 Requires further investigation

---

### 🔹 Port 31337 — tcpwrapped

```
31337/tcp open tcpwrapped
```

#### Analysis:

* Connection is controlled or restricted
* Likely protected by access rules or wrappers

#### Security Insight:

* Service exists but **access is limited**
* Could be:

  * Admin service
  * Hidden backend service

👉 Indicates **restricted exposure**

---

# 🧠 OS Detection Analysis

```
Aggressive OS guesses: Linux 4.x – 5.x
```

#### Interpretation:

* System is **Linux-based**
* Kernel range identified (but not exact version)

#### Important Note:

* OS detection is probabilistic
* “No exact match” is normal in real-world scans

👉 Still sufficient for:

* exploit research
* attack planning

---

# 🔐 Overall Security Assessment

The target system exposes multiple services, including SSH and HTTP, which represent primary entry points. The detected service versions (OpenSSH 6.6.1 and Apache 2.4.7) are outdated and may contain known vulnerabilities.

The presence of:

* **Filtered ports** → indicates firewall usage
* **tcpwrapped services** → suggests access control mechanisms

This reflects a **moderately secured but still exposed system**.

---

## 🎯 Attack Surface Summary

* SSH → remote access vector
* HTTP → web-based attack surface
* Service versions → potential vulnerability entry points
* Filtered ports → partial defensive controls

---

# 🧠 Key Learnings

* Network reconnaissance is not just scanning — it is **interpretation**
* Service versions are critical for vulnerability identification
* OS detection supports attack strategy development
* NSE scripts enhance visibility into system behavior
* Understanding port states reveals security posture

---

# ⚠️ Disclaimer

This analysis was performed on an authorized target for educational purposes only. No unauthorized systems were accessed or exploited.


## 📈 Skills Demonstrated
- Network Scanning
- Service Enumeration
- OS Fingerprinting
- Security Analysis
- Attack Surface Identification
