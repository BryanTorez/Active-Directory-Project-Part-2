<h1>SOC Automation (Home Lab) - Part 1</h1>

<p align="center">
<img src="https://snipboard.io/6rb2ue.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h2>Description</h2>
<br />
<p align="center">
welcome to part two of five for the series on the active directory project if you haven't seen part one where we go over on how to build out a diagram for this lab I highly recommend that you go and watch that as I will be referencing that diagram throughout this five-part series today our objective is to install our virtual machines on Virtual Box by the end of the video you should have W Windows 10 machine one Cali Linux one yuntu server and one Windows Server 2020 22 as a quick side note if you are running M1 M2 or M3 Mac you will have to create these in the cloud and previously we used digital ocean however it did cause some issues when trying to connect or spin up windows so instead I would highly recommend you use either vulture or Microsoft Azure I'll leave a link down below for those who want to sign up with vulture and you'll get a free $100 credit if you use that link for those that don't know what act active What is Active Directory directory is here is a quick highle overview active directory is simply a database that contains users computers groups and many more in order to use active directory a server must install a service called active directory domain services or adds and the server must then be promoted to a domain controller AKA DC by promoting our server to a DC it will grant us the capability to perform a authentication using a protocol called keros and authorization for our domain with adds we will have a database that will contain objects such as users computers groups and many more as previously mentioned and these objects will contain attributes which is information about the object for example an object user AB Bob may contain the attribute of Bob's first and last name that is a highle overview for our virtual machine we will be using using Windows 10 as our Target machine Cali Linux for the attacker machine Windows Server 2022 for active directory and Ubuntu server 22.041 and Cali I'll replay a previous video that I've done to show you otherwise feel free to skip ahead all right so first we'll begin with installing virtual Box by heading over to their site virtualbox.org now depending on the operating system you have that is the one that we're going to be downloading so we can go ahead and click download Virtual box 7.0 from here we know that this machine that I'm using is a Windows host machine so I'll go ahead and click download on that while that's downloading we can actually go ahead and check out the shaw 256 check sums as well when you go into the check sums it will provide you with a list of Shaw 256 hashes and then this way we can verify the downloaded file to determine whether or not it has been altered so let's go ahead and do that we'll head over to the downloads directory in which our file lives in we'll open Powershell and then I'll do a get file hash virtual box hit tab click on enter and by default sha 256 is generated what we can do is double click that and then we can paste it in and see if it matches up so we know for a fact that the file in transit was not changed whatsoever now we can go ahead and double click virtual box to start installing it now we might get hit with a compatibility issue or missing some software dependencies but we'll deal with that when the time comes click on yes and from here we notice that there is a Microsoft Visual C++ 2019 package dependency so what we'll do is we'll go ahead and install this dependency and I'll put the link down in the description below just in case that you get hit with this dependency as well I went and downloaded the dependency and installed it so now we can go ahead and double click the virtual box installer again hit yes and now it doesn't give me that dependency error anymore we are presented with some of the features which we can install and they are all set to be installed by default but you do have that option to customize it which is quite nice here you can change where you want virtual box to be installed in for example if you don't have enough space in the C drive you can always install it in a different drive if you like but in this case we'll go with the default and hit next this will provide you with a warning that it will reset your network connection and temporarily disconnect you he hit yes and install the needed dependencies once it's done installing you should see the sign all you got to do is click on finish and then virtual box should automatically pop up and just like that we'll navigate to the link which I'll list down in the description for you and once we're on this page we can go ahead and scroll down and click on download tool now this will download what is called a media creation tool which will help you generate a Windows ISO image file so we can go ahead and double click that to open the file click on yes and now it will get a few things ready you'll eventually be presentedcwith this license agreements page and we can go ahead and hit accept it will say getting a few things ready again once it is done checking things you should be presented with this screen now displaying two options one to upgrade your PC or two create an installation media what we want to select is create the installation media and hit next you have the option to customize your settings such as language addition and architecture but I'll leave mine checked to use the recommended option for this PC and hit next now we are presented with two media choices to use a USB flash drive or an ISO file we'll select the ISO file and hit next and save the ISO file anywhere you like and it will start downloading so now that my windows ISO image has been successfully downloaded we can now jump over to our virtual box and start creating a virtual machine we'll open up the window for virtual box and click on new here we can enter a name for a virtual machine and select the directory where we want to store our files so I will go ahead and name our virtual machine demo I'll leave the folder as is as for the iso image I will click on this and select the drop down click on other and now I'll find the iso image that I just downloaded it was listed under document and double click the windows ISO at the bottom there's an option where you can check skip unintended installation which I will do actually that way I can install the operating system manually now you can uncheck this or check this it's up to you I'll click on next here we have the options to configure our virtual machine specifications however do be aware that this will be relying on your computer's specifications for this demo I'll set my base memory for this virtual machine as 4 gigs and we'll have it as one CPU I'll click on next for the virtual hard disk I'll leave it as 50 gigs and hit next now this will give you a nice summary as to what your settings are for this virtual machine if you're good to go click on finish and now we can go ahead and start powering it on to power it on you just hit this arrow that says start now once it's running we should be able to start seeing this Windows 10 setup so we'll go ahead and select next and hit install now once you're presented with this activate Windows screen go ahead and select I don't have a product key and as for the option select Windows 10 Pro hit next accept the license terms and here you have the option to upgrade or custom install Windows only I'm going to select custom install Windows only hit next and then now Windows 10 should be installing in the background to install Cali we want want to head over to their site cali.org once we're on their site we want to click on download and we'll be presented with a bunch of different options the nice thing about Cali is that they have a pre-built virtual machine which we can download and import into our own virtual box which is what we'll do now you do have the option to go ahead and manually download Cali Linux via an ISO file similar to how we did it with Windows 10 let's go and download the pre-built virtual machine I'll be downloading the 64-bit version of Cali but if you have a 32-bit machine you'll have to select the 32-bit and to do that you click on the 32-bit option here but I'll be going to the 64-bit and downloading the virtual box 64 to check whether or not you have a 32 or 64 bit machine you can click on the Windows key and type in system click on the system in information and from here you can take a look at your system type in my case it's an x64 meaning it's a 64-bit another way to look at it is if you click on the file explorer so open up your directories click on the C drive if you happen to notice two individual directories so your program files and a programs files x86 that's another Telltale sign that your computer is a 64-bit computer now if you only have one of these directories it is likely your computer is a 32-bit machine looking at the download for Cali Linux I noticed that it is a seven zip file extension meaning that if you don't have seven zip installed on your machine yet I would highly recommend it to install 7zip we'll go ahead and navigate to their website 7-zip. take a look at your architecture if it's a Windows 64-bit machine or 30 32bit machine download the appropriate one for you in my case it's a 64-bit machine so I'll go ahead and download that once that is downloaded I'll go ahead and install it and it's installed perfect C has finished downloading and there is one thing I forgot to mention and that is the default credentials to log into Cali Linux the default credentials is the username C and the password c as well let's head over to our our downloads folder and now since we have seven zip installed we can go ahead and rightclick the Cali Linux archive go to szip and click on extract to directory now that it is done extracting let's head into that folder and all you need to do is doubleclick on the vbox file if you don't see the file extension you can simply click on view and check file name extension once we do that we can now see the vbox file extension and once we double click that it should automatically be imported into our virtual box so we can go ahead and start Cali and when you're on the log on screen just remember to log in with C and C as the password once you have virtual box installed along with Windows 10 and Cali Linux we can now begin installing our Windows Server over to Google we want to search up Windows Install Windows Server Server 2022 ISO and we want to select the Windows Server 2022 Microsoft evaluation center this is where we will download our ISO file by clicking on download the iso and then we need to fill in the information once you fill in the information you should be presented with the screen the next thing to do is click on 64-bit Edition under ISO downloads and depending on your speeds this might take a while however once the iso is finished downloading we then want
13:03
to start adding this onto our virtual
13:05
machine to do this we want to click on
13:07
the new icon and then provide your
13:10
virtual machine with a name I will call
13:12
it add
13:14
dc01 and then the folder you can select
13:16
the folder of where you want to Output
13:18
your virtual machine as for the iso
13:20
image we want to select the one that we
13:22
just downloaded and we want to leave all
13:24
of this as default but I will select
13:27
skip unintended installation because I
13:30
don't want virtual box to automatically
13:32
install this as I have experienced some
13:35
errors in the past when I was using it
13:37
now under the hardware tab it is set to
13:39
2 gigs by default so I will actually
13:42
change this over to four now this might
13:45
be a little slow but that is okay as
13:47
long as it works and if you have a
13:49
computer that only has 8 gigs of RAM for
13:51
example I would recommend you shut off
13:53
all of your virtual machines and install
13:55
them one at a time once everything is
13:58
installed
13:59
then you want to change your specs back
14:01
to 2 gigs instead of four as this will
14:04
help you save some resources but in the
14:07
beginning stay with 4 gigs until
14:08
everything is installed as for hard disk
14:11
I am going to leave it as 50 gigs
14:14
because I think that's good enough and I
14:16
will select finish now we can go ahead
14:18
and just hit start so once the virtual
14:21
machine is booted up you'll see the
14:23
setup and I will leave it as default and
14:26
hit next and select install now as for
14:30
the operating system you want to install
14:32
you want to select the second option
14:34
which is Windows Server 2022 standard
14:37
edition desktop experience if you don't
14:39
select that you'll just get a CLI a
14:41
command line interface and it can be
14:43
pretty tough to navigate around it so
14:45
make sure you select the second option
14:48
and then hit next accept the terms and
14:50
agreements and we want to select custom
14:53
and hit next now this will take its time
14:56
and install Windows Server 2022 on onto
14:59
our virtual machine all right so this
15:00
took about 10 minutes and after the
15:03
setup is completed you should be
15:05
presented with this screen to create our
15:07
own password now of course I will type
15:10
in a super secure password and then I'll
15:13
click on finish after a couple seconds
15:16
we can now start to log in using the
15:18
username administrator and the password
15:21
that we had just set as an FYI to
15:23
perform a control alt delete onto your
15:26
virtual machine because it does say hey
15:28
press control alt delete to unlock we
15:30
can do this by selecting the input tab
15:33
at the top go over to keyboard and
15:35
insert control alt delete or you can use
15:38
the shortcut key that is listed over
15:40
here we'll log in with the password that
15:42
we just created and once we log in we
15:45
can just go ahead and select no for now
15:47
and we'll see an application called
15:49
server manager which is what we'll use
15:52
to install our active directory but that
15:54
will be in part four of the series now
15:57
that we have our Windows Target machine
16:00
Cali Linux and Windows Server installed
16:03
the last thing to do is install our
16:06
Splunk server over to our web browser
Install Splunk Server
16:08
let's head over to ubuntu.com and under
16:11
products we want to select Ubuntu Server
16:14
now we can click on download Ubuntu
16:16
server and as of recording the version
16:18
that we are downloading is Ubuntu server
16:27
22.04.2012 any form of
16:58
but of course we want to skip the
17:00
unintended installation as for Hardware
17:03
I am going to set this to 8 gigs but
17:06
again depending on your hardware specs
17:08
you can set this to four and I'll also
17:11
select my processors to two we want to
17:14
make Splunk a little beefier compared to
17:16
our other virtual machines because this
17:18
is going to be ingesting data and we'll
17:20
be running searches on it for our hard
17:23
disk I'll go ahead and bump this over to
17:24
100 gigs and hit finish now we can go
17:28
ahead and Power It On by clicking on
17:30
start once you're presented with the
17:31
screen go ahead and select the first
17:33
option which is try or install UB buntu
17:36
server for the options I'll leave it as
17:38
default and continue hitting enter
17:40
continue without updating that's fine
17:43
done done done done and done perfect so
17:49
now we want to select continue and with
17:51
the guided storage configuration we need
17:54
to use the down arrow to go over to done
17:56
click done and go into to continue
17:59
finally we are presented with the
18:01
options to enter in your name your
18:03
username and password for my name I'll
18:05
just select Bob the server name I'm
18:06
going to say Splunk the username I'll
18:09
say my dfir and the password make it
18:12
super secure and hit done now we don't
18:15
need Ubuntu Pro so we can go ahead and
18:17
skip that for now and open SSH it is up
18:21
to you if you want to install it I'm
18:23
just going to skip it and we don't need
18:25
any of these options so scroll all the
18:27
way down and hit done now our setup is
18:30
going to start installing Ubuntu Server
18:33
onto our virtual machine so you know
18:35
when your installer is completed after
18:37
you see a reboot now option so we'll go
18:40
ahead and select that and hit enter you
18:42
will get an error saying failed
18:44
unmounting CD ROM but don't worry we can
18:48
simply hit enter and if you want you can
18:50
go ahead and remove the ISO file but
18:52
again I'll just leave it as is once
18:55
Ubuntu finishes up with its reboot we
18:57
are now presented with a loog loog on
18:58
screen and we'll use the account that we
19:00
just created earlier so in my case it is
19:03
my dfir and of course the password if
19:06
this is your first time doing this you
19:08
might notice that when typing in a
19:10
password you don't see any input and
19:12
don't worry this is by design it is not
19:14
shown for security purposes but do note
19:17
if you do make a mistake just go ahead
19:19
and hit backspace to remove everything
19:21
or you can go ahead and hit enter to
19:23
reset everything and then try Rel
19:25
logging in again I'll type in my dfir
19:28
and and my password once we're logged in
19:31
let's run a quick pseudo AP get update
19:36
and PSE sudo apt get upgrade Dy and hit
19:41
enter It'll ask for my password again
19:44
using this command will go out and
19:46
update and upgrade all of our
19:48
repositories once you are presented with
19:50
this screen you can go ahead and hit
19:52
enter and now our server is ready to go
19:55
we should have a total of four virtual
19:57
machines ready to go and in part three
19:59
we will start to install cismon and
20:02
Splunk onto our Target machine and
20:04
server and that is it for the video I
20:07
hope this has been helpful for you so
20:08
far and if you stumbled across any
20:10
errors along the way leave it in the
20:13
comment section down below remember to
20:16
stay curious and do things
20:21
differently
