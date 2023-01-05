---
layout: blog
title: Offensive Powershell
tags: RedTeam, ActiveDirectory, Powershell
comments: true
date: 2022-12-10
---

# 0ffensive Powershell

### PowerShell - Filter Installed Software

    Get-CimInstance Win32_Product | fl
    
### PowerShell - Filter Out Microsoft Software

    Get-CimInstance Win32_Product -Filter "NOT Vendor like '%Microsoft%'  "| fl
    
### Filter

| Filter          | Meaning                  |
|-----------------|--------------------------|
| -eq             | Equal to                 |
| -le             | Less than or equal to    |
| -ge             | Greater than or equal to |
| -ne             | Not equal to             |
| -lt             | Less than                |
| -gt             | Greater than             |
| -approx         | Approximately equal to   |
| -bor            | Bitwise OR               |
| -band           | Bitwise AND              |
| -recursivematch | Recursive match          |
| -like           | Like                     |
| -notlike        | Not like                 |
| -and            | Boolean AND              |
| -or             | Boolean OR               |
| -not            | Boolean NOT              |


### Filter Examples: AD Object Properties

| Escaped Character | As  | Note                                                                                                                  |
|-------------------|-----|-----------------------------------------------------------------------------------------------------------------------|
| “                 | `”  | Only needed if the data is enclosed in double-quotes.                                                                 |
| ‘                 | \’  | Only needed if the data is enclosed in single quotes.                                                                 |
| NUL               | \00 | Standard LDAP escape sequence.                                                                                        |
| \                 | \5c | Standard LDAP escape sequence.                                                                                        |
| *                 | \2a | Escaped automatically, but only in -eq and -ne comparisons. Use -like and -notlike operators for wildcard comparison. |
| (                 | /28 | Escaped automatically.                                                                                                |
| )                 | /29 | Escaped automatically.                                                                                                |
| /                 | /2f | Escaped automatically.                                                                                                |
