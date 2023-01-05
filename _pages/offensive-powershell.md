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
