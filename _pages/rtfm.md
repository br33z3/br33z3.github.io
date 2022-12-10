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
