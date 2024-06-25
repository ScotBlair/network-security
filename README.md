<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (ICMP, SSH, DNS, RDP)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

  - Step 1<br />
Two Virtual Machines were created in Microsoft Azure: VM1 running Windows 10 (21H2) and VM2 running Ubuntu Server 20.04.
On VM1, a perpetual ping was sent using the "ping -t" command in Command Prompt to the private IP address of VM2.  Being that the two VM's were on the same network with no restrictions, a reply was received.

  - Step 2<br />
In Azure, by going to Network security groups -> VM2 -> Inbound security rules, a new security rule was added.  The "Protocol" was set to ICMP (Internet Control Messaging Protocol), the "Action," set to Deny, and the "Priority" set to 200 to ensure the rule was checked before all others.
<br />![Screenshot 2024-06-25 111852](https://github.com/ScotBlair/network-security/assets/171102023/0215355a-4dd7-490b-b1e3-8ce3da386a78)<br />

  - Step 3<br />
Back on VM1, the ping to VM2 had stopped and the words "Request timed out" now appeared.
<br />![ICMP ping 1](https://github.com/ScotBlair/network-security/assets/171102023/973dc6f7-3b66-4edd-9b16-28f8e4464cd0)<br />
Once the security rule was deleted, the reply to VM2 was received once again.

<h2></h2>

  - Step 1<br />
Wireshark was downloaded onto VM1, and once opened up network traffic was first filtered by "tcp.port == 22" (SSH).

  - Step 2<br />
Using Command Prompt, VM1 remotely accessed VM2 using the command "ssh labuser@48.217.123.158," and after entering the password, was given access.
*NOTE: "labuser" is the name of VM2, and the numbers that follow are VM2's private ip address*
<br />![1](https://github.com/ScotBlair/network-security/assets/171102023/e98e97cf-b5b7-4f2a-a2ac-a0bba56c579a)<br />

  - Step 3<br />
At this point, Wireshark started to display traffic between the two VM's.  Any keystroke made would produce new traffic, such as the set of words "bread markers paper box."
<br />![2](https://github.com/ScotBlair/network-security/assets/171102023/7d7d0edf-8fd9-47fc-ac2a-a44a1de99c7d)<br />

  - Step 4<br />
Network traffic was then filtered by "udp.port == 53" (DNS).

  - Step 5<br />
Using Command Prompt, VM1 looked up Disney using "nslookup www.disney.com."  Disney's server information and public IP addresses displayed in the prompt and also appeared in Wireshark.
 <br />![nslookup udp port == 53](https://github.com/ScotBlair/network-security/assets/171102023/56353172-3306-4b41-96d2-23c83eae25f2)<br />

  - Step 6<br />
Lastly, network traffic was filtered by "tcp.port == 3389" (RDP).  Since VM1 was logged into via Remote Desktop, Wireshark was already being spammed with traffic.
<br />![tcp port == 3389](https://github.com/ScotBlair/network-security/assets/171102023/df5362fe-eaa0-4c43-b13a-59c698f665f0)<br />
