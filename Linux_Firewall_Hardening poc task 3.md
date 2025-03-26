\# POC-TASKS \# 📌 Linux Security - Exploitation & Hardening (PoC)

This repository demonstrates \*\*firewall and network security
misconfigurations\*\* in Linux, including \*\*exploitation and
mitigation\*\*.

\-\--

\## 🔹 \*\*Task 3: Firewall & Network Security\*\*

\### ✅ \*\*Setup: Installing & Configuring a Basic Web Server\*\*

\`\`\`bash \# Update system and install Apache web server
┌──(kali㉿kali)-\[\~\] └─\$ sudo apt update && sudo apt install -y
apache2

\# Enable Apache to start on boot ┌──(kali㉿kali)-\[\~\] └─\$ sudo
systemctl enable apache2

\# Start Apache service ┌──(kali㉿kali)-\[\~\] └─\$ sudo systemctl start
apache2

\# Verify Apache is running ┌──(kali㉿kali)-\[\~\] └─\$ sudo systemctl
status apache2

\# Disable UFW to allow all traffic (Very Insecure!)
┌──(kali㉿kali)-\[\~\] └─\$ sudo ufw disable \`\`\`

\### ✅ \*\*Exploitation: Brute-Force Attack on SSH\*\*

\`\`\`bash \# Check open ports on the system ┌──(kali㉿kali)-\[\~\] └─\$
sudo ss -tuln

\# Scan for open ports using Nmap ┌──(kali㉿kali)-\[\~\] └─\$ sudo nmap
-sV -sC -A localhost

\# Check ports are open with Netcat ┌──(kali㉿kali)-\[\~\] └─\$ nc -zv
localhost 80

\# Optional: Use Hydra to brute-force SSH (for testing purposes only)
┌──(kali㉿kali)-\[\~\] └─\$ hydra -l root -P
/usr/share/wordlists/rockyou.txt ssh://localhost \`\`\`

\### ✅ \*\*Mitigation: Hardening the System with UFW & iptables\*\*

\`\`\`bash \# Enable UFW firewall ┌──(kali㉿kali)-\[\~\] └─\$ sudo ufw
enable

\# Allow only SSH (22) and HTTP (80) ┌──(kali㉿kali)-\[\~\] └─\$ sudo
ufw allow 22/tcp ┌──(kali㉿kali)-\[\~\] └─\$ sudo ufw allow 80/tcp

\# Set default UFW rules to block other traffic ┌──(kali㉿kali)-\[\~\]
└─\$ sudo ufw default deny incoming ┌──(kali㉿kali)-\[\~\] └─\$ sudo ufw
default allow outgoing

\# Verify UFW rules ┌──(kali㉿kali)-\[\~\] └─\$ sudo ufw status verbose

\# Implement iptables rules to further restrict access
┌──(kali㉿kali)-\[\~\] └─\$ sudo iptables -A INPUT -p tcp \--dport 22 -j
ACCEPT ┌──(kali㉿kali)-\[\~\] └─\$ sudo iptables -A INPUT -p tcp
\--dport 80 -j ACCEPT

\# Drop all other inbound traffic (optional, increases security)
┌──(kali㉿kali)-\[\~\] └─\$ sudo iptables -P INPUT DROP

\# Save iptables rules ┌──(kali㉿kali)-\[\~\] └─\$ sudo
netfilter-persistent save \`\`\`

\## 📌 Task 3 - Summary

\| \*\*Step\*\* \| \*\*Action\*\* \| \*\*Command\*\* \|
\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--\|
\| 🔹 \*\*Setup\*\* \| Install and start Apache2 web server \| \`sudo
apt update && sudo apt install -y apache2\`\<br\>\`sudo systemctl enable
apache2\`\<br\>\`sudo systemctl start apache2\` \| \| \| Verify Apache
is running \| \`sudo systemctl status apache2\` \| \| \| Disable UFW to
allow all traffic (INSECURE) \| \`sudo ufw disable\` \| \| 🔹
\*\*Exploitation\*\* \| Check open ports using ss \| \`sudo ss -tuln\`
\| \| \| Scan for open ports using Nmap \| \`sudo nmap -sV -sC -A
localhost\` \| \| \| Check specific port availability with Netcat \|
\`nc -zv localhost 80\` \| \| \| Optional: Brute-force SSH (for testing)
\| \`hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://localhost\`
\| \| 🔹 \*\*Mitigation (UFW)\*\* \| Enable UFW and allow only SSH &
HTTP \| \`sudo ufw enable\`\<br\>\`sudo ufw allow 22/tcp\`\<br\>\`sudo
ufw allow 80/tcp\` \| \| \| Set default UFW rules (deny incoming, allow
outgoing) \| \`sudo ufw default deny incoming\`\<br\>\`sudo ufw default
allow outgoing\` \| \| \| Verify UFW rules \| \`sudo ufw status
verbose\` \| \| 🔹 \*\*Mitigation (iptables)\*\* \| Allow only SSH &
HTTP traffic using iptables \| \`sudo iptables -A INPUT -p tcp \--dport
22 -j ACCEPT\`\<br\>\`sudo iptables -A INPUT -p tcp \--dport 80 -j
ACCEPT\` \| \| \| Drop all other inbound traffic (optional) \| \`sudo
iptables -P INPUT DROP\` \| \| \| Save iptables rules \| \`sudo
netfilter-persistent save\` \|

\-\-- \### END -x-
