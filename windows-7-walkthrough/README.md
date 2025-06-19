# Windows 7 Exploitation Walkthrough

This folder provides a detailed walkthrough of exploiting a Windows 7 system using tools like Netdiscover, Nmap, Searchsploit, and leveraging the EternalBlue vulnerability to gain access.

## Table of Contents

- Introduction
- Tools Used
- Exploitation Steps
- Important Links
- Disclaimer

## Introduction

This guide demonstrates a penetration testing scenario where a Windows 7 system is exploited using EternalBlue. The walkthrough includes:

- Network reconnaissance.
- Vulnerability identification.
- Exploitation using a payload to gain shell access.

This material is intended for ethical hacking and cybersecurity training purposes only.

## Tools Used

- **Netdiscover**: Network reconnaissance tool to identify devices in a network.
- **Nmap**: Network scanning tool to discover hosts, services, and vulnerabilities.
- **Searchsploit**: Tool for searching exploits in the Exploit-DB database.
- **Metasploit Framework**: Framework for developing and executing exploit code.

## Exploitation Steps

1. **Network Discovery**: Use Netdiscover to identify devices on the network.
2. **Network Scanning**: Run Nmap to scan for open ports and services.
3. **Identifying Vulnerabilities**: Search for the EternalBlue exploit using Searchsploit.
4. **Preparing the Exploit**: Use Searchsploit to locate EternalBlue in Exploit-DB.
5. **Setting Up the Exploit**: Load EternalBlue exploit in Metasploit, set RHOSTS and LHOST.
6. **Configure the Payload**: Select `generic/shell_reverse_tcp` for a reverse shell.
7. **Exploit the Target**: Run the exploit to gain access.
8. **Gaining a Shell**: Use Meterpreter to interact with the target system.

## Important Links

- [Exploit-DB](https://www.exploit-db.com/)
- [Metasploit Framework](https://www.metasploit.com/)

## Disclaimer

This guide is for educational purposes and authorized testing only. Unauthorized access to systems is illegal and unethical. Always obtain proper permission.

---

**You can find the full walkthrough as a PDF in this directory: _windows 7 walkthrough.pdf_**
