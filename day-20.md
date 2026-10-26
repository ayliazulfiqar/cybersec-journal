# Day 20 — Linux Privilege Escalation Checkpoint

## Checkpoint Score: 2/6 Green

Today I completed a closed-book checkpoint on Linux privilege escalation. I tested my understanding of privilege escalation, common weaknesses, enumeration commands, LinPEAS, and GTFOBins.

### Results

| # | Topic                             | Score                                   |
| - | --------------------------------- | --------------------------------------- |
| 1 | Privilege escalation              | 🟢 Green                                |
| 2 | Four weaknesses and their fixes   | 🟢 Green for identifying the weaknesses |
| 3 | `sudo -l` and SUID search         | 🟡 Yellow                               |
| 4 | Writable scripts executed by root | 🟡 Yellow                               |
| 5 | LinPEAS                           | 🟢 Green                                |
| 6 | GTFOBins                          | 🟡 Yellow                               |

## What I learned

1\. Privilege escalation

Privilege escalation means gaining access to permissions higher than those originally assigned to a user.

2\. Four common Linux weaknesses

I correctly identified the four weaknesses I had practised:

- Misconfigured sudo permissions
- SUID files
- Writable scripts
- Misconfigured cron jobs

I need to keep practising the fixes for each weakness, not just remembering their names.

3\. Enumeration commands

- `sudo -l` shows which commands the current user can run using sudo.
- `find / -perm -4000 2>/dev/null` searches for files with the SUID permission bit set.
- `2>/dev/null` hides error messages, including permission-denied messages.

My main mistake was describing SUID files as sudo files. They are different security mechanisms.

4\. Writable scripts run by root

A writable script executed by a root cron job is dangerous because a user who can modify the script may be able to execute malicious commands with root privileges.

The fix is to restrict write access to trusted administrators and secure the script's permissions and directory.

5\. LinPEAS

LinPEAS is a Linux privilege-escalation enumeration script that searches for potential security weaknesses. Its output must be verified manually because some findings may be false positives, and it may miss issues.

6\. GTFOBins

GTFOBins is a reference documenting ways Unix binaries can be abused under certain configurations. It is useful during authorized security assessments to investigate whether a binary could allow privilege escalation or bypass restrictions.

## Weak spots to improve

- Understand the difference between sudo permissions and SUID permissions.
- Explain why writable scripts executed by root are dangerous.
- Memorize the appropriate fix for each of the four weaknesses.
- Remember that GTFOBins covers Unix binaries, not just scripts.
- Practise explaining every concept clearly without notes.

## Final reflection

I understand the basic concepts of Linux privilege escalation and can identify common weaknesses. However, I need more practice explaining the security impact of misconfigurations and their fixes.

Goal for Day 22: Repeat the checkpoint without notes and aim to answer all six questions confidently, especially the questions about enumeration commands, root cron jobs, and GTFOBins.
