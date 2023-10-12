<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this section, I observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04



<h2>Actions and Observations</h2>

<p>
<img <img width="1080" alt="image" src="https://github.com/maria-benitez/azure-network-protocols/assets/147643771/34d356c3-b9b5-46d4-bd2f-a97fc35ffdc5">
</p>
<p>
Created two virtual machines with Microsoft Azure to observe traffic between them. Virtual Machine 1 (VM1) is running Windows 10 while Virtual Machine 2 (VM2) is running Linux (Ubuntu).
</p>
<br />

<p>
<img <img width="1080" alt="image" src="https://github.com/maria-benitez/azure-network-protocols/assets/147643771/6166f277-dad0-46ee-a1a3-0a6a35b43f50">

</p>
<p>
Used Microsoft Remote Desktop available in the App Store to connect with VM1. From there, I am installing Wireshark onto VM1 to inspect traffic as I interact with VM2.
</p>
<br />

<p>
<img width="1080" alt="image" src="https://github.com/maria-benitez/azure-network-protocols/assets/147643771/5ffac65d-d526-4f5f-bcf7-216d03e2c998">
</p>
<p>
After installing Wireshark on VM1, I filtered the traffic to ensure it only displayed ICMP traffic. From Microsoft Azure, I obtained VM2's private IP address to ping from VM1. I then used Powershell on VM1 to ping VM2. Then, I observed the traffic on Wireshark.
<p>
**Note:
<p>
Virtual Machine 1 (VM1) Private IP address: 10.0.0.4
<p>
Virtual Machine 2 (VM2) Private IP address: 10.0.0.5
</p>
<br />

<p>
<img width="1080" alt="image" src="https://github.com/maria-benitez/azure-network-protocols/assets/147643771/964da0b5-4bc7-4ef6-a2f3-b438fd34b393">
</p>
<p>
I initiated a perpetual ping from VM1 to VM2; this will ping VM2 non-stop.  I did this because I am going to change VM2's firewall to not allow ICMP traffic to come through. 
</p>
<br />

<p>
<img width="1080" alt="image" src="https://github.com/maria-benitez/azure-network-protocols/assets/147643771/a13ee58b-7c1e-4b09-a66d-6a4cd4f5075d">
<p>
<img width="1080" alt="image" src="https://github.com/maria-benitez/azure-network-protocols/assets/147643771/76353236-0970-417f-a783-fb49aaec2e18">
</p>
<p>
In Microsoft Azure, I implement a new Inbound Port Rule on VM2 that denies any inbound ICMP traffic.
<p>
Once the rule is implemented, I can observe the changes from VM1. On Powershell I observe that the ping request to VM2 has timed out.  On Wireshark, I observe that replies have stopped coming in from VM2. I then went back into Microsoft Azure and changed that rule to Allow ICMP traffic. 
</p>
<br />

<p>
<img width="1080" alt="image" src="https://github.com/maria-benitez/azure-network-protocols/assets/147643771/50fefb2b-375b-4860-848d-6c9083f9ad9a"/>
<p></p>
<img width="1080" alt="image" src="https://github.com/maria-benitez/azure-network-protocols/assets/147643771/b175c3e8-3709-4720-bdc3-88637608a1e6"/>

</p>
<p>
Once ICMP traffic has been re-established, I then explore SSH traffic. I did this by connecting to VM2 from VM1 via Secure Shell (SSH). Once connection has been established, I can observe traffic on Wireshark.
</p>
<br />

<p>
<img width="1080" alt="image" src="https://github.com/maria-benitez/azure-network-protocols/assets/147643771/a959ffea-c8e7-403d-b3ba-c5dc06239518">
<img width="1080" alt="image" src="https://github.com/maria-benitez/azure-network-protocols/assets/147643771/bdb2a439-9475-4afb-af28-54e12d2f7359"/>


</p>
<p>
Finally, I observed DHCP and DNS traffic.
</p>
<br />
