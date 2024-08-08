# Application Pools

Application Pools in IIS (Internet Information Services) are a fundamental feature that **provides a way to isolate and manage web applications.** Each application pool runs its **own set of worker processes (w3wp.exe)**, ensuring that the applications within it do not affect applications in other pools. This isolation enhances security, reliability, and performance.

*You can think Application Pools is the container where the website will executed and be processed in.*


## Key Features of Application Pools

1. **Isolation**:
   - **Process Isolation**: Applications running in different application pools are isolated from each other. If an application in one pool crashes, it doesn't affect applications in other pools.
   - **Security Isolation**: Application pools can run under different user identities, providing security boundaries between applications.

2. **Performance**:
   - **Resource Management**: Each application pool can have its own settings for CPU, memory usage, and other resources.
   - **Process Recycling**: Application pools can be configured to recycle worker processes periodically or based on specific conditions (e.g., memory usage limits), helping to maintain optimal performance.

3. **Reliability**:
   - **Health Monitoring**: IIS can monitor the health of worker processes and automatically restart them if they become unresponsive or crash.
   - **Rapid-Fail Protection**: Limits the number of times a worker process can fail within a specified period, preventing continuous restarts.

4. **Scalability**:
   - Multiple application pools can be created to distribute the load across different processes, improving the scalability of web applications.

## How to Configure Application Pools in IIS

### Using IIS Manager (GUI)

1. **Open IIS Manager**:
   - Click on the **Start** button, type **IIS Manager**, and open it.

2. **Application Pools**:
   - In the left-hand Connections pane, click on the **Application Pools** node.

3. **Add Application Pool**:
   - In the right-hand Actions pane, click on **Add Application Pool**.
   - Enter a name for the new application pool.
   - Select the .NET CLR version if needed (e.g., .NET CLR Version v4.0).

4. **Configure Application Pool Settings**:
   - Click **OK** to create the new application pool.

5. **Application Pool Settings**:
   - Select the newly created application pool from the list.
   - In the right-hand Actions pane, click on **Advanced Settings** to configure various settings, such as the identity, recycling settings, and process model.

### Using PowerShell

You can also manage application pools using PowerShell, which is particularly useful for automation and scripting.

#### Create a New Application Pool
```powershell
Import-Module WebAdministration
New-Item IIS:\AppPools\MyNewAppPool
```

#### Configure Application Pool Settings
```powershell
Set-ItemProperty IIS:\AppPools\MyNewAppPool -Name processModel.identityType -Value "NetworkService"
```

#### Remove an Application Pool
```powershell
Remove-Item IIS:\AppPools\MyOldAppPool
```

## Use Cases for Application Pools
- **Hosting Multiple Applications:** You can host multiple web applications on the same server while ensuring they run independently.
- **Improving Security:** By running applications in separate pools with different identities, you can limit the impact of a security breach.
- **Enhancing Performance and Reliability:** Process recycling and health monitoring help maintain the performance and reliability of web applications.
- **Resource Management:** Application pools allow you to allocate and manage resources for different applications more effectively.

## Advanced Settings of Application Pools

### General Settings

#### .NET CLR Version
- **Description**: Specifies the version of the .NET Common Language Runtime (CLR) used by the application pool.
- **Options**: v2.0, v4.0, No Managed Code (for non-ASP.NET applications).

#### Enable 32-Bit Applications
- **Description**: Allows 32-bit applications to run on a 64-bit server.
- **Default**: False.

#### Managed Pipeline Mode
- **Description**: Determines the pipeline mode used for processing requests.
- **Options**: 
  - **Classic**: Uses the traditional IIS and ASP.NET separation.
  - **Integrated**: Combines IIS and ASP.NET into a single, unified pipeline for processing requests.

#### Name
- **Description**: The name of the application pool. This is a unique identifier used to manage and configure the application pool.
- **Usage**: Used for identifying and selecting the application pool in IIS Manager or through scripting.

#### Queue Length
- **Description**: Specifies the maximum number of requests that can be queued for the application pool. Requests that exceed this limit are rejected until space becomes available.
- **Default**: 1000 requests.
- **Usage**: Helps manage and control how many incoming requests are handled before they are queued.

#### Start Mode
- **Description**: Determines how and when the application pool is started.
- **Options**:
  - **AlwaysRunning**: The application pool starts when IIS starts and remains running, regardless of whether there are active requests.
  - **OnDemand**: The application pool starts only when there is a request for it. It shuts down after a period of inactivity.

