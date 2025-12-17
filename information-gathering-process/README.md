# 🖥️ Exercise – Information Gathering Process

**Author:** Felipe Chicangana  
**Target Machine:** Metasploitable 2  
**Environment:** Controlled lab, private network (host-only/NAT)  
**Attacker Machine:** Kali Linux (IP: 192.168.220.130)  

---

## 1️⃣ Introduction

This report documents the **information gathering (reconnaissance) process** carried out on the vulnerable machine **Metasploitable 2**.  

The main goal is to identify key information that could be useful for **future security analysis or controlled penetration testing**.  

Reconnaissance allows to:

- Identify active systems and services  
- Discover users and potential credentials  
- Detect exposed sensitive files  

**Tools used:**

- `netdiscover`, `arp-scan` – Discover IPs on the local network  
- `nmap` – Scan ports and services  
- `enum4linux`, `smbclient`, `ftp`, `dirb`, `nikto`, `hydra` – Enumerate and test services  

The report includes screenshots, logs, and relevant findings.

---

## 2️⃣ Scope

The scope is limited to the **passive and active reconnaissance phase** on the Metasploitable 2 machine:

- Identify the **target system's IP address**  
- Discover **open ports and services**  
- Enumerate **users, passwords, and exposed sensitive files**  

**Best practices:** All tests were conducted in a **secure environment**, without affecting other systems.

| Element              | Description |
|---------------------|-------------|
| IP Address           | 192.168.220.128 |
| Open Ports/Services  | See Section 4 |
| Users                | msfadmin, user, postgres |
| Passwords            | msfadmin, user, postgres |
| Sensitive Files      | See Section 4 |

---

## 3️⃣ Process

1. **Network Discovery:**  
   - Scanned the network using:  
     ```bash
     sudo netdiscover -i eth0 -r 192.168.220.0/24
     ```  
   - Target IP discovered: **192.168.220.128**

2. **Port Scanning with Nmap:**  
   - Identified which services were running and open.

3. **FTP Service Enumeration (Port 21):**  
   - Tried login with `anonymous` – successful login but directory listing was empty.  
   - Also tested credentials: `guest`, `admin` – unsuccessful.  
   - `user` account allowed same limited access as `anonymous`.  
   - Tested known vulnerability in vsftpd 2.3.4 – no success.

4. **SMB Service Enumeration:**  
   - Used `enum4linux` to identify users and accessible folders.  
   - Only `tmp` shared folder allowed listing without credentials.  
   - Admin shares (`print$`, `opt`, `ADMIN$`, `IPC$`) denied access.  
   - SMB1 presence indicates outdated protocol, posing additional risks.

5. **Password Attacks:**  
   - Created a user list from gathered info.  
   - Performed brute-force attack with `hydra` using user list and password guesses.  
   - Discovered repeated passwords among some users.

6. **FTP Access with Discovered Credentials:**  
   - Tested `postgres` credentials – accessed multiple sensitive files in `8.3/main`.  
   - Tested `msfadmin` credentials – found vulnerable paths.  
   - Accessed `mysql-ssl` – downloaded several vulnerable files.

---

## 4️⃣ Findings

**IP Address:** 192.168.220.128  

**Open Ports and Services:**

| Port  | Protocol | Service      | Version/Notes |
|-------|---------|-------------|---------------|
| 21    | tcp     | ftp         | vsftpd 2.3.4 |
| 22    | tcp     | ssh         | OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0) |
| 23    | tcp     | telnet      | Linux telnetd |
| 25    | tcp     | smtp        | Postfix smtpd |
| 53    | tcp     | domain      | ISC BIND 9.4.2 |
| 80    | tcp     | http        | Apache httpd 2.2.8 ((Ubuntu) DAV/2) |
| 111   | tcp     | rpcbind     | 2 (RPC #100000) |
| 139   | tcp     | netbios-ssn | Samba smbd 3.X - 4.X (workgroup: WORKGROUP) |
| 445   | tcp     | netbios-ssn | Samba smbd 3.X - 4.X (workgroup: WORKGROUP) |
| 512   | tcp     | exec        | netkit-rsh rexecd |
| 513   | tcp     | login       | OpenBSD or Solaris rlogind |
| 514   | tcp     | tcpwrapped  | - |
| 1099  | tcp     | java-rmi    | GNU Classpath grmiregistry |
| 1524  | tcp     | bindshell   | Metasploitable root shell |
| 2049  | tcp     | nfs         | 2-4 (RPC #100003) |
| 2121  | tcp     | ftp         | ProFTPD 1.3.1 |
| 3306  | tcp     | mysql       | MySQL 5.0.51a-3ubuntu5 |
| 5432  | tcp     | postgresql  | PostgreSQL DB 8.3.0 - 8.3.7 |
| 5900  | tcp     | vnc         | VNC (protocol 3.3) |
| 6000  | tcp     | X11         | Access denied |
| 6667  | tcp     | irc         | UnrealIRCd |
| 8009  | tcp     | ajp13       | Apache Jserv (Protocol v1.3) |
| 8180  | tcp     | http        | Apache Tomcat/Coyote JSP engine 1.1 |

**Users:**

- msfadmin  
- user  
- postgres  

**Passwords:**

- msfadmin  
- user  
- postgres  

**Sensitive Files:**

- my.cnf  
- mysql-keys
  - server-key.pem  
  - client-key.pem  
- samba  
- tikiwiki  
- twiki2003021  

---
