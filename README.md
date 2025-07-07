# Active-Directory-Project
## Index 
1. [Introduction](#introduction)
2. [Setup VMs](#setup-vms)
   - [Software Requirements](#software-requirements)
   - [Create a New Virtual Machine](#create-a-new-virtual-machine)
   - [Install Kali Linux](#install-kali-linux)
   - [Install Windows Server](#install-windows-server)
   - [Install Splunk Server](#install-splunk-server)
3. [Installation of Software](#installation-of-software)
   - [Splunk](#splunk)
   - [Splunk Forwarder and Sysmon](#splunk-forwarder-and-sysmon)
4. [Install and Configure Active Directory](#install-and-configure-active-directory)
5. [Brute Force Attack with Kali Linux](#brute-force-attack-with-kali-linux)
6. [Testing with Atomic Red Team](#testing-with-atomic-red-team)
7. [Conclusion](#conclusion)

## Introduction
This project aims to enhance our IT administration knowledge by deploying an Active Directory environment. Additionally, we will configure a Splunk instance to collect event logs from both a Windows Server running Active Directory and a target Windows machine. In the final phase, we will simulate a brute force attack using a Kali Linux machine to analyze the resulting telemetry and leverage Atomic Red Team for supplementary testing.

![Network Diagram](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Active-Directory-diagram.png)

The diagram illustrates the network setup for our project:

- **Windows Server**: This server will run Active Directory.
- **Windows 10 Machine**: This will be the target machine for the Active Directory.
- **Kali Linux Machine**: This machine will be used to perform brute force attacks and other security testing.
- **Splunk Server**: This will be running on an Ubuntu server to collect and analyze logs and events from the Windows Server and Windows 10 machine.
- **Network Infrastructure**: Includes a router and a switch to connect all devices to the Internet and each other.

## Setup VMs
### Software Requirements
- **Virtual Machine Provider**: We will use VMWare WorkStation.
- **Assets**:
    - **Windows Server**
    - **Windows 10**
    - **Kali Linux**
    - **Splunk on Ubuntu Server**

### Install Windows 10 
- First we need to create Windows 10 image to install in VMWare
- Download Create Windows 10 Installion media tool on Microsoft Web Page

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/1.jpg)

- Run the Create Windows 10 Installion media tool

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/2.jpg)

- Choose 'Create Installation media for another PC'

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/3.jpg)

- Keep default setting and next
  
![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/4.jpg)

- Select 'ISO file' and continue
  
![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/5.jpg)

- We can name the iso file that the tool will create, after that we will have a Windows 10 image to install in VMWare
  
![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/6.jpg)

- Next we will install Windows 10 in VMWare with the Windows 10 .iso file
![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/7.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/8.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/9.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/10.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/11.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/12.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/13.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/14.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/15.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/16.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/17.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/18.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/19.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/20.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/21.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/22.jpg)

### Install Kali Linux
Next, we will install Kali Linux using a pre-built virtual machine image. Pre-built images are available for VMware, VirtualBox, Hyper-V, and QEMU. Here are the steps to set up Kali Linux in VMWare:
**Pre-built Virtual Machines**
Kali Linux VMware & VirtualBox images are available for users who prefer or whose specific needs require a virtual machine installation. These images come with the default credentials "kali/kali".

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/23.jpg)

After downloading the zip file, you will find two files in the directory. One of them is `kali-linux-2024.3-vmware-amd64.vmx`.
When we click this, it will automatically be imported into VMWare.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/24.jpg)

And just like that, our Kali Linux is ready.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/25.jpg)

### Install Windows Server
Next, we will install Windows Server.

Go to https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022, fill in the information, and select the ISO edition - 64 bit.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/26.jpg)

After downloading the ISO file, create another machine on VMWare, the same as our Windows 10.

During the installation, make sure to select the second option: Desktop Experience.
![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/27.jpg)

And then you will come to this page. Create a secure password and finish the installation.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/28.jpg)

To be able to log in, it will say that you need to press Ctrl + Alt + Del. In VMWare we can use Ctrl + Alt + Insert instead

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/29.jpg)

### Install Splunk Server
Lastly, we will install our Splunk server. I will use Ubuntu-22.04-live-server-amd64.iso

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/30.jpg)

And same as before, we create another VMWare VM for Ubuntu/Splunk.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/31.jpg)

For the hardware, I will set the memory to 4 GB and Processors to 2. You may want to make the Splunk machine a little better in terms of hardware compared to other machines because this is going to be ingesting data and running searches on it. Set the hard disk to 50 GB and finish the installation.

When we start, we click the first option.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/32.jpg)

After this, it will ask us to select a language, and next, it will ask for an update.

Select Continue without updating and continue.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/33.jpg)

After filling out this form, you can skip and continue every other page without adding any package, and the installation will start.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/34.jpg)

