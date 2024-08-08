# Authentication in IIS

Authentication in IIS is **the process of verifying the identity of users who access web applications or services.** IIS supports various authentication methods to ensure that only authorized users can access resources. Here’s an overview of the authentication options available in IIS:

## Authentication Methods

### 1. Anonymous Authentication
- **Description**: Allows users to access the web application without providing credentials.
- **Use Case**: Suitable for public websites where no user identification is required.

### 2. Basic Authentication
- **Description**: Requires users to provide a username and password to access the application. Credentials are sent in plain text (not encrypted).
- **Use Case**: Used when secure transport (e.g., HTTPS) is available, and simple authentication is sufficient, not encrypted.

### 3. Digest Authentication
- **Description**: Similar to Basic Authentication but uses a hashed password for authentication, improving security over Basic Authentication.
- **Use Case**: Used in environments where the transport layer security is not guaranteed but better security than Basic Authentication is needed, only with Active Directory Domains.

### 4. Windows Authentication
- **Description**: Leverages Windows credentials to authenticate users. Includes options for NTLM and Kerberos authentication.
- **Use Case**: Suitable for intranet applications where users are authenticated via Windows domains.

### 5. Forms Authentication
- **Description**: Uses custom web forms to authenticate users. Users provide credentials through a login form, and authentication is handled by ASP.NET.
- **Use Case**: Commonly used in ASP.NET applications for custom authentication schemes, need a Web.config file and configure the form authentication to check the login page.

### 6. Client Certificate Authentication
- **Description**: Requires users to present a client certificate for authentication. Certificates are issued and managed by a certificate authority.
- **Use Case**: Used for high-security applications where users must authenticate with a certificate.

## How to Configure Authentication

1. **Open IIS Manager**:
   - Click on the **Start** button, then select **IIS Manager**.

2. **Select Your Site or Application**:
   - Navigate to the site or application where you want to configure authentication.

3. **Open Authentication Settings**:
   - In the Features View, double-click on **Authentication**.

4. **Configure Authentication Methods**:
   - Select the authentication method you want to configure and choose **Enable** or **Disable** as needed.

5. **Apply Changes**:
   - Click **Apply** in the Actions pane to save your changes.

## Summary

IIS supports multiple authentication methods to secure access to web applications:

- **Anonymous Authentication**: No credentials required.
- **Basic Authentication**: Username and password (unencrypted).
- **Digest Authentication**: Hashed password for better security.
- **Windows Authentication**: Uses Windows credentials (NTLM/Kerberos).
- **Forms Authentication**: Custom login forms (configured in ASP.NET).
- **Client Certificate Authentication**: Requires a client certificate.

By configuring these authentication methods, you can control how users access your web applications and ensure appropriate security measures are in place.

## Notes

**#1:** Authentication vs. Authorization
- Authentication is the process of identifying thr user.
- Authorization is the process of giving each user his own roles and rights

**#2:** To use the real windows account we have to enable impersonation - Built-In Account (IUSR).

**#3:** You need to install the Authentication in Server Manager. 