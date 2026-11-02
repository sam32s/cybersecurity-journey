# Network Scanning and Service Enumeration

## 1. Introduction

This exercise involved scanning the Metasploitable 2 virtual machine from Kali Linux using Nmap.

The objective was to identify open ports, discover running services, and understand the target's network exposure.

## 2. Lab Environment

- Attacker: Kali Linux
- Target: Metasploitable 2
- Network: Isolated VirtualBox Internal Network
- Scanning Tool: Nmap

## 3. Host Discovery

Command:

```bash
ping -c 3 192.168.50.20

### Host Discovery Result

The ping test was successful. The target machine was reachable from Kali Linux.

```bash
ping -c 3 192.168.50.20
4. Port Scanning

Command:

sudo nmap -sS 192.168.50.20

Result:

Target host was discovered as UP.
Multiple TCP ports were found OPEN.
The target exposed several network services.
5. Service and Version Detection

Command:

sudo nmap -sV 192.168.50.20

Important services identified:

Port	Service	Detected Version
21	FTP	vsftpd 2.3.4
22	SSH	OpenSSH 4.7p1
23	Telnet	Linux telnetd
25	SMTP	Postfix
53	DNS	BIND 9.4.2
80	HTTP	Apache 2.2.8
3306	MySQL	5.0.51a
5432	PostgreSQL	8.3.x
6667	IRC	UnrealIRCd
8180	HTTP	Apache Tomcat
6. SSH Enumeration

Command:

sudo nmap --script ssh2-enum-algos -p 22 192.168.50.20

Finding:

The SSH server supported several older cryptographic algorithms.
Legacy algorithms such as ssh-rsa and ssh-dss were offered.
7. SSH Authentication

Command:

ssh -o HostKeyAlgorithms=+ssh-rsa msfadmin@192.168.50.20

Result:

Successfully established an SSH session in the authorized lab.
Logged in as the user msfadmin.
8. Linux Privilege Enumeration

Commands:

whoami
id
sudo -l
sudo whoami

Results:

Current user: msfadmin.
The account had unrestricted sudo privileges.
Running sudo whoami returned root.
9. Security Findings

The assessment identified:

Multiple exposed network services.
Outdated service versions.
Legacy SSH cryptographic algorithms.
An account with excessive sudo privileges.
An unnecessarily large network attack surface.
10. Conclusion

The assessment demonstrated how Nmap can identify active hosts, discover open ports, detect running services, and support security enumeration.

SSH testing also demonstrated why weak configurations and excessive user privileges create security risks.

All testing was performed against an intentionally vulnerable Metasploitable 2 virtual machine in an isolated VirtualBox lab.


**Important:** The commands above document the work we actually performed. Don't add results from tests we haven't completed.

Once you've pasted it, send me a screenshot before committing. We'll check the formatting together.
