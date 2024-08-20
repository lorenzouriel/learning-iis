# HTTP x HTTPS
- Tool to test: [Wireshark]( )

HTTP (HyperText Transfer Protocol) and HTTPS (HyperText Transfer Protocol Secure) are protocols used to transfer data over the web. The main differences between them are:

### 1. Security
- HTTP: Data transmitted over HTTP is not encrypted, making it vulnerable to interception by attackers (e.g., man-in-the-middle attacks).
- HTTPS: Data transmitted over HTTPS is encrypted using SSL/TLS, which secures the communication between the client and the server, protecting it from eavesdropping and tampering.

### 2. Port Number
- HTTP: Uses port 80 by default.
- HTTPS: Uses port 443 by default.

### 3. Data Integrity
- HTTP: Data can be intercepted or altered by attackers without the user’s knowledge.
- HTTPS: Ensures data integrity, meaning the data sent and received cannot be modified without detection.

### 4. Authentication
- HTTP: Does not provide any verification of the identity of the website, which can lead to users unknowingly interacting with malicious sites.
- HTTPS: Provides authentication through SSL/TLS certificates, ensuring that the user is connected to the legitimate website.

### 5. SEO Impact
- HTTP: Websites using HTTP may be penalized by search engines like Google, which prioritize HTTPS sites for security reasons.
- HTTPS: Google and other search engines favor HTTPS websites, which can improve search rankings.

### 6. User Trust
- HTTP: Browsers may warn users when accessing sites via HTTP, indicating the connection is "Not Secure."
- HTTPS: Users are more likely to trust sites using HTTPS as their browsers show a padlock icon or a similar indicator of security.

### 7. Performance
- HTTP: Generally faster since it does not have the overhead of encryption, but this is less of an advantage with modern HTTP/2.
- HTTPS: Slightly slower due to the encryption/decryption process, though the difference is minimal with optimizations like HTTP/2 and TLS session resumption.

## HTTP Parameters Types

**a. Query Parameters:** Used to pass filters and options via URL.
```json
https://example.com/search?query=chatgpt&lang=pt
```

**b. Path Parameters:** Used to identify specific resources in an API.
```json
https://example.com/users/12345
```

**c. Body Parameters:** Used to send complex data in the body of a request.
```json
{
  "username": "lorenzo",
  "password": "secret"
}
```

**d. Header parameters:** Used for metadata and authentication.
```json
Authorization: Bearer <token>
Content-Type: application/json
```

**e. Matrix parameters:** Used within URL path segments.
```json
https://example.com/users;id=123;type=admin
```

**f. Cookie Parameters:** Used to maintain session state on the client side.
```json
Cookie: sessionId=abc123
```

**g. Form Parameters:** Used to submit HTML form data.
```json
//Example application/x-www-form-urlencoded
POST /submit HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 29

username=lorenzo&age=30


// Example (multipart/form-data)
POST /upload HTTP/1.1
Host: example.com
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW

------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="file"; filename="photo.jpg"
Content-Type: image/jpeg
```

**h. Fragment Parameters:** Used to reference a specific part of a document.
```json
https://example.com/page#section2
```

## SSL x TLS
SSL (Secure Sockets Layer) and TLS (Transport Layer Security) are cryptographic protocols designed to secure communications over a network. TLS is the successor to SSL, and while they are often referred to interchangeably, they have important differences:

### 1. Development History
**SSL:**
- SSL was developed by Netscape in the mid-1990s.
- The first version, SSL 2.0, was released in 1995, but it had several security flaws.
- SSL 3.0, released in 1996, addressed many of these issues but still had vulnerabilities.

**TLS:**
- TLS was developed as an upgrade to SSL by the Internet Engineering Task Force (IETF).
- TLS 1.0 was released in 1999, with improvements over SSL 3.0.
- Subsequent versions (TLS 1.1, TLS 1.2, and TLS 1.3) have continued to enhance security and performance.

### 2. Security
**SSL:**
- SSL is considered insecure today due to vulnerabilities like the POODLE attack that affect SSL 3.0.
- SSL 2.0 and SSL 3.0 are both deprecated, and their use is strongly discouraged.

**TLS:**
- TLS is much more secure than SSL, with each new version addressing vulnerabilities found in older versions.
- TLS 1.2 and TLS 1.3 are currently the most widely used versions, with TLS 1.3 offering significant security improvements and performance enhancements.

### 3. Protocol Handshake
**SSL:**
- The SSL handshake involves more steps and is less efficient, which can lead to slower connections.
- SSL relies on outdated cryptographic algorithms that are now considered insecure.

**TLS:**
- The TLS handshake is more streamlined and secure, especially in TLS 1.3, where the handshake has been simplified.
- TLS uses stronger cryptographic algorithms and provides options for forward secrecy, ensuring that even if a session key is compromised, past communications remain secure.

### 4. Backward Compatibility
**SSL:**
- While SSL is no longer used, some older systems may still support it for compatibility reasons, though this is not recommended.

**TLS:**
- TLS is designed to be backward compatible with SSL 3.0, but most modern implementations disable this compatibility to avoid security risks.

