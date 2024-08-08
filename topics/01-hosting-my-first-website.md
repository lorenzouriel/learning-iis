# Hosting My First Website

## Prerequisites

- A Windows server with IIS installed
- A basic understanding of HTML/CSS
- Your website files ready for deployment

## Steps to Host Your Website

### 1. Prepare Your Website Files

Make sure your website files (HTML, CSS, JavaScript, images, etc.) are organized and ready. Typically, you should have an `index.html` file as the main entry point of your website.

### 2. Open IIS Manager

- Click on the **Start** button, type **IIS Manager**, and open it.

### 3. Create a New Website

1. **Open IIS Manager**:
   - In the left-hand Connections pane, right-click on the **Sites** node.
   - Select **Add Website**.

2. **Site Information**:
   - **Site name**: Enter a name for your website.
   - **Physical path**: Browse to the folder where your website files are located.
   - **Binding**:
     - **Type**: Select `http`.
     - **IP address**: Select `All Unassigned` or specify an IP address.
     - **Port**: Enter `80` (default port for HTTP).
     - **Host name**: Enter your domain name (e.g., `www.example.com`).

3. **Configure Bindings**:
   - Click **OK** to create the website.

### 4. Configure Website Settings

1. **Application Pool**:
   - Ensure the website is using the appropriate application pool. By default, a new application pool is created with the same name as your website.
   - If needed, you can configure the application pool settings by selecting **Application Pools** in the left-hand Connections pane, right-clicking on your application pool, and selecting **Advanced Settings**.

2. **Authentication and Authorization**:
   - In the left-hand Connections pane, click on your website.
   - Under **IIS** in the middle pane, open **Authentication** to configure authentication settings.
   - Open **Authorization Rules** to configure access permissions.

### 5. Test Your Website

1. **Start the Website**:
   - In the left-hand Connections pane, right-click on your website and select **Manage Website > Start**.

2. **Verify Access**:
   - Open a web browser and navigate to `http://localhost` or `http://your-domain-name`.

### 6. DNS Configuration (if using a custom domain)

1. **Register Domain**:
   - If you haven't already, register a domain name through a domain registrar.

2. **DNS Settings**:
   - Log in to your domain registrar's website.
   - Update the DNS records to point to your server's IP address. Typically, you'll need to create an `A` record with your domain name pointing to your server's public IP address.

3. **Propagation**:
   - DNS changes can take some time to propagate. This process can take anywhere from a few minutes to 48 hours.
