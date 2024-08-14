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
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create Resources in Azure
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic


<h2>Actions and Observations</h2>

Step 1: Create a Resource Group in Azure
   - Enter 'Resource Groups' in the search bar at the top
   - Click '+Create'
   - Enter your Resource Group  name, and select whichever Region that works for you
   - Click 'Review + Create' -> then click 'Create'

![image](https://github.com/user-attachments/assets/002358c1-2f1e-4dcf-8725-cbab1e39f12a)



Step 2: Create two Virtual Machines in Azure
   - Enter 'Virtual Machines' in the search bar at the top
   - Click '+Create'
   - Select your Resource Group that was just created
   - Name you Virtual Machine 'VM1'
   - Select whichever Region that works for you (Note: In this case US East 2 was selected)
   - Select 'No infrastructure redundancy required' for Availability options
   - Select 'Standard' for the Security type
   - Select 'Window 10 Pro' for the Image field
   - Select at least 2 vcpus for the Size
   - Create your Username and Password
   - Check the 'Licensing' box
   - Click 'Review + Create' -> then click 'Create'

*Repeat steps and create the second Virtual Machine
   - Select the same Resource Group that was created
   - Name your Virtual Machine 'VM2'
   - Select the same Region as 'VM1'
   - Select 'No infrastructure redundancy required' for Availability options
   - Select 'Standard' for the Security type
   - Select 'Ubuntu Server 24.04'
   - Select at least 2 vcpus for the Size
   - Select 'Password' for the Authentication type
   - Create your Username and Password
   - Click 'Review + Create' -> then click 'Create'


![image](https://github.com/user-attachments/assets/5c33935a-f593-4a3f-b6aa-fc0448227fe7)

![image](https://github.com/user-attachments/assets/0f9bd7d6-d805-4d3b-8d86-ab903c94a7bc)

![image](https://github.com/user-attachments/assets/7e2837b7-47d7-4373-98f2-29c7bd2a8d92)

![image](https://github.com/user-attachments/assets/8d1c0d29-d87e-4f47-aed9-33362c2e5885)

![image](https://github.com/user-attachments/assets/743845d9-0d82-4fc4-a618-ebabb1379e40)


*Note: Ensure VM1 and VM2 are in the same region/ location
![image](https://github.com/user-attachments/assets/ce102413-8c1f-4d13-be05-5cbf7e396fe3)



Step 3: Use Remote Desktop to connect to Windows 10 Virtual Machine (VM1)
   - Select VM1 in Azure
   - Copy the Public IP Address and paste it in the 'Computer' field in the Remote Desktop App
   - Click 'Connect'
   - Log in using yor credentials created for VM1
   - Install Wireshark in VM1
       - Open Microsoft Edge
       - Go to 'google.com'
       - In the search bar enter 'download wireshark'
       - Select the first link that says' Wireshark Download' -> download the 'Windows Installer' -> after the download finished, click 'Open file' -> select all the defaults by clicking 'Next' and click 'Install' and 'Finish'
       - Open Wireshark by going to the start menu and entering 'Wireshark'
  - Once Wireshark is open, select 'Ethernet' and click on the blue fin icon (top left) to start capturing packets and see the live traffic happening
  - Filter for ICMP traffic only by entering 'icmp' in the 'Apply a display filter' field at the top -> hit enter on your keyboard
  - Retrieve the Private IP Address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM
       - Minimize VM1
       - Go to VM2 in Azure to copy the Private IP Address -> scroll to 'Networking'
       - Go back to VM1
       - Open Windows Powershell -> click the start menu and enter 'Powershell'
       - Ping VM2 Private IP Address (in this case: 10.0.0.5)
       - You'll notice ping replies from VM2 and ICMP traffic in Wireshark
       - Observe ping replies from 'www.google.com -4' be entering it in Window Powershell



![image](https://github.com/user-attachments/assets/fad65b70-f892-4d97-ba0c-095dbf663cb0)

![image](https://github.com/user-attachments/assets/f0098553-6627-4ebd-9ae7-70d1aca5f176)

![image](https://github.com/user-attachments/assets/9d6ce97d-d8e8-4177-873b-4f2cf7c9e772)

![image](https://github.com/user-attachments/assets/8d331686-816c-42b0-bd60-32764354ec26)

![image](https://github.com/user-attachments/assets/d6b5e0e0-c363-44ec-b9e9-67b3eac7150a)

![image](https://github.com/user-attachments/assets/be498f0b-b8cf-41e1-8b07-5065f3e1239d)

![image](https://github.com/user-attachments/assets/e2a56415-000e-482f-824d-8844e750dde0)

![image](https://github.com/user-attachments/assets/107418b3-5d12-49be-87d3-361507a7de55)

![image](https://github.com/user-attachments/assets/6cdf08a0-86c3-4a3f-a707-e38321dc4b13)

![image](https://github.com/user-attachments/assets/bb13f451-d146-4afd-b79f-4100ea6c50b5)

![image](https://github.com/user-attachments/assets/b3c2f0a7-5437-47ad-8644-bf4e33f2cf46)

![image](https://github.com/user-attachments/assets/3e0a14f8-58e9-4052-a6c9-8639b0e65f13)

![image](https://github.com/user-attachments/assets/0be11270-8601-4b63-a291-b414a819923c)

![image](https://github.com/user-attachments/assets/6c4b78d1-127c-417d-95fb-d802f8991673)




Step 4: Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM

   - Open VM1 and clear the data in Wireshark by click the green refresh icon at the top and click 'Continue without Saving'
   - Go back into Windows Powershell
   - Ping VM2 Private IP Address nonstop by entering 'ping 10.0.0.5 -t' -> hit enter on your keyboard
   - Oberseve the nonstop pings
   - Block the firewall on VM2 to not allow ICMP traffic to come through
      - Minimize VM1
      - Open up Azure and enter 'network security groups' (aka the firewall) in the seach bar at the top and select it
      - Click on VM2 NSG
      - Go to 'Settings'
      - Click on 'Inbound security rules'
      - Click 'Add' to add a rule
      - Scoll a little bit and select ICMPv4 under 'Protocol' ( Note: You'll notice the 'Destination port ranges' changes to 'any' which looks like this -> * )
      - Select 'Deny' for the 'Action'
      - Set the 'Prioirty' to 200 by entering it in the field
      - Name the rule 'DENY_ICMP_PING_FROM_ANYWHERE'
      - Click 'Add'
   - Open back up VM1
   - You should notice the pings will start to 'time out'
   - Open up Azure and go to NSG and allow the ICMPv4 traffic to come back through
      - Select the rule we created to edit it
      - Select 'Allow' under 'Action'
      - Click 'Save'
   - Open up VM1
   - Observe the traffic responses coming back through as 'Reply'
   - ctrl+c to stop the traffic in Windows Powershell



![image](https://github.com/user-attachments/assets/933a0662-81bc-4e60-94c0-348be818e57b)

![image](https://github.com/user-attachments/assets/47f19420-dd89-4d73-9aa4-bfd946649a4a)

![image](https://github.com/user-attachments/assets/f106f1d0-d1b6-4ec6-a498-1a99dba12111)

![image](https://github.com/user-attachments/assets/c7421000-a68a-4cfc-917e-4143e757b3a2)

![image](https://github.com/user-attachments/assets/c2effa5e-53f8-4e76-9074-be123f658141)

![image](https://github.com/user-attachments/assets/2d3f4de4-b444-4a36-b7b5-da8d6d44225b)

![image](https://github.com/user-attachments/assets/7c87b0be-3902-42b9-b5a7-f9ac7b6c7514)

![image](https://github.com/user-attachments/assets/10735a5b-363d-4c7f-ac58-2410ef198c00)



Step 5: Explore SSH Traffic

  - Open VM1
  - Open up Wireshark
  - Filter for SSH traffic only by entering 'ssh' in the 'Apply a display filter' field at the top -> click the green icon to refresh Wireshark -> click 'Continue without Saving'
  - Open Windows Powershell and ping VM2 by entering 'ssh labuser@10.0.0.5' -> hit enter on your keyboard
  - You'll be asked 'Are you sure you want to continue?' -> enter 'yes'
  - Enter your VM2 password that was created in Azure (*Note: You will not be able to see the password, in this case you'll see I had to try again lol)
  - You now have a connection to VM2
  - Observe traffic by entering Linux commands aka Ubuntu
    - ping 'id' -> and hit enter
    - ping 'uname -a' -> hit enter
    - ping 'pwd' -> hit enter
    - ping 'exit' to close VM2 connection
  

![image](https://github.com/user-attachments/assets/80d20a56-3af4-4331-9a60-3ff886963a13)

![image](https://github.com/user-attachments/assets/1586260d-f03b-47a5-8589-a0109b11d848)

![image](https://github.com/user-attachments/assets/9f5da043-80a3-49b2-9348-440b39c436ff)

![image](https://github.com/user-attachments/assets/89ed035f-5608-4e58-8acd-5419abbd1098)

![image](https://github.com/user-attachments/assets/ac4f3c6b-03db-484f-b57f-2aa3a1d3ffa1)

![image](https://github.com/user-attachments/assets/bd75d018-db66-4a7f-a363-a6da30ddf85b)

![image](https://github.com/user-attachments/assets/72b6a363-8b36-4538-9460-7b6927506349)




Step 6: Explore DHCP Traffic

  - Open VM1
  - Open up Wireshark
  - Filter for DCHP traffic only by entering 'dhcp' in the 'Apply a display filter' field at the top -> hit enter on your keyboard
  - Open Windows Powershell and ping 'ipconfig /renew' to issue VM1 a new IP address -> hit enter on your keyboard
  - Observe DHCP traffic


![image](https://github.com/user-attachments/assets/b2bd58f2-a5de-47ba-adea-90590fd89995)

![image](https://github.com/user-attachments/assets/e904791c-007f-45ba-a29e-5c007ea8f1e0)



Step 7: Explore DNS Traffic

  - Open VM1
  - Filter for DNS traffic only by entering 'dns' in the 'Apply a display filter' field at the top -> hit enter on your keyboard
  - You'll notice traffice already happening, click the green refresh icon at the top and 'Continue without Saving' to clear the traffic
  - Open Windows Powershell and ping 'nslookup www.google.com' to see what the IP address is
  - Observe DNS traffic and view a few of Google's IP addresses in Windows Powershell
  - Ping 'nslookup www.disney.com' to see whatr the IP address is in Windows Powershell
  - Observe DNS traffic and view a few of Disney's IP addresses in Windows Powershell



![image](https://github.com/user-attachments/assets/d0628b32-cc7b-4c24-bf42-abbfb486ee1f)

![image](https://github.com/user-attachments/assets/ff7579ea-a26e-4fe9-86fc-0ca31c5eb7c7)

![image](https://github.com/user-attachments/assets/63a38b7f-452e-42ad-8338-cafb43bcf9d6)




Step 8: Explore RDP Traffic

  - Open VM1
  - Filter for RDP traffic only by entering 'rdp' in the 'Apply a display filter' field at the top -> hit enter on your keyboard
  - You'll notice traffice already happening nonstop (*Note: The RDP (Protocol) is constantly showing you a live stream from one computer to another, therefore traffic is always being transmitted)
  - Observe RDP traffic



![image](https://github.com/user-attachments/assets/83277a84-b664-4eb8-96c8-a37519157938)



That concludes this project.




