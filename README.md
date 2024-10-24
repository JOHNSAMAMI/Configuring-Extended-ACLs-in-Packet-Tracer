# Configuring-Extended-ACLs-in-Packet-Tracer

Project Overview
This project involved configuring extended Access Control Lists (ACLs) on Cisco routers to manage traffic between different devices within a network. The primary focus was on allowing specific access to a server for two employees with different access requirements.
Business Understanding
Effective network security requires controlling which devices can access specific services. By implementing ACLs, organizations can ensure that only authorized users can reach critical services, such as FTP and web applications, thereby minimizing security risks and optimizing network performance.
Tools and Frameworks Used
•	Packet Tracer: A network simulation tool for configuring and testing Cisco routers.
•	Cisco IOS Commands: Utilized for executing configurations on routers.
Project Description
The project was structured into two main parts: configuring a numbered extended ACL and a named extended ACL. Below is a detailed breakdown of the configurations performed:
Topology and Addressing Table:
•	Configured Router R1 with multiple interfaces to connect to PC1, PC2, and a server, with specific IP addresses for each device to ensure proper communication.
Objectives and Configuration Steps:
Part 1: Configure, Apply, and Verify an Extended Numbered ACL
1.	Configure ACL for FTP and ICMP Access:
o	Created an extended numbered ACL (100) on R1 to permit FTP and ICMP traffic from PC1 to the server.
o	Used commands to permit TCP traffic specifically for FTP and ICMP traffic, applying appropriate source and destination addresses along with wildcard masks.
Example ACL Configuration:
R1(config)# access-list 100 permit tcp 172.22.34.64 0.0.0.31 host 172.22.34.62 eq ftp
R1(config)# access-list 100 permit icmp 172.22.34.64 0.0.0.31 host 172.22.34.62

2.	Apply the ACL to the Interface:
•	Applied the ACL to the inbound traffic on the Gigabit Ethernet 0/0 interface of R1.
Command:
R1(config)# interface gigabitEthernet 0/0
R1(config-if)# ip access-group 100 in
3.	Verify Implementation:
o	Tested connectivity by pinging the server from PC1 and performing an FTP transfer. Ensured that PC1 could ping PC2 but could not establish a connection, confirming proper ACL enforcement.
Part 2: Configure, Apply, and Verify an Extended Named ACL
1.	Configure Named ACL for HTTP and ICMP Access:
o	Created an extended named ACL (HTTP_ONLY) to permit HTTP and ICMP traffic from PC2 to the server.
o	Specified TCP access for HTTP and ICMP in the named ACL configuration mode.
Example Named ACL Configuration:
R1(config)# ip access-list extended HTTP_ONLY
R1(config-ext-nacl)# permit tcp 172.22.34.96 0.0.0.15 host 172.22.34.62 eq www
R1(config-ext-nacl)# permit icmp 172.22.34.96 0.0.0.15 host 172.22.34.62
Apply the Named ACL to the Interface:
2.	Applied the named ACL to the inbound traffic on the Gigabit Ethernet 0/1 interface of R1.
Command:
R1(config)# interface gigabitEthernet 0/1
R1(config-if)# ip access-group HTTP_ONLY in
3.	Verify Implementation:
o	Tested connectivity by pinging the server from PC2, ensuring the connection was successful. Attempted FTP access, which should fail due to ACL restrictions, and verified successful HTTP access through a web browser.
Conclusion: The successful implementation of extended ACLs enhanced security by restricting access to server resources based on specific requirements. By allowing only necessary traffic, the network maintains integrity and reduces potential vulnerabilities.





