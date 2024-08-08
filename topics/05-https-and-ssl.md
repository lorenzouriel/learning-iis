# HTTPS and SSL Certificates

**HTTPS (Hypertext Transfer Protocol Secure)** is an extension of HTTP that provides a secure communication channel over a computer network. It ensures data integrity, confidentiality, and authentication through encryption using SSL/TLS protocols. Here’s an overview of how HTTPS works and how to configure SSL certificates in IIS:

## What is HTTPS?

- **Description**: HTTPS uses encryption to secure the data transmitted between a web server and a client (e.g., a web browser). It combines HTTP with SSL/TLS protocols to protect data from eavesdropping, tampering, and forgery.
- **Port**: HTTPS typically operates over port 443.

## What is SSL/TLS?

- **SSL (Secure Sockets Layer)**: The original protocol for establishing a secure connection. It has been deprecated in favor of TLS.
- **TLS (Transport Layer Security)**: The modern protocol that replaced SSL. It provides improved security and is the standard for HTTPS.

## How to Install and Configure SSL Certificates in IIS

### 1. Obtain an SSL Certificate

- **Description**: An SSL certificate is a digital certificate issued by a Certificate Authority (CA) that verifies the identity of your website and enables encryption.
- **Steps to Obtain**:
  - **Generate a CSR (Certificate Signing Request)**: Use IIS Manager or OpenSSL to generate a CSR.
  - **Submit the CSR**: Provide the CSR to a CA to obtain the SSL certificate.
  - **Receive the Certificate**: Download the SSL certificate from the CA.

### 2. Install the SSL Certificate

1. **Open IIS Manager**:
   - Click on the **Start** button, then select **IIS Manager**.

2. **Select Your Server**:
   - In the Connections pane, select the server node where you want to install the certificate.

3. **Open Server Certificates**:
   - In the Features View, double-click on **Server Certificates**.

4. **Complete Certificate Request**:
   - In the Actions pane, click on **Complete Certificate Request**.
   - Provide the certificate file, a friendly name, and the certificate store (usually Personal).

5. **Install the Certificate**:
   - Click **OK** to install the certificate.

### 3. Bind the SSL Certificate to Your Website

1. **Select Your Site**:
   - In the Connections pane, expand the server node and select the site you want to configure.

2. **Open Bindings**:
   - In the Actions pane, click on **Bindings**.

3. **Add HTTPS Binding**:
   - Click **Add** to create a new binding.
   - Set the type to **https**, select the installed SSL certificate from the dropdown menu, and set the port (usually 443).

4. **Configure Binding**:
   - Click **OK** to apply the binding.

### 4. Verify SSL Configuration

1. **Open a Web Browser**:
   - Navigate to your website using `https://` to check if the SSL certificate is working correctly.

2. **Check the Certificate**:
   - Click on the padlock icon in the address bar to view certificate details and verify its validity.

## SSL Certificates Types

- **Domain Verified (DV)**: Basic validation for domain ownership.
- **Organizational Verified (OV)**: Moderate validation for business legitimacy.
- **Enterprise Verified (EV)**: Extensive validation for maximum trust.
- **Wildcard Certificates**: Secure a domain and its subdomains.
- **Multi-Domain (SAN)**: Secure multiple domains with one certificate.
- **UCC Certificates**: Designed for Microsoft environments, can cover multiple domains and services.

## Notes

**#1:** The certificate needs to be purchased and validated for an organization.