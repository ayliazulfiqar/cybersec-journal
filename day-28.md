# Day 28 – Cross-Site Request Forgery (CSRF) and Server-Side Request Forgery (SSRF)

## 1. Learning Objectives

Today I studied two important web application vulnerabilities:

- Cross-Site Request Forgery (CSRF)
- Server-Side Request Forgery (SSRF)

I learned how attackers can abuse a victim's authenticated browser or a vulnerable server to perform unauthorized actions.

I also completed three practical PortSwigger Web Security Academy labs using Burp Suite Community Edition.

---

## 2. Cross-Site Request Forgery (CSRF)

### What is CSRF?

Cross-Site Request Forgery is a web security vulnerability that allows an attacker to trick a logged-in user into performing an unwanted action on a website.

For example, imagine that a user is logged in to an online banking website. The browser stores an authentication cookie.

An attacker creates a malicious webpage containing a request that transfers money. If the victim visits that page while still logged in, the browser may automatically send the request with the victim's authentication cookie.

The website may believe the request came from the legitimate user.

### How CSRF works

1. The victim logs in to a trusted website.
2. The website stores an authentication cookie in the browser.
3. The victim visits an attacker's webpage.
4. The attacker's page causes the browser to send a request to the trusted website.
5. The browser automatically attaches the relevant authentication cookie.
6. If the website does not properly validate the request, the unwanted action may succeed.

### Common CSRF defenses

- Unpredictable CSRF tokens.
- SameSite cookie attributes.
- Checking the Origin or Referer header as an additional defense.
- Requiring reauthentication for sensitive operations.

---

## 3. Server-Side Request Forgery (SSRF)

### What is SSRF?

Server-Side Request Forgery is a vulnerability that allows an attacker to make a vulnerable server send HTTP requests to unintended destinations.

For example, a website might provide a feature that checks the availability of a product using a URL supplied to the server.

If the server does not validate the destination properly, an attacker may manipulate the URL to make the server access internal resources.

Possible targets include:

- Localhost services.
- Internal company applications.
- Private network addresses.
- Cloud metadata services.
- Internal administrative interfaces.

### How SSRF works

1. A website accepts a URL or destination from a user.
2. The server uses that destination to make an HTTP request.
3. The application does not properly restrict the destination.
4. An attacker supplies an unintended internal destination.
5. The server makes the request and may return sensitive information or trigger an internal action.

### Common SSRF defenses

- Use strict destination allow-lists.
- Block requests to private and loopback IP addresses unless explicitly required.
- Validate DNS resolution and check for DNS rebinding.
- Restrict outbound network traffic.
- Protect cloud metadata services.
- Avoid accepting arbitrary URLs when possible.

---
# 4. Practical Labs – PortSwigger Web Security Academy

## Lab 1 – CSRF vulnerability with no defenses

**Objective:** Change a victim's email address through a forged request.

**Steps performed:**
1. Logged in using `wiener:peter`.
2. Captured the email-change request using Burp Proxy.
3. Created an HTML form containing a hidden email field.
4. Hosted the form on the Exploit Server.
5. Delivered the exploit to the victim.
6. Verified that the lab was solved.

**Key learning:** Without CSRF protection, an attacker can trick a logged-in user's browser into performing unwanted actions.

## Lab 2 – Basic SSRF against localhost

**Objective:** Access an internal admin interface and delete the user `carlos`.

**Steps performed:**
1. Located the product stock-checking feature.
2. Intercepted the stock-check request using Burp Proxy.
3. Sent the request to Burp Repeater.
4. Modified the `stockApi` parameter to access `http://localhost/admin`.
5. Identified the user deletion endpoint.
6. Used the SSRF vulnerability to access the deletion endpoint.
7. Verified that the lab was solved.

**Key learning:** SSRF can allow attackers to access internal services through a vulnerable server.

## Lab 3 – CSRF token validation depends on request method

**Objective:** Bypass CSRF token validation by changing the HTTP request method.

**Steps performed:**
1. Logged in using `wiener:peter`.
2. Captured the email-change request using Burp Proxy.
3. Sent the request to Burp Repeater.
4. Tested an invalid CSRF token with POST and observed rejection.
5. Changed the request method to GET and observed that token validation was bypassed.
6. Created an auto-submitting HTML GET form without a CSRF token.
7. Hosted the exploit and delivered it to the victim.
8. Verified that the lab was solved.

**Key learning:** CSRF protection must be consistently enforced across all relevant HTTP methods.

**Important observation:** The form does not specify a method, so the browser uses GET by default. The exploit does not include a CSRF token.

### What I learned

I learned that CSRF protection must be applied consistently across HTTP methods.

If an application checks CSRF tokens on POST requests but skips validation on GET requests, an attacker may bypass the protection by changing the request method.

---

# 5. Important Questions and Answers

## Q1. Why does CSRF need a logged-in victim, while SSRF doesn't?

CSRF and SSRF exploit different trust relationships.

**CSRF needs a logged-in victim** because it abuses the victim's authenticated browser session. The browser automatically sends authentication cookies with requests to the target website.

