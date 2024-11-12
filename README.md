# Analyzing-Network-Layer-Communication
### Analysis of DNS and ICMP traffic 

You are a cybersecurity analyst working at a company that specializes in providing IT services for clients. Several customers of clients reported that they were not able to access the client company website www.yummyrecipesforme.com, and saw the error “destination port unreachable” after waiting for the page to load. 

You are tasked with analyzing the situation and determining which network protocol was affected during this incident. To start, you attempt to visit the website and you also receive the error “destination port unreachable.” To troubleshoot the issue, you load your network analyzer tool, tcpdump, and attempt to load the webpage again. To load the webpage, your browser sends a query to a DNS server via the UDP protocol to retrieve the IP address for the website's domain name; this is part of the DNS protocol. Your browser then uses this IP address as the destination IP for sending an HTTPS request to the web server to display the webpage  The analyzer shows that when you send UDP packets to the DNS server, you receive ICMP packets containing the error message: “udp port 53 unreachable.” 

13:24:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24) 
13:24:36.098564 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 254 

13:26:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24) 
13:27:15.934126 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 320 

13:28:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24) 
13:28:50.022967 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 150

------------------------


### Summary of the Problem in the DNS and ICMP Traffic Log


The UDP protocol reveals that: The DNS query sent to resolve the domain name "www.yummyrecipesforme.com" via UDP could not be completed because the destination port was unreachable.

● Based on the results of the network analysis, which show that: The ICMP packets contain error messages indicating that the UDP packets sent to port 53 are not being delivered.

● The ICMP echo reply returned the error message: “udp port 53 unreachable”

● The port noted in the error message is used for: DNS service (Port 53 is the standard port for DNS queries using the UDP protocol).

● The most likely issue is: The DNS server is not reachable on port 53, which could be due to the DNS server being down, a misconfiguration, or a firewall blocking the traffic.

------------------------

### Incident Analysis and Explanation

Time Incident Occurred: The incident occurred on 13:24:32.192571 (1:24 PM), as indicated by the first timestamp in the tcpdump log.

How the IT Team Became Aware of the Incident: The IT team became aware of the incident after several customers reported that they were unable to access the client company website www.yummyrecipesforme.com and received the error message “destination port unreachable.”

### Actions Taken by the IT Department to Investigate the Incident:

1. The IT department attempted to visit the website and confirmed that the same error message was received.

2. They loaded the network analyzer tool, tcpdump, to capture and analyze the network traffic while attempting to load the webpage.

### Key Findings of the IT Department's Investigation:

1. Network Traffic Analysis: The tcpdump log showed DNS queries sent to the DNS server via UDP protocol and subsequent ICMP error messages indicating that the DNS server's port 53 was unreachable.

2. Error Messages: The error message “udp port 53 unreachable” was observed multiple times, indicating a consistent issue with reaching the DNS server's port 53.

3. Traffic Patterns: Multiple attempts to resolve the domain name using the UDP protocol resulted in ICMP error responses, suggesting a persistent problem with DNS resolution.

### Likely Cause of the Incident: 
The likely cause of the incident is that the DNS server's port 53 is not reachable, which could be due to:

- The DNS server being down or unresponsive.

- Misconfiguration of the DNS server.

- A firewall or network ACL blocking UDP traffic on port 53.

Summary:
The issue stems from the DNS protocol using UDP on port 53. The network traffic analysis reveals that ICMP error messages consistently indicate that the DNS server's port 53 is unreachable, preventing DNS resolution and causing the website to be inaccessible.

------------------------

### tcpdump Log Analysis Summary

### Protocols Used for Network Traffic:

● UDP (User Datagram Protocol): Used for DNS queries.

● ICMP (Internet Control Message Protocol): Used for error messages indicating the issue.

### Details Indicated in the Log:

1. DNS Queries Sent via UDP:

   - The queries were sent to resolve the domain name "yummyrecipesforme.com".

   - Example log entry: 13:24:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)

2. ICMP Error Responses:

   - The responses indicated that the DNS server's port 53 was unreachable.

   - Example log entry: 13:24:36.098564 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 254

### Trends in the Data:

