# Lab 1.1.6: Perform System Configuration Gap Analysis

### Objective
Identify configuration discrepancies between a Windows Server 2019 system and a Microsoft 
security baseline using Policy Analyser in order to assess compliance and perform a gap analysis of the system's
current configurations.

### Overview
In this lab, I used Microsoft's Policy Analyser to compare the live system configuration of a 
Windows Server 2019 VM against a predefined security baseline. This exercise focused on recognising 
misconfigurations that could impact the organisation's security posture.

### Lab Steps 
1. **Log into the VM**
2. **Check OS Version & Build**
Search: ``winver`` 
Confirm that the version is 1809 and build 17763
3. **Launch PowerShell as Admin**
Search ``powershell`` -> Right click -> Run as administrator
4. **Copy Toolkit Files**
```copy D:\* C:\LABFILES```
5. **Navigate to LABFILES Directory**
```cd C:\LABFILES```
```ls```
6. **Extract ZIP Files**
```Expand-Archive -Path PolicyAnalyzer.zip```
```Expand-Archive -Path "Windows 10 Version 1809 and Windows Server 2019 Security Baseline.zip"```
7. **Launch Policy Analyser through PowerShell**
```C:\LABFILES\PolicyAnalyzer\PolicyAnalyzer_40\PolicyAnalyzer.exe```
8. **Load Baseline Policy Files**
* Select folder
``C:\LABFILES\Windows 10 Version 1809 and Windows Server 2019 Security Baseline\Documentation``
9. **View Baseline Settings**
* Check: ``MSFT-Win10-v1809-RS5-WS2019-FINAL``
* Click: View/Compare
<img width="628" height="345" alt="Screenshot 2025-10-07 at 4 39 28 pm" src="https://github.com/user-attachments/assets/11811013-b93c-4f82-80de-4a275c21b3a8" />

10. **Perform Gap Analysis**
* Check: ``MSFT-Win10-v1809-RS5-WS2019-FINAL``
* Click: Compare to Effective State
* Review highlighted differences (e.g. ``LockoutBadCount``, ``MinimumPasswordLength``)
<img width="476" height="285" alt="Screenshot 2025-10-07 at 4 40 16 pm" src="https://github.com/user-attachments/assets/f6fa818b-3985-4321-b961-2ceb80641615" />

### My Final Thoughts
Gap analysis isn't really about blindly enforcing templates, but more about informed decision
making. While the templates provided do offer a solid benchmark, real-world configurations have to 
reflect both best practices and business needs. Tools such as Policy Analyser simplify this process and give 
visibility into where systems might fall short.

### Key takeaways
* Always verify OS version/build to select the correct security baseline
* Gap analysis shows where configurations differ, no why. Interpretation matters
* Security baselines are a starting point, not a one-size fits all solution
* Regular analysis helps maintain compliance and improve overall system hardening

