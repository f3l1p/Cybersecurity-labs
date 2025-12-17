# Wireshark Sniffing with Results

**Author:** Carlos Felipe Chicangana

---

## 1. Introduction

This report documents the process of performing network traffic sniffing against a vulnerable machine (Metasploitable2) using Wireshark. The main objective was to capture and analyze network traffic using protocol-specific filters in order to identify sensitive information such as credentials transmitted over the network.

---

## 2. Scope

The scope of this exercise is limited to the analysis of sniffed traffic between the attacker machine and the target system:

- Attacker machine (Kali Linux): `192.168.200.8`
- Target machine (Metasploitable2): `192.168.200.6`

The analysis focuses on identifying credentials and sensitive data transmitted over the following services:

- HTTP
- FTP
- MySQL

Wireshark display filters were used to isolate and analyze relevant traffic.

---

## 3. Methodology

The exercise began by enabling IP forwarding on the attacker machine to allow proper traffic handling.

Wireshark was then launched on Kali Linux, selecting the active network interface `eth0` to begin packet capture.

An FTP connection was initiated from Kali Linux to Metasploitable2 using the credentials `msfadmin:msfadmin`. Once the connection was established, Wireshark successfully captured the network traffic generated during the authentication process.

Basic filters such as `icmp` were tested initially to validate packet capture functionality.

Next, access to the DVWA web application hosted on Metasploitable2 was performed in order to generate HTTP traffic. Unlike previous exercises, this time the captured traffic produced clear and useful results.

By filtering HTTP traffic and focusing on POST requests, it was possible to observe transmitted credentials in clear text, confirming a successful capture.

The ARP filter was also tested, but no relevant results were captured during this phase.

To reduce noise, a filter was applied to display only traffic exchanged between the two machines:

`ip.addr == 192.168.200.8 && ip.addr == 192.168.200.6`

FTP traffic was then analyzed in detail, revealing a significant amount of sensitive information. Even though capturing credentials was not explicitly required, the analysis showed that the FTP username and password were transmitted in clear text.

To confirm this, the following filter was applied:

`ftp.request.command == "USER" || ftp.request.command == "PASS"`

This filter clearly displayed the FTP authentication credentials.

Finally, an attempt was made to connect to the MySQL service running on Metasploitable2. Traffic was filtered using:

`tcp.port == 3306`

While MySQL authentication traffic was captured, the credentials were not visible in plain text, as the protocol obfuscates sensitive information during authentication.

---

## 4. Findings

### FTP

- Vulnerable protocol: FTP
- Source IP: `192.168.200.8`
- Destination IP: `192.168.200.6`
- Credentials captured successfully
- Applied filter: `ftp.request.command == "USER" || ftp.request.command == "PASS"`

### HTTP

- POST requests captured containing credentials in clear text
- Username: `admin`
- Password: `password`
- Vulnerable service: HTTP (no HTTPS encryption)

### MySQL

- Authentication attempt observed from Kali Linux
- Traffic captured but credentials not readable
- Port: `3306`

---

## 5. Conclusion

In this exercise, Wireshark was used to capture and analyze network traffic between a Kali Linux machine and Metasploitable2. Multiple services were tested, including FTP, HTTP (DVWA), and MySQL.

The results demonstrated that:

- FTP and HTTP transmit credentials in clear text, making it trivial to extract usernames and passwords using Wireshark.
- MySQL traffic was visible, but credentials were not easily recoverable due to protocol-level protections.

This exercise highlights the effectiveness of Wireshark for network analysis and reinforces the critical security risks associated with using unencrypted protocols in production environments.
