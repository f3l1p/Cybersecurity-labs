# 🛡️ Corporate Network Security Audit – Master’s Final Project

**Author:** Felipe Chicangana  
**Environment:** Controlled lab setup using Windows Server (WS2012_MD) and Linux (linux_md)  
**Tools:** Kali Linux, Nmap, Nikto, Gobuster, Hydra, Metasploit, WPScan, LinPEAS, WinPEAS  

---

## 📋 Executive Summary

This project presents a **security audit** of a simulated corporate network conducted as part of the **Ethical Hacking Master’s program** at MasterD.  

The audit aimed to:

- Identify vulnerabilities  
- Evaluate potential risks  
- Provide actionable recommendations to improve the security posture  

Two systems were analyzed:

| System       | Summary |
|--------------|---------|
| **WS2012_MD (Windows Server)** | Multiple vulnerabilities detected, including weak passwords, exposed services, and insecure WordPress configuration |
| **linux_md (Linux Server)** | Minimal exposure: only DNS (port 53) open. Demonstrates proper network segmentation and restricted service exposure |

---

## 🔍 Key Findings

| System       | Vulnerabilities | Risk Level Summary |
|--------------|----------------|-----------------|
| **WS2012_MD**    | 7              | 1 Critical, 2 Medium, 4 Low/Informational |
| **linux_md**     | 0              | No exploitable vulnerabilities detected |

**Main Risks Identified:**

- Weak or easily guessable passwords  
- User enumeration via WordPress and MSRPC  
- Exposure of sensitive services (RPC, SMB) and web files  
- Poor WordPress configuration enabling brute-force attacks  
- Minimal exposure on Linux shows good segmentation and firewall policies  

---

## 🛠️ Methodology

1. **Reconnaissance** – Identified hosts, services, open ports, and users using Nmap, Netdiscover, WPScan, etc.  
2. **Vulnerability Assessment** – Classified vulnerabilities by severity: Critical, High, Medium, Low/Informational  
3. **Exploitation & Validation** – Controlled exploitation using Hydra, Metasploit, Gobuster, and scripts  
4. **Risk Analysis** – Evaluated impact on **Confidentiality, Integrity, Availability (CIA)**  
5. **Reporting & Recommendations** – Provided actionable remediation steps  

---

## ⚠️ Detailed Vulnerabilities (WS2012_MD)

1. **Weak WordPress passwords** – Critical risk, allows unauthorized access  
2. **Enumeration of WordPress users** – Medium risk, exposes valid usernames  
3. **Enumeration via MSRPC** – Low risk, reveals system accounts & policies  
4. **Weak password policies** – Medium risk, facilitates brute-force attacks  
5. **Exposed SMB/IPC$ shares** – Low risk, leaks system information  
6. **Exposed RPC service** – Informational, potential attack surface for historical exploits  
7. **Exposed web files** – Informational/Low risk, allows CMS structure enumeration  

**Linux server (linux_md)**: Only DNS (port 53) open; no exploitable vulnerabilities detected.

---

## 🔧 Recommendations

**1️⃣ Password & Credential Management**

- Enforce strong passwords: **≥12 characters, mix of upper/lower case, numbers, symbols**  
- Disable/review accounts with default or weak passwords  
- Implement **2FA** for critical services  

**2️⃣ CMS Security (WordPress)**

- Restrict user enumeration (`/author=ID`)  
- Disable registration if not required  
- Update WordPress core, plugins, and themes  
- Use security plugins: **Wordfence**, **iThemes Security**  
- Restrict access to sensitive directories (`/wp-admin`, `/wp-content`)  

**3️⃣ Network & Service Hardening**

- Close/filter unnecessary services: **MSRPC, SMB, WinRM**  
- Use firewalls & VLAN segmentation  
- Continuously monitor open ports and services  

**4️⃣ Monitoring & Audit**

- Deploy **IDS/IPS** to detect anomalous activity  
- Audit file uploads, logs, and access patterns regularly  
- Document all changes and track security incidents  

---

## 🛠️ Tools Used

- **Network Recon:** Nmap, Netdiscover, Gobuster  
- **Web & CMS Security:** WPScan, Nikto, Hydra  
- **Exploitation & Pivoting:** Metasploit, LinPEAS, WinPEAS  
- **Utilities:** curl, requestly, rpcclient  

---

## 📚 References

- [Nmap Network Scanning](https://nmap.org/book)  
- [OWASP Top Ten](https://owasp.org/www-project-top-ten/)  
- [CVE Database](https://cve.mitre.org)  
- [WordPress Hardening Guide](https://wordpress.org/support/article/hardening-wordpress/)  
- [Metasploit Framework Documentation](https://docs.rapid7.com/metasploit/)  
- [LinPEAS & WinPEAS](https://github.com/carlospolop/PEASS-ng)  

---

> ⚠️ **Note:** This audit was performed in a **controlled lab environment**. Results reflect the simulated network setup and are intended for educational purposes.
