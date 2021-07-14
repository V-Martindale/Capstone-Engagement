# Capstone-Engagement
This report outlines our assessment and analysis of the Capstone Company's network. The weaknesses in the Capstone Web Server security led to the network being successfully exploited. Ultimately this breach led to files being stolen and the implementation of a backdoor through an unsecured port. As the vulnerabilities are documented, so are the methods in which to harden the system against them.

# Red-Team
The Red team used a Kali virtual machine in order to reveal the different vulnerabilities within the Capstone network security. First reconnaissance was done by running a nmap scan against the network revealing the apache server at ip address 192.168.1.105. Inputs along the URL led to the discovery of the ability to use directory traversal on the apache server. Using directory traversal the attacker was able to find the "secret_folder" which listed the hashed password of employee Ashton. Due to the lack of password security there were no limits to password attempts or requirements for strong passwords. Exploiting this the attacker was able to run the Hydra command against Ashton's hash decoding his password and thus allowing access to the WebDav server. Finally with WebDav access achieving root escalation was simple and a reverse shell was uploaded on an open and unmonitored port.


# Blue-Team
After the Red Team's penetration of the Capstone Network the Blue Team used a virtual machine configured with an ELK instance to identify what was exploited on the network. Using the filters provided by the ELK server the Blue Team was able to identify the time and origin of each instance in which a vulnerability was exploited. After documenting the circumstances of each exploitation the Blue came up with a hardening strategy for each vulnerability: 

Nmap Scan: Implement a default-deny rule set on the firewall of the host, and only allow ports 80 and 443 to be open to allowed Ip addresses.

Hidden Directory: Create a whitelist of Ip addresses to minimize those who can access the hidden “secret_folder” directory.

Brute Force Attack(Hydra): Stronger password policies need to be implemented such as multiple failed-login lockdown, secondary login question, and/or captcha(bot prevention). 

Reverse Shell Upload- Limit users to only using the “put” command on protected files as to prevent an accidental “get” upload of a malicious shell.

# Conclusion
Although the vulnerabilities in the Capstone network led to crucial information being stolen the methods in which to mitigate this breach were simple. The Capstone Company was informed of the hardening methods and implemented them fast. We also encouraged educating the Capstone workforce on cyber security as this breach could have been easily prevented by a few simple rules and policies.

