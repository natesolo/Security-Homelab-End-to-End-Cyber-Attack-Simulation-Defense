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
