# Privilege Escalation

The example demonstrates a privilege escalation vulnerability and how to exploit it.

## Steps to reproduce

1. Install all dependencies

   `$ npm install`

2. Start the **insecure.ts** server

   `$ npx ts-node insecure.ts`

3. In the browser, send a GET request

   ```
       http://localhost:3000/send-form
   ```

4. Try different UserIds and see which one gives you authorized access to change the role of that user.

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
   No Authentication: The server doesn’t verify whether the user making the request is authenticated, allowing anyone to attempt changes to user roles.

Unrestricted Access to User Data: The server grants direct access to user data without checking the user’s identity or permissions, making it easy for attackers to manipulate roles.

2. Briefly explain how a malicious attacker can exploit them.

Skipping Authentication: An attacker can bypass authentication and perform unauthorized actions.

Altering User Roles: They can change their own or others’ roles to gain higher privileges.

Direct Data Manipulation: The attacker can directly access and modify user data, escalating privileges without proper checks.

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?

Authentication: Requiring users to authenticate before granting access to sensitive operations.

Authorization Checks: Ensuring that the authenticated user has the correct permissions for specific actions.

Input Validation and Sanitization: Validating and sanitizing inputs to prevent injection attacks and unauthorized data changes.
