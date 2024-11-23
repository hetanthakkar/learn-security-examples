# Repudiation

The example demonstrates a vulnerability that can lead to repudiation by malicious users attempting to access the services provided by a server.

## Steps to reproduce

1. Install all dependencies

   `$ npm install`

2. Run the server **insecure.ts**.

3. Pretend to be a malicous user and interact with the services by sending requests from the browser.

4. Do you think your actions can be repudiated?

## For you to do

1. Briefly explain the vulnerability.
   The vulnerability in insecure.ts lies in the absence of proper logging and auditing mechanisms. This allows malicious users to carry out actions without leaving any trace, making it impossible to track or attribute their behavior. As a result, users can deny their actions (repudiation) without evidence to hold them accountable.
2. Briefly explain why the vulnerability is addressed in **secure.ts**.
   The issue is resolved in secure.ts by introducing robust logging and auditing mechanisms. These systems record all user actions and changes, creating a clear history of events. This ensures that actions can be traced back to specific users, preventing repudiation and ensuring accountability.
3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?
   Design Pattern Used: Chain of Responsibility.
   How It Works: In the Chain of Responsibility pattern, a request is passed along a sequence of handlers. Each handler either processes the request or forwards it to the next handler in the chain.
   Application in secure.ts:
   Middleware Handlers: Each middleware handles a specific task, such as authentication, authorization, or logging.
   Logging Middleware: A dedicated middleware captures important details like the user’s identity, action performed, and the timestamp of each request, ensuring comprehensive tracking and auditing.
