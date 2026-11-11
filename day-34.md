# Day 34 – Linux Server Hardening

## Project

[Project 3 – Linux Server Hardening](/hardened-server/README.md)

## Objective

Improve Linux server security by implementing SSH key authentication, hardening SSH configuration, and configuring the UFW firewall.

## Work Completed

- Generated an Ed25519 SSH key pair on Kali Linux.
- Installed the public key on the Linux server.
- Configured SSH to disable root login and password authentication.
- Enabled public-key authentication.
- Limited SSH authentication attempts to 3.
- Validated SSH configuration.
- Configured UFW to deny incoming connections by default.
- Allowed outgoing connections.
- Allowed SSH traffic through the firewall.
- Enabled UFW and checked its status.

## SSH Configuration

```text
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
MaxAuthTries 3
```

## Firewall Configuration

```bash
sudo ufw allow OpenSSH
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw enable
sudo ufw status verbose
```

## Evidence

Screenshots are stored in the Project 3 `screenshots` folder.

- `ssh-config.png` – SSH hardening configuration.
- `ufw-status.png` – UFW firewall status.

## Problems I Hit

- SSH public key was already present, so I used `ssh-copy-id -f` to install it again.
- SSH configuration options were commented out, so I had to activate the required settings.
- I initially used the wrong SSH validation command and corrected it to `sudo /usr/sbin/sshd -t`.
- UFW remained inactive after installation until I configured its rules and enabled it.

## Result

Successfully completed SSH hardening and UFW firewall configuration for Project 3.