After the installation is complete, click the reboot button, and you will come to this page to enter the Splunk login and password.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/35.jpg)

After entering the username and password, the first thing we will do is update our system:

```
sudo apt-get update && sudo apt-get upgrade -y
```

Our server is now ready to go for the Splunk installation.

Optional: In this project, i use Terminus, a SSH tool that help us access Splunk Server easily and copy/paste command quickly.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/36.jpg)

## Installation of Software
### Splunk
Now we can download and install Splunk. To do this, we will go to the Splunk website from our Host machine and register/log in. We can copy wget link of Splunk Enterprise.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/37.jpg)

Paste the link in Splunk Machine and it will automatically download splunk .deb file. After that, run the installation command: sudo dpkg -i splunk and tab to complete the Splunk file.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/38.jpg)

After the installation is complete, we go to the Splunk directory with cd /opt/splunk/.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/39.jpg)

Now you'll notice that all of the user and group belong to Splunk, which is a good thing as it limits the permissions to that user. Let's change into the user Splunk by typing `sudo -u splunk bash`.

Now we are acting as the user splunk.

Change into the directory called 'bin' as the files listed here are all binaries that Splunk can use.

Here we run the command `./splunk start` to run the installer.
Accepting the agreement and then creating a username and password, our installation will be completed.
The Splunk web interface is at http://splunk:8000 or http://"SplunkIPAddress":8000.

Let's run one more command to make sure that our Splunk starts up every time our virtual machine reboots.

Type 'exit' to exit out of the user splunk first. Then go to the 'bin' directory again under the main user, whatever it is for you. And run:
`sudo ./splunk enable boot-start -user splunk`

This will make it so that anytime the VM reboots, Splunk will run with the user splunk.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/40.jpg)

### Splunk Forwarder and Sysmon
Now that we have Splunk up and running, we want to install the Splunk Universal Forwarder and Sysmon on both our target machine and our server.
First, let's start with renaming our PC to Target-PC.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/41.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/42.jpg)

Now let's open a browser window and try to connect to our Splunk server. Our Splunk IP address was 192.168.193.157, and we know that Splunk listens to port 8000:

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/43.jpg)

And as you can see, we can connect to its login page with no problem. Now let's install the Splunk Universal Forwarder on this machine so we can forward our logs to the Splunk server. Go to the Splunk website and log in with the account that you created. And download the Universal Forwarder for Windows.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/44.jpg)

After the download is complete, start the setup.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/45.jpg)

On the next page, for the username, you can put anything you like. I will put "Admin" and clicked the "Generate random password". On the next page, for the deployment server, just skip without entering anything because we don't have one.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/46.jpg)

On the next page, which is the Indexer page, here we will enter our Splunk server's IP and put the port as 9997, which is the default port for the Splunk indexer. Then click "Next" and start the installation.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/47.jpg)

Meanwhile, we want to start downloading Sysmon, so go to the [Sysmon - Sysinternals | Microsoft Learn](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon) and download Sysmon. The Sysmon configuration that we will be using is Olaf. So go to the [GitHub - olafhartong/sysmon-modular: A repository of sysmon configuration modules](https://github.com/olafhartong/sysmon-modular)
and download the `sysmonconfig.xml` file to the target machine.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/48.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/49.jpg)

You can click "Raw" and right-click "Save as" and download the file. Next, go to the downloads directory and extract Sysmon from the zip file.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/50.jpg)

