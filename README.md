# Security-Homelab-End-to-End-Cyber-Attack-Simulation-Defense
This project demonstrates a complete cyber attack simulation on a business network environment (Project-X), covering all phases of the cyber kill chain from initial reconnaissance to data exfiltration and persistence. The lab also includes defensive monitoring and incident response using Wazuh SIEM.

Attack Goal: Exfiltrate sensitive data and establish persistent access to the compromised network.
Defense Goal: Detect, alert, and investigate malicious activity using security monitoring tools.

Lab Environment
Virtual Machines

Kali Linux (Attacker Machine) - 10.0.0.50
Corp-SVR (Corporate Server) - Linux-based mail server
Linux-Client - Ubuntu 22.04 workstation
Windows-Client - Windows workstation
Domain Controller - corp.project-x-dc.com
Project-X-Sec-Box - Wazuh security monitoring

Technologies Used

Attack Tools: Nmap, Hydra, Evil-WinRM, Netexec, XFreeRDP
Defense Tools: Wazuh SIEM
Services: MailHog SMTP, Apache2, WinRM, RDP
Protocols: SSH, SMTP, WinRM, RDP, SCP

 Ethical Disclaimer
This project was conducted in a controlled, isolated lab environment for educational purposes only. All systems were personally owned and configured specifically for security research and training.
Important: Unauthorized access to computer systems is illegal. This demonstration is intended to:

Educate on offensive and defensive cybersecurity techniques
Showcase practical security skills for portfolio purposes
Highlight the importance of proper security controls

Never attempt these techniques on systems you do not own or have explicit permission to test.
🔗 Resources & Credits

Project Inspiration: projectsecurity.io by Grant Collins
Phishing Templates: collinsmc23 on GitHub
MITRE ATT&CK Framework: attack.mitre.org
Tools: Kali Linux, Wazuh, Nmap, Hydra, Evil-WinRM, Netexec
