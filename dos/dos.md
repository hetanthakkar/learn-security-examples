# Denial-of-Service (DoS)

This example demonstrates DoS vulnerabilities and how they can be exploited.

## Steps to reproduce

1. Install all dependencies

   `$ npm install`

2. Ignore if you have already done this once. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

   `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called **infodisclosure**. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

   `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

   ```
       http://localhost:3000/userinfo?id[$ne]=
   ```

4. Do you see the server crashing?

yes

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts** that can lead to a DoS attack.
   The attacker takes advantage of a vulnerability by sending a malicious script in place of an expected id. This causes the server to crash, resulting in a denial of service.
2. Briefly explain how a malicious attacker can exploit them.
   The id parameter, which follows a specific format, is provided by the client through the HTTP request. If an attacker sends a script instead of a valid id, it causes Mongoose to crash. Because the developer didn’t properly handle this error, the entire server ends up crashing.
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the DoS vulnerability?
   Added proper error handling with try-catch blocks to prevent server crashes.
   Implemented a rate limiter, restricting each IP to only one request every 5 seconds, to control the flow of incoming requests.
