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

## How to Perform a Pass-the-Hash Attack

Here is a step-by-step guide to performing a PtH attack, including the tools and commands necessary:

1. **Capture the password hash**: The first step is to obtain the target user's password hash. This can be done using various methods, such as dumping hashes from the Security Account Manager (SAM) database or extracting hashes from a system's memory using tools like Mimikatz.

Example command using Mimikatz:

```bash
mimikatz.exe privilege::debug sekurlsa::logonpasswords
```

2. **Use the captured hash for authentication**: Once the password hash is obtained, the attacker can use it to authenticate to network resources. Tools like PsExec or CrackMapExec can be used to perform PtH attacks.

Example command using PsExec:

```bash
psexec.exe \\TARGET-SYSTEM -u TARGET-USER -p PASSWORD-HASH cmd.exe
```


Example command using CrackMapExec:

```bash
crackmapexec smb TARGET-IP -u TARGET-USER -H PASSWORD-HASH -x "cmd.exe"
```


## Real-World Attack Scenario

Here's an example scenario illustrating how a Pass-the-Hash attack could unfold:

1. An attacker gains access to a low-privileged user's machine via a phishing attack or exploiting a software vulnerability.
2. The attacker uses a tool like Mimikatz to dump password hashes from the system's memory.
3. The attacker identifies a high-privileged user's password hash, such as a domain administrator.
4. Using PsExec or CrackMapExec, the attacker leverages the captured domain administrator's hash to authenticate to a domain controller.
5. The attacker gains domain administrator privileges, enabling them to access sensitive data, create new user accounts, or modify existing accounts for persistence.

## Conclusion

Pass-the-Hash attacks are dangerous because they exploit inherent weaknesses in Windows authentication mechanisms. To defend against PtH attacks, organizations should adopt a multi-layered security approach, including:

- Implementing privileged access management (PAM)
- Regularly patching and updating software
- Using strong, unique passwords
- Enabling security features like Credential Guard
- Restricting the use of administrative accounts

Understanding how Pass-the-Hash attacks work, along with effective mitigation strategies, is essential to protect your organization from unauthorized access and data breaches.

