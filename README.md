<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Microsoft Remote Desktop (MAC)
- Various Command-Line Tools
- Network Protocol (ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create resources (resource group, windows 10 VM, Linux(Ubuntu) VM) 
- Observe ICMP Traffic (Use NSG to stop inbound ICMP traffic)
- Step 3
- Step 4

<h2>Actions and Observations</h2>

![image](https://github.com/OmarJamaladdin/azure-network-protocols/assets/140512686/c06ca1ad-9431-4f62-857a-951d4fd539a7)

First I created a resource group RG-Lab and then I created a Windows 10 Virtual Machine (VM1)
While creating the VM, I allowed it to create a new Virtual Network (Vnet) and Subnet. Following this I created a Linux (Ubuntu) VM (VM2)
and when creating the VM I selected the previously created Resource Group and Vnet from my first VM. Since I am using a Macbook, I also had to install Microsoft Remote Desktop in oder to remotely connect to my created VM's.

![image](https://github.com/OmarJamaladdin/azure-network-protocols/assets/140512686/35d6fb97-75eb-46e8-83f3-5ef615d32298)

In step 2 I am now using powershell and using ping (icmp protocol) to send icmp traffic to VM2's private IP address and as you can see the ping is continuous meaning it will not end.

![image](https://github.com/OmarJamaladdin/azure-network-protocols/assets/140512686/bcf152ba-9c25-4b19-9ba7-d32bf5bb2bf0)

Now as you can see I went back into Azure and started to configure with VM2's NSG or Network Security Group. Here I added an inbound security rule to deny all inbound icmp traffic to VM2.


![image](https://github.com/OmarJamaladdin/azure-network-protocols/assets/140512686/e4d4048b-5b4b-4a31-82ca-a854b9c82546)


As a result of creating the Inbound security rule in VM2's Network security group, you can see that the icmp traffic no longer comes through and is being denied. In the image above, you can see that in Powershell there are no more replies and the requests continuosly times out. Also you can see via Wireshark in the background that there are still ping (icmp) requests coming from VM1 but there are no more replies coming from VM2's private IP address.
