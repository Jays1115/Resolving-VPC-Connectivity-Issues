<h5>Directory</h5> 

<b>[Tech Portfolio Home](https://github.com/Jays1115/Jalen-Smith.git)</b> /
<b>[AWS Projects](https://github.com/Jays1115/AWS-Projects.git)</b>

# Resolving-VPC-Connectivity-Issues

<h2>Description</h2>
Request: A bank recently migrated to the cloud and is encountering connectivity issues with its EC2 instances and databases. The EC2 instances are unable to access the internet, and the databases are failing to communicate with the instances.
<br><br>
Solution: Update the routing table for the public subnet to route HTTP traffic through the internet gateway. Adjust the security group settings for the web server to permit inbound HTTP traffic, and configure the database server's security group to allow TCP traffic from the web server.

<h2>Program walk-through:</h2>

<p align="center">
Navigated to the EC2 Section within AWS and reviewed the selected region, making sure its set to N. Virginia (us-east-1): <br/>
<img src="images/Screenshot 2024-09-17 at 8.45.55 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
</p>

<p align="center">
Navigated to instances via the left side bar: <br/>
<img src="images/Screenshot 2024-09-17 at 8.47.56 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
</p>

<p align="center">
Copied and pasted the IPv4 address of the web server into a new tab to confirm there is an issue with the server’s internet connectivity: <br/>
<img src="images/Screenshot 2024-09-17 at 8.49.10 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<img src="images/Screenshot 2024-09-17 at 8.50.47 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
</p>

<p align="center">
Returned to the EC2 instance hosting the web server, reviewed its networking details, and accessed the associated subnet by clicking on the subnet ID: <br/>
<img src="images/Screenshot 2024-09-17 at 8.54.02 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<img src="images/Screenshot 2024-09-17 at 8.54.15 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
</p>

<p align="center">
Selected the subnet, navigated to the "Route Table" tab, and clicked the route table link to access the route table associated with the public subnet: <br/>
<img src="images/Screenshot 2024-09-17 at 8.57.57 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<img src="images/Screenshot 2024-09-17 at 8.59.01 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
</p>

<p align="center">
In the "Routes" tab, reviewed the existing routes and proceeded to edit them: <br/>
<img src="images/Screenshot 2024-09-17 at 9.01.45 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>

<br />
<br />
</p>

<p align="center">
Deleted the NAT gateway from the route table: <br/>
<img src="images/Screenshot 2024-09-17 at 9.01.58 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<img src="images/Screenshot 2024-09-17 at 9.04.23 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
</p>

<p align="center">
Added an internet gateway to the route table to enable inbound and outbound internet traffic for the web server within the public subnet: <br/>
<img src="images/Screenshot 2024-09-17 at 9.07.43 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<img src="images/Screenshot 2024-09-17 at 9.08.18 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
</p>

<p align="center">
Navigated back to the web server EC2 instance, accessed its associated security group, and began editing the inbound rules for the security group: <br/>
<img src="images/Screenshot 2024-09-17 at 9.10.44 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<img src="images/Screenshot 2024-09-17 at 9.11.01 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
</p>

<p align="center">
Added a rule to the security group to accept inbound HTTP traffic from anywhere (0.0.0.0/0): <br/>
<img src="images/Screenshot 2024-09-17 at 9.11.21 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<img src="images/Screenshot 2024-09-17 at 9.15.07 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<img src="images/Screenshot 2024-09-17 at 9.15.16 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
</p>

<p align="center">
Returned to the web server EC2 instance, copied its IPv4 address, and pasted it into another browser tab to verify that the web server is now accessible and allowing internet traffic: <br/>
<img src="images/Screenshot 2024-09-17 at 9.17.08 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<img src="images/Screenshot 2024-09-17 at 9.17.49 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
</p>

<p align="center">
Next, we need to configure the web server to communicate with the database. <br/> <br/>
Selected the DB server EC2 instance and navigated to the security tab to access its associated security group. Added an inbound rule allowing TCP traffic on port 3306, specifically from the web server (10.10.0.0/24): <br/>
<img src="images/Screenshot 2024-09-17 at 9.20.49 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<img src="images/Screenshot 2024-09-17 at 9.21.14 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<img src="images/Screenshot 2024-09-17 at 9.23.56 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<img src="images/Screenshot 2024-09-17 at 9.24.05 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
</p>

<p align="center">
After refreshing the web server session, it is confirmed that the web server can now successfully communicate with the DB server: <br/>
<img src="images/Screenshot 2024-09-17 at 9.24.47 AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
</p>

<p align="center">
The Bank is no longer experiencing network connectivity issues between the internet and its web server or between its web server and DB server! <br/>
</p>
