# Start With IIS
IIS (Internet Information Services) **is a flexible, secure, and manageable web server for hosting websites, services, and applications.** Developed by Microsoft, it runs on Windows and supports HTTP, HTTPS, FTP, FTPS, SMTP, and NNTP. IIS is **widely used for hosting websites and web applications on Windows servers.**

## How IIS Works

### Architecture and Components

**Kernel Mode:**
- HTTP.sys: The kernel-mode driver responsible for handling HTTP requests. It listens for HTTP requests and routes them to the appropriate worker process.

**User Mode:**
- Windows Process Activation Service (WAS): Manages the lifecycle of application pools and worker processes.
- Worker Process (w3wp.exe): Handles requests assigned to it by HTTP.sys. Each application pool has its own worker process.

**Application Pools:**
- Isolate applications for better security, reliability, and availability.
- Each pool runs one or more worker processes.
- Configurable to recycle worker processes, limit resource usage, and more.

**Modules:**
- Native Modules: Implement core server functionality (e.g., authentication, logging).
- Managed Modules: Written using .NET and can handle request processing.

### Request Processing Flow

1. **Request Reception**:
   - HTTP.sys receives the request and checks the routing rules to determine the appropriate application pool.

2. **Routing**:
   - HTTP.sys forwards the request to the WAS.

3. **Worker Process Activation**:
   - WAS checks if a worker process for the application pool is already running. If not, it starts one.
   - The worker process (w3wp.exe) begins handling the request.

4. **Request Handling**:
   - The request passes through various IIS modules for processing (e.g., authentication, authorization, URL rewriting).
   - If using ASP.NET, the request is further processed by the ASP.NET runtime.

5. **Response Generation**:
   - The worker process generates the response and sends it back to HTTP.sys.
   - HTTP.sys sends the response to the client.

### Key Features

- **Security**: Supports various authentication methods (Basic, Digest, Windows, etc.), TLS/SSL, IP restrictions, and more.
- **Performance**: Kernel-mode caching, request queueing, process recycling, and more.
- **Scalability**: Supports load balancing, clustering, and multiple server configurations.
- **Manageability**: GUI-based management via IIS Manager, scripting with PowerShell, and configuration through XML files.

## Difference Between Windows Server vs. Windows Server Core

### Windows Server

**Windows Server** is a full-featured version of Microsoft's server operating system that includes a graphical user interface (GUI). It is designed for enterprises of all sizes and includes a broad range of features and functionalities, such as:

- **GUI**: Provides a full desktop environment, similar to Windows client operating systems.
- **Management Tools**: Includes a wide array of graphical tools for system administration, such as Server Manager, MMC snap-ins, and other GUI-based tools.
- **Application Compatibility**: Supports a broad range of applications, particularly those that require a GUI.
- **Ease of Use**: The graphical interface makes it easier to manage and configure the server, particularly for administrators who are more comfortable with a GUI.

### Windows Server Core

**Windows Server Core** is a minimal installation option for Windows Server, offering a more lightweight and streamlined version without a GUI. It is designed for experienced administrators who are comfortable managing servers using command-line tools and PowerShell. Key characteristics include:

- **No GUI**: Only provides a command-line interface (CLI), reducing the overhead and resource consumption associated with the GUI.
- **Reduced Attack Surface**: With fewer components installed, there are fewer potential attack vectors, enhancing security.
- **Lower Resource Usage**: Consumes fewer system resources (CPU, memory, disk space), leading to better performance and efficiency.
- **Remote Management**: Often managed remotely using tools like PowerShell, Windows Admin Center, or Remote Server Administration Tools (RSAT).

## How To Install IIS in Windows Server and Windows Server Core

### Installing IIS on Windows Server (with GUI)

1. **Open Server Manager**:
   - Click on the **Start** button, then select **Server Manager**.

2. **Add Roles and Features**:
   - In the Server Manager Dashboard, click on **Add roles and features**.

3. **Role-Based or Feature-Based Installation**:
   - In the **Add Roles and Features Wizard**, select **Role-based or feature-based installation** and click **Next**.

4. **Select Destination Server**:
   - Choose the server on which you want to install IIS and click **Next**.

5. **Select Server Roles**:
   - In the **Select server roles** section, check the box for **Web Server (IIS)**. A dialog box will appear to add required features. Click **Add Features**, then click **Next**.

6. **Select Features**:
   - You can choose additional features if needed, but for a basic installation, click **Next**.

7. **Web Server Role (IIS)**:
   - Review the information about the Web Server role, then click **Next**.

8. **Select Role Services**:
   - Choose the role services you want to install. For a basic installation, the default selections are sufficient. Click **Next**.

9. **Confirm Installation Selections**:
   - Review your selections and click **Install**.

10. **Installation Progress**:
    - The installation process will begin. Once completed, click **Close**.

### Installing IIS on Windows Server Core

1. **Open Command Prompt or PowerShell**:
   - You can use either the Command Prompt or PowerShell to install IIS on Windows Server Core.

2. **Install IIS using DISM**:
   - Open Command Prompt and run the following command:
     ```bash
     dism /online /enable-feature /featurename:IIS-WebServerRole /all
     ```
   - This command enables the Web Server role and all required features.

3. **Install IIS using PowerShell**:
   - Open PowerShell and run the following command:
     ```powershell
     Install-WindowsFeature -name Web-Server -IncludeManagementTools
     ```
   - This command installs the Web Server (IIS) role and includes management tools.

4. **Verify Installation**:
   - To verify the installation, run the following command in PowerShell:
     ```powershell
     Get-WindowsFeature -name Web-Server
     ```
   - The output should indicate that the Web Server role is installed.

## Post-Installation Steps

1. **Open IIS Manager** (for Windows Server with GUI):
   - Click on the **Start** button, type **IIS Manager**, and open it to manage your IIS server.

2. **Configure IIS**:
   - Set up your websites, application pools, and other settings as needed.

3. **Verify IIS Installation**:
   - Open a web browser and navigate to `http://localhost` to see the default IIS welcome page.

By following these steps, you can successfully install IIS on both Windows Server and Windows Server Core.
