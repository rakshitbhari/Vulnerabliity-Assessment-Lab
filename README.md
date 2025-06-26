<h1>Vulnerability Assessment Lab</h1>

<h2>Description</h2>
This is a walkthrough of how I created A Virtual Machine environment using VMWare running Windows 10. I did this project to gain experience with Nessus Essentials and learn how to scan for vulnerabilities and remediate them. This project will showcase two of the main steps in the Vulnerability Management Lifecycle. I will be using Nessus Essentials to scan local VMs hosted on VMWare Workstation in order run credentialed scans to discover vulnerabilities, remediate some of the vulnerabilities, then perform a rescan to verify remediation.
<br />

<h2>Utilities Used</h2>

- <b>Nessus Essentials</b> 
- <b>CMD</b>

<h2>Environments Used </h2>

- <b>VMWare</b>
- <b>Windows 10</b> (21H2)

<h2>Links</h2>

- <b>VMWare Workstation Pro:</b> https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html
- <b>Nessus Essentials:</b> https://www.tenable.com/products/nessus/nessus-essentials
- <b>Windows 10 ISO:</b> https://www.microsoft.com/en-us/software-download/windows10

<h2 align="center">Program walk-through</h2>

<p align="center">
<b>The first thing I am going to do is Download Nessus Essentials, my Vulnerability management software. It takes a long time to download so I can accomplish a few things while it is downloading, like downloading Windows 10 on a Virtual Machine and configuring it (which also takes a long time)</b> <br/>
</p>

