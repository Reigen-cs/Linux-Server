# Monitoring 101

- Module: **Linux Administration** 
- Competence: `is able to gather information about the state of a linux machine`
- Type of Challenge: `Consolidation`
- Duration: `2 day`
- Deadline: `08/10/2024`
- Participants: : `solo`

## The Mission

One of the most important responsibilities a system administrator or SOC analyst have is monitoring the systems he manages. Indeed it's one thing to set them up and install software on them, but then what!? Well the next step is ensuring that the machines you provisioned as well as the services you deployed on them remain **available**, **reliable** and **secure**!
This challenge is divided in two tasks, the first one having you **research how to monitor** a Linux system as well as **what to look for** when doing so. You will have to **take note** of all your findings in a text file (EX: _markdown_) while being as **exhaustive** as possible (_what to monitor_, _how to monitor it_, _commands used_, _..._). Try to answer, but **don't limit yourself to**, the questions below to guide you through 
the research process:

- What are the main area of concern when monitoring a system? (EX: _CPU load_, _disk usage_, ...)
  ``
  answer: Ram - Cpu load (usage, loade avrage,...) - Disk space - Bandwidth Usage - Connection Counts - packets losts - Zombie processes ( processes monitoring) - Response Time - Application performances (       
          Respons time, Error rates) - Security Monitoring ( Intrusion detection, Logs anlyses) - Themperature monitoring and hardware healt - Backups and recovery (status, restore tests) - Users activity (user 
          session, user behavious)
  ``
  
