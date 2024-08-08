# Performance Monitoring Counters

## Key Counters to Monitor in IIS

### Processor
- **Processor\% Processor Time**
  - Indicates the average percentage of processor time occupied.
  - >80% suggests high load on the server, possibly due to high website load or other applications.

- **System\Processor Queue Length**
  - Indicates threads waiting for processor time.
  - >2 suggests a bottleneck if % Processor Time is also high.

### Memory
- **Memory\Available Mbytes**
  - Amount of free physical memory.
  - >50%: Healthy, 25%: Potential problem, <5%: Performance impacted.

- **Memory\Pages/sec**
  - Amount of read/write requests from memory to disk.
  - > Less than 500 Pages/sec is normal.

### Disk
- **Physical Disk\% Disk Time**
  - Percentage of time the disk is occupied.
  - High values affect read/write performance.

### Network
- **Network Interface\Bytes Total/sec**
  - Total bytes sent and received over the network.
  - High values may require additional network cards or higher speed.

### System
- **System\Context Switches/sec**
  - Number of context switches per second.
  - >5000: High, >15,000: Very high.
  - Indicates too many threads competing for the processor.

### Web Service
- **Web Service\Bytes Total/sec**
  - Tracks potential spikes in traffic.

- **Web Service\Total Method Requests/sec**
  - Number of all HTTP requests since service startup.

- **Web Service\Current Connections**
  - Number of current connections established.

### ASP.NET Applications
- **ASP.NET Applications\Requests/Sec**
  - Throughput of the ASP.NET application.
  - High values suggest heavy application; monitor other counters.

- **ASP.NET\Application Restarts**
  - High values may indicate bugs in the application.

- **ASP.NET\Request Wait Time**
  - Time the last request was held in the queue.
  - >1000 ms indicates poor performance.

- **ASP.NET\Requests Queued**
  - Number of requests waiting to be processed.
  - Should be as low as 2-3 requests.

### .NET CLR
- **.NET CLR Exceptions\# of Exceps Thrown/sec**
  - Number of exceptions thrown per second.
  - High values suggest bugs and potential application pool reboots.

- **.NET CLR Memory\# Total Committed Bytes**
  - Amount of virtual memory reserved on the paging file.
  - Should be low and monitored with other factors.

### Additional Counter
- **Web Service\Get Requests/sec**
  - Number of GET requests processed per second.
  - High values may require load balancing or clustering.

There are many more counters for detailed analysis. For specifics on a certain counter, feel free to contact me for help.


## Performance Opmization Tips

1. Disable logging for IIS or configure very well.
2. Disable Debugging.
3. Optimize the number of threads per processor: `Threade Per Processor Limit`.
4. HTTP compression, will increase CPU and low performance.
5. Use Output Caching, this allow you to store your data or your page to memory.