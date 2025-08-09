# 🔐 Hackathon Machine Walkthrough

This repository contains a detailed walkthrough of how I successfully compromised a Hackathon machine. This document outlines the steps taken, from initial reconnaissance to privilege escalation, providing commands and explanations for each phase.

---

## 🚀 Getting Started

This walkthrough assumes basic familiarity with Kali Linux and common penetration testing tools.

**Tools Used:**
- **Netdiscover:** For network reconnaissance.
- **Nmap:** For port scanning and service enumeration.
- **Gobuster:** For directory brute-forcing.
- **Medusa:** For SSH brute-forcing.
- **SSH Client:** To connect to the target machine.
- **Vim:** For privilege escalation.

---

## 👣 Walkthrough Steps

### Step 1: Network Reconnaissance with Netdiscover

The initial step involved identifying live hosts on the network using Netdiscover. This tool leverages ARP requests to discover active devices. The scan revealed a target IP address of `192.168.1.22`.

> **Example command:**
> ```bash
> sudo netdiscover -r 192.168.1.0/24
> ```

---

### Step 2: Port and Service Scanning with Nmap

After identifying the target, I used Nmap (`192.168.1.22`) to scan for open ports and enumerate services. The scan revealed several key services:

- **Port 21 (ftp):** vsftpd 3.0.2
- **Port 23 (telnet):** Linux telnetd
- **Port 80 (http):** Apache httpd 2.4.7
- **Port 7223 (ssh):** OpenSSH 6.6.1p1

> **Command:**
> ```bash
> nmap -sV -sC 192.168.1.22
> ```

---

### Step 3: Directory Brute-Forcing with Gobuster

I then used Gobuster to discover hidden directories and files on the web server (port 80). The command specified the URL, a common wordlist, and common web file extensions (`.php`, `.html`, `.zip`). This led to the discovery of the `/sudo.html` directory.

> **Command:**
> ```bash
> gobuster dir -u http://192.168.1.22 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,html,zip
> ```

---

### Step 4: Examining the HTML Source of `/sudo.html`

Navigating to `http://192.168.1.22/sudo.html` in a web browser displayed a simple page. However, by inspecting the HTML source code, a hidden comment was uncovered, revealing a potential username:  
**Funame:** `test`.  
This clue was crucial for the next steps.

---

### Step 5: Brute-Forcing SSH Credentials with Medusa

With the `test` username in hand, I employed Medusa, a fast and modular login brute-forcer, to find the password for the SSH service on port 7223. I used the `rockyou.txt` wordlist for this attack. Medusa successfully identified the credentials:

- **User:** test
- **Password:** jordan23

> **Command:**
> ```bash
> medusa -u test -P /usr/share/wordlists/rockyou.txt -h 192.168.1.22 -M ssh -p 7223
> ```

---

### Step 6: Gaining a Foothold via SSH

Using the found credentials (`test:jordan23`), I logged into the target system via SSH on port 7223. Once connected, I navigated through the file system and located a file named `ctf` within the `/home` directory, which contained the flag.

> **Command:**
> ```bash
> ssh test@192.168.1.22 -p 7223
> ```

---

### Step 7: Privilege Escalation and Root Access

To achieve root access, I investigated hidden files, specifically `.bash_history` in the user's home directory. This file revealed a previously executed command:
`sudo -u#-1 /bin/bash`

This is a known privilege escalation technique. By executing this command, I successfully obtained a root shell, gaining full control of the machine.

---

## 🎉 Conclusion

This walkthrough demonstrates a typical approach to compromising a vulnerable machine, covering essential stages of penetration testing from initial reconnaissance to gaining root privileges. Each step built upon the last, leveraging various tools and techniques to progressively exploit the machine's weaknesses.

---

**Disclaimer:**  
This walkthrough is for educational purposes only. Do not attempt unauthorized access to systems. Always have proper authorization before conducting penetration testing.
