Phishing Incident Response – Windows 10 Workstation
Overview

This project documents a real-world phishing response scenario involving:

Malicious email link

Suspicious file download

Fake credential verification popup

Offline forensic inspection

Persistence checks

Host-based blocking

Full antivirus verification

All identifiers and domains have been sanitized.

Scenario

A user clicked a malicious email link which triggered:

A file download (malicious_download.exe)

A fake Windows credential verification prompt

User:

Did NOT enter password

Did NOT execute the downloaded file

System was immediately powered off for containment.

Incident Response Workflow
1. Containment

Disconnected from network

Powered off system

Booted into recovery environment

2. User Account Verification (Offline)

Loaded SAM hive to inspect local accounts:

reg load HKLM\TempHive C:\Windows\System32\Config\SAM
reg query HKLM\TempHive\SAM\Domains\Account\Users
reg query HKLM\TempHive\SAM\Domains\Account\Users\Names

Confirmed:

No new users created

No unauthorized admin privileges

3. Startup Persistence Check

Checked startup directories:

dir C:\Users\Username\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup

No unauthorized startup entries found.

4. Scheduled Task Review
dir C:\Windows\System32\Tasks

Only legitimate system tasks detected (Microsoft, Edge Update, OneDrive, etc).

5. Malware Execution Analysis

Downloaded file:

Present in Downloads

Not executed

No service creation

No new scheduled tasks

No registry persistence

6. Domain Blocking via Hosts File

Added:

127.0.0.1 maliciousdomain.com
127.0.0.1 www.maliciousdomain.com

Flushed DNS:

ipconfig /flushdns
7. Antivirus Verification

Windows Defender Quick Scan

Windows Defender Full Scan

No threats detected

Ransomware Assessment

Verified:

No encrypted files

No ransom notes

No abnormal file extensions

No system instability

Conclusion: No ransomware activity detected.

Final Risk Assessment

Low Risk – Phishing Attempt Only

Because:

File was not executed

No credentials entered

No persistence found

Full disk scan clean

Lessons Learned

Immediate power-off limits attack surface

Offline registry inspection is effective for user validation

Hosts file blocking is useful for quick containment

Always perform full disk scan even if threat appears inactive
