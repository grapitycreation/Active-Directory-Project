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



