Open up a PowerShell in administrator mode and go to the location of this directory. You can copy the location from the menu bar and paste it into the PowerShell with the `cd` command.
To install Sysmon, run the command `.\Sysmon64.exe -i` with a configuration file. And since the config file that we installed is in the downloads folder, we can run this command:
`.\Sysmon64.exe -i ..\sysmonconfig.xml`

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/51.jpg)

And Sysmon will be installed shortly. And meanwhile, our Splunk Universal Forwarder is also installed.

Now is the most important part. We need to instruct our Splunk Forwarder on what we want to send over to our Splunk server. To do this, we must configure a file called `input.conf`. This file is located at
`C:\Program Files\SplunkUniversalForwarder\etc\system\default`

**But we will not edit the `input.conf` file under the default directory because the configs in this directory are there just in case we mess anything up, so we will create a new file under the local directory.**

Now, to be able to create a new file in the local directory, we need to be an administrator. So to do this, we will search for Notepad from the search bar and open it as an administrator.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/52.jpg)

Now, this is the content from the `input.conf` file that I copied here:

```
[WinEventLog://Application]
index = endpoint
disabled = false

[WinEventLog://Security]
index = endpoint
disabled = false

[WinEventLog://System]
index = endpoint
disabled = false

[WinEventLog://Microsoft-Windows-Sysmon/Operational]
index = endpoint
disabled = false
renderXml = true
source = XmlWinEventLog:Microsoft-Windows-Sysmon/Operational
```

You can copy and paste this into the new Notepad that you opened. This is instructing our Splunk Forwarder to push events related to the application, security, system, and also Sysmon to our Splunk server.

Important note: See that the index that we are pointing to is `index = endpoint`. This is important because whatever events fall under these categories will be sent over to Splunk and placed under the index "endpoint". If our Splunk server does not have an index named "endpoint", it will not receive any of these events.

After filling in the config file, save it under the local directory as we mentioned before as `inputs.conf`.
`C:\Program Files\SplunkUniversalForwarder\etc\system\local`

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/53.jpg)

Another important note: If we see that the "Log on as" line is "NT SERVICE" and double-click it, and look at the "Log On" tab from the menu

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/54.jpg)

If you see that it is using "This account" and it is "NT SERVICE\SplunkForwarder", it might not be able to collect some of the logs due to some of the permissions. So you want to select "Local System account" and hit "Apply".

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/55.jpg)

Which then will ask us to stop and restart the service, and we will do so. Just double-check on the Services menu that SplunkForwarder is "Log on as" Local System and also that Sysmon64 is running.

After finishing these steps, we can finalize our Splunk server configuration. Head over to
http://192.168.193.157:8000/ and log in with the credentials that we set during the Splunk server installation.

On the menu, we want to go to the **Indexes** from the **Settings** menu. Now recall that our index name was "endpoint" from the Splunk Universal Forwarder `inputs.conf` file. We now will create this index. Just click on the "New Index" button from the top right and enter the name "endpoint" and save.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/56.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/57.jpg)

Now you will be able to see the "endpoint" index on the list.
Next, we need to make sure that we enable our Splunk server to receive the data. In order to do that, go to **Settings > Forwarding and receiving** and under the "Receive data", click on the **Configure receiving** button, and there click on the **New Receiving Port** on the top right, and recall that during the setup, we mentioned that the default port is 9997, enter it and hit save.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/58.jpg)

Now at this point, if we set up everything correctly, we should start seeing data coming in from our target machine. Click on the **Apps** from the top left corner, and select **Search & Reporting**.
And here on the search bar, write `index="endpoint"` and click enter.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/59.jpg)

And we do see some events, and if we scroll down a little bit and see the "host" field from the left, we see that it is **TARGET-PC**. We also see some sources and sourcetypes, which is exactly what we entered in our `input.conf` file on the Target-PC.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/60.jpg)

Now it is time to do this same setup on our Active Directory (Windows Server). Also, change the name of the Windows Server machine to ADDC01.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/61.jpg)

Other than that, everything is the same as with the Target-PC, so I will not show this part here.
And after if everything is successful, you should be seeing 2 hosts like this when you search for `index=endpoint`.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/62.jpg)

## Install and Configure Active Directory

