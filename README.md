# SOC-Analyst-Labs
Windows Event Log Analysis Lab

1. Lab Overview

  This lab simulates common authentication-based attacks on a Windows system and demonstrates how a SOC analyst can detect them using Windows Event Logs.
  
  The goal is to understand how real attacker behavior appears in logs and how defenders can identify suspicious activity.
  
  In this lab we simulate:
  
  Brute-force login attempts
  
  Successful login after brute force
  
  Administrative logon
  
  Remote Desktop (RDP) login
  
  Account lockout
  
  These events represent some of the most common alerts investigated by Security Operations Centers (SOC).

2. Lab Setup

  Environment
  
  Windows 10/11 Virtual Machine
  
  Event Viewer
  
  Security auditing enabled
  
  Enable Windows auditing
  
  Open PowerShell as Administrator:
  
  auditpol /set /category:* /success:enable /failure:enable
  
  This enables logging for authentication and security activity.

3. Attack Simulation
  Brute-force login attempts
  
  Generated repeated failed login attempts:
  
  runas /user:Administrator cmd
  
  Incorrect passwords were entered multiple times to simulate password guessing.
  
  Successful login after brute force
  
  After several failures, the correct password was entered once to simulate attacker success.
  
  Remote Desktop login
  
  RDP was enabled and a remote login session was created from another machine.
  
  Account lockout
  
  Continuous failed login attempts triggered an account lockout.

4. Log Analysis

  Logs were analyzed in:
  
  Event Viewer → Windows Logs → Security
  Event ID 4625 — Failed Login
  
  Indicates unsuccessful authentication attempts.
  Multiple events in short time = brute force indicator.
  
  <img width="543" height="170" alt="image" src="https://github.com/user-attachments/assets/562fc8e6-c49f-4ad3-a10a-19055e3c9515" />
  
  
  Event ID 4624 — Successful Login
  
  Represents successful authentication.
  Suspicious when occurring after many failures.
  
  <img width="506" height="153" alt="image" src="https://github.com/user-attachments/assets/56c4231e-9ca3-42d9-98ab-8e8948121805" />
  
  
  Event ID 4672 — Administrative Logon
  
  Triggered when administrative privileges are used.
  
  <img width="544" height="181" alt="image" src="https://github.com/user-attachments/assets/a1505b3c-e8e7-4472-a44d-d0aaab17bdb6" />
  
  
  Event ID 4740 — Account Lockout
  
  Indicates too many failed login attempts.
  
  <img width="569" height="165" alt="image" src="https://github.com/user-attachments/assets/51e8477a-55db-4509-bec9-7aff8cc3331f" />


5. Detection Ideas

  Possible SIEM detection rules:\
  
  Alert if >5 Event ID 4625 within 5 minutes
  
  Alert on successful login after multiple failures
  
  Alert on administrative logons outside business hours
  
  Alert on RDP logins from unusual sources
  
  Alert when account lockout occurs

6. MITRE ATT&CK Mapping
  Activity	Technique
  Brute Force Login	T1110 – Brute Force
  Valid Account Login	T1078 – Valid Accounts
  RDP Login	T1021.001 – Remote Services
  Privileged Login	T1078 – Valid Accounts

8. How to Prevent

  Recommended defenses:
  
  Strong password policies
  
  Account lockout policies
  
  Multi-Factor Authentication (MFA)
  
  Restrict RDP access via VPN/firewall
  
  Centralized logging with SIEM
  
  Continuous monitoring of authentication events

9. Key Findings

  Multiple Event ID 4625 entries within a short timeframe indicate brute-force activity.
  
  A successful login (4624) following repeated failures is a strong compromise indicator.
  
  Event ID 4672 confirms privileged access, which should always be monitored.
  
  Event ID 4740 confirms account lockout triggered by excessive failed authentication attempts.
  
  This pattern mimics real-world credential attacks observed in enterprise environments.
