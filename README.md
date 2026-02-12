Security Homelab: Cyber Attack Simulation & Defense
What I Built
I created a complete business network in my homelab and simulated a real cyber attack from start to finish. Then I switched sides and played defender to detect everything I did.
The Challenge: Can I break into a company network and steal data? Can I then find evidence of my own attack?

The Lab Setup
I built a fake company network called "Project-X" with:

Kali Linux (10.0.0.50) - My hacker machine
Corporate Mail Server - Running email services
Employee Workstation (Ubuntu) - A regular user's computer
Windows Workstation - Another employee computer
Domain Controller - The main server controlling everything
Security Monitoring - Wazuh SIEM watching for attacks

Why this matters: This mirrors a real company network, not just toy examples.

The Attack Story
Step 1: Reconnaissance - "Who's on the network?"
What I did: Scanned the network to find computers and see what services were running
Tool used: Nmap
What I found:

Mail server on port 8025
SSH services exposed
Windows computers with remote management enabled

screenshots/01-recon-and-access/nmap-scan.png


Real-world lesson: Attackers always start by mapping your network. Unused services = attack opportunities.

Step 2: Breaking In - "Let's get access"
Attack #1: Password Cracking
What I did: Used Hydra to try thousands of passwords against the SSH service
Result: Cracked the root password in minutes
screenshots/01-recon-and-access/hydra-bruteforce.png
Real-world lesson: Weak passwords = open door. This is why companies require complex passwords.
Attack #2: Phishing Email
What I did:

Created a fake login page that looked legitimate
Sent an email to an employee pretending to be from HR
Employee clicked the link and entered their password
Their credentials were saved to my system

screenshots/01-recon-and-access/phishing-email.png
screenshots/01-recon-and-access/captured-creds.png
Result: Got valid username and password for an employee workstation
screenshots/01-recon-and-access/linux-client-access.png
Real-world lesson: 90% of breaches start with phishing. Employee training is critical.

Step 3: Moving Sideways - "One computer isn't enough"
What I did: From the employee's Linux computer, I looked for Windows machines on the network
Tool used: Netexec for password spraying (trying common passwords across many accounts)
screenshots/02-lateral-movement/netexec-spray.png
Result: Found a Windows admin account with a weak password
Then: Connected to that Windows computer using Evil-WinRM (remote PowerShell)
screenshots/02-lateral-movement/evil-winrm-session.png
Real-world lesson: Attackers don't stop at one computer. They keep moving until they find the crown jewels.

Step 4: Taking Over - "I want full control"
What I did: Checked what network this Windows computer was on
Discovery: It was part of a Windows domain (corp.project-x-dc.com)
screenshots/02-lateral-movement/domain-admin-access.png
Next move: Used Remote Desktop (RDP) to connect to the Domain Controller
screenshots/03-objectives/rdp-domain-controller.png
Result: Full administrative access to the entire network
Real-world lesson: Once attackers get Domain Admin, it's game over. They control everything.

Step 5: Stealing Data - "Mission objective"
What I did: Found sensitive production files on the Domain Controller
Method: Used SCP (Secure Copy) to transfer files back to my attacker machine
screenshots/03-objectives/scp-exfiltration.png
Why SCP?: Blends in with normal network traffic, harder to detect than uploading to Dropbox
Real-world lesson: Data exfiltration is the goal. All the earlier steps were just getting here.

Step 6: Staying Hidden - "Make sure I can come back"
I didn't want to lose access, so I created backdoors:
Backdoor #1: Secret Admin Account
What I did: Created a new user account and added it to Domain Admins group
screenshots/03-objectives/backdoor-account.png
Why this works: Even if they find the original compromised accounts, I still have access
Backdoor #2: Automated Access
What I did:

Downloaded a reverse shell script
Created a scheduled task called "PersistenceTask"
Set it to run every day at noon
When it runs, it automatically connects back to my computer

screenshots/03-objectives/scheduled-task.png
screenshots/03-objectives/reverse-shell.png
Real-world lesson: Persistence is key for attackers. They want to maintain access for months.

Playing Defense - "Can I catch myself?"
Now I switched to the blue team side and tried to detect my own attack.
Defense Tool: Wazuh SIEM
What it does: Collects logs from all computers and alerts on suspicious activity
What I Found:
Alert Dashboard showed multiple security events
screenshots/04-defense/wazuh-alerts.png
Windows Logon Analysis - I searched for Event ID 4624 (successful logins)
screenshots/04-defense/event-4624-analysis.png
What this revealed:

Hundreds of login attempts in a short time (brute force attack)
Logins from unusual IP addresses
New user account created
Scheduled task added

Forensic Investigation - Looked at detailed logs
screenshots/04-defense/log-forensics.png
Found:

Administrator account accessing sensitive files
Unauthorized modifications
Complete timeline of the attack

Real-world lesson: This is why SIEMs are critical. Without logging, you're blind to attacks.

What I Learned
Offensive Skills
How attackers think and operate
Why password policies matter
How easy phishing actually works
Lateral movement techniques
Persistence methods attackers use
Defensive Skills
How to detect brute force attacks
Identifying phishing campaigns
Spotting lateral movement
Finding persistence mechanisms
Log analysis and investigation

How to Defend Against This
Based on my attack, here's what would have stopped me:
Prevention:

Strong Passwords + MFA - Would have stopped brute force and password spray
Disable WinRM - Blocks lateral movement technique I used
Email Security - Catches phishing emails before they reach users
Least Privilege - Users shouldn't be local admins
Security Training - Teach employees to spot phishing

Detection:

SIEM Monitoring (I had this!) - Alerts on suspicious activity
Failed Login Alerts - Would catch brute force immediately
Account Creation Alerts - Would detect backdoor account
Scheduled Task Monitoring - Would find persistence mechanism


Tools I Used
Attack Tools: Kali Linux, Nmap, Hydra, Netexec, Evil-WinRM, Apache2, Python
Defense Tools: Wazuh SIEM
Environment: VirtualBox, Ubuntu 22.04, Windows Server, Active Directory

Important Legal Note
This was done in my own isolated lab with virtual machines I own.
I did NOT:

Attack real companies
Access systems without permission
Steal real data

This is for educational purposes to:

 Learn offensive and defensive security
 Build practical skills for a security career
 Understand how to protect real networks

Never attempt this on systems you don't own. Unauthorized access is illegal.

Summary
What happened: I simulated a complete cyber attack from reconnaissance to data theft, then detected it using security monitoring.
Why it matters: This demonstrates real-world attack patterns and defensive techniques that security professionals need to know.
The takeaway: Both offense and defense are necessary. You need to think like an attacker to defend properly

Credits & Resources

Project Guide: projectsecurity.io by Grant Collins
Phishing Templates: collinsmc23 on GitHub
MITRE ATT&CK Framework: attack.mitre.org