Now it is time to configure our Active Directory and then promote it to a Domain Controller. And then we will be configuring the target machine to join this domain.
Double-check the IP address of the Windows Server, and then open **Server Manager** and on the top right go to **Manager > Add Roles and Features**.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/63.jpg)

Click "Next" and on the next page, select "Role-based or feature-based installation".

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/64.jpg)

Next, you will select the server from the list, since we only have one server, there will be only one on the list, and we select and go "Next".

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/65.jpg)

On the next page, we will set the Server Roles. Here we want to select the **Active Directory Domain Services**. Click on the "Add Features" on the pop-up page and go "Next".

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/66.jpg)

From this point, click on "Next" until you get to the "Install" step, and start installing.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/67.jpg)

Click on "Close" when you see this "Installation succeeded" message.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/68.jpg)

On the top right, click on the Flag with the yellow sign and click on "Promote this server to a domain controller".

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/69.jpg)

And next, select the "Add a new forest" option because we are creating a brand new domain.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/70.jpg)

On the next page, leave everything as it is and create a password, and from this point, just click "Next" for the upcoming pages.
![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/71.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/72.jpg)

Quick note for this page: These are the paths used to store our database file named "NTDS.dit", and for your information, attackers love to target domain controllers, not only because it has access to everything but also because of this file as it contains everything related to Active Directory, including password hashes.

If you do notice any unauthorized activity towards this file, you can assume that your entire domain is unfortunately compromised.
Click "Next" a couple more times, and after all prerequisite checks have passed, click on "Install".

Once the setup is completed, the server will automatically restart.

And we will see our domain followed by a backslash, which indicates that we successfully installed ADDS and promoted our server to a domain controller.

Next step is to start creating some users, so let's log in and do just that.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/73.jpg)

On our server manager, we want to click on the **Tools** at the top right corner and select **Active Directory Users and Computers**.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/74.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/75.jpg)

And if we click on the "Builtin", we see all of the groups listed on the right side. These groups have all been automatically created by the AD, and we can double-click any of these and read the description.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/76.jpg)

And under the "Members" tab, we will see who is assigned to this group, and under the "Member Of" tab, we will see what groups this group is in.

Note: You cannot add additional groups within a built-in group, but you can create a custom group and add that built-in group to that custom group.

Now if we click on the "Users" folder, we see different users and groups in here. You can right-click and create a group or user here, but in a real-world environment, it is likely broken up into different departments, AKA organizational units, for example, HR, Finance, IT, Sales...

To mimic this, we can right-click on the domain and go under **New > Organizational Unit** and name it, for example, "IT", and click OK, and now you have a new organizational unit created.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/77.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/78.jpg)

Under this "IT" organizational unit, right-click and create a new user, and put a name and username:

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/79.jpg)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/80.jpg)

Click "Next" and create a password, and finish.

And let's create another organizational unit and create another user under it.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/81.jpg)

There are many scripts out there that can help auto-create users, groups, and computers, but for this project, it is not necessary.

Now that we have our ADDC, we will now head over to our Windows Target-PC and join it to our newly created domain called "thh.local" and authenticate using the "Jenny Smith" account.
Power up our Windows 10 machine and search for **PC > Properties > Advanced system settings**.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/82.jpg)

Under the "Computer Name" tab, click "Change" and select "Member of Domain", and write our domain name "adlab.local".

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/83.jpg)

When we click OK, we might get an error saying the domain could not be contacted. This is because the machine does not know how to resolve our domain, "thh.local", and this is how DNS works.

To fix this, go to the network adapter > change adapter options > select the adapter and right-click and go to properties and change the DNS server to our ADDC IP.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/84.jpg)

And to check the configuration is set, open a command prompt and run `ipconfig /all`.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/85.jpg

Now let's try again to join our domain. And now we are prompted to log in with some credentials.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/86.jpg

Log in with the Administrator account and password.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/87.jpg

In a real-world environment, you would create users and put them into a custom group that is authorized to allow computers to join the domain.

You will be prompted to restart the computer, and once we are on the log-on screen, we want to log in with the "Jenny Smith" account. In order to do so, we want to click on the "Other user" and make sure that our "Sign in to" is pointing to our domain, and we see that it is "THH", so we are good.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/88.jpg

