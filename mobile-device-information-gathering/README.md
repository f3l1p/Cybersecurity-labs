# 📱 Exercise – Mobile Device Information Gathering

**Author:** Felipe Chicangana  
**Environment:** Controlled laboratory (Android + Kali Linux)  
**Focus:** Mobile device reconnaissance and enumeration  

---

## 1️⃣ Introduction

The objective of this report is to document the **full information gathering process** performed against an **Android laboratory environment** provided as part of a cybersecurity training course.

The report includes all relevant data collected during the exercise, such as:

- Network discovery results  
- Service and port enumeration  
- Logs from security tools  
- Screenshots and evidence of findings  

Unlike previous exercises where the target IP address is known from the beginning, this scenario intentionally starts **without prior knowledge of the target device**. The goal is to simulate a more realistic situation by scanning the network to identify the mobile device and progressively collect as much information as possible from the earliest stages of reconnaissance.

---

## 2️⃣ Scope

The scope of this exercise is limited to the **information gathering phase** and includes the identification and enumeration of the following elements:

- IP address  
- Open ports and services  
- Users  
- Passwords  
- Sensitive files  

The tools used during this exercise include:

- `nmap`  
- `Burp Suite`  
- `airgeddon`  
- `ip`  
- `Metasploit Framework`  

All activities were conducted in a **controlled and isolated environment**.

---

## 3️⃣ Methodology & Lab Configuration

As an initial configuration:

- Both virtual machines (**Kali Linux** and the Android laboratory environment) are connected to the **same NAT network**.
- This setup allows controlled network communication while preventing external exposure.

The methodology follows a standard penetration testing reconnaissance workflow:

1. Network discovery  
2. Target identification  
3. Port and service enumeration  
4. Preliminary vulnerability assessment  

---

## 4️⃣ Process

1. **Environment Initialization**  
   - Both virtual machines (Kali Linux and the Android lab) were powered on.

2. **Network Discovery**  
   - Network scanning was performed to identify nearby systems and detect the target device.
   - The target mobile device was successfully identified along with its associated IP address.
   - Additional information such as operating system details was also collected.

3. **Port Scanning and Service Enumeration**  
   - An initial `nmap` scan was executed against the discovered IP address to identify open ports.
   - The results showed a significant number of open ports, indicating a potentially vulnerable system.

4. **Advanced Service Detection**  
   - A more advanced `nmap` scan was performed to gather detailed information about the services and their versions.
   - This step enabled deeper analysis and helped identify potential attack vectors.

5. **Service-Based Testing**  
   - Based on the information gathered, the assessment proceeded **port by port**, evaluating each exposed service.
   - The first test focused on **TCP port 21 (FTP)**, attempting common credentials such as:
     - `admin`
     - `user`
     - `guest`

This structured approach mirrors real-world reconnaissance techniques used during mobile and network security assessments.

---

## 5️⃣ Findings

> The following findings summarize the results obtained during the reconnaissance phase.

- Target IP address successfully identified  
- Multiple open ports and exposed services detected  
- Service versions identified, indicating potential vulnerabilities  
- Authentication mechanisms found to be weak or misconfigured in certain services  

*(Detailed logs and screenshots are included in the appendices.)*

---

## 6️⃣ Recommendations

Based on the findings, the following recommendations are proposed:

- Minimize exposed services by closing unnecessary ports  
- Enforce strong authentication policies  
- Regularly update and patch services and operating systems  
- Segment mobile devices from critical internal networks  
- Monitor network traffic for anomalous activity  

---

## 7️⃣ Conclusion

This exercise successfully demonstrated a **realistic information gathering process** against a mobile device without prior knowledge of its network configuration.

Starting from basic network discovery, the assessment progressively identified the target system, enumerated open ports and services, and revealed multiple potential attack vectors. The results highlight the importance of proper network segmentation, secure service configuration, and continuous monitoring, especially in mobile environments.

The exercise reinforces core skills in reconnaissance, analysis, and documentation—fundamental competencies for cybersecurity professionals.

---

## 8️⃣ Appendices

- Network scan logs  
- `nmap` output files  
- Tool execution evidence  
- Screenshots supporting each phase of the process  