Without a valid authenticated session, the unwanted request may not have the permissions needed to perform the action.

**SSRF does not necessarily need a logged-in victim** because it abuses the vulnerable server itself. The attacker tricks the server into making requests to other destinations.

The vulnerable server may already have network access or privileges that the external attacker does not have.

For example:

- CSRF: An attacker tricks a logged-in user into changing their account email.
- SSRF: An attacker tricks a website server into accessing an internal administrative service.

**Key difference:** CSRF abuses the victim's browser and session, while SSRF abuses the server's ability to make network requests.

## Q2. How does a CSRF token stop a request from another website?

A CSRF token is a secret, unpredictable value associated with a user's session or a particular request.

When a legitimate user submits a sensitive form, the application includes the CSRF token in the request.

The server checks whether the submitted token is valid.

An attacker's website generally cannot read the legitimate website's page because of the browser's Same-Origin Policy. Therefore, it normally cannot obtain the correct CSRF token.

When the attacker's website tries to submit a forged request, it cannot provide the correct token, so the server rejects the request.

**Example:**

A legitimate request might contain:

```http
POST /my-account/change-email HTTP/1.1
Host: example.com
Cookie: session=abc123

email=new@example.com
csrf=valid-random-token
```

A forged request may contain:

```http
POST /my-account/change-email HTTP/1.1
Host: example.com
Cookie: session=abc123

email=attacker@example.com
csrf=wrong-token
```

The server rejects the forged request because the token is missing or invalid.

**Important:** CSRF tokens must be unpredictable, properly validated, and protected from leakage. A token that is predictable or not checked on every relevant request may not provide effective protection.

## Q3. Why is SSRF especially serious in cloud environments?

SSRF is particularly serious in cloud environments because cloud servers often have access to internal resources that are not publicly accessible.

For example, a cloud application server may be able to communicate with:

- Internal databases.
- Private APIs.
- Administrative services.
- Internal management interfaces.
- Cloud metadata services.

An attacker on the internet may not be able to reach these resources directly. However, if the application has an SSRF vulnerability, the attacker may use the application server to send requests to them.

### Cloud metadata risk

Some cloud environments expose metadata services that provide information about the virtual machine.

Depending on the cloud provider and configuration, metadata services may expose temporary credentials or other sensitive information.

If an attacker can exploit SSRF to reach a metadata service, they may be able to obtain credentials and potentially access other cloud resources.

For example, in some AWS configurations, the instance metadata service is available at:

```text
http://169.254.169.254/
```

Modern AWS environments can use Instance Metadata Service Version 2 (IMDSv2), which requires a token and provides additional protection against many SSRF attacks. However, cloud metadata protections should be combined with network restrictions and least-privilege IAM permissions.

### Why this matters for cloud security

In cloud environments, one vulnerable web application may become an entry point to other internal services.

This can potentially lead to:

- Exposure of sensitive information.
- Unauthorized access to internal APIs.
- Theft or misuse of cloud credentials.
- Access to cloud resources.
- Further compromise of an organization's infrastructure.

**My understanding:** SSRF is especially dangerous in cloud environments because a public-facing application may have more network access and privileges than an external attacker. If those permissions are abused, the impact can extend beyond the vulnerable application.

---

# 6. Key Differences Between CSRF and SSRF

| Feature | CSRF | SSRF |
|---|---|---|
| Full form | Cross-Site Request Forgery | Server-Side Request Forgery |
| Main target | Victim's browser | Vulnerable server |
| Requires logged-in victim? | Usually, for authenticated actions | No |
| Exploits | Browser session and cookies | Server-side network access |
| Example | Changing a victim's email | Accessing localhost admin |
| Main defense | CSRF tokens, SameSite cookies | Destination validation, egress restrictions |

---

# 7. Tools and Skills Practiced

During these labs, I practiced:

- Burp Suite Proxy.
- Burp Suite Repeater.
- HTTP request inspection.
- GET and POST methods.
- HTML forms.
- Hidden form fields.
- JavaScript form submission.
- CSRF token validation.
- SSRF parameter manipulation.
- Accessing localhost services.
- Using the PortSwigger Exploit Server.

I completed these exercises using **Burp Suite Community Edition**.

---

# 8. Final Reflection

Day 28 helped me understand two important web application vulnerabilities.

Before these exercises, I understood that web applications use sessions, cookies, and server-side requests, but the practical labs helped me understand how attackers can abuse these mechanisms.

The CSRF labs demonstrated how an attacker can exploit a victim's authenticated browser session, especially when CSRF protection is missing or incorrectly implemented.

The SSRF lab demonstrated how a vulnerable server can be manipulated into accessing internal resources that an external attacker cannot reach directly.

The cloud security connection was particularly important because cloud applications often communicate with private services and metadata endpoints.

### My main takeaways

1. Authentication cookies alone do not protect against CSRF.
2. CSRF tokens must be validated consistently.
3. Changing an HTTP request method can expose weaknesses in CSRF protection.
4. SSRF can expose internal services.
5. Cloud metadata services and excessive server permissions can increase SSRF impact.
6. Burp Suite Community Edition is sufficient for manually testing these vulnerabilities.
