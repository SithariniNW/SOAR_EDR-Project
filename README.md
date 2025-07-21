<h1 style="color:blue;"> SOAR EDR Project</h1>


<h3> Resources Used </h3>
<p> <ul type="circle">
 <li>Tines - Security Ooperations Automation Response Platform</li>
 <li>LimaCharlie - Endpoint Detection Response Platform</li>
 <li>Windows Virtual Machine as an agent</li>
 <li>Slack - Messaging Channel </li>
</ul> </p>


<h3>Overview</h3>
The lab consists of gaining hands-on experience with the use of SOAR and EDR platforms.

<br>SOAR implementations are increasingly used by a wide variety of Security Operations Centres (SOC) to reduce repetitive tasks and automate their processes. Security processes are developed as playbooks by professionals in SOAR platforms to enable integration with various tools and systems across the security infrastructure. 

The SOAR vendor used for this product is Tines, while Limacharlie is used as the EDR vendor.

<h3>Part 1 - Diagram</h3>

The purpose of this part of the project is to create a playbook workflow and brainstorm actions taken by the mentioned playbook.

<br> <h1> Playbook Objective </h1>
<ul type="circle"> 
  <li> Send a Slack message and email containing information about the detection </li>
  <li> Generate user prompt to action necessary precautions </li> </ul>

<br> <img src="Images/Screenshot 2025-02-13 152426.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

Story - Tines
Create detection in LimaCharlie - Detect HackTool > Tines > Slack & Email

Slack and email will contain
- Time
- Computer name
- Source IP
- Process
- Command Line
- File Path
- Sensor ID
- Link to detection if applicable

Tines > Prompt user to isolate the machine (YES/NO)
- if yes = LimaCharlie should automatically isolate the machine and a message should be sent to Slack
- Message: Isolation status with note of "The Computer has been isolated"
- If not = LimaCharlie will not isolate
- Message: Isolation statis with note of "The Computer was not isolated, please investigate"

<br> <img src="Images/Screenshot 2025-02-13 221617.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<br> <img src="Images/Screenshot 2025-02-13 220114.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<br> Then within the VM, Windows Firewall settings were completely turned off, to ensure that the machine was completely vulnerable. This can be tested by sending a ping request to the VM through the host machine. Which became successful since it is open to making connections.

<br> <img src="Images/Screenshot 2025-02-16 153308.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<h3>Log Repository Creation</h3>

For the use of our log repository, a Log Analytics Workspace is created within Microsoft Azure.

<br> <img src="Images/Screenshot 2025-02-13 154136.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

To analyze the collected log data further using an SIEM, a  Microsoft Sentinel instance is also created and connected to the log analytics workspace. 

<br> <img src="Images/Screenshot 2025-02-13 213622.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<br> Furthermore, a connection between the VM and log analytics workspace should also be created. This is done through several steps,
<ul>
 <li> Installing Windows Security Events in Sentinel</li>
 <li> Installing Windows Security Events via AMA package </li>
 <li> Configure data connection rule (allows VM to forward security logs to log analytics workspaces) </li>
</ul>

<br> <img src="Images/Screenshot 2025-02-17 170046.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<br> After the above steps are completed, the logs at the created Log Analytics Workspaces will be able to display logs regarding any activities taking place within the VM.

<br> <img src="Images/Screenshot 2025-02-17 220447.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<h3> Querting log repository using KQL</h3>

KQL or Kusto Query Language is a tool in Microsoft Azure similar to SQL that can be used to explore and filter data.

<br> KQL can be used to filter through the many security events that occur within the VM to narrow down specific events. As an example to analyze results that indicate a failed login attempt the following query can be used,

<br> <img src="Images/Screenshot 2025-02-18 213548.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<h3> Uploading data to SIEM </h3>

Using a table of geographical locations of IP address ranges combined with the security event logs of the VM, a mapping of the locations of the attacks can be created through the Microsoft Sentinel SIEM.

<br> <img src="Images/Screenshot 2025-02-17 230830.png" height="60%" width="60%" alt="Virtual Machine creation" align="center"/>

<h3> Conclusion </h3>

This project successfully demonstrated how to configure a Security Information and Event Management (SIEM) system using Microsoft Sentinel within Azure. By creating a honeypot VM, disabling security measures, and logging failed login attempts, we were able to collect valuable security data and analyze it using Kusto Query Language (KQL). The integration of Microsoft Sentinel allowed us to visualize attack patterns and understand potential threats targeting the system.

<h3> Reflection </h3>

One of the key takeaways from this project was the importance of proactive monitoring and logging in cybersecurity. It also gave me a glimpse of the workings of real-world SIEM and SOC. This lab served me as a foundational exercise for building more advanced security monitoring solutions.

<h5> Skills obtained </h5>

<ul> 
 <li> Microsoft Azure configurations </li>
 <li> Kusto Qurey Language </li>
 <li> Working with SOC and SIEM setup </li>
</ul>

<h5> References </h5>
https://www.youtube.com/watch?v=g5JL2RIbThM
<br> https://www.youtube.com/watch?v=RoZeVbbZ0o0&t=1580s
<br> https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/data-collection-transformations
<br> https://learn.microsoft.com/en-us/azure/azure-monitor/logs/custom-fields
