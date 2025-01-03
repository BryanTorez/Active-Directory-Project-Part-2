<h1>Active Directory Project (Home Lab) | Part 2
</h1>

<p align="center">
<img src="https://snipboard.io/Y2tWKl.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h2>Description</h2>
<br />
<p align="center">
Welcome to part two of five for the series on the active directory project. If you haven't seen part one where we go over how to build a diagram for this lab I highly recommend that you go and see that. I will be referencing that diagram throughout this five-part series. 
<br />
<br />
<img src="https://snipboard.io/xSDvyl.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
  Today our objective is to install our virtual machines on Virtual Box. By the end of this part, you should have a Windows 10 machine, one Kali Linux, one Ubuntu server, and one Windows Server 2022. As a quick side note, you will have to create these in the cloud if you are running M1, M2, or M3 Mac. Previously we used Digital Ocean, however, it did cause some issues when trying to connect or spin up Windows so instead, I would highly recommend you use either Vultur or Microsoft Azure. I'll leave a link down below for those who want to sign up with Vultur to get $100 free credit.
<br />
<br />
<img src="https://snipboard.io/ZXMbKL.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
An Active Directory is simply a database that contains users, computers, groups, and many more. To use the active directory, a server must install a service called Active Directory Domain Services, and the server must then be promoted to a domain controller. By promoting our server to a DC, it will grant us the capability to perform an authentication using a protocol called Kerberos and Authorization for our domain. 
<br />
<br />
<img src="https://snipboard.io/WDkzcf.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
 With AD DS, we will have a database that will contain objects such as users, computers, groups, and many more, as previously mentioned. These objects will contain attributes which are information about the object. For example, an object user "Bob" may contain the attribute of Bob's first and last name. That is a quick overview of our virtual machine.
<br />
<br />
<img src="https://snipboard.io/lI0EOB.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/EftopT.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/qEMmVH.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
 We will be using Windows 10 as our target machine, Kali Linux for the attacker machine, Windows Server 2022 for the active directory, and Ubuntu Server 22.04 for Splunk. Now I will be hosting all of these virtual machines on Virtual Box, but you can always use the cloud. If you aren't sure how to install Virtual Box with both Windows 10 and Kali, I'll help you go through that right now.
