# Day 09 - SQL Injection Basics

## Review

**1. Explain what a request is and what Burp’s Repeater does.**

A request is a message sent to the server asking for a response or information, and Burp's Repeater is a tool that lets us modify and resend the web request to see what the server would respond with and how



One more security detail: applications should also store passwords using an appropriate password-hashing algorithm and verify them securely, rather than comparing plaintext passwords in a database. Parameterized queries remain essential even when password handling is done correctly.

While Error-Based Injection can reveal structural information, Union-Based Injection is the primary method for extracting large amounts of data.

## TryHackMe
This room covered a lot of ground. You picked up the SQL injection syntax, saw how the vulnerability occurs when apps shove user input into queries, and worked through the main SQLi types: In-Band (Error-Based and Union-Based), Blind (Authentication Bypass, Boolean-Based, Time-Based), and Out-of-Band. The four lab levels had you pulling credentials out of databases, bypassing logins, and guessing passwords one character at a time. On the defence side, you looked at prepared statements, input validation, and least privilege.
Objectives Learned

    Identified the SQL syntax attackers use in injection payloads (UNION, LIKE, comments, information_schema)
    Understood how SQL Injection occurs when user input gets concatenated into queries
    Detected injection points by testing with special characters and watching application responses
    Exploited In-Band SQL Injection with Error-Based and Union-Based techniques to extract database contents
    Bypassed authentication using Blind SQL Injection
    Extracted data character-by-character using Boolean-Based and Time-Based Blind SQL Injection
    Understood Out-of-Band SQL Injection and DNS/HTTP exfiltration
    Applied remediation strategies: prepared statements, input validation, and least privilege