● Repeated Errors: The error message “udp port 53 unreachable” was consistently returned for each DNS query attempt, indicating a persistent issue with the DNS server's availability on port 53.

● Timestamps: The errors occurred repeatedly over a period of time, showing that the issue was not intermittent but continuous.

### Issues Found in the Log:

● DNS Resolution Failure: The DNS server was not reachable on port 53, preventing the resolution of the domain name "yummyrecipesforme.com".

● Consistent ICMP Errors: The consistent ICMP error messages suggest a network or configuration issue with the DNS server or its accessibility.

### Interpretation of Issues:

● Unreachable DNS Server: The primary issue is that the DNS server is not accessible on port 53. This could be due to the server being down, a misconfiguration, or a network-level block (such as a firewall) preventing UDP traffic from reaching port 53.

### Cybersecurity Incident Report (Part One)

Summary of the Problem: The problem lies in the DNS resolution process using the UDP protocol on port 53. The DNS server for the domain "yummyrecipesforme.com" is unreachable, resulting in ICMP error messages indicating that port 53 is not accessible.

Analysis of the Data: The tcpdump log shows repeated attempts to send DNS queries to the server, all resulting in ICMP error messages. This indicates a persistent issue with the DNS server's availability on port 53.

Likely Cause of the Incident: The likely cause is that the DNS server's port 53 is either blocked, the server is down, or there is a network configuration issue preventing access to the port.

### Next Steps:
1. Verify DNS Server Accessibility: Check if the DNS server is operational and reachable.

2. Firewall Configuration Check: Ensure that no firewall or ACL is blocking UDP traffic on port 53.

3. DNS Server Configuration: Verify that the DNS server is correctly configured to respond to queries on port 53.

Suspected Root Cause:
The suspected root cause is the inaccessibility of the DNS server on port 53, potentially due to a server outage, misconfiguration, or network-level block.

------------------------

### Cybersecurity Incident Report (Part Two)

When the Problem Was First Reported: The problem was first reported at 13:24:32.192571 (1:24 PM) when customers were unable to access the client company website www.yummyrecipesforme.com and encountered the error “destination port unreachable.”

Scenario, Events, and Symptoms Identified: Several customers reported that they could not access the website and saw the error message “destination port unreachable.” Upon attempting to visit the website yourself, you received the same error. Using the network analyzer tool, tcpdump, you attempted to load the webpage again and noticed that the browser sent a query to the DNS server via the UDP protocol to retrieve the IP address, but you received ICMP error messages.

Current Status of the Issue: The issue is still ongoing. The DNS server's port 53 is unreachable, preventing DNS resolution and causing the website to be inaccessible.

### Information Discovered During Investigation:

1. Traffic Analysis: The tcpdump log revealed that DNS queries sent via UDP to the DNS server failed. The ICMP error messages indicated that the DNS server's port 53 was unreachable.

2. Repeated ICMP Errors: The log showed consistent ICMP error messages for each DNS query attempt, suggesting a persistent issue with the DNS server's availability on port 53.

3. Protocols Involved: The UDP protocol was used for DNS queries, and the ICMP protocol was used for error messages.

### Next Steps in Troubleshooting and Resolving the Issue:

1. Verify DNS Server: Check if the DNS server is operational and reachable.

2. Firewall Configuration Check: Ensure that no firewall or ACL is blocking UDP traffic on port 53.

3. Network Configuration Review: Verify the network configuration to ensure correct routing and accessibility of the DNS server.

4. Server Configuration: Confirm that the DNS server is correctly configured to respond to queries on port 53.

Suspected Root Cause of the Problem: The suspected root cause of the problem is that the DNS server's port 53 is either blocked, the server is down, or there is a misconfiguration preventing access to the port.

Solution to Implement: To resolve the issue, the following steps should be taken:

1. DNS Server Check: Verify the operational status of the DNS server.

2. Firewall Rules Update: Ensure that firewall rules allow UDP traffic on port 53.

3. DNS Configuration Verification: Confirm the DNS server is correctly configured to respond to queries on port 53.

4. Network Infrastructure Review: Inspect the network infrastructure for any issues that may be blocking or misrouting the DNS traffic.
