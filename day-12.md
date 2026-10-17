# Day 12 — Cross-Site Scripting (XSS)

## 1. What is XSS?

Cross-Site Scripting (XSS) is a web security vulnerability that occurs when an application allows untrusted input to be interpreted as executable code in a user's browser. An attacker may exploit this to run JavaScript in the context of a vulnerable website. Depending on the vulnerability and the application's protections, this can expose sensitive page data, enable phishing, or allow actions to be performed using the user's existing session. XSS can be reflected, stored, or DOM-based.

_The website takes data that should be treated as data and accidentally allows it to become executable code_
_SQL injection tricks the database. XSS tricks the visitor’s browser._
_XSS is a client-side vulnerability that targets other application users, while SQL injection is a server-side vulnerability that targets the application's database._

## 2. Types of XSS

| Type | How it works | Example |
|---|---|---|
| Reflected XSS | User input is returned in the immediate HTTP response without safe handling. | A search term is reflected into the results page. |
| Stored XSS | Untrusted input is saved and later displayed unsafely. | A blog comment executes JavaScript when someone opens the post. |
| DOM-based XSS | Client-side JavaScript handles untrusted data unsafely, allowing code execution in the browser. | A URL parameter flows into an unsafe `innerHTML` assignment. |

### Easy way to remember

- Reflected = sent and returned immediately.
- Stored = saved and displayed later.
- DOM-based = unsafe processing in client-side JavaScript.

_Sink:
The place where JavaScript uses the data. Examples include unsafe assignments to innerHTML or calls to document.write()._

## 3. Why XSS is dangerous

XSS can allow attackers to manipulate a website as seen by a user. Depending on the context and protections, the impact may include:

- Stealing accessible sensitive information.
- Hijacking sessions when session tokens or other necessary credentials are accessible.
- Displaying fake login forms to trick users.
- Performing actions using the victim's existing session.
- Reading sensitive information displayed on the affected page.

HttpOnly cookies cannot be read directly by JavaScript, but they do not prevent all session abuse through XSS.

## 4. How to prevent XSS

### Output encoding
Encode untrusted data for its intended output context so that it is treated as data rather than executable markup. Prefer safe framework defaults and established encoding libraries.

### Input validation
Validate input against the expected type, format, length, and allowed values. Validation is an additional defense and does not replace output encoding.

### Content Security Policy (CSP)
Configure a CSP response header to restrict script execution and permitted resource sources. CSP is an additional layer of protection, not a substitute for fixing the underlying vulnerability.

### Safe DOM manipulation
Prefer `textContent` when displaying untrusted text. Avoid passing untrusted data into dangerous HTML or script-processing sinks such as `innerHTML` without appropriate protections.

## 5. Hands-on lab notes

### Reflected XSS into HTML context with nothing encoded
- Target: PortSwigger Web Security Academy.
- Input location: Search field.
- Test payload: `<script>alert(1)</script>`
- Expected result: The browser displays an alert and the lab is solved.
- Main lesson: The search input is reflected into the immediate response without proper encoding.

### Stored XSS into HTML context with nothing encoded
- Target: PortSwigger Web Security Academy.
- Input location: Blog comment field.
- Test payload: `<script>alert(1)</script>`
- Expected result: The alert executes when the affected post displays the stored comment.
- Main lesson: The input persists and is rendered unsafely on a later page view.

## 6. Ethical testing

Only test applications that I own or have explicit permission to assess. Use harmless proof-of-concept payloads to demonstrate vulnerabilities without accessing real user data or performing unauthorized actions.

## 7. What I learned today

I can explain reflected, stored, and DOM-based XSS without looking at my notes.
I completed the reflected XSS lab.
I completed the stored XSS lab.
- [ ] I can explain why XSS puts users and their accounts at risk.
- [ ] I can describe output encoding, input validation, and CSP.
