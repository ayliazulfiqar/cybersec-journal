# Day 34 – Project 3: Hardened Linux Server

## Objectives

- Configure Fail2ban to protect SSH against repeated failed login attempts.
- Enable automatic security updates.
- Review least-privilege settings and sudo users.
- Review SSH authentication logs.
- Perform a new Lynis security audit.
- Update the main Project 3 README with the completed stages, results, and screenshots.

## Tasks Completed

### 1. Fail2ban Configuration

Installed Fail2ban and configured the SSH jail.

Configuration:

```ini
[sshd]
enabled = true
maxretry = 3
findtime = 10m
bantime = 10m
backend = systemd
```

Checked the SSH jail using:

```bash
sudo fail2ban-client status sshd
```

Fail2ban configuration was completed. However, successful IP banning was not confirmed during the initial testing.

### 2. Automatic Security Updates

Worked on configuring unattended upgrades to automate security updates.

Configuration file:

```text
/etc/apt/apt.conf.d/20auto-upgrades
```

### 3. Least-Privilege Review

Reviewed sudo group membership:

```bash
getent group sudo
```

Also reviewed privileged access as part of the server security assessment.

### 4. Logging and Monitoring

Reviewed SSH authentication logs:

```bash
sudo journalctl -u ssh -n 30 --no-pager
```

Looked for failed login attempts and SSH authentication activity.

### 5. Final Lynis Security Audit

Performed a new Lynis audit and saved the output:

```bash
sudo lynis audit system > lynis-after.txt 2>&1
```

Final results:

| Metric | Result |
|---|---:|
| Hardening Index | 61 |
| Warnings | 1 |
| Suggestions | 44 |
| Tests Performed | 257 |
| Lynis Version | 3.1.6 |

## Screenshots

Screenshots are stored in the `screenshots/` directory of the Project 3 repository.

## Final Results

The initial Lynis hardening index was 63, while the final score was 61.

The final audit reported one warning and 44 suggestions. These findings indicate that additional security improvements may still be possible.

Fail2ban was configured, although successful IP banning was not verified during the initial test.

