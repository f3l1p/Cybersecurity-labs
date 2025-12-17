# Pivoting – Internal Network Access via Metasploitable 2

## 📌 Objective
Demonstrate a **pivoting attack scenario** by compromising an initial vulnerable host and using it as an entry point to access an otherwise unreachable internal network.

The goal of this laboratory is to show how an attacker can leverage an initial foothold to **route traffic, scan internal hosts and interact with internal services** using Metasploit.

---

## 🧪 Laboratory Environment
- **Attacker machine:** Kali Linux  
- **Initial target:** Metasploitable 2  
- **Secondary target:** Internal host (isolated network)  
- **Virtualization:** VMware  
- **Network configuration:**
  - NAT network (external)
  - Host‑Only network (internal)

### Network overview
- Kali Linux: `192.168.220.0/24`
- Metasploitable 2:
  - External interface: `192.168.220.128`
  - Internal interface: `10.10.0.128`
- Internal host: `10.10.0.130`

> ⚠️ All actions were performed in a controlled and isolated lab environment.

---

## 🧭 Methodology

### 1. Initial Access
Access to the first Metasploitable 2 machine was obtained using a known vulnerable service (`vsftpd 2.3.4`), resulting in a remote session with elevated privileges.

This initial compromise provided the necessary foothold to perform lateral movement.

---

### 2. Meterpreter Session
A **Meterpreter session** was established on the compromised host, allowing full interaction with the system and visibility of its network configuration.

By inspecting the network interfaces, a **second internal network (10.10.0.0/24)** was identified, which was not directly accessible from Kali Linux.

---

### 3. Route Injection (Autoroute)
The internal network was added to Metasploit’s routing table using post‑exploitation modules, enabling traffic to be forwarded through the compromised host.

This step effectively turned the initial victim into a **pivot point**.

---

### 4. Internal Network Reconnaissance
Once routing was configured, internal network reconnaissance was performed:

- Scanning internal IP ranges
- Identifying reachable hosts and exposed services
- Validating connectivity from the attacker machine through the pivot

Both Metasploit auxiliary modules and external tools were tested to assess reliability.

---

### 5. Proxy and Port Forwarding
To interact with internal services using standard Kali tools:

- A **SOCKS proxy** was configured inside Metasploit
- Proxychains was used to route external tools through the Meterpreter session
- **Port forwarding (portfwd)** was applied to expose internal services (e.g. FTP) to Kali Linux

This allowed direct interaction with internal services that were otherwise unreachable.

---

## 📷 Evidence
Screenshots included in this lab document:
- Network discovery and target identification
- Meterpreter session establishment
- Internal network detection
- Route injection and proxy configuration
- Access to internal services via port forwarding

---

## 🔍 Results
- Initial access to Metasploitable 2 was successfully achieved.
- A Meterpreter session was established with root privileges.
- An internal, isolated network was identified and accessed.
- Traffic was routed through the compromised host.
- Internal services were enumerated and accessed from Kali Linux.

---

## 🛡️ Mitigation and Best Practices
- Proper network segmentation and isolation.
- Removal of vulnerable legacy services (e.g. insecure FTP).
- Monitoring of lateral movement and routing anomalies.
- Limiting administrative access and enforcing least privilege.
- Detection of tunneling, proxying and abnormal traffic patterns.

---

## 📚 Key Takeaways
This laboratory demonstrates:
- The critical role of pivoting in real‑world attacks.
- How a single compromised host can expose internal networks.
- The importance of monitoring post‑exploitation activity.
- Why internal services should never rely solely on network isolation for security.

---

## ⚖️ Legal Disclaimer
This project was conducted **strictly for educational purposes** in a controlled laboratory environment.  
It must not be used against real systems without explicit authorization.