### 5. Cipher Suites
**SSL:**
- SSL supports a limited set of cipher suites, many of which are now considered weak.

**TLS:**
- TLS supports a broader and more secure set of cipher suites, with TLS 1.3 reducing the number of available cipher suites to only the most secure options.

### 6. Performance
**SSL:**
- SSL has higher overhead due to its more complex handshake and less efficient cryptography.

**TLS:**
- TLS offers better performance, especially with newer versions like TLS 1.3, which reduces latency and enhances speed.

### Summary:
- **SSL** is an older, less secure protocol that has been phased out in favor of TLS.
- **TLS:** is the modern standard for securing network communications, offering stronger security, better performance, and ongoing support.

## How the Communication Works and Types of Criptography?

When we talk about secure communication using protocols like SSL (Secure Sockets Layer) and TLS (Transport Layer Security), the process involves several steps and types of cryptography to ensure that data exchanged between a client (like a web browser) and a server remains private, intact, and authenticated. Here’s how the communication works and the types of cryptography involved:

### 1. TLS/SSL Handshake Process
The handshake is the initial phase where the client and server establish a secure communication channel. This involves:

**a. Client Hello**
- The client sends a "Client Hello" message to the server, which includes:
   - Supported versions of SSL/TLS.
   - A list of supported cipher suites (encryption algorithms).
   - A randomly generated number (nonce).
   - Any extensions that might be needed for additional features.

**b. Server Hello**
- The server responds with a "Server Hello" message, which includes:
   - The chosen SSL/TLS version.
   - The selected cipher suite from the list provided by the client.
   - A randomly generated number (nonce).
   - The server’s digital certificate (includes the server's public key) issued by a trusted Certificate Authority (CA).
   - If required, a request for the client’s certificate (in mutual authentication scenarios).

**c. Certificate Exchange and Authentication**
- The server sends its certificate to the client, which includes the server’s public key.
- The client verifies the server’s certificate using the Certificate Authority (CA) that issued it.
- If mutual authentication is required, the client sends its certificate to the server.

**d. Session Key Generation**
- The client generates a "pre-master secret" (a random number), encrypts it with the server’s public key (asymmetric encryption), and sends it to the server.
- Both the client and server use this pre-master secret, along with the two nonces exchanged earlier, to independently generate the same session key (symmetric encryption).

**e. Session Key Exchange**
- The session key, used for symmetric encryption, is now shared between the client and server.
- Both parties send a message to each other indicating that future messages will be encrypted with this session key.

**f. Secure Communication**
- From this point on, all communication between the client and server is encrypted with the session key using symmetric encryption. This ensures confidentiality and efficiency in data transfer.

### 2. Types of Cryptography Used
**a. Symmetric Encryption**
- **Definition:** Uses a single key for both encryption and decryption. The same key must be shared between the communicating parties.

- **Example Algorithms:** AES (Advanced Encryption Standard), DES (Data Encryption Standard), 3DES (Triple DES).

- **Use in TLS/SSL:** Symmetric encryption is used for encrypting the bulk of the data after the session key is established. It is faster and more efficient than asymmetric encryption for large amounts of data.

**b. Asymmetric Encryption**
- **Definition:** Uses a pair of keys—public and private keys. The public key is used for encryption, and the private key is used for decryption.

- **Example Algorithms:** RSA, ECC (Elliptic Curve Cryptography), DSA (Digital Signature Algorithm).

- **Use in TLS/SSL:** Asymmetric encryption is used during the handshake process to securely exchange the session key. The client encrypts the pre-master secret with the server’s public key, and only the server can decrypt it using its private key.

**c. Hash Functions**
- **Definition:** Hashing transforms data into a fixed-size string of characters, which is typically a digest that is unique to the input data.

- **Example Algorithms:** SHA-2 (Secure Hash Algorithm 2), SHA-3, MD5 (although MD5 is now considered insecure).

- **Use in TLS/SSL:** Hash functions are used to ensure data integrity. They create a unique fingerprint (hash) of the data that can be checked to detect any changes during transmission. TLS also uses HMAC (Hash-based Message Authentication Code) for authenticating messages.

**d. Digital Signatures**
- **Definition:** A digital signature is a cryptographic technique that verifies the authenticity and integrity of a message or document. It involves hashing the data and then encrypting the hash with the sender's private key.

- **Example Algorithms:** RSA, DSA, ECDSA.

- **Use in TLS/SSL:** Digital signatures are used in certificates to prove that the certificate was issued by a trusted Certificate Authority (CA) and that it hasn't been tampered with.

### 3. TLS/SSL Communication Workflow
To summarize the workflow:
- The client initiates a connection by sending a "Client Hello" to the server.
- The server responds with a "Server Hello" and sends its certificate containing its public key.
- The client verifies the server's certificate and generates a pre-master secret, encrypting it with the server’s public key.
- Both the client and server derive the session key from the pre-master secret and use it for symmetric encryption of subsequent communications.
- All data transmitted between the client and server is now encrypted, ensuring confidentiality, integrity, and authenticity.