<br />
<br />
<img src="https://snipboard.io/Aj9i73.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
First, we'll begin with installing Virtual Box by heading over to their site virtualbox.org. Now depending on the operating system you have, that is the one that we're going to be downloading. So we can go ahead and click "Download Virtual box 7.0". From here we know that this machine that I'm using is a Windows host machine. So I'll go ahead and click download on that.
<br />
<br />
<img src="https://snipboard.io/UI5jnJ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/vRyPaF.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
While that's downloading, we can go ahead and check out the sha256 checksums as well. When you go into the check sums, it will provide you with a list of Sha256 hashes and then this way we can verify the downloaded file to determine whether or not it has been altered, so let's go ahead and do that.
<br />
<br />
<img src="https://snipboard.io/YnaVLJ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/sDXpNK.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
We'll head over to the downloads directory in which our file lives. We'll open Powershell, and then I'll type "Get-FileHash .\VirtualBox-7.0.10-158379-win.exe". click on "enter" and by default, sha256 is generated. What we can do is double-click that and then we can paste it in and see if it matches up.
<br />
<br />
<img src="https://snipboard.io/kcr6uZ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/hwWum5.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/AswC4k.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So we know for a fact that the file in transit was not changed whatsoever. Now we can go ahead and double-click Virtual Box to start installing it. Now we might get hit with a compatibility issue or missing some software dependencies, but we'll deal with that when the time comes.
<br />
<br />
<img src="https://snipboard.io/52Du4m.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/sQciaO.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Click on "yes" and from here we notice that there is a "Microsoft Visual C++ 2019" package dependency. So what we'll do is go ahead and install this dependency. I'll put the link down in the description below just in case that you get hit with this dependency as well.
<br />
<br />
<img src="https://snipboard.io/EwzZeW.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/gEqVrn.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I went ahead and downloaded the dependency and installed it, so now we can go ahead and double-click the Virtual Box installer again. Hit "yes" and now it doesn't give me that dependency error anymore.
<br />
<br />
<img src="https://snipboard.io/7kx9Kd.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/zASBXW.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/V12GXh.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
We are presented with some of the features which we can install and they are all set to be installed by default, but you do have the option to customize it; which is quite nice.
<br />
<br />
<img src="https://snipboard.io/P3pCOK.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Here you can change where you want Virtual Box to be installed in. For example, if you don't have enough space in the "C" drive, you can always install it in a different drive if you like, but in this case, we'll go with the default and hit "Next".
<br />
<br />
<img src="https://snipboard.io/pRxMsE.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
This will provide you with a warning that it will reset your network connection and temporarily disconnect you. Hit "Yes" and install the needed dependencies. Once it's done installing, you should see this sign and all you have to do is click on "Finish". Now Virtual Box should automatically pop up.
<br />
<br />
<img src="https://snipboard.io/lvEmNW.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/HGV8aw.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/vGMXCs.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
We'll navigate to the link which I'll list down in the description for you and once we're on the page, we can go ahead and scroll down and click on "Download tool now". This will download what is called a media creation tool which will help you generate a Windows ISO image file.
<br />
<br />
<img src="https://snipboard.io/aViWcY.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So we can go ahead and double-click that to open the file. Click on "yes" and now it will get a few things ready. You'll eventually be presented with this license agreements page and we can go ahead and hit "Accept". It will say getting a few things ready again.
<br />
<br />
<img src="https://snipboard.io/DZ1ruK.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/decRMS.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/8pAQwT.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Once it's done checking things, you should be presented with a screen displaying two options. One to upgrade your PC, or two, to "create an installation media". What we want to select is "Create the installation media" and hit "Next".
<br />
<br />
<img src="https://snipboard.io/d7RlA3.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
You have the option to customize your settings such as language, edition, and architecture, but I'll leave mine checked to use the recommended option for this PC. Hit "Next". Now we are presented with two media choices, to use a USB flash drive or an ISO file. We'll select the ISO file. Hit "Next" and save the ISO file anywhere you like.
<br />
<br />
<img src="https://snipboard.io/wWdTvu.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/WG6K20.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So now that my Windows ISO image has been successfully downloaded, we can now jump over to our Virtual Box and start creating a virtual machine. We'll open up the window for Virtual Box and click on "New". We can enter a name for a virtual machine and select the directory where we want to store our files.
<br />
<br />
<img src="https://snipboard.io/SJPA60.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So I'll go ahead and name our virtual machine "demo". I'll leave the folder as it is for the iso image. I'll click on this and select the drop down. Click on "Other" and now I'll find the iso image that I just downloaded. It was listed under "Document" and double-click the windows ISO.  
<br />
<br />
<img src="https://snipboard.io/1QyxeE.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
At the bottom there's an option where you can check skip unintended installation, which I will do. That way I can install the operating system manually. Now you can uncheck this or check this it's up to you. I'll click on "Next". Here we have the option to configure our virtual machine specifications. However, do be aware that this will be relying on your computer's specifications for this demo.
<br />
<br />
<img src="https://snipboard.io/G4q6dz.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/l9ukRK.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I'll set my base memory for this virtual machine as 4 gigs and we'll have it as one CPU. I'll click on "Next". For the virtual hard disk, I'll leave it as 50 gigs and hit "Next". Now this will give you a nice summary as to what your settings are for this virtual machine. 
<br />
<br />
<img src="https://snipboard.io/AGVEuB.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/h08rNS.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/ykCxNT.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
If you're good to go, click on "Finish" and now we can go ahead and start powering it on. To power it on, you just hit this arrow that says "Start". Now once it's running, we should be able to start seeing this Windows 10 setup. So we'll go ahead and select "Next" and hit "Install now".
<br />
<br />
<img src="https://snipboard.io/OBFYhs.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/7Camch.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/Iqub7C.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Once you're presented with this activated Windows screen, go ahead and select "I don't have a product key", and as for the option select "Windows 10 Pro". Hit "Next", and accept the license terms. Here you have the option to upgrade, or custom install Windows only. I'm going to select "Custom: Install Windows only".
<br />
<br />
<img src="https://snipboard.io/3K8nRq.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/HXeDPJ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/IYSL3x.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Hit "Next" and now Windows 10 should be installed in the background. To install Kali, we want to head over to their site "Kali.org". Once we're on their site, we want to click on "Download" and we'll be presented with a bunch of different options.
<br />
<br />
<img src="https://snipboard.io/Le9Dov.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/k8WKOA.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/EZ1q3s.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
The nice thing about Kali is that they have a pre-built virtual machine that we can download and import into our own Virtual Box, which is what we'll do now. You do have the option to go ahead and manually download Kali Linux via an ISO file, similar to how we did it with Windows 10. Let's go and download the pre-built virtual machine.
<br />
<br />
<img src="https://snipboard.io/5tmfOd.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/JBysPM.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I'll be downloading the 64-bit version of Kali, but if you have a 32-bit machine, select the 32-bit. To check whether or not you have a 32 or 64-bit machine, you can click on the Windows key and type in "System Information. From here, you can take a look at your system type. In my case, it's an 'x64' meaning it's a 64-bit.
<br />
<br />
<img src="https://snipboard.io/ocaLCM.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/eJhYjo.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/NxuzhP.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/OVp18x.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Another way to look at it is if you click on the File Explorer. Then open up your directories. Click on the "C drive". If you happen to notice two individual directories, your program files, and a program file x86, that's another telltale sign that your computer is a 64-bit computer. Now if you only have one of these directories, it is likely your computer is a 32-bit machine.
<br />
<br />
<img src="https://snipboard.io/92CzgY.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Looking at the download for Kali Linux, I noticed that it is a seven-zip file extension. Meaning that if you don't have seven-zip installed on your machine, I would highly recommend it to install 7zip.
<br />
<br />
<img src="https://snipboard.io/sVHlwO.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
We'll go ahead and navigate to their website 7-zip. Take a look at your architecture, if it's a Windows 64-bit machine or 32-bit machine, download the appropriate one for you. In my case, it's a 64-bit machine, so I'll go ahead and download that. Once that is downloaded, I'll go ahead and install it.
<br />
<br />
<img src="https://snipboard.io/BiLAfl.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Kali has finished downloading and there is one thing I forgot to mention, and that is the default credentials. To log into Kali Linux, the default credentials is the username "Kali" and the password "Kali" as well. Let's head over to our our downloads folder and now since we have seven zip installed, we can go ahead and right-click the Kali Linux archive.
<br />
<br />
<img src="https://snipboard.io/cBqIpm.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/qfI7oU.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Go to 7-zip and click on "Extract to" directory. Now that it is done extracting, let's head into that folder. All you need to do is double-click on the ".vBox" file. If you don't see the file extension, you can simply click on "View" and check "File name extensions". Once we do that, we can now see the vbox file extension.
<br />
<br />
<img src="https://snipboard.io/wElJM6.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/KadxYP.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/zxPXIq.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/QTZYg6.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Once we double-click that, it should automatically be imported into our virtual box. So we can go ahead and start Kali and when you're on the log-on screen just remember to log in with "Kali" and "Kali" as the password. Once you have virtual box installed, along with Windows 10 and Cali Linux, we can now begin installing our Windows Server.
<br />
<br />
<img src="https://snipboard.io/KyJ9wq.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Over to Google, we want to search up "Windows Server 2022 ISO" and we want to select "Windows Server 2022 Microsoft Evaluation Center". This is where we will download our ISO file by clicking on "Download the ISO". Then we need to fill in the information. Once you fill in the information, you should be presented with this screen.
<br />
<br />
<img src="https://snipboard.io/mrs7GY.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/KMpEj4.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/8O1Y0b.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/jT9inY.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
The next thing to do is click on 64-bit Edition under "ISO Downloads" and depending on your speeds, this might take a while. However, once the ISO is finished downloading, we then want to start adding this onto our virtual machine. To do this, we want to click on the "NEW" icon and then provide your virtual machine with a name.
<br />
<br />
<img src="https://snipboard.io/jT9inY.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/1sunD0.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I will call it "ADDC01" and then for the "Folder", you can select the folder of where you want to open your virtual machine. As for the iso image, we want to select the one that we just downloaded and we want to leave all of this as default. I will select skip unintended installation because I don't want Virtual Box to automatically install this as I have experienced some errors in the past when I was using it.
<br />
<br />
<img src="https://snipboard.io/SrqkED.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/iDRVQc.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/mfHW1k.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now under the "Hardware" tab, it is set to 2 gigs by default. So I will actually change this over to four. Now this might be a little slow, but that is okay, as long as it works and if you have a computer that only has 8 gigs of RAM. For example, I would recommend you shut off all of your virtual machines and install them one at a time.
<br />
<br />
<img src="https://snipboard.io/TZV2RF.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Once everything is installed, then you want to change your specs back to 2 gigs, instead of four. As this will help you save some resources, but in the beginning stay with 4 gigs until everything is installed. As for "Hard Disk", I am going to leave it as 50 gigs because I think that's good enough and I will select "Finish".
<br />
<br />
<img src="https://snipboard.io/aSuXw4.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now we can go ahead and just hit "Start". So once the virtual machine is booted up, you'll see the setup and I will leave it as default. Hit "Next" and select "Install Now". As for the operating system you want to install, you want to select the second option which is "Windows Server 2022 Standard Evaluation (Desktop Experience)".
<br />
<br />
<img src="https://snipboard.io/zoJc7r.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/c5uGEM.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/GK4v2q.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
If you don't select, that you'll just get a CLI, a command line interface, and it can be pretty tough to navigate around it so make sure you select the second option. Then hit "Next" and accept the terms and agreements. Now we want to select "Custom" and hit "Next".
<br />
<br />
<img src="https://snipboard.io/IuTHzZ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/iRr7gS.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now this will take its time and install Windows Server 2022 on onto our virtual machine. All right, so this took about 10 minutes and after the setup is completed you should be presented with this screen to create your own password. I'll type in a super secure password and then I'll click on "Finish".
<br />
<br />
<img src="https://snipboard.io/cDeL9u.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/b1tNvR.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
After a couple seconds, we can now start to log in using the username "administrator" and the password that we had just set. As an FYI, to perform a cntrl+alt+delete onto your virtual machine because it does say, "Hey, press cntrl+alt+delete to unlock." We can do this by selecting the "Input" tab at the top. Go over to "Keyboard" and click "Insert Ctrl+Alt+Del".
<br />
<br />
<img src="https://snipboard.io/IGa1AD.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/EyjIH8.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
We'll log in with the password that we just created and once we log in we can just go ahead and select "No" for now. We'll see an application called "Server Manager". Which is what we'll use to install our active directory, but that will be in part four of the series.
<br />
<br />
<img src="https://snipboard.io/BvCuE7.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/ubAaR6.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/4wMQnX.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now that we have our Windows target machine, Kali Linux, and Windows Server installed, the last thing to do is install our Splunk server. Over to our web browser, let's head over to "ubuntu.com" and under "Products" we want to select "Ubuntu Server". 
<br />
<br />
<img src="https://snipboard.io/czxAWs.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now we can click on "Download Ubuntu Server" and as of creating this project, the version that we are downloading is "Ubuntu server 22.04.3". Now this version might be different depending on when you are reading this form, but as long as you download any form of '22.04.03', you should be fine.
<br />
<br />
<img src="https://snipboard.io/hFKqjW.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/3E6QFZ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I'll go ahead and select that. Now, your download should begin. Of course, if your download doesn't start, you can just click "download now." Similar to how we downloaded other virtual machines on Virtual Box, we want to go ahead and select "New". I'll name our server "Splunk" and our folder should be under our active directory folder.
<br />
<br />
<img src="https://snipboard.io/l9mH7N.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/719YGH.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
For the ISO Image, we want to select the one we just downloaded. Then we'll leave everything as default, but click on "Skip Unattended Installation". As for Hardware, I am going to set this to 8 gigs, but again depending on your hardware specs, you can set this to four. 
<br />
<br />
<img src="https://snipboard.io/LrJeKC.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/A90vra.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/qAzahZ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I'll also select my processors to two since we want to make Splunk a little beefier compared to our other virtual machines because this is going to be ingesting data and we'll be running searches on it. For our hard disk, I'll go ahead and bump this over to 100 gigs and hit "Finish".
<br />
<br />
<img src="https://snipboard.io/dwkDex.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/1GaulV.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, we can go ahead and power it on by clicking on "Start". Once you're presented with the screen, go ahead and select the first option which is "Try or Install Ubuntu Server". For the options, I'll leave it as default and continue hitting "Enter". 
<br />
<br />
<img src="https://snipboard.io/pwkhAX.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/BhnQd5.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/YELyCo.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Perfect, so now we want to select "Continue" and with the guided storage configuration, we need to use the down arrow to go over to "Done". Click "Done", and click "Continue". Finally, we are presented with the options to enter in your name, your username, and password.
<br />
<br />
<img src="https://snipboard.io/TEgOGP.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/x7JeFv.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/tabdSQ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
For my name, I'll just select "Bob". For the server name, I'm going to say "Splunk". For the username, I'll say "mydfir", and for the password, make it super secure. Then hit "Done". Now, we don't need Ubuntu Pro so we can go ahead and skip that for now, and open SSH. It is up to you if you want to install it, I'm just going to skip it.
<br />
<br />
<img src="https://snipboard.io/9xYkaM.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/9xYkaM.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/BAthRX.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
We don't need any of these options so scroll down and hit "Done". Now our setup is going to start installing Ubuntu Server onto our virtual machine. So you know when your installer is completed after you see a "Reboot now" option. So we'll go ahead and select that and hit "Enter".
<br />
<br />
<img src="https://snipboard.io/TWBC10.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/8MJVeB.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/68Uoec.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
You will get an error saying "Failed unmounting /cdrom", but don't worry, we can simply hit "Enter". If you want, you can go ahead and remove the ISO file, but again I'll just leave it as it is. Once Ubuntu finishes up with its reboot, we are now presented with a log-on screen. 
<br />
<br />
<img src="https://snipboard.io/gZuI4M.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/CFeduj.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
We'll use the account that we just created earlier, so in my case, it is "mydfir" and of course the password. If this is your first time doing this, you might notice that when typing in a password you don't see any input. Don't worry, this is by design. It is not shown for security purposes, but do note if you do make a mistake just go ahead and hit backspace to remove everything or you can go ahead and hit "Enter" to reset everything and then try logging in again.
<br />
<br />
<img src="https://snipboard.io/CFeduj.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I'll type in "mydfir" and my password. Once we're logged in, let's run a quick "sudo apt-get update && sudo apt-get upgrade -y". It'll ask for my password again. Using this command, we'll go out and update and upgrade all of our repositories. Once you are presented with this screen, you can go ahead and hit "Enter" and now our server is ready to go.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
We should have a total of four virtual machines ready to go and in part three we will start to install Sysmon and Splunk onto our target machine and server. That is it for this part and I hope this has been helpful for you so far. Remember to stay curious and do things differently
