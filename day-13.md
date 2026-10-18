# Day 13 - Authentication Vulnerabilities

## What are authentication vulnerabilities?

Authentication vulnerabilities are weaknesses in a website's login or identity verification process. They can allow attackers to discover valid usernames, guess passwords, or bypass security checks. A secure authentication system should verify a user's identity correctly before granting access.

## Three common weaknesses

1. **Username enumeration:** The website reveals whether a username exists by showing different error messages. Example: "Username not found" versus "Incorrect password."

2. **Brute force and weak passwords:** Attackers repeatedly guess passwords, especially when accounts use simple passwords or the website lacks effective attempt limits. Example: using a common password such as `12345678`.

3. **Flawed authentication logic:** The website incorrectly implements the login process. Example: granting access without properly verifying the second authentication factor.

## How to prevent authentication vulnerabilities

- Use generic login errors, such as "Invalid username or password."
- Apply rate limiting and carefully designed account-lockout protections.
- Encourage long, unique passwords and block commonly used or compromised passwords.
- Enforce multi-factor authentication on the server.
- Use secure password-reset tokens that are random, expire, and can only be used as intended.
- Test the complete authentication process for bypasses.

## What I learned today

I learned how login systems can expose usernames, allow excessive password guessing, or incorrectly skip verification steps.

## Hands-on Labs

### Lab 1: Username Enumeration via Different Responses

**Objective:** Understand how a website can reveal valid usernames through different login error messages.

**Tools used:** Burp Suite Browser, Proxy, Repeater, and Intruder.

**What I did:**
- Opened the lab and inspected the login page.
- Used Burp Suite Proxy to observe the login requests and responses.
- Compared the responses for different username attempts.
- Used Burp Suite Intruder to test the provided list of usernames.
- Looked for differences in response messages or response lengths.

**Vulnerability:** Username enumeration.

**Why it matters:** An attacker may discover valid usernames and use that information to target accounts with further attacks.

**Prevention:** Use generic login error messages, such as "Invalid username or password," and avoid revealing account existence through response timing or other differences.

**What I learned:** I learned how differences in website responses can reveal whether a username exists, even when the attacker does not know the password.

---

### Lab 2: 2FA Simple Bypass

**Objective:** Understand how an authentication flow can allow a user to bypass the second verification step.

**Tools used:** Burp Suite Browser, Proxy, and Repeater.

**What I did:**
- Opened the lab and followed the login process.
- Observed the requests sent during authentication.
- Examined how the website handled the second verification step.
- Investigated whether the website properly enforced the second factor.
- Tested the intended vulnerability within the authorized lab environment.

**Vulnerability:** Broken multi-factor authentication logic.

**Why it matters:** If a website does not properly enforce the second factor, someone who knows a user's password may be able to access the account without completing the additional verification step.

**Prevention:** Verify every authentication step on the server and grant full access only after all required checks succeed.

**What I learned:** I learned that enabling two-factor authentication is not enough on its own. The website must correctly enforce the verification process before granting access.

---

## Overall Lab Summary

Today, I studied authentication vulnerabilities and practiced identifying weaknesses in login systems using Burp Suite. I learned about username enumeration, which can reveal valid accounts, and multi-factor authentication bypasses, which can occur when the login process is implemented incorrectly. These labs helped me understand why secure authentication logic and proper error handling are important for protecting user accounts.

