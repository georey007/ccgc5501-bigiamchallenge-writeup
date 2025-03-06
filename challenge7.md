Challenge: Bastion Host
Category: Assumed Breach - Application Compromise/Network Access
Points: 100
Description:
A Bastion Host is a security-hardened server designed to allow controlled access to a private network. Attackers often target bastion hosts as an entry point into internal systems. Your goal in this challenge is to identify misconfigurations, weak credentials, or exposed services that could lead to unauthorized access.
________________________________________
Approach & Solution:
1.	Identify the Bastion Host:
o	Check the public-facing IP addresses in the environment.
o	Use tools like nmap to scan for open ports and running services:
nmap -sV -p- <target-IP>
o	Look for services like SSH (port 22), RDP (port 3389), or other remote access protocols.
2.	Enumerate SSH Access:
o	If SSH is open, check for weak or default credentials using:
hydra -L users.txt -P passwords.txt ssh://<target-IP>
o	If public key authentication is used, check for misconfigured .ssh/authorized_keys files.
3.	Privilege Escalation:
o	Once inside, enumerate the system for misconfigurations:
sudo -l
o	Check for readable private keys in /home or /etc/ssh/.
o	Look for hardcoded credentials in configuration files.
4.	Lateral Movement:
o	If the bastion host has access to internal systems, check for accessible networks:
ip a
netstat -rn
o	Use proxying (e.g., ssh -D 1080 user@target) to pivot into internal resources.
________________________________________
Mitigation Recommendations:
•	Use Multi-Factor Authentication (MFA) for SSH.
•	Restrict SSH access to specific IP addresses.
•	Rotate credentials and use strong SSH key pairs.
•	Disable password authentication and enforce public key authentication.
•	Implement network segmentation to limit internal exposure.
________________________________________
Conclusion:
By exploiting misconfigured bastion host access, an attacker could pivot into the internal network. Secure your bastion host with strict access controls and monitoring to prevent breaches.

