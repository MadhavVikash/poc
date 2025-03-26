\# 📌 Linux Security - Automated Security Auditing (PoC) \# This script
demonstrates automated security auditing, weak configuration detection,
and alert mechanisms.

\-\--

\## 🔹 Task 5: Automated Security Auditing & Scripting

\### ✅ Setup: Creating the Security Audit Script

1\. \*\*Create the Security Audit Script:\*\*

┌──(kali㉿kali)-\[\~\] nano /path/to/security_audit.sh

2\. \*\*Paste the Following Script:\*\*

┌──(kali㉿kali)-\[\~\] #!/bin/bash \# Security Audit PoC Script \#
Purpose: Demonstrate security auditing capabilities, detect weak
configurations, and provide alerts.

LOG_FILE=\"/var/log/security_audit.log\" echo \"\-\-- Security Audit:
\$(date) \-\--\" \| tee -a \"\$LOG_FILE\"

\# Check user login attempts echo \" === User Login Attempts ===\" \|
tee -a \"\$LOG_FILE\" last \| head -n 10 \| tee -a \"\$LOG_FILE\"

\# Check unauthorized access attempts echo \" === Unauthorized Access
Attempts (auth.log) ===\" \| tee -a \"\$LOG_FILE\" sudo grep \"Failed
password\" /var/log/auth.log \| tail -n 10 \| tee -a \"\$LOG_FILE\"

\# Detect running services echo \" === Running Services ===\" \| tee -a
\"\$LOG_FILE\" systemctl list-units \--type=service \--state=running \|
tee -a \"\$LOG_FILE\"

\# Monitor disk usage echo \" === Disk Usage ===\" \| tee -a
\"\$LOG_FILE\" df -h \| tee -a \"\$LOG_FILE\"

\# Security alert: Monitor unauthorized SSH access
UNAUTH_ATTEMPTS=\$(sudo grep \"Failed password\" /var/log/auth.log \| wc
-l) if \[ \"\$UNAUTH_ATTEMPTS\" -gt 0 \]; then ALERT_MSG=\"Alert:
Unauthorized SSH login attempts detected! (\$UNAUTH_ATTEMPTS attempts)\"
echo \"\$ALERT_MSG\" \| tee -a \"\$LOG_FILE\" echo \"\$ALERT_MSG on
\$(date)\" \| mail -s \"Security Alert\" admin@example.com fi

echo \" Audit complete. Results saved to \$LOG_FILE.\" \| tee -a
\"\$LOG_FILE\"

\# Schedule with cron (add this manually to crontab): \# \*/5 \* \* \*
\* /path/to/security_audit.sh exit 0

3\. \*\*Make the Script Executable:\*\*

┌──(kali㉿kali)-\[\~\] chmod +x /path/to/security_audit.sh

4\. \*\*Test the Script:\*\*

┌──(kali㉿kali)-\[\~\] /path/to/security_audit.sh

\-\--

\### ✅ Exploitation: Identifying Weak Configurations

1\. \*\*Detect Unauthorized Access Attempts:\*\*

┌──(kali㉿kali)-\[\~\] sudo grep \"Failed password\" /var/log/auth.log

2\. \*\*Check for Old User Accounts:\*\*

┌──(kali㉿kali)-\[\~\] awk -F: \'(\$3\<1000){print \$1}\' /etc/passwd

3\. \*\*Verify Running Services:\*\*

┌──(kali㉿kali)-\[\~\] systemctl list-units \--type=service
\--state=running

\-\--

\### ✅ Mitigation: Automating Monitoring and Alerts

1\. \*\*Automate with Cron:\*\*

┌──(kali㉿kali)-\[\~\] crontab -e

Add the following line to run every 5 minutes:

┌──(kali㉿kali)-\[\~\] \*/5 \* \* \* \* /path/to/security_audit.sh

2\. \*\*Implement Security Alerts:\*\*

Ensure you have \`mailutils\` installed to receive email alerts:

┌──(kali㉿kali)-\[\~\] sudo apt install mailutils

Verify alerts by attempting an unauthorized SSH login and checking the
email inbox.

\-\--

\### 📌 Task 5 - Summary

\| \*\*Step\*\* \| \*\*Action\*\* \| \*\*Command\*\* \|
\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--\|
\| 🔹 \*\*Setup\*\* \| Create the script \| \`nano
/path/to/security_audit.sh\` \| \| \| Make the script executable \|
\`chmod +x /path/to/security_audit.sh\` \| \| \| Test the script \|
\`/path/to/security_audit.sh\` \| \| 🔹 \*\*Exploitation\*\* \| Detect
unauthorized SSH attempts \| \`sudo grep \"Failed password\"
/var/log/auth.log\` \| \| \| Check for old user accounts \| \`awk -F:
\'(\$3\<1000){print \$1}\' /etc/passwd\` \| \| \| List running services
\| \`systemctl list-units \--type=service \--state=running\` \| \| 🔹
\*\*Mitigation\*\* \| Automate script execution with cron \| \`crontab
-e\` \| \| \| Implement security alerts \| \`sudo apt install
mailutils\` \|

\-\--

\### \*\*END-x-\*\*