### Process Model

#### Identity
- **Description**: Defines the user account under which the application pool runs.
- **Options**: NetworkService, LocalSystem, LocalService, ApplicationPoolIdentity, or a custom user account.

#### Idle Time-out (minutes)
- **Description**: Specifies the time, in minutes, that a worker process will remain idle before it is shut down.
- **Default**: 20 minutes.

#### Load User Profile
- **Description**: Indicates whether the user profile for the application pool identity should be loaded.
- **Default**: False.

#### Maximum Worker Processes
- **Description**: Sets the maximum number of worker processes that can be used for the application pool. A value greater than 1 indicates a web garden.
- **Default**: 1.

#### Ping Enabled
- **Description**: Determines whether IIS pings the worker process to check its health.
- **Default**: True.

#### Ping Maximum Response Time (seconds)
- **Description**: Specifies the maximum time, in seconds, that a worker process can take to respond to a ping.
- **Default**: 90 seconds.

#### Ping Period (seconds)
- **Description**: Sets the interval, in seconds, between pings sent to the worker process.
- **Default**: 30 seconds.

### Recycling

#### Regular Time Interval (minutes)
- **Description**: Specifies the regular time interval, in minutes, for recycling the worker process.
- **Default**: 1740 minutes (29 hours).

#### Specific Times
- **Description**: Allows you to specify exact times at which the worker process should be recycled.

#### Requests Limit
- **Description**: Defines the maximum number of requests that the worker process can handle before it is recycled.
- **Default**: 0 (no limit).

#### Virtual Memory Limit (KB)
- **Description**: Sets the virtual memory threshold, in kilobytes, for recycling the worker process.
- **Default**: 0 (no limit).

#### Private Memory Limit (KB)
- **Description**: Defines the private memory threshold, in kilobytes, for recycling the worker process.
- **Default**: 0 (no limit).

### Rapid-Fail Protection

#### Enabled
- **Description**: Determines whether rapid-fail protection is enabled. This helps prevent the application pool from failing continuously by automatically stopping it.
- **Default**: True.

#### Failures
- **Description**: Specifies the maximum number of failures allowed within the time interval.
- **Default**: 5.

#### Time Interval (minutes)
- **Description**: Defines the time interval, in minutes, for tracking failures.
- **Default**: 5 minutes.

#### Auto-Shutdown Exe
- **Description**: Specifies the executable to run when the application pool is shut down due to rapid-fail protection.

#### Auto-Shutdown Params
- **Description**: Defines the parameters for the auto-shutdown executable.

### CPU

#### Limit
- **Description**: Sets the maximum CPU usage, as a percentage, allowed for the application pool.
- **Default**: 0 (no limit).

#### Limit Action
- **Description**: Specifies the action to take when the CPU usage limit is reached.
- **Options**: NoAction, Throttle, ThrottleUnderLoad, KillW3wp.

#### Limit Interval (minutes)
- **Description**: Defines the interval, in minutes, for monitoring CPU usage.
- **Default**: 5 minutes.

#### Processor Affinity Mask
- **Description**: Sets the processor affinity mask, which binds the worker process to specific CPUs.
- **Default**: 0 (no affinity).

#### Processor Affinity Enabled
- **Description**: Indicates whether processor affinity is enabled.
- **Default**: False.

### Process Orphaning

#### Orphan Action Exe
- **Description**: Specifies the executable to run when a worker process is orphaned.
- **Usage**: This can be used to run diagnostic tools or custom scripts to log information about the orphaned process.

#### Orphan Action Params
- **Description**: Defines the parameters for the orphan action executable.

#### Orphan Worker Process
- **Description**: Indicates whether to enable orphaning of worker processes. When enabled, IIS will not terminate the worker process immediately upon failure but will instead mark it as orphaned and execute the specified orphan action.
- **Default**: False.

## Notes

**#1:** When usign Aplication Pools, try to ensure tht you are using a less privilege account (ApplicationPoolIdentity), is a good security practice to prevent users from hacking your system if you applicaation has a certain bug.

**#2:** When two or more websites are on the same application pool, whatever happens on the application pool, will reflect in all websites.

**#3:** The key difference between Classic and Integrated in Managed Pipeline Mode is:
- Classic mode: Your application will run in one container and your application pool will run in another one.

- Integrated Mode: Everything will run in one container, more performance.

**#4:** If you want to change the application pools defaults you can go to Application Pools > Set Application Pool Defaults.