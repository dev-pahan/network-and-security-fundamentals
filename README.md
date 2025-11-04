# Network and Security Fundamentals  

This repository documents my hands-on journey through **network fundamentals**, **security configurations**, and **log analysis** as part of my BSc Cyber Security at ECU.  

I use this repo to record the tools, configurations, and experiments that help me build a base foundation for my future in **cyber security** and **network defense**.  


## Tools & Technologies  
- **Ubuntu / Kali Linux** – primary environments for configuration and testing  
- **Nmap** – network and service scanning  
- **Wireshark** – packet capture and protocol inspection  
- **Linux Firewalls (iptables / nftables)** – packet filtering, NAT, and custom rule sets  
- **OpenSSH (with Google Authenticator MFA)** – secure remote access and multi-factor authentication setup
- **Cowrie Honeypot** – simulating SSH attacks and analyzing malicious activity  
- **Encryption Methods** – symmetric & asymmetric cryptography (AES, RSA)  
- **Log Analysis** – reviewing system, firewall, and honeypot logs for anomalies  


## Key Practical Labs  

### 🔹 **1. Nmap Scanning & Network Enumeration**  
  - Performed host discovery, port scans, and service identification using:  
    ```
    nmap -sV -A 192.168.1.10
    ```
  - Learned to interpret open ports, banners, and OS fingerprints.
  
  Compared scan outputs between Kali and Ubuntu environments.

### 🔹 2. Linux Firewall Configuration (iptables / nftables)
  - Configured iptables to define custom firewall rules:
    ```
    sudo iptables -P INPUT DROP
    sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
    sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
    sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
    sudo iptables -L -v
    ```
  - Logged dropped packets for later analysis via /var/log/syslog.
  
  - Explored nftables for modern rule management and compared efficiency with iptables.
  
  - Practiced packet tracing with:
  ```
  sudo iptables -A INPUT -j LOG --log-prefix "Dropped Packet: "
  ```
  - Understood rule chains, persistence, and NAT translation.

### 🔹 3. Secure Remote Access with OpenSSH (with MFA)

  - Installed and configured an OpenSSH server on Ubuntu for secure remote access.
  
  - Implemented key-based authentication and integrated Google Authenticator MFA for an additional security layer.
  Steps included:
  
  1. Installed the PAM module for Google Authenticator:
  ```
  sudo apt install libpam-google-authenticator
  ```
  
  2. Enabled MFA per user:
  ```
  google-authenticator
  ```
  
  3. Updated the PAM config at /etc/pam.d/sshd:
  ```
  auth required pam_google_authenticator.so
  ```
  
  4. Edited /etc/ssh/sshd_config to allow both public key and MFA:
  ```
  ChallengeResponseAuthentication yes
  AuthenticationMethods publickey,keyboard-interactive
  ```
  
  5. Restarted SSH and tested login using a one-time MFA code.
  
  Monitored /var/log/auth.log for failed logins, brute-force attempts, and MFA validation.
  Restricted SSH access to specific IP ranges for better control.

### 🔹 4. Cowrie Honeypot Deployment & Log Analysis
  - Deployed a Cowrie SSH honeypot to observe attacker interactions.
  
  - Captured logs containing:
  
  - Attacker IP addresses, timestamps, and entered commands
  
  - Common brute-force credentials
  
  - File download attempts and malware behavior
  
  - Analyzed logs to understand common attack patterns and indicators of compromise (IOCs).


### 🔹 5. Encryption Practice
  - Implemented AES and RSA encryption using Python and OpenSSL.
  
  - Practiced hashing and verification:
    ```
    md5sum file.txt
    sha256sum file.txt
    ```
  - Learned the differences between encryption, hashing, and encoding, and how to combine them for data integrity.

## What I’ve Learned
  - Fundamentals of TCP/IP, subnetting, and network protocols.
  
  - Secure access management using OpenSSH.
  
  - Firewall management with iptables/nftables and packet filtering logic.
  
  - Hands-on log analysis to detect suspicious activity.
  
  - Practical exposure to honeypots and real-world attack data.
  
  - Strengthened command-line confidence in Linux environments.
