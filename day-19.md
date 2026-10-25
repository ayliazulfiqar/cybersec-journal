# Day 19 — Linux Privilege Escalation, Part 2

Today I continued learning about Linux privilege escalation by focusing on weak file permissions, cron jobs, and automated enumeration with LinPEAS. I learned how insecure file permissions can allow a normal user to modify a script that runs with root privileges. I also explored how cron schedules tasks and how poorly configured scheduled jobs can introduce security vulnerabilities.

## Four Common Privilege Escalation Paths

1. **Sudo Misconfigurations:** Incorrect sudo rules may allow users to run powerful programs as root and gain unintended privileges.

2. **SUID Files:** Programs with the SUID bit can run with their file owner's effective privileges. Unsafe SUID programs may expose elevated access.

3. **Weak File Permissions:** Files writable by untrusted users can create security risks when privileged processes execute or trust those files.

4. **Cron Jobs:** Scheduled tasks running as root can introduce privilege escalation risks if their scripts or dependencies can be modified by ordinary users.

## Practical Lab — Writable Script and Cron Job

### Objective

Create a harmless scheduled task in my Kali Linux VM, inspect its permissions, and understand how an insecure configuration could allow a normal user to influence a root process.

### What I Did

- Created a script at `/opt/backup.sh` that writes the date to a log file.
- Configured a cron job to execute the script as root every minute.
- Deliberately made the script writable by all users using `chmod 777`.
- Inspected the script permissions with `ls -l`.
- Examined `/etc/crontab` to identify the scheduled task and its execution user.
- Tested the risk by changing the script to write the output of `id` to `/tmp/proof.txt`.
- Checked whether the resulting output showed the root user.

### Findings

The script was writable by the `practice` user even though cron executed it as root. This created a privilege escalation risk because an ordinary user could influence the commands executed by a privileged scheduled task.

**Actual result:** /tmp/proof.txt showed uid=0(root). The root cron job executed the writable /opt/backup.sh script, demonstrating how a script writable by a low-privileged user can lead to privilege escalation.

## LinPEAS Enumeration

I used LinPEAS from the official PEASS-ng repository to inspect the system for potential security weaknesses.

Areas reviewed included:

- Sudo permissions
- SUID files
- Cron jobs
- Writable files and directories

**Observations:** 
- **Sudo:** Reviewed available sudo permissions for the practice user.
- **SUID:** Scanned for SUID executables and noted any unusual entries for further investigation.
- **Cron:** Identified the scheduled root job that runs `/opt/backup.sh`.
- **File permissions:** Confirmed that `/opt/backup.sh` was writable by other users during the intentionally vulnerable lab.
- **Conclusion:** The writable script combined with a root-run cron job demonstrates a privilege-escalation risk. The script should be owned by root and not writable by untrusted users.

## Remediation

- **Sudo:** Apply least privilege and avoid unrestricted sudo access to programs that can launch shells or execute arbitrary commands.
- **SUID:** Audit SUID programs and remove unnecessary special permissions.
- **File permissions:** Make privileged scripts owned by root and prevent ordinary users from modifying them. For example, use `chown root:root` and suitable permissions such as `chmod 755`.
- **Cron jobs:** Protect scheduled scripts, directories, and dependencies from unauthorized modification.
- **Enumeration:** Verify potential findings manually instead of treating every automated warning as a confirmed vulnerability.

## Key Takeaways

I learned how writable scripts and root cron jobs can combine to create a privilege escalation vulnerability. I also learned how LinPEAS can assist with Linux enumeration and why administrators must carefully manage permissions on files executed by privileged processes.
