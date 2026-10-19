# Day 14 — Web Security Review

## Objective
Review web security fundamentals, identify weak areas through a closed-book checkpoint, correct misconceptions, and strengthen my understanding through follow-up questions.

## 1. Initial Closed-Book Checkpoint

I answered six questions without notes.

| Topic | Initial Grade | Initial Feedback |
|---|---|---|
| SQL Injection | Yellow | Understood malicious input but confused SQL queries with response scripts. |
| UNION-Based SQL Injection | Red | Did not fully understand how UNION combines query results or why column counts must match. |
| Cross-Site Scripting (XSS) | Yellow | Recognised stored and DOM-based XSS but needed clarification on reflected XSS. |
| Username Enumeration | Yellow | Recognised differences in login errors but initially confused enumeration with brute-force attacks. |
| HTTP and Burp Repeater | Green | Correctly explained requests, responses, and modifying and resending requests. |
| DNS, ARP, TCP and HTTP | Green | Correctly explained DNS, ARP, the TCP three-way handshake, and the basic request-response process. |

**Initial checkpoint score:** 2/6 fully correct under strict grading.

## 2. Remedial Practice and Updated Understanding

After the checkpoint, I answered follow-up questions to improve my weak areas.

### SQL Injection — Improved
I correctly explained that parameterised queries treat user input as data rather than executable SQL.

**Key takeaway:** Parameterised queries separate SQL commands from user-supplied values and are the primary defence against SQL injection.

### UNION-Based SQL Injection — Improved
I correctly explained that the query fails when the two SELECT statements return different numbers of columns.

**Key takeaway:** UNION combines result sets. Both SELECT statements must return the same number of columns, with compatible data types.

### Cross-Site Scripting (XSS) — Improved
I correctly identified a scenario in which malicious content is saved in a comment and runs when other users view the page.

**Key takeaway:**
- Reflected XSS: input is reflected in a response.
- Stored XSS: malicious content is stored and later served to users.
- DOM-based XSS: unsafe client-side JavaScript handling causes the vulnerability.

I still need to practise distinguishing reflected XSS from DOM-based XSS independently.

### Username Enumeration — Improved
I correctly identified username enumeration and explained that consistent login error messages make it harder to discover valid usernames.

**Key takeaway:** Generic authentication errors help prevent enumeration. Rate limiting and multi-factor authentication provide additional protection but do not replace consistent error handling.

## 3. Current Understanding

| Topic | Current Status |
|---|---|
| SQL Injection | Improved through remedial practice |
| UNION-Based SQL Injection | Improved through remedial practice |
| Cross-Site Scripting | Improved; more independent practice needed |
| Username Enumeration | Improved through remedial practice |
| HTTP and Burp Repeater | Strong initial understanding |
| DNS, ARP, TCP and HTTP | Strong initial understanding |

These updated statuses reflect my follow-up answers, not a new closed-book test of all six topics.

independently in practical labs.