- How can you check what are the most memory intensive [running processes](https://www.computerhope.com/jargon/p/process.htm) ?
  ``
  answer: On Windows; Ctrl + Shift + esc. | For Powershell; lunch the commande "Get-Process | Sort-Object -Property WorkingSet -Descending | Select-Object -First 10"  it ists the top 10 processes by memory usage
          On linux; by using top, htop, ps ( ps aux --sort=-%mem | head -n 10) , smem (smem -r -k | sort -k 4 -nr | head -n 10)
  ``
- What are log files? Where can you fin them on a typical Linux system ?
  ``
  answer: Log files are files that record events, processes, and activities that occur within a system, application, or service. They are essential for monitoring, troubleshooting, and auditing purposes.
          You can find a variety of information as System Events (Information about system startup, shutdown, and errors), Application Logs (Details about application behavior, errors, and user interactions),
          Security Logs (Records of authentication attempts, access control, and security-related events), Network Logs (Information about network traffic, connections, and errors).
  ``

   For the interest i have in it, i will put all the commands that i find during my reseaches that could be useful to me for the nexte project.

  ``
  /var/log/syslog or /var/log/messages:General system log that records various system events, including kernel messages, system startup, and shutdown events.

  /var/log/auth.log or /var/log/secure:Contains authentication-related events, such as login attempts, sudo commands, and other security-related messages.

  /var/log/kern.log:Logs kernel messages, which can be useful for diagnosing hardware and driver issues.

  /var/log/dmesg:Contains messages from the kernel ring buffer, typically related to hardware and system boot processes.

  /var/log/boot.log:Records messages related to the boot process, including services that started successfully or failed to start.

  /var/log/httpd/ or /var/log/apache2/:Contains logs for the Apache web server, including access logs and error logs.

  /var/log/nginx/:Contains logs for the Nginx web server, including access logs and error logs.

  /var/log/mysql/ or /var/log/mariadb/:Contains logs for MySQL or MariaDB databases, including error logs and query logs.

  /var/log/cron.log: Records events related to scheduled tasks (cron jobs).

  /var/log/user.log: Contains user-level messages and events.
  ``
  
- How can you check who where the last connected users, what they did, when they left ?
  ``
  answer:
          Access to user login information on a Linux system is typically granted to:
          -Regular Users: Can view their own login history and currently logged-in users;
          -Root/Sudo Users: Have full access to all login information and logs;
          -Auditors/Security Personnel: May have access based on specific roles and permissions.
          Access can be regulated by assigning authorization privileges to the relevant individuals, ensuring that only authorized users can view sensitive login data.
  ``
- What are the different metrics of health and performance of a system ?
  ``
  answer:
  Of course! Here’s a summarized version of the key metrics to monitor for assessing the health and performance of a system, which could be useful for study purposes and future projects:

### 1. **CPU Metrics**
   - **CPU Utilization**: Measures CPU usage to avoid overload or underuse.
   - **Load Average**: Assesses average CPU load to detect spikes.
   - **Context Switches**: Counts task switches on the CPU; high numbers may indicate a need for optimization.

### 2. **Memory Metrics**
   - **Memory Usage**: Shows total, used, and free memory to manage system load.
   - **Swap Usage**: Indicates use of virtual memory, which could point to insufficient physical RAM.
   - **Cache Hit Ratio**: Measures the effectiveness of data retrieval from cache; higher is better.

### 3. **Disk and Storage Metrics**
   - **Disk Utilization**: Tracks used capacity to monitor remaining space.
   - **Disk Latency and Throughput**: Measures response time and data transfer speed, helping identify slowdowns.
   - **I/O Operations**: Counts read/write operations to spot potential disk bottlenecks.

### 4. **Network Metrics**
   - **Network Throughput and Latency**: Monitors data flow and travel time for network requests.
   - **Packet Loss and Error Rates**: Helps identify connectivity or hardware issues.

### 5. **Application Performance Metrics**
   - **Response Time and Throughput**: Key for evaluating user experience and request handling speed.
   - **Error Rate**: Tracks the frequency of application errors, indicating possible issues with stability.

### 6. **System Availability and Reliability Metrics**
   - **Uptime**: Shows how long the system has been continuously operational.
   - **MTBF and MTTR** (Mean Time Between Failures and Mean Time to Repair): Metrics for reliability and recovery time after failures.

     One ce again i put all the parameters to take into account that i could find in my reasearch.
     These metrics give a well-rounded view of system health and can help proactively maintain stability and efficiency, making them valuable for planning and optimizing systems in any project.
  ``
- How can you check the uptime of a machine ?
  ``
  answer: For linux; the command "uptime"  will display the current time, how long the machine has been running, the number of active users, and the system load averages.
                     the command "cat /proc/uptime" will show the total uptime (in seconds) and the time spent in idle mode. The first number is the uptime in seconds.
                     the command "who -b" will  displays the last time the system was booted, which helps determine how long it has been running since.
          For windows; the command "systeminfo" (systeminfo | find "System Boot Time) will show shows the last boot time of the machine.
                       the command "net stats srv" (net stats srv | find "Statistics since) will shows the time the server started collecting statistics, which correlates with system uptime.
                       by using powershell command "(Get-CimInstance -ClassName win32_operatingsystem).LastBootUpTime" it shows the last boot time, helping you calculate uptime.
         Each of these methods gives you a quick view of system uptime to assess reliability or troubleshoot issues.
  ``
- How can you assess the network traffic ?
  for thins question i must put all the info a find, the answer is so releveant and i thing it is important that i carefully keep everything i have found on this question.

  Assessing network traffic is essential for understanding network performance, identifying bottlenecks, ensuring security, and optimizing bandwidth usage. Here are several effective methods and tools to monitor and analyze network traffic:

### 1. **Using Built-in Command-Line Tools**

#### **Linux/Unix**
   - **`netstat`**: Displays network connections, routing tables, interface statistics, masquerade connections, and more. Example:
     ```bash
     netstat -i
     ```
   - **`iftop`**: Provides real-time bandwidth usage by interface and shows connections between local and remote hosts.
     ```bash
     iftop -i <interface>
     ```
   - **`tcpdump`**: Captures and analyzes packets on the network; useful for deep packet inspection.
     ```bash
     tcpdump -i <interface> -c <count>
     ```

#### **Windows**
   - **Resource Monitor**: Available in Task Manager, allows real-time monitoring of network traffic per application.
   - **PowerShell `Get-NetTCPConnection`**: Lists TCP connections, which can help in identifying active connections and traffic sources.
   - **`netstat`**: Also available on Windows, provides similar functionality as on Linux.

### 2. **Network Monitoring Tools**

   - **Wireshark**: A powerful packet analyzer that captures and inspects network packets in detail. It’s useful for troubleshooting, security analysis, and protocol understanding.
   - **Ntopng**: A high-performance web-based traffic monitoring application. It displays real-time network usage and provides detailed statistics on network protocols, hosts, and flows.
   - **SolarWinds Network Performance Monitor**: A comprehensive tool for monitoring network performance, alerting on issues, and providing detailed insights into bandwidth usage.
   - **Nagios**: Known for infrastructure monitoring, Nagios can track network performance by collecting data on bandwidth, latency, and packet loss.
   - **PRTG Network Monitor**: Offers detailed visualizations of network traffic, uptime, and server status, with customizable alerts.

### 3. **Protocol and Flow Analysis**

   - **NetFlow (Cisco)**, **sFlow (Standard)**, and **IPFIX**: These protocols export flow information from network devices to be analyzed. Flow-based tools such as **SolarWinds NetFlow Traffic Analyzer** or **Ntopng** can help identify top users, devices, and protocols by capturing flow data.

### 4. **Cloud and Web-Based Network Monitoring Services**
   
   - **AWS CloudWatch (for AWS networks)**, **Azure Network Watcher (for Azure)**, and **Google Cloud Operations**: These services provide traffic insights specifically for cloud-based network resources.
   - **ThousandEyes**: Offers insights into network performance across internet paths and can help troubleshoot issues across multi-cloud and on-premise environments.

### 5. **Bandwidth Monitoring**

   - **VNStat** (Linux): Tracks network bandwidth usage over time and provides historical data, making it useful for spotting trends.
   - **bmon** (Linux): Monitors bandwidth usage and visually displays network load in real time.
   - **NetWorx** (Windows/MacOS): Monitors bandwidth usage for each device, helping track per-application usage.

### 6. **SNMP Monitoring**
   
   - **SNMP (Simple Network Management Protocol)**: Enables monitoring of network devices like routers, switches, and firewalls. Tools like **Cacti** or **Zabbix** can collect SNMP data and provide graphs of network performance, including traffic, errors, and device health.

### 7. **Synthetic Testing and Probes**

   - **Ping and Traceroute**: Basic tools to test latency and reachability across network paths. They can help identify slow or failed paths in the network.
   - **Synthetic Transaction Monitoring**: Tools like **Pingdom** and **Catchpoint** create synthetic requests to simulate user behavior, testing response times and traffic handling capabilities.

### 8. **Logging and Anomaly Detection**

   - **SIEM Tools (e.g., Splunk, ELK Stack)**: These tools collect and analyze network logs to detect unusual traffic patterns, intrusions, or potential security threats.
   - **IDS/IPS (Intrusion Detection/Prevention Systems)**: Systems like **Snort** or **Suricata** can monitor for suspicious traffic patterns that might indicate security incidents.

### Summary

Using these methods together provides a comprehensive view of network traffic, letting you analyze both real-time and historical data, drill down into specific packets, and monitor performance across devices and applications.

``

The second task is meant to serve as practice and will have you, in a different file, **write a report** with as many relevant information (_what would make sense in a report_) as you can muster on a system you manage. It most preferably would be a remote machine, but it can also be your local machine as this is just practice.


> **IMPORTANT**: Take your time when researching, it's the most important part of this challenge as you'll need to be able to find out what is happening on any given system at any given time. Whether it's the percentage of system's resources currently used, what commands are being run, who is logged in, and so on...

## Complementary Resources

* [Useful monitoring commands](https://www.ubuntupit.com/most-comprehensive-list-of-linux-monitoring-tools-for-sysadmin/)
* [Linux system monitoring fundamentals](https://www.linode.com/docs/guides/linux-system-monitoring-fundamentals/)

## Final Words

There are plenty of tools out there but remember that collecting the metrics is only the first step towards an end goal, which is, to be able to keep track of the state of machines, troubleshoot them to understand errors and in the best cases prevent issues before they even happen!

One last thing, we cannot understate how **important**, even **crucial**, monitoring for servers, services and applications deployment.

<br>
<p align="center">
  <img src="https://c.tenor.com/FSFcij2DJkAAAAAC/watching-you-warning.gif" />
</p>
