# Day 26 — Path Traversal and OS Command Injection

## 1. Path Traversal

Path traversal is a vulnerability that occurs when a website trusts user input to decide which file to open without checking whether the file is allowed. On Linux, `../` means moving up to the parent directory, which can allow an attacker to escape the intended folder and attempt to access sensitive files. Developers can prevent this by avoiding arbitrary user-supplied file paths, using an allow list of permitted filenames or file IDs, validating resolved paths, and checking file permissions.

## 2. OS Command Injection

OS command injection occurs when an application passes user input into an operating system command unsafely. An attacker may manipulate the input so that the server executes unintended commands. This can be especially dangerous because commands may run with the privileges of the application, potentially allowing access to files, sensitive information, or internal systems. Developers should avoid using a shell, use safe library functions or process-execution APIs, validate input against an allow list, and apply least-privilege permissions.

## 3. Comparison of Four Vulnerabilities

| Vulnerability | What input was trusted? | What went wrong? | Prevention |
|---|---|---|---|
| Path Traversal | A filename or file path supplied by the user | The application may access files outside the intended directory. | Use predefined file IDs, allow-listed filenames, and path validation. |
| OS Command Injection | Input passed into an operating system command | The input may change the command and cause unintended execution. | Avoid the shell, use safe APIs, and validate arguments. |
| SQL Injection (SQLi) | Input included in a database query | The input may change the query's meaning or operation. | Use parameterized queries. |
| Cross-Site Scripting (XSS) | User-supplied content displayed in a webpage | The browser may interpret untrusted content as executable JavaScript. | Use context-appropriate output encoding and safe DOM APIs. |

## 4. PortSwigger Labs Completed

### Lab 1: File Path Traversal — Simple Case

**Status:** Completed

I completed the PortSwigger File path traversal, simple case lab. This exercise helped me understand how an application that does not properly validate a user-controlled file path may allow access outside the intended directory. I learned the importance of restricting file access to permitted locations and validating filenames.

### Lab 2: OS Command Injection — Simple Case

**Status:** Completed

I completed the PortSwigger OS command injection, simple case lab. This exercise helped me understand how unsafe handling of user input in operating system commands can cause unintended command execution. I learned why developers should avoid passing user input through a shell and use safe APIs and input validation instead.

## 5. Review Questions

### Why does Linux treat `../` as “go up one folder”?

In Linux and other Unix-like systems, `..` is a special directory entry that refers to the parent directory. Therefore, `../` moves a relative path one directory level upward. Repeating it can move further up the directory structure, depending on the filesystem layout.

### Why can command injection be more serious than SQL injection or XSS?

Command injection can allow an attacker to execute operating system commands with the privileges of the vulnerable application. Depending on the server's permissions and security controls, this may expose files, sensitive data, or internal services. SQL injection primarily affects database operations, while XSS primarily affects users through their browsers. The severity of each vulnerability depends on the specific circumstances.

### What is the safest way to prevent each vulnerability?

- **Path traversal:** Avoid arbitrary user-supplied file paths. Use an allow list of permitted filenames or file IDs, validate paths, and enforce authorization.
- **OS command injection:** Avoid invoking a shell with user input. Prefer safe library functions; if a subprocess is necessary, pass arguments separately and validate them against an allow list.
- **SQL injection:** Use parameterized queries so user input remains data rather than becoming part of the SQL instructions.
- **XSS:** Use context-appropriate output encoding, safe DOM APIs, and appropriate sanitization when HTML is intentionally allowed.

## 6. Key Lesson

All four vulnerabilities demonstrate the importance of handling untrusted input securely. Applications must keep user data separate from instructions, use safe APIs, validate input appropriately, and enforce authorization. Security should be built into the application's design rather than relying on input filtering alone.
