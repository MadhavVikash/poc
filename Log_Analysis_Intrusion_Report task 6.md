\# POC-TASKS \# 📌 Linux Security - Exploitation & Hardening (PoC)

This repository demonstrates \*\*Log Analysis and Intrusion
Detection\*\* in Linux, including \*\*exploitation and mitigation\*\*.

\-\--

\## 🔹 \*\*Task 6: Log Analysis & Intrusion Detection\*\*

This task demonstrates how to \*\*analyze logs for unauthorized access
attempts\*\* and implement \*\*mitigation strategies\*\* like
\`fail2ban\` and automated log monitoring.

\-\--

\## ✅ \*\*Setup: Enabling System Logging\*\*

\### \*\*1️⃣ Enable System Logging\*\*

\`\`\` ┌──(kali㉿kali)-\[\~\] └─\$ sudo systemctl status
systemd-journald ┌──(kali㉿kali)-\[\~\] └─\$ sudo systemctl status
rsyslog

┌──(kali㉿kali)-\[\~\] └─\$ ls /var/log/auth.log \`\`\`

\### \*\*2️⃣ Simulate Multiple Failed SSH Login Attempts\*\*

\`\`\` ┌──(kali㉿kali)-\[\~\] └─\$ for i in {1..5}; do ssh
invaliduser@localhost; done \`\`\`

\-\--

\## ✅ \*\*Exploit: Analyzing Logs\*\*

\### \*\*1️⃣ Extract Failed Login Attempts\*\*

\`\`\` ┌──(kali㉿kali)-\[\~\] └─\$ grep \"Failed password\"
/var/log/auth.log \`\`\`

\### \*\*2️⃣ Identify Brute-Force Attempts\*\*

\`\`\` ┌──(kali㉿kali)-\[\~\] └─\$ grep \"Failed password\"
/var/log/auth.log \| awk \'{print \$11}\' \| sort \| uniq -c \| sort -nr
\`\`\`

\### \*\*3️⃣ Detect Unauthorized Access\*\*

\`\`\` ┌──(kali㉿kali)-\[\~\] └─\$ grep \"Invalid user\"
/var/log/auth.log \`\`\`

\-\--

\## ✅ \*\*Mitigation: Implementing Security Measures\*\*

\### \*\*1️⃣ Install and Configure fail2ban\*\*

\`\`\` ┌──(kali㉿kali)-\[\~\] └─\$ sudo apt update
┌──(kali㉿kali)-\[\~\] └─\$ sudo apt install fail2ban

┌──(kali㉿kali)-\[\~\] └─\$ sudo cp /etc/fail2ban/jail.conf
/etc/fail2ban/jail.local ┌──(kali㉿kali)-\[\~\] └─\$ sudo nano
/etc/fail2ban/jail.local \`\`\`

\`\`\`plaintext \[sshd\] enabled = true maxretry = 3 findtime = 600
bantime = 3600 \`\`\`

\`\`\` ┌──(kali㉿kali)-\[\~\] └─\$ sudo systemctl restart fail2ban
┌──(kali㉿kali)-\[\~\] └─\$ sudo fail2ban-client status sshd \`\`\`

\### \*\*2️⃣ Set Up Log Monitoring\*\*

\`\`\` ┌──(kali㉿kali)-\[\~\] └─\$ sudo apt install logwatch
┌──(kali㉿kali)-\[\~\] └─\$ sudo logwatch \--detail High \--mailto root
\--service sshd \`\`\`

\`\`\` ┌──(kali㉿kali)-\[\~\] └─\$ sudo nano /etc/rsyslog.conf \*.\*
\@192.168.1.200:514

┌──(kali㉿kali)-\[\~\] └─\$ sudo systemctl restart rsyslog \`\`\`

\-\--

\## ✅ \*\*Summary\*\*

\| \*\*Step\*\* \| \*\*Action\*\* \| \*\*Command\*\* \|
\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--\|
\| 🔹 \*\*Setup\*\* \| Enable system logging \| \`sudo systemctl status
systemd-journald\` \| \| \| Simulate multiple failed SSH login attempts
\| \`for i in {1..5}; do ssh invaliduser@localhost; done\` \| \| 🔹
\*\*Exploit\*\* \| Extract failed SSH login attempts \| \`grep \"Failed
password\" /var/log/auth.log\` \| \| \| Identify brute-force attempts \|
\`grep \"Failed password\" /var/log/auth.log \| awk \'{print \$11}\' \|
sort \| uniq -c \| sort -nr\` \| \| \| Detect unauthorized access \|
\`grep \"Invalid user\" /var/log/auth.log\` \| \| 🔹 \*\*Mitigation\*\*
\| Install and configure fail2ban \| \`sudo apt install fail2ban\` \| \|
\| Set up log monitoring with logwatch \| \`sudo apt install logwatch\`
\| \| \| Configure rsyslog for centralized logging \| \`sudo nano
/etc/rsyslog.conf\` \| \| \| Restart fail2ban and rsyslog \| \`sudo
systemctl restart fail2ban\` / \`sudo systemctl restart rsyslog\` \|

\-\--

\### \*\*END-x-\*\*
