# Android – Malicious APK Delivery (Laboratory)

## 📌 Objective
Simulate the **delivery phase of a malicious Android application** in a controlled laboratory environment, using the Metasploit Framework to generate a malicious APK and verify its presence on a target device.

This lab focuses on **payload creation, delivery and evidence collection**, adapting the methodology to non‑ideal environments and system limitations.

---

## 🧪 Laboratory Environment
- **Attacker machine:** Kali Linux  
- **Target device:** Android x86 (virtualized environment)  
- **Network:** Isolated local network (NAT)  
- **Tools used:**
  - Metasploit Framework (msfvenom)
  - Android Debug Bridge (ADB)
  - Nmap
  - arp-scan

> ⚠️ All activities were performed in a controlled environment for educational purposes only.

---

## 🧭 Methodology

### 1. Target Discovery
The Android device was identified within the local network using reconnaissance techniques to validate connectivity and confirm its presence in the lab environment.

### 2. Surface Analysis
A port scan was performed to identify exposed services and ensure the target was reachable before proceeding with payload delivery.

### 3. Malicious APK Generation
A malicious Android application was generated using Metasploit, embedding a **Meterpreter payload** to simulate a realistic malware delivery scenario.

### 4. Payload Delivery
The generated APK was transferred to the Android system using **ADB**, verifying that the file was successfully copied to the target device.

### 5. Evidence Collection
Due to limitations of the Android x86 environment (lack of graphical interface, inactive system services and framebuffer), it was not possible to install or execute the application normally.

Evidence was therefore collected from the attacker machine, confirming the **presence of the malicious APK in the Android file system**, which validates the delivery phase of the attack.

---

## 📷 Evidence
Screenshots included in this lab document:
- Network discovery and connectivity validation
- Payload delivery process
- Verification of the malicious APK on the target system

> Evidence was captured from the attacker environment due to the absence of a functional GUI on the Android system.

---

## 🔍 Results
- A malicious Android APK was successfully generated.
- The payload was delivered to the target device.
- The presence of the malicious file was confirmed in the Android file system.
- Environmental limitations did not prevent achieving the objectives of the lab.

---

## 🛡️ Mitigation and Best Practices
- Disable installation from unknown sources.
- Restrict or monitor ADB access.
- Implement application integrity validation.
- Apply device hardening and continuous monitoring.

---

## 📚 Key Takeaways
This laboratory highlights:
- The importance of the delivery phase in mobile attack chains.
- The need for adaptability when working with restricted environments.
- The value of proper documentation and evidence collection.
- How offensive techniques can be leveraged to improve defensive awareness.

---

## ⚖️ Legal Disclaimer
This project was conducted **strictly for educational purposes** in a controlled laboratory environment.  
It must not be used against real systems without explicit authorization.
