# Windows-1


## Project Overview

This project demonstrates a vulnerable Windows-based lab designed for offensive cybersecurity training. The lab simulates a legacy enterprise file server running an outdated Windows operating system that is vulnerable to the EternalBlue exploit (MS17-010). The goal of this lab is to help learners understand real-world exploitation of unpatched SMB services, post-exploitation enumeration, and privilege escalation in a controlled environment.

This lab is intended strictly for educational and ethical security research purposes.

---

## Lab Links

Download Windows-1 : https://mega.nz/file/TRQmGJIC#syfm00N_z1xcUVrsYSTzyW3Qv0fc5CRCW8UDLKvysKM
Documentation for Windows-1 With Walkthrough: https://drive.google.com/file/d/1sEMaauP_jIeu_CvYPWvRZ7Q4vXVPUKfD/view?usp=drive_link

---

## Vulnerability Summary

- Vulnerability Name: EternalBlue
- Microsoft Security Bulletin: MS17-010
- CVE Identifier: CVE-2017-0144
- Vulnerability Type: Remote Code Execution (RCE)
- Attack Vector: Network (SMBv1)
- Authentication Required: No
- User Interaction: None

---

## CVE Impact Description

CVE-2017-0144 is a critical remote code execution vulnerability in the Microsoft Server Message Block version 1 (SMBv1) protocol. The vulnerability exists due to improper handling of specially crafted SMB packets. An unauthenticated attacker can exploit this vulnerability to execute arbitrary code with SYSTEM-level privileges.

Because the vulnerability is wormable, it can be used to spread laterally across a network without user interaction. This flaw was notably exploited by ransomware campaigns such as WannaCry and NotPetya.

---

## Exploited Service Details

- Service Name: Server Message Block (SMB)
- Protocol Version: SMBv1
- Default Port: TCP 445
- Exploit Target: srv.sys kernel driver
- Privilege Gained: NT AUTHORITY\SYSTEM

---

## Exploitable Operating System

The vulnerability is exploitable only on specific unpatched Windows versions.

### Tested and Recommended Version

- Operating System: Windows 7 Professional SP1
- Architecture: x64 (64-bit)
- Patch Status: Unpatched (MS17-010 not installed)
- SMBv1: Enabled
- Windows Updates: Disabled

### Non-Exploitable Configurations

- Windows 7 with MS17-010 patches installed
- Windows 10 and newer versions
- Windows 7 x86 (32-bit) due to exploit instability

---

## Lab Objectives

- Identify vulnerable SMB services using network enumeration
- Exploit MS17-010 to gain remote access
- Achieve SYSTEM-level privileges
- Perform post-exploitation enumeration
- Retrieve user and administrator flags
- Understand risks of legacy Windows systems in enterprise environments

---

## Flag Structure

This lab uses a Capture The Flag (CTF)-style approach.

- User Flag Location: C:\Users\support\Desktop\user.txt

- Administrator Flag Location: C:\Windows\System32\config\admin.txt

---

## Minimum System Requirements

### Host Machine (Virtualization Host)

- CPU: Quad-core processor with virtualization support
- RAM: Minimum 8 GB (16 GB recommended)
- Storage: At least 80 GB free disk space
- Virtualization Software:
- VMware Workstation
- VirtualBox

---

### Vulnerable Machine (Windows 7)

- RAM: 2 GB minimum
- CPU: 1 core
- Disk Space: 40 GB
- Network Adapters:
- NAT (external access)
- Host-only or Internal (pivoting)

---

### Attacker Machine (Kali Linux)

- RAM: 2–4 GB
- CPU: 2 cores
- Disk Space: 20 GB
- Tools Required:
- Nmap
- Metasploit Framework
- smbclient
- Netcat

---

# Steps to Recreate the Lab Environment

### Step 1: Create the Windows 7 Virtual Machine

1. Create a new virtual machine in VMware or VirtualBox
2. Install Windows 7 Professional SP1 (x64)
3. Disable automatic updates during installation
4. Do not install any security patches
5. Disable Windows Defender and Firewall

---

### Step 2: Verify SMBv1 and Patch Status

1. Open Command Prompt as Administrator
2. Ensure SMBv1 is enabled
3. Confirm MS17-010 patches are not installed: wmic qfe

---

### Step 3: Create User Accounts

1. Create a low-privilege user:

- net user support Password@123 /add
- net localgroup users support /add

2. Ensure the user is not part of the Administrators group

---

### Step 4: Add Flags

1. Create user flag: echo FLAG{WIN7-ETERNALBLUE-USER} > C:\Users\support\Desktop\user.txt

2. Create administrator flag:  echo FLAG{WIN7-ETERNALBLUE-ADMIN} > C:\Windows\System32\config\admin.txt

3. Restrict permissions using `icacls` as needed

---

### Step 5: Network Configuration

- Adapter 1: NAT
- Adapter 2: Host-only or Internal Network

This allows external exploitation and internal pivoting.

---

## Legal Disclaimer

This project is intended for educational and authorized security testing purposes only. Unauthorized exploitation of systems without explicit permission is illegal. The author is not responsible for misuse of this material.

---

## Created By

- Name: Gopesh Kachhadiya
- Role: Junior Penetration Tester 
- Purpose: Internship Project and Skill Demonstration
- Domain: Offensive Security and AI Penetration Testing
- This lab was created as part of an offensive cybersecurity internship project focused on realistic attack simulations and hands-on learning.
