<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- ICMP (Internet Control Messaging Protocol)
  - Step 1<br />
Two Virtual Machines were created in Microsoft Azure: VM1 and VM2.
On VM1, a perpetual ping was sent using the "ping -t" command in Command Prompt to the private IP address of VM2.  Being that the two VM's were on the same network with no restrictions, a reply was received.

  - Step 2<br />
In Azure, by going to Network security groups -> VM2 -> Inbound security rules, a new security rule was added.  The "Protocol" was set to ICMP, the "Action," set to Deny, and the "Priority" set to 200 to ensure the rule was checked before all others.
<br />![Screenshot 2024-06-25 111852](https://github.com/ScotBlair/network-security/assets/171102023/0215355a-4dd7-490b-b1e3-8ce3da386a78)<br />

  - Step 3<br />
Back on VM1, the ping to VM2 had stopped and the words "Request timed out" now appeared.
<br />![ICMP ping 1](https://github.com/ScotBlair/network-security/assets/171102023/973dc6f7-3b66-4edd-9b16-28f8e4464cd0)<br />
Once the security rule was deleted, the reply to VM2 was received once again.


<h2>Actions and Observations</h2>


