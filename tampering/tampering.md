# Tampering

This example demonstrates tampering through script injection.

## Steps to reproduce

1. Install all dependencies

   `npm install`

2. Start the **insecure.ts** server

   `npx ts-node insecure.ts`

3. In the browser, type a potentially malicious script in the name field of the form

   ```
       <script> document.body.innerHTML = "<a href='https://google.com'> Gotcha </a>"</script>
   ```

4. Do you see the potentially malicious hyperlink being injected into the form?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
   The code does not validate user input, allowing users to inject scripts instead of plain strings. These scripts can link to malicious applications. This lack of validation means inputs meant to be simple strings can include executable code, which the server redirects as a hyperlink.

2. Briefly explain how a malicious attacker can exploit them.
   An attacker can inject code in place of a string through the input form. This code will execute on the server, violating its integrity by running unauthorized code. Since the server accepts input directly from the request without validation, any client can send malicious input that the server processes as if it were legitimate.

3. Briefly explain why **secure.ts** does not have the same vulnerabilties?
   In secure.ts, the input is sanitized using the escapeHTML function. This function converts the input into the expected format by replacing any code-like keywords with plain strings, effectively neutralizing the risk of code injection.
