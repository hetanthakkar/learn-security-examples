# Tampering

This example demonstrates information disclosure by injecting malicious query objects to a NoSQL database.

## Steps to reproduce

1. Install all dependencies

   `$ npm install`

2. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

   `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called **infodisclosure**. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

   `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

   ```
       http://localhost:3000/userinfo?username[$ne]=
   ```

4. Do you see user information being displayed despite the malicious request not having a valid username in the request?

Yes

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
   The database is queried using a username parameter taken directly from the HTTP request. If this username contains a script or a NoSQL query, it can manipulate the Mongoose query to behave in unexpected ways, resulting in a NoSQL injection attack.
2. Briefly explain how a malicious attacker can exploit them.
   An attacker can send a specially crafted query in place of the username that instructs the server to return sensitive data, such as all usernames. For instance, the server might return the first document in the database without verifying proper authorization. This happens because the input isn’t sanitized, making it a serious security vulnerability.
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the information disclosure vulnerability?
   The input from the HTTP request is sanitized to ensure it is a string and not a script or code.
   Non-alphanumeric characters like semicolons and brackets are removed to block potential NoSQL injection attempts.
