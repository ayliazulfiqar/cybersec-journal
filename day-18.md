# Day 18 — Linux Privilege Escalation

Linux privilege escalation occurs when a user gains permissions beyond those originally assigned to their account. For example, a normal user may exploit a system misconfiguration or vulnerable program to obtain root privileges. Understanding privilege escalation helps security professionals identify weaknesses, assess security risks, and protect Linux systems against unauthorized access.

## Common Privilege Escalation Paths

### 1. Sudo Misconfigurations

Incorrect sudo permissions may allow a normal user to execute powerful commands as root and gain unauthorised privileges.

**Enumeration command:**
```bash
sudo -l
```

### 2. SUID Files

SUID (Set User ID) is a special permission that allows a program to run with its file owner's effective privileges. Insecure SUID programs may expose elevated access.

**Enumeration command:**
```bash
find / -perm -4000 -type f 2>/dev/null
```

### 3. Weak File Permissions

Scripts, configuration files, or other resources that can be modified by unauthorized users may allow privilege escalation when those files are trusted or executed by privileged processes.

**Inspection command:**
```bash
ls -l /path/to/file
```

### 4. Cron Jobs

Cron jobs are scheduled tasks that run automatically. If a task runs as root and uses scripts or files that ordinary users can modify, it may create a privilege escalation risk.

**Inspection commands:**
```bash
cat /etc/crontab
ls -la /etc/cron.d
```

## Linux Enumeration Commands

The following commands help identify the current user's identity, privileges, and potential permission-related weaknesses.

```bash
id
whoami
sudo -l
find / -perm -4000 -type f 2>/dev/null
```

- `id` displays the current user's UID, GID, and group memberships.
- `whoami` displays the current username.
- `sudo -l` lists commands the current user is allowed to execute through sudo.
- `find / -perm -4000 -type f 2>/dev/null` searches for regular files with the SUID permission bit set while suppressing error messages.

These commands support initial enumeration. Their output must be investigated carefully because not every privileged permission or SUID file represents a vulnerability.

## Remediation and Prevention

Administrators can reduce privilege escalation risks by following the principle of least privilege and regularly reviewing system configurations.

- **Sudo:** Grant only the permissions required for a user's responsibilities. Avoid unrestricted sudo access to programs that can launch shells or execute arbitrary commands.
- **SUID files:** Audit SUID programs and remove unnecessary SUID permissions.
- **File permissions:** Ensure privileged scripts and configuration files are writable only by trusted users.
- **Cron jobs:** Protect scheduled tasks, their scripts, directories, and dependencies from unauthorised modification.
- **System maintenance:** Keep the operating system and installed software updated and review security configurations regularly.

## Key Takeaways

- Learned two common Linux privilege escalation paths.
- Reviewed Linux user identities and sudo permissions.
- Learned how to enumerate SUID files.
- Understood how weak file permissions and insecure scheduled tasks can introduce security risks.
- Learned how least privilege and secure file permissions help prevent privilege escalation.

