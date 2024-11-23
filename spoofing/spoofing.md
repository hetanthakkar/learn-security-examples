# Spoofing

This example demonstrates spoofind through two ways -- Stealing cookies programmatically and cross site request forgery (CSRF).

## Steps to reproduce the vulnerability

1. Install dependencies

   `$ npx install`

2. Start the **insecure.ts** server

   `npx ts-node insecure.ts`

3. Start the malicious server **mal.ts**

   `npx ts-node mal.ts`

4. Open **http://localhost:8000** in a browser, type a name and Submit.

5. Open the **Application** tab in the Browser's inspect pane. Find the **Cookies** under **Storage**. You should see a **connect.sid** cookie being set.

6. Open the HTML file **mal-steal-cookie.html** file in the same browser (different tab). Open inspect and view the console.
   When the user is not logged out, we see : { message: 'Operation successful' }
   When the user is logged out, we see : { message: 'Unauthorized Access' }

7. Click the link in the HTML file. Do you see the cookie being stolen in the console?
   Yes

8. Open the HTML file **mal-csrf.html** file in the same browser (different tab). What do you see if the user has not logged out of **insecure.ts**? What do you see if the user has logged out?

## For you to answer

1. Briefly explain the spoofing vulnerability in **insecure.ts**.
   The server uses cookies to identify users by sending them with each request. However, these cookies can be read programmatically by a malicious attacker, making them vulnerable to theft.
2. Briefly explain different ways in which vulnerability can be exploited.
   For instance, if a phishing link is opened in the same browser where the cookie is stored, the link could include a script to read all saved cookies. Once the attacker obtains the cookie, they can use it along with the server URL to send requests impersonating the authenticated user, enabling spoofing.
3. Briefly explain why **secure.ts** does not have the spoofing vulnerability in **insecure.ts**.
   In secure.ts, cookies are configured with additional security features:
   httpOnly: This prevents the cookie from being accessed programmatically by scripts, protecting it from theft.
   sameSite: Ensures the cookie is only sent if the client and server domains match, preventing it from being sent with requests originating from other sites.
   These configurations effectively guard against cookie theft and cross-site request forgery (CSRF).