## Brute Force Attack with Kali Linux
Check ip address in Kali Linux with command `ip a`

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/89.jpg

Also, ping google.com and the IP of the Splunk server to make sure that you have a connection.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/90.jpg

Next, before going with any procedure, let's update and upgrade our Kali:
`sudo apt-get update && sudo apt-get upgrade -y`

After the updates have finished, we can start setting up our attack by first creating a new directory called "ad-lab". `cd Desktop` and `mkdir ad-lab`
And all of the files that we will create and use will be put into this directory.

For our attack today, we will be using a tool called **crowbar**.
`sudo apt-get install -y crowbar`

So this is the tool that we will use to perform brute force attacks, and we can target either the domain controller or our target machine.
Now that our tool is installed, we can use the popular wordlist called "rockyou.txt" that comes with Kali Linux. You can find it under `/usr/share/wordlists`.

Unzip file with `sudo gunzip rockyou.txt.gz`
And copy the wordlist to "ad-project" directory with `cp rockyou.txt ~/Desktop/ad-project`

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/91.jpg

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/92.jpg

The wordlist's size is 134MB, which is very big, and for the purpose of this attack, we do not need this many passwords. So let's only get the first 20 lines.
And if we use this command, it will copy these 20 lines into a new file:
`head -n 20 rockyou.txt > passwords.txt`
Now, as an attacker, you would probably do a lot of reconnaissance, probably set up some basic AD attacks, and let's just say in our scenario, we know we want to target a certain password, so that's what we will do with `nano passwords.txt`.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/93.jpg

Now before we launch our attack, let's head over to our Windows target machine. On this machine, we want to enable Remote Desktop. And to do that, we want to search for "PC" and then "Properties" > "Advanced system settings". It will ask you for the admin username and password; enter them and continue. (This is the username and password for ADDC.)

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/94.jpg

On the opening page, select the "Remote" tab and then pick the **Allow remote connections to this computer** option. And then click on the **Select Users** button.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/95.jpg

Search for the names that are members of our AD group.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/96.jpg

After selecting them, click "OK" and then "Apply". And now Remote Desktop for our target machine is enabled.

Let's head back to our Kali Linux machine. And to use our tool, we'll just type `crowbar -h` to see the help menu and to see what kind of options are available for us.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/97.jpg

The service that we are interested in is RDP; this is why we are using this tool and why we enabled RDP. The command that we will use with crowbar is the following:
`crowbar -b rdp -u tsmith -C passwords.txt -s 192.168.193.155/32`

Now to explain this command:
- `-b rdp` is to select which service you want to use.
- `-u tsmith` is the username that we are targeting.
- `-C passwords.txt` is to specify the password list that we want to use.
- `-s` is to specify the IP, and we entered the target machine's IP.
- `/32` is to specify that this is only 1 IP address.

Specifying the subnet mask or CIDR notation, especially in network configurations, helps avoid ambiguity and ensures that the intended network size and address range are clearly understood.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/98.jpg

It actually starts and tries every password on the list. And from the result, we can see that we have an RDP success with the username "tsmith" and password "Password1!".

Now let's head over to Splunk and see what telemetry we had generated.
In Splunk, go to "Search & Reporting". Because we know when the attack occurred, let's filter it out by the last 15 minutes. And also, we know the targeted user was "Terry Smith". By using these, let's narrow down our search.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/99.jpg

Now on the left side, we have interesting fields. And if we look at "# EventCode", we see that an event ID of 4625 occurred 20 times. Let's search this event ID to see what that is.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/100.jpg

So this means that there were 20 failed attempts to log in to Adam's account, which is correct because if you recall, there was a total of 21 passwords in the "passwords.txt" file, of which 20 were incorrect.
Let's filter down the EventCode 4625 by clicking on it.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/101.jpg

Now when you see the times of these 20 events, you will see that all these events are happening pretty much at the same time, which can be a clear indication of brute force activity.
Now if we look at the EventCode 4624, you will see only one event.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/102.jpg

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/103.jpg

Now let's expand the log by clicking on "Show all 70 lines" and scroll down a bit.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/104.jpg

We do happen to see our workstation name as "Kali" and the IP address it is trying to log in from, and this does indeed belong to our Kali Linux machine.

