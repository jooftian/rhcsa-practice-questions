# Enable SELinux in enforcing mode

## Question
Enable SELinux in enforcing mode

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

## Answer
This procedure requires a reboot. Issue the command `getenforce` and check the status of SELinux, it should return `Enforcing`. If you see `Disabled` or `Permissive` then edit the file `/etc/selinux/config` and change SELINUX=disabled or SELINUX=permissive for SELINUX=enforcing. Save the file and reboot the system. Check again the status of SELinux.
