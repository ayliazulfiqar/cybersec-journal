# Day 30 - Active Directory Basics

## 1. What is Active Directory?

Active Directory is a Microsoft technology
used by organisations to centrally manage
users, computers, groups and permissions.

I think of it as a company's central reception
desk that checks employee identities and
controls access to company resources.

## 2. Important Terms

- Domain: A managed directory environment.

- Domain Controller: A server running AD DS.

- User: An individual account.

- Group: A collection of accounts.

- OU: A container used to organise directory objects.

- Group Policy: Centralised rules and settings.

- Kerberos: A ticket-based authentication protocol.

- NTLM: An older challenge-response authentication protocol.

- Domain Admin: A highly privileged domain account.

## 3. How Kerberos Works

1. User logs into a computer.

2. Domain Controller authenticates the user.

3. User receives a Ticket Granting Ticket.

4. User requests a service ticket.

5. User presents the service ticket to a server.

6. Server checks access permissions.

## 4. Active Directory Attacks

### Password Spraying
Trying a small number of passwords against
many accounts.

ATT&CK: T1110.003
Tactic: Credential Access

Defence: Strong passwords, MFA and monitoring.

### Kerberoasting
Requesting Kerberos service tickets and
attempting to crack their associated
encrypted information offline.

ATT&CK: T1558.003
Tactic: Credential Access

Defence: Strong service account passwords
and monitoring unusual ticket requests.

### BloodHound
A tool that maps Active Directory users,
groups, permissions and relationships.

Related tactic: Discovery

Defence: Regular permission reviews and
monitoring unusual directory queries.

## 5. My Active Directory Diagram

<img width="472" height="512" alt="ad-network-diagram" src="https://github.com/user-attachments/assets/a6598f08-9824-4e2d-bf05-ce86e1d78237" />

## 6. What I Learned

Today I learned how companies use Active
Directory to manage their Windows networks.

I understood domains, Domain Controllers,
users, groups, OUs and Group Policy.

I also learned how Kerberos and NTLM
are used for authentication.

Finally, I learned why attackers target
Active Directory and why protecting
privileged accounts is important.

