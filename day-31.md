# Day 31 — Vulnerability Assessment Findings

## Finding 1: Anonymous FTP Access Enabled

- **Where:** Metasploitable 2 — FTP service, TCP port 21 (`vsftpd 2.3.4`).
- **What:** The FTP server allows users to log in anonymously without providing a regular username and password.
- **Evidence:** Nmap identified anonymous FTP login as allowed. Manual FTP login returned `230 Login successful`. The remote directory listing showed only `.` and `..`.
- **Impact:** Unauthorized users can establish FTP sessions. Depending on directory permissions, this could expose files or allow unintended access. No sensitive files or write permissions were confirmed.
- **Fix:** Disable anonymous FTP access if it is not required. Restrict access to authorized users, apply appropriate directory permissions, and use secure file transfer protocols such as SFTP or FTPS.
- **ATT&CK:** No specific technique is confirmed by the observed evidence. Anonymous authentication alone does not establish account abuse.

---

## Finding 2: Anonymous SMB Share Access

- **Where:** Metasploitable 2 — SMB/Samba service, TCP ports 139 and 445; share name `tmp` (`Samba 3.0.20-Debian`).
- **What:** The SMB server allows anonymous users to connect to the `tmp` share and list its directory contents without providing a password.
- **Evidence:** SMB share enumeration using `smbclient` returned `Anonymous login successful`. Connecting to the `tmp` share also returned `Anonymous login successful`. The directory listing displayed `.ICE-unix`, `.X11-unix`, `.X0-lock`, and `4608.jsvc_up`.
- **Impact:** Unauthenticated network users can view directory entries in the exposed share. Depending on the contents and permissions, this could lead to information disclosure or unauthorized file access. Reading sensitive files and writing to the share were not verified.
- **Fix:** Disable guest or anonymous SMB access where unnecessary. Restrict share access to authenticated users, apply least-privilege permissions, review shared directories for sensitive information, and limit SMB access to trusted networks.
- **ATT&CK:** No specific technique is confirmed by the observed evidence. If anonymous access is later used to discover files or collect data, a relevant technique may be considered based on that additional activity.

---

## Additional Observation: Telnet Service Enabled

- **Where:** Metasploitable 2 — Telnet service, TCP port 23 (`Linux telnetd`).
- **What:** The target is running Telnet, a remote-access protocol that does not encrypt session traffic.
- **Evidence:** Nmap service detection identified `23/tcp open telnet Linux telnetd`.
- **Impact:** If users authenticate through Telnet, usernames, passwords, and session information may be exposed to someone monitoring the network.
- **Fix:** Disable Telnet and use SSH for encrypted remote administration.
- **ATT&CK:** No ATT&CK technique is confirmed because no credential interception or unauthorized access was observed.
<img width="1672" height="941" alt="Untitled" src="https://github.com/user-attachments/assets/22577e21-e47c-4859-a5c1-e69dfacda9a0" />
