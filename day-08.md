# Day 08 - Burp Suite Basics

## What I did today

Today I got started with Burp Suite and learned how it helps with web security testing. I set up Burp Suite, opened its built-in browser, and followed the getting-started tutorials on PortSwigger Web Security Academy.

At first, websites weren't loading in the Burp browser when Intercept was on. After turning it off, the pages loaded. I figured out that Burp was pausing requests and that I needed to click Forward to let them continue.

## What I practised

### 1. Intercepting HTTP traffic

I learned how to intercept HTTP requests using Burp's Proxy tool.

With Intercept turned on, I could see requests before they were sent to the server. I practised looking at the request details and using Forward to let requests continue.

[PortSwigger tutorial - Intercepting HTTP traffic](https://portswigger.net/burp/documentation/desktop/getting-started/intercepting-http-traffic)

### 2. Modifying requests

I practised modifying HTTP requests in Burp and saw how changing request details can affect what gets sent to the server.

I also got more familiar with the different parts of a request, including the method, path, headers, and parameters.

[PortSwigger tutorial - Modifying requests](https://portswigger.net/burp/documentation/desktop/getting-started/modifying-http-requests)

### 3. Setting the target scope

I learned how to set a target scope in Burp so I can focus on the website I'm testing instead of collecting traffic from unrelated sites.

This is useful for keeping my testing organised and making sure I focus on the intended target.

[PortSwigger tutorial - Setting the target scope](https://portswigger.net/burp/documentation/desktop/getting-started/setting-target-scope)

### 4. Reissuing requests

I practised reissuing HTTP requests using Burp's Repeater tool.

Repeater lets me take an existing request, make changes, send it again, and compare the response. This is useful for testing how a website handles different inputs without having to repeat the same actions in the browser.

[PortSwigger tutorial - Reissuing requests](https://portswigger.net/burp/documentation/desktop/getting-started/reissuing-http-requests)

## Things I learned

- **Proxy:** Intercepts requests so I can inspect them and decide when to forward them.
- **HTTP history:** Keeps track of the requests and responses passing through Burp.
- **Repeater:** Lets me modify and resend requests to compare responses.
- **Target scope:** Helps me focus on the website I'm testing.
- **HTTP requests:** Contain useful information such as the method, path, headers, and sometimes cookies.


![Intercepted HTTP request in Burp Suite](screenshots/day-08-intercepted-request.png)

## What I still want to improve

- Get more comfortable reading HTTP requests and responses.
- Practice changing request parameters and observing the results.
- Learn more about cookies and how sessions work.
- Continue practising with beginner-friendly PortSwigger labs.

## Overall

Today was about getting comfortable with Burp Suite and learning the basics of intercepting, modifying, and reissuing HTTP requests. I also learned how to set the target scope so I can keep my testing focused.

Still have a lot to learn, but this was a good starting point for understanding how web requests work and how Burp helps analyse them.

# TryHackMe 

I have completed the *** 25 Days Of Cyber Security *** 

## Day-01 Web Exploitation (A Christmas Crisis)

• Objective: Achieved Authentication Bypass on a web application by tampering with client-side session cookies.

• Key Takeaways:

	• Cookie Analysis: Used browser Developer Tools to find and inspect the active session cookies.
	• Data Manipulation: Recognised the cookie was Hex-encoded JSON and used CyberChef to decode the payload.
	• Privilege Escalation: Changed the username value from guest to santa, re-encoded it, and modified the cookie in the browser to log in without credentials.
	• Security Flaw: Demonstrated how relying entirely on client-side data for authentication without backend validation leads to easy bypasses.

