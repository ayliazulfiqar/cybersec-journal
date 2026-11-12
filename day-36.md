# Day 36 – Final Re-test and Project 3 Completion

## Objective

Complete the final security checks for Project 3: Hardened Linux Server. Re-test the security configurations, compare the final results with the baseline, and organise the project documentation for GitHub.

## Work Completed

### 1. Final Lynis Audit

Ran a final system security audit using:

```bash
sudo lynis audit system
```

The results were the same as the previous audit.

| Measurement | Baseline | Previous audit | Day 36 |
|---|---:|---:|---:|
| Hardening index | 63 | 61 | 61 |
| Warnings | 0 | 1 | 1 |
| Suggestions | 36 | 44 | 44 |

The hardening index remained at 61. The audit still reported one warning and 44 suggestions, showing that there are areas for further improvement.

### 2. Final Nmap Scan

Performed the final network scan from Kali Linux against the Ubuntu Server:

```bash
nmap -sV -p- <server-ip> -oN final-scan.txt
```

The final scan was saved as `final-scan.txt` for comparison with the baseline scan.

### 3. SSH Security Verification

Tested SSH access from Kali Linux.

| Test | Result |
|---|---|
| SSH key authentication | Successful |
| Password authentication | Refused |
| Root login | Refused |

These checks confirmed that key-based SSH access was working and that password-based and root SSH login were refused.

### 4. UFW Firewall Verification

Checked the firewall using:

```bash
sudo ufw status verbose
```

Confirmed that UFW was active, incoming connections were denied by default, outgoing connections were allowed, and the configured firewall rules were present.

### 5. Fail2ban Verification

Fail2ban had been installed and configured to protect SSH against repeated failed login attempts.

The final SSH jail status still needs to be recorded:

```bash
sudo fail2ban-client status sshd
```

An active jail does not by itself confirm that a test IP was successfully banned.

### 6. Automatic Updates

Automatic security updates had been configured using `unattended-upgrades`.

Configuration can be checked with:

```bash
cat /etc/apt/apt.conf.d/20auto-upgrades
```

## Problems and Lessons Learned

- Fail2ban did not trigger a ban during an earlier failed-login test. Further troubleshooting is needed to confirm successful banning.
- The Lynis hardening index remained at 61 rather than increasing. The audit also continued to report one warning and 44 suggestions.
- I learned that configuring a security tool and successfully verifying its behaviour are two different things.
- Re-testing is important because it provides evidence that security controls are working rather than relying only on configuration files.

## Limitations and Future Improvements

- Investigate the remaining Lynis warning and suggestions.
- Verify that Fail2ban successfully blocks repeated SSH login attempts.
- Introduce centralised logging and monitoring with Wazuh in a future project.
- Explore additional AppArmor profiles.
- Consider creating an automated server-hardening script.

**Project 3: Hardened Linux Server – Final re-testing completed.**

[← Back to Project 3 README](../README.md)
