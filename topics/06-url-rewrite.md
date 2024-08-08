# URL Rewrite

**URL Rewrite** is a powerful module in IIS (Internet Information Services) that allows web administrators to define rules for modifying URL requests. This module is essential for managing URLs, enhancing SEO, creating user-friendly URLs, and ensuring backward compatibility. Here's a comprehensive guide on URL Rewrite in IIS:

## What is URL Rewrite?

- **Description**: URL Rewrite allows the rewriting of URLs based on specific rules and conditions. It helps in transforming URLs into a more user-friendly format and routing requests to different resources.
- **Use Cases**: 
  - Simplifying complex URLs.
  - Redirecting old URLs to new ones.
  - Enforcing URL consistency.
  - Enhancing SEO by creating clean, readable URLs.

## Key Features

- **Pattern Matching**: Uses regular expressions to match URL patterns.
- **Conditions**: Applies additional criteria to the rewrite rules, such as checking server variables, headers, or query strings.
- **Rewrite vs. Redirect**:
  - **Rewrite**: Changes the URL before the request is processed by the server.
  - **Redirect**: Instructs the client to request a different URL.
- **Lower Case:** You can lower case all your URLs.
- **Non www to www:** You can redirect the URL without www to www.
- **Remove aspx Extension:** To prevent something to attack your code, you can remove the aspx extension and others files extensions from your URL.
- **HTTP Requests to HTTPS:** You can add a rule to redirect URLs with HTTP to HTTPS.
- **Redirect for a Maintenance Page:** You can add a rule to redirect to a error 503, going to maintenance page.

## How to Configure URL Rewrite in IIS

### 1. Installing URL Rewrite Module

1. **Download the Module**:
   - Visit the [IIS URL Rewrite Module page](https://www.iis.net/downloads/microsoft/url-rewrite) and download the module.

2. **Install the Module**:
   - Run the installer and follow the prompts to complete the installation.

### 2. Creating Rewrite Rules

1. **Open IIS Manager**:
   - Click on the **Start** button, then select **IIS Manager**.

2. **Select Your Site**:
   - In the Connections pane, expand the server node and select the site you want to configure.

3. **Open URL Rewrite**:
   - In the Features View, double-click on **URL Rewrite**.

4. **Add a New Rule**:
   - In the Actions pane, click **Add Rule(s)**.

5. **Select Rule Type**:
   - Choose the appropriate rule template (e.g., **Blank rule**, **Canonical domain name**, **Redirect to HTTPS**).

### 3. Configuring a Rewrite Rule

1. **Name the Rule**:
   - Provide a meaningful name for the rule.

2. **Pattern Matching**:
   - Define the URL pattern to match using regular expressions.
   - Example: `^old-page/(.*)$` to match URLs starting with `old-page`.

3. **Define Conditions (Optional)**:
   - Add conditions to refine when the rule should be applied.
   - Example: `{HTTP_HOST}` matches `www.example.com`.

4. **Action Type**:
   - Choose the action to be taken (e.g., **Rewrite**, **Redirect**, **Abort Request**, **Custom Response**).
   - Example: **Redirect** to `new-page/{R:1}`.

5. **Apply Changes**:
   - Click **Apply** in the Actions pane to save the rule.

### 4. Testing and Verifying Rules

1. **Test the Rule**:
   - Use the **Test Pattern** feature in the URL Rewrite module to test your pattern matching and conditions.

2. **Verify in Browser**:
   - Open a web browser and navigate to the URL to ensure the rewrite or redirect works as expected.

## Example: Redirecting HTTP to HTTPS

Here’s an example of a rule that redirects all HTTP requests to HTTPS:

1. **Add a Blank Rule**.
2. **Name the Rule**: `Redirect to HTTPS`.
3. **Pattern Matching**:
   - Match URL: `.*` (matches all URLs).
4. **Conditions**:
   - Add Condition: `{HTTPS}` does not match `on`.
5. **Action**:
   - Action Type: **Redirect**.
   - Redirect URL: `https://{HTTP_HOST}{REQUEST_URI}`.
   - Redirect Type: **Permanent (301)**.
6. **Apply Changes**.

## Summary

**URL Rewrite** in IIS provides robust capabilities to modify URL requests, enhance SEO, and improve user experience:

- **Pattern Matching**: Uses regular expressions to define URL patterns.
- **Conditions**: Adds criteria for applying rules.
- **Rewrite vs. Redirect**: Changes URL internally vs. instructs client to use a new URL.

By leveraging URL Rewrite, administrators can efficiently manage URLs, enforce security protocols, and ensure backward compatibility for web applications.
