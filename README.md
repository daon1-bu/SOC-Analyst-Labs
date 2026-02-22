# SOC Analyst Labs

This repo is where I document hands-on labs while learning blue-team / SOC skills using my Windows Active Directory home lab.

The goal is simple: simulate real attacker behavior, then learn how to detect it using logs.

---

## What I'm practicing

- Windows Event Log analysis  
- Detecting brute force attacks  
- Investigating account lockouts  
- Monitoring admin logons  
- Mapping activity to MITRE ATT&CK  
- Building basic detection ideas  
- PowerShell logging and analysis (next lab)

---

## Labs

### Windows Event Log Analysis Lab
Simulated authentication attacks and analyzed Windows Security logs.

Covers:
- Failed logins (Event ID 4625)
- Successful logins (Event ID 4624)
- Admin logons (Event ID 4672)
- Account lockouts (Event ID 4740)

Folder:
Windows-Event-Log-Analysis-Lab/

---

### PowerShell Attack Detection Lab (in progress)
Next lab will focus on suspicious PowerShell activity and script block logging.

Folder:
PowerShell-Attack-Detection-Lab/

---

## Why this repo exists

I'm building a portfolio of practical SOC skills and documenting the learning process as I go.
