# Day - 27 TryHackMe Web Application Security Lab Report

**1. Box Name and Difficulty**

- **Box/Room Name:** Web Application Security
- **Platform:** TryHackMe
- **Difficulty:** Beginner (confirm the difficulty shown on the room page)

**2. My Method**

I started by exploring the web application and understanding its functionality. I scanned the target using the tools available in the lab and checked the website for possible security weaknesses. I inspected the pages, tested user input fields, and looked for unusual application behavior. During testing, I identified a potential web application vulnerability that could be exploited due to insufficient input validation or security controls.

**3. What I Would Tell a Developer to Fix**

I would recommend implementing proper input validation and server-side security checks. The application should validate all user-supplied data, use parameterized queries where database interactions are involved, and enforce appropriate authentication and authorization controls. Error messages should also avoid revealing sensitive technical information. Regular security testing would help identify and fix similar vulnerabilities.

**4. One Thing I Got Stuck On and How I Solved It**

One challenge I faced was figuring out where to start testing the web application and which inputs might be vulnerable. I solved this by exploring the website systematically, testing one feature at a time, and reviewing the application's responses. This helped me narrow down the possible weakness and understand how web application vulnerabilities can be identified and investigated.
