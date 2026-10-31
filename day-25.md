# Day 25 — Access Control and IDOR

## 1. What is access control?

Access control determines what a user can view or do. Authentication verifies who the user is, while access control checks what they can do.

## 2. Horizontal vs. vertical privilege escalation

- **Horizontal:** Accessing another user's information or resources at the same privilege level.
- **Vertical:** Gaining access to actions or resources meant for a higher-privilege user, such as an administrator.

## 3. What is IDOR?

IDOR stands for Insecure Direct Object Reference. It occurs when an application uses an object identifier but fails to check whether the requesting user is authorized to access that object.

Example: A user can view their own invoice, but a broken authorisation check lets them view another customer's invoice by changing the requested identifier.

## 4. How can developers prevent it?

- Check authorisation on the server for every request.
- Verify that the user has permission to access the specific object.
- Never trust client-supplied IDs as proof of permission.
- Deny access by default unless permission is explicitly granted.
- Test authorisation rules for different users and roles.

## 5. What I learned from the labs

- **Lab 1: Unprotected admin functionality**  
  I learned that hiding an admin page or removing its link does not protect it. If the server does not check a user's permissions, an unauthorized user may still access administrative functionality.

- **Lab 2: User ID controlled by request parameter**  
  I learned that an application can have an IDOR vulnerability when it trusts a user ID supplied in a request without checking whether the logged-in user is authorized to access that account's information.

- **Lab 3: Insecure direct object references (IDOR)**  
  I learned that object identifiers, such as account IDs or document IDs, can expose private information if the application does not properly verify access permissions. Knowing an object's ID should never be enough to access it.

- **What caused the vulnerabilities?**  
  The vulnerabilities were caused by missing or incorrect server-side access control checks. The application did not properly verify whether the requesting user had permission to access a particular page, account, or resource.

- **How could the developer fix them?**  
  Developers should enforce authorization checks on the server for every request. They should verify that users have permission to access the specific resource or perform the requested action, never trust client-supplied IDs alone, and deny access by default unless permission is explicitly granted.

### Key takeaway

I learned that authentication and authorization are different. Authentication verifies who a user is, while authorization determines what they are allowed to access. Proper server-side authorization checks help prevent IDOR and privilege escalation vulnerabilities.