![Downloading Nessus](https://github.com/user-attachments/assets/aca7f452-47b3-495d-ad63-9c63b84d53f7)

<br />
<br />
<p align="center">
<b>For the Virtual Machine that I will be managing vulnerabilities on, I have to configure the network adapter to be bridged so it can be on the same network as my native. I do this because Nessus has to Secure Server Login (SSL) into the Virtual Machine and it's just easier if it's using my local network.</b> <br/>
</p>

![Configure_Network_Adapters](https://user-images.githubusercontent.com/108043108/177885541-29039f1c-6217-43b4-92ca-86a60d092d3b.JPG)

<br />
<br />
<p align="center">
<b>Nessus at this point is still downloading and my Virtual Machine successfully downloads Windows 10, so I open up CMD to figure out it's IP address which I will need to be able to run vulnerability scans on Nessus. I named the VM Admin. The screenshot shows that the IP address is 192.168.50.185</b> <br/>
</p>

![VM_IP](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/257102247bcfd428118dfdcf510d6935f08fe60d/Images/3.jpeg)


<br />
<br />
<p align="center">
<b>I try to ping the VM from my native computer to see if I can communicate with the VM. The reason I am doing this is because of I can't ping the VM then Nessus won't be able to as well and can't run its scans. As we can see the pings are timing out, meaning my native PC can't establish a connection with it at the moment.</b> <br/>
</p>

![trying_to_ping_VM_Fails](https://user-images.githubusercontent.com/108043108/177886078-cec7b98b-60da-47a6-8e70-838a649a456f.JPG)

<br />
<br />
<p align="center">
<b>The reason my PC can't establish a connection is because the VM has a firewall active and it is blocking all connection attempts (which is a good thing, but not for the purposes of this lab) so I have to disable the firewalls. This is something I would NEVER do in a production environment as it could and would be catastrophic, but this is a just a junk VM so no worries.</b> <br/>
</p>

![windows_firewall_disable](https://user-images.githubusercontent.com/108043108/177886413-df1ba042-8e42-4ff6-a004-0057ac793cd1.JPG)

<br />
<br />
<p align="center">
<b>I have to turn off all three firewalls which are circled at the top in Red, Blue, and Green. Circled in Yellow is showing that the firewalls are currently On. I have to turn them Off to be able to communicate properly with the VM.</b> <br/>
</p>

![Turning_off_Firewalls](https://user-images.githubusercontent.com/108043108/177886437-e6b4addf-99e3-455f-b46f-c3941a433109.JPG)

<br />
<br />
<p align="center">
<b>Now that the VM's firewall is disabled, I try to Ping it again from my native PC and this time it is successful.</b> <br/>
</p>

![Ping_works](https://user-images.githubusercontent.com/108043108/177887412-f8078e7b-13a3-4480-b000-5ae84108cfab.JPG)

<br />
<br />
<p align="center">
<b>By this time Nessus Essentials successfully downloads. The first thing I want to do is create a new scan, then select Basic Network Scan.</b> <br/>
</p>

![Create_New_Scan](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/8.jpeg)

![basic_network_scan](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/9.jpeg)


<br />
<br />
<p align="center">
<b>The newly created scan asks me to name the scan and select a target to scan. I configure it to scan the VM's IP address which is 192.168.50.185</b> <br/>
</p>

![Scan_VM_IP](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/10.jpeg)

<br />
<br />
<p align="center">
<b>I launch the newly created scan and it immediately goes to work scanning for any known vulnerabilities. When the grey checkmark appears, the scan is complete.</b> <br/>
</p>

![Launch_newly_created_scan](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/11.jpeg)

![Scan_Running](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/12.gif)

![Scan_Completed](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/13.jpeg)

<br />
<br />
<p align="center">
<b>Lets look at the results! It is showing 33 results, 32 of which are info and 1 low. If this was an actual production environment these most likely would be left alone. The Info results are probably because some things don't have proper credentials and are not essentially vulnerabilities</b> <br/>
</p>

![Results_Of_Scan](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/14.gif)

<br />
<br />
<p align="center">
<b>Looking at one of the INFO results you can see that the Target Credential Status By Authentication Procotol was triggered because we did not actually provide any credentials for this scan.</b> <br/>
</p>

![No_credentials_Given](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/15.jpeg)

<br />
<br />
<p align="center">
<b>Next thing I do is configure the VM to be able to accept authenticated scans and provide credentials to Nessus. I will then rescan the VM and compare the results. I go to services.MSC to start this process and enable Remote Registry. This will allow Nessus to connect to the VM's registry and properly scan for vulnerabilities such as insecure connections or deprecated cipher suites. I'm following these steps from Nessus and what they recommend to actually do credentialed scans. There might be a better way to do this.</b> <br/>
</p>

![Services_MSC](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/16.jpeg)

![Enabling_Remote_Registry](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/17.gif)

<br />
<br />
<p align="center">
<b>From there I go to User Account Controls and disable it. I have to do this because this VM is not on a domain so I kind of have to do hacker stuff to get it to work properly. I would never do this in an actual organization or production environment.</b> <br/>
</p>

![user_account_Settings](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/18.jpeg)

![User_Account_settings_configuration](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/19.gif)

<br />
<br />
<p align="center">
<b>Then I'm going to open the registry and add a key that is suppose to allow Nessus to connect in by further disabling user account controls.</b> <br/>
</p>

![Registry_editor](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/20.jpeg)

<br />
<br />
<p align="center">
<b>Now I navigate the Registry to the file that Nessus instructs us to (highlighted Yellow in the search bar) and I have to add a DWORD value and name it LocalAccountTokenFilterPolicy and give it a value of 1. </b> <br/>
</p>

![Creating_a_new_DWORD](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/21.jpeg)

![DWORD_name](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/22.jpeg)

![Edit_DWORD](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/23.jpeg)

<br />
<br />
<p align="center">
<b>After doing that I have to restart the VM so the changes can take effect.</b> <br/>
</p>

![Restart_The_VM](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/24.jpeg)

<br />
<br />
<p align="center">
<b>With the registry configured, it is now time to go back into Nessus and configure the scan I created. I have to add the Credentials to the scan so it can work properly. The credentials I'm talking about is the username and password of the VM. This will allow Nessus to use those credentials in places where it is required in the VM registry.</b> <br/>
</p>

![Configure_Nessus](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/25.jpeg)

![Adding_Credentials](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/26.gif)

<br />
<br />
<p align="center">
<b>After the scan is properly configured with the right credentials, I run it again.</b> <br/>
</p>

![Run_The_Scan_Again](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/27.jpeg)

<br />
<br />
<p align="center">
<b>This new scan has given us a lot more vulnerabilities than the first one because it is able to scan deeper into the VM due to having credentials. The top picture is the new credentialed scan and the bottom picture is from the first non-credentialed scan. Most of the vulnerabilities found is probably because the version of Windows 10 this VM is running is not up to date.</b> <br/>
</p>

![new_scan_properly_credentialed](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/28.jpeg)

![Old_scan_not_credentialed](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/29.jpeg)

<br />
<br />
<p align="center">
<b>I want to see how powerful this Nessus Scanner is so I'm going to download a very old version of Firefox which probably has many vulnerabilities and see if Nessus can discover them (I'm sure it will.)</b><br/>
</p>

![downloading_an_old_version_of_firefox](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/30.jpeg)

<br />
<br />
<p align="center">
<b>After a deprecated version of Firefox is downloaded, I run another scan. We can see many new alerts and vulnerabilities just from Firefox! 68 Critical!</b> <br/>
</p>

![Old_Firefox_Scan](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/31.jpeg)

<br />
<br />
<p align="center">
<b>A comparison between scans to show the progression of alerts and vulnerabilities.</b>  <br/>
</p>

![Vulnerability_Comparison](https://user-images.githubusercontent.com/108043108/177890918-c2fc7078-34b9-4120-a430-f096169ae177.jpg)

<br />
<br />
<p align="center">
<b>Showing what some of the alerts and vulnerabilites look like. We can see most of the Critical alerts are just from Firefox. A few ways we can remediate some of the vulnerabilities is by either Updated Firefox, which will probably remediate a lot of them, or we can simply delete Firefox.</b>  <br/>
</p>

![Showing_Vulnerabilities](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/33.gif)

<br />
<br />
<p align="center">
<b>To start the process of remediating vulnerabilities, I elect to just delete Firefox. That will instantly fix a lot of these issues.</b>  <br/>
</p>

![Fixing_Vulnerabilities_Uninstall_Firefox](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/34.jpeg)

<br />
<br />
<p align="center">
<b>To remediate the Windows vulnerabilities, I choose to update Windows. This version is old so it takes a few restarts to get it up to date.</b>  <br/>
</p>

![Remediating_Vulnerabilities_Updating_WIndows_1](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/35.gif)

![Remediating_Vulnerabilities_Updating_Windows](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/36.jpeg)

<br />
<br />
<p align="center">
<b>After a few restarts, Windows is finally up to date. I run one more Nessus scan to find if the steps I took to remediate some of the alerts worked.</b>  <br/>
</p>

![VM_Up_To_date](https://github.com/rakshitbhari/Vulnerabliity-Assessment-Lab/blob/0f2a6bc12f9d597a6c6a526a508e146fc9cadea6/Images/37.jpeg)

<br />
<br />
<p align="center">
<b>Here is a final comparison between the four scans I took while doing this lab. The last picture is the after remediation scan. There we can see a lot of the vulnerabilities that were being alerted are gone! Still a 1 critical but I'll remediate that another time!</b>  <br/>
</p>

![After_Vulnerability_Remediation](https://user-images.githubusercontent.com/108043108/177891719-3066c9bb-38dd-4b10-b8bb-6f9dd8a45a09.JPG)

<br />
<br />


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