## Testing with Atomic Red Team
Atomic Red Team is an open-source project that provides a library of small, discrete tests to simulate real-world attack techniques as defined by the MITRE ATT&CK framework. These tests help security teams evaluate and improve their detection and response capabilities by identifying gaps in their defenses. The tests are easy to use, well-documented, and can be tailored to fit various environments.

Now let's install Atomic Red Team on our target machine and run some tests on it.
Let's open a PowerShell with administrator privileges and then run the following command:
`Set-ExecutionPolicy Bypass -Scope CurrentUser`, then enter "Y" to confirm.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/105.jpg

Now before installing Atomic Red Team on this PC, let's set an exclusion for the entire C drive because Microsoft Defender will detect and remove some of the files of Atomic Red Team.
Go to Windows Security > Virus & threat protection > Manage Settings > Exclusions.
Then click on the "Add an exclusion" button > "Folder" and select our C drive.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/106.jpg

And you should be able to see "C:/" under the exclusions now. And we can now install Atomic Red Team by using these two commands:
`IEX (IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing);`
and then
`Install-AtomicRedTeam -getAtomics`
Enter "Y" when prompted.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/107.jpg

After installation, go into the C drive, and inside the "AtomicRedTeam" directory, there is an "atomics" folder. Here we see a bunch of technique IDs, and these map back to the MITRE ATT&CK framework. When we go to [MITRE ATT&CK®](https://attack.mitre.org/), all of these techniques have a unique ID.

Check on the MITRE ATT&CK website, we see that 001 is for Local, 002 is for Domain, and 003 is for Cloud Account.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/108.jpg

In this example, let's go ahead and use the first one, T1136.001.
To do this, we go back to PowerShell and write this command:
`Invoke-AtomicTest T1136.001`
and this will automatically generate telemetry based on creating a local account.

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/109.jpg

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/110.jpg

And now that our command has finished running, we can go and look into Splunk and search specifically for "new local user".

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/111.jpg

And we observed 12 raw events related to the activity. This confirms that our monitoring setup is capturing relevant data for this type of attack technique. The detailed logging will help us analyze and improve our detection and response capabilities.
Let's try another one, "T1059: Command and Scripting Interpreter".

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/112.jpg

Let's go with PowerShell, which is T1059.001.

Running this code, Defender catches a couple of things, and let's see what is going on with Splunk.

Run the search with `index=endpoint powershell`, and we see that 523 events occurred in the last 15 minutes. And for example, when we check this event:

![image](https://github.com/grapitycreation/Active-Directory-Project/blob/main/Images/113.jpg

We actually see that this event indicates that the PowerShell executable (`powershell.exe`) running under the `ADLAB\Administrator` account modified a registry value. Specifically, the registry key `HKLM\System\CurrentControlSet\Services\bam\State\UserSettings` was altered. The `bam` registry key typically relates to the Background Activity Moderator, which Windows uses to manage app background activity.

The event captured shows the simulated attack test (T1059.001) modifying a registry value using PowerShell. It indicates that our Sysmon configuration is capturing relevant events, which is crucial for detecting and responding to such activities. Review the surrounding events for a complete picture and ensure your detection mechanisms in Splunk are tuned to catch and alert on such activities.

## Conclusion
In this project, we set up an Active Directory environment, installed and configured Splunk to ingest logs from our Windows machines, performed a brute force attack using Kali Linux, and tested our detection capabilities using Atomic Red Team.
Key takeaways:
- Setting up an Active Directory environment allows us to understand how user and computer management works in an enterprise setting.
- Splunk is a powerful tool for collecting, indexing, and analyzing machine-generated data, which is essential for security monitoring and incident response.
- Brute force attacks are a common threat, and it's crucial to have mechanisms in place to detect and prevent them.
- Atomic Red Team provides a practical way to test our detection and response capabilities against real-world attack techniques.
- Continuous monitoring, tuning, and improvement of our security controls are necessary to stay ahead of evolving threats.
By going through this project, we have gained hands-on experience in setting up and securing an Active Directory environment, as well as leveraging Splunk for security monitoring. This knowledge will be valuable in real-world scenarios where securing and monitoring Windows environments is critical.
































