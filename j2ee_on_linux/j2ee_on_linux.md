# Deploy a J2EE Application on Debian #
This guide will walk you through deploying a J2EE application on the Debian operating system. Once the application is up and running, you should be able to point your browser to it an it should display the classic, "Hello World!"

Along the way, you're going to learn a lot more than just deploying a J2EE application. You're going to learn how to do the following.

- Install and run VMware Player
- Install (a really light version of) Debian
- Run Debian using VM Player
- Install J2EE on Debian
- Deploy a simple J2EE application

### My System ###
I used my Toshiba Satellite L675D laptop for this project. The laptop runs on **64-bit** Windows 7, with an AMD Athlon II P340 Dual-Core 2.20 GHz Processor. If this guide proves useful, I'll update it to cover other systems.

## Install VM Player ##
I love virtual machine (VM) software. I can run a new machine (guest operating system) on an existing machine (host operating system), play around with the new machine and stop it (or delete it) once I'm done. It's perfect for what we want to do here.

This section describes how to install VMware Player on Windows 7. VMware Player lets you create Virtual Machines. At the time I wrote this guide, the VMware Player on my laptop was version 3.1.3 build-324285, but I updated it to version 5.0 so I could walk you through the install.

TODO...

## Install Debian ##
Once you've installed VMware Player, you can download a small Debian image file and use VMware Player to create a guest operating system (a.k.a. a Virtual Machine, or VM)that boots using the image file. Once you boot the VM, you can complete the Debian install.

When I wrote this guide Debian was at version 7.

### Prerequisites ###
- An Internet connection.

### Download a Debian Image ###
1. Visit [http://www.debian.org/distrib/netinst](http://www.debian.org/distrib/netinst "the Debian download page")
2. Download the Small CD that fits your system. For my laptop, it's amd64. Yours may be different. (The amd64 file is about 221 MB and on my system, it took about 7 minutes to download--I have a 6 Mbit connection).
3. Once downloaded, we can create a virtual Debian machine

### Create a Debian Virtual Machine ###
1. Open VMware Player
2. Hit Ctrl-N to create a new virtual machine
3. Select the option to install from a disk image file
4. Browse to where you downloaded the Debian Small CD image. VMware Player may complain that it couldn't automatically detect the OS. Ignore it and Click Next.
5. Select Linux from Guest Operating System options and then choose the Debian version that **most closely matches** the Debian version you're installing. In my case I selected Debian 6 64-bit. Select Next.
6. Give your virtual machine a name (I chose Debian 7 64-bit) and select a place where to store it. Click Next
7. Accept the recommended disk size, but choose **Store virtual disk as a single file** option. Click Next.
8. Accept the default settings unless you know enough to change them.
9. Click Finish. Your virtual machine will show up in a list of machines and you can now "play" it by selecting Play virtual machine.
10. You should now see a menu giving you an option to install Debian.

### Install and Configure Debian ###
Assuming you've created a Debian virtual machine (VM) and started it, here's how to  install Debian.

**TIP** Sometimes you may want to switch between the VM window and your browser during the install. When the VMware Player window is the active window it takes control of your mouse and keyboard. To get VMware Player to relinquish control, hit Ctrl-Alt. To give VMware Player control again, click anywhere in its window.

1. When you start your Debian VM, you'll see a menu. Select the Install option. This starts the Debian install process.
2. Choose a language. I choose English
3. Select a locale. A locale is a group of TODO. I selected the default, United States.
4. Select a keyboard layout aka a key map. I selected American English.
5. The install program will go off and do some uninteresting things and eventually ask you to choose a host name for your Debian machine. Remember, you're building a new server that runs Debian as its operating system. You should give it a unique name to identify it on your network. I choose, appsvr1, since this is VM represents a J2EE application server.
6. I skipped the option to set a domain name. TODO explain why.
7. The install now asks you to choose a password for your "root" account. Root is the almighty account. Root can do anything, like erase all your files. Choose a complex password for root.
8. Once you set the root password, the install will ask you to create a "normal" (non-root) user. Enter the full name for your user. I entered my name "James Punnett".
9. Now select a user name for your "normal" user account. I choose my first name, "james". In fact, the install choose it for me.
10. Now choose a password. As usual, make it complex.
11. The installer then asks you how you want partition your disks. Remember, this is a virtual machine. The disks you're partitioning are not the disks on your real machine. VMware Player is using a single file to represent your VM so you're actually partitioning that file (this explanation is not entirely accurate, but it's helpful enough.) VMware Player makes that file look like an entire server, with disks, keyboard, mouse, etc. just like a real machine.
12. Select the "Guided - use entire disk" option.
13. The installer tells you it's going to erase all data on the disk. Relax, this is not your real machine's disk. Hit Enter.
14. Select the third partioning option, "Seaprate /home, /usr, ..."
15. The installer shows you how your disk is going to be partitioned. You can change some other options, but we're keeping it simple. Just hit Enter to finish the partiioning.
16. Select Yes (use the tab key to move from No to Yes) and hit Enter.
17. The installer goes off and does something useful. Eventually, it'll ask you to choose a mirror site. This a stupid section of an otherwise simple install because the installer is asking you you to choose a mirror that's "close to you". A mirror site is where Debian will look for updates and software you ask it to install. The best advice I can give you is to choose the country that's geographically closest to you. I live the Caribbean so I could have chosen from several countries in South America (e.g. Venezuela), but decided to choose the United States.
18. Next the installer gives you a list of mirror sites in the country you chose in the previous step. I choose the first on the list, "ftp.us.debian.org".
19. After you select the mirror, the installer asks you to enter a proxy server. If you're not using a proxy server, just hit enter. If I was doing this at my office, I would have to enter my proxy server's address. A proxy server is a program that sits between users and the Internet i.e. it controls access to the Internet. It's useful for companies because they can prevent users from visiting inappropriate sites (porn, baby, porn.) Most users at home don't use a proxy.
20. The installer goes off and configures something called apt. Apt is Debian's package manager. A package manage allows you to download and install programs.
21. The installer uses Apt to download and install the remaining packages needed by the installer.
22. At some point, the installer may ask you if you wish to participate in a package usage survey. Select No.
23. Eventually, the installer will tell you that only the core system is installed and gives you the chance to install other software. Since this is supposed to be a light-weight system, I only installed the following packages: SSH Server, Standard system utilities.
24. The installer goes off and installs what you asked it to install and eventually ask you about installing the GRUB boot loader. Just select Yes.
25. Finally! The install will say it's done. Select Continue.

If all went well, you should see a login prompt. It looks like this. `appsv1 login:`

Congratulations! You're running a Debian VM using VMware Player.

So, try logging into your new server using your user name and password you set up during the install. If you were successful, you should see something like this. `james@appsvr1:~$`

To log out, hit Ctrl-D or type `logout`.

Although you can log into your server using the method just described, I recommend you use another method: use a telnet/ssh client application, like putty. To download putty, go to [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html "Putty download page") and download the Windows installer.

Once putty is downloaded and installed, connect to appsvr1. You'll need to figure out the IP address assigned to appsvr1, first. Log in to appsvr1 as root and type `ifconfig`. On my system, my IP address is 192.168.248.128.

Before going further, let's install your first Debian package.

- Use putty to log into appsvr1 as the normal user
- Now switch to the root user (`su -` and enter root's password)
- Type `aptitude install sudo`. You've just installed the sudo application. sudo allows a normal user to run as root. This saves you time and adds an audit trail of everything you did as root. We'll be using sudo in the following steps, so install it. It's good for you, trust me.
- Once sudo is installed, give sudo permission to the user you normally use to log into appsvr1 by typing, `useradd -G {sudo} username`, where `username` is your user name. In my case, I typed, `useradd -G {sudo} james`
- Make sure the command worked by typing, `groups username`, where `username` is the user you just added to the sudo group. You should see a list of groups that the user belongs to and sudo should be one of them.
- Hit Ctrl-D to log out as the root user. You're back to the "normal user" prompt.
- Hit Ctrl-D to log out completely. The change to the user won't take effect until you log in again. (This last log out may close your putty window.)
- Log back in as the normal user and type `sudo aptitude sudo`. The sudo application will ask you for your password and execute the command after `sudo`, in this case, sudo will execute `aptitude show sudo`, which just shows you details about the sudo package.


## Install J2EE on Debian ##
J2EE allows you to run Java Enterprise Edition applications. J2EE is a specification with many implementations. For example, IBM implements J2EE with its WebSphere Application Server product. Redhat implements J2EE with its JBoss product. We're going to install JBoss Application Version 7. It's free!

First, we need to install a Java Runtime environment.


### Install Java Runtime ###

1. Go to [http://java.com/en/download/linux_manual.jsp](http://java.com/en/download/linux_manual.jsp "Java Download"). This takes you to the Java download page for Linux operating systems (Debian is a Linux based OS)
2. I downloaded the Linux x64 file since I have a 64-bit system and I'm running a VM of the **64-bit** version of Debian 7. When I wrote this, Java Runtime was at Version 7 Update 21.
3. The download will start and once complete, we need to copy it to appsvr1.

The download should have place a file named jre-7u21-linux-x64.gz in your browser's download folder. We need to copy that file to the appsvr1. If you installed putty correctly, you can copy the file following these steps.


1. Open a Windows command prompt (on my Windows 7 system, I do this: Start > Run and type cmd then click OK.)
2. In the command prompt, type in `pscp`. If you get an error saying something like "pscp is not recognized as an internal or external command...", then you have to add the path to the putty applications to your PATH environment variable. TODO: Show them how... If pscp is in your path, then it will display its help. 
3. Change to the directory where you downloaded jre-7u21-linux-x64.gz.
4. To copy jre-7u21-linux-x64.gz to the tmp filesystem on appsvr1, type `pscp jre-7u21-linux-x64.gz james@192.168.248.128:/tmp`, where james is the user name I normally use to log into appsvr1 and 192.168.248.128 is appavr1's IP address.
5. pscp will prompt you for a password and then copy the file to /tmp
6. Use putty to log into appsvr1 and list the contents of /tmp (`ls -l /tmp`). You should see jre-7u21-linux-x64.gz

Now that we've copied the Java Runtime install file, we have to unzip it. (We know it's zipped because of the .gz extension.) We're going to unzip it to a folder called /usr/local. This is where system-wide applications should go. Because only root has write access to /usr/local we have to use sudo to run the command: `sudo tar -xzvf /tmp/jre-7u21-linux-x64.gz -C /usr/local`.

Once the unzip is complete, do an `ls -l /usr/local`. You should see a sub-directory called jre1.7.0_21.

Test that the Java Runtime is installed by typing, `/usr/local/jre1.7.0_21/bin/java -version`. You should see output that looks like this, `java version "1.7.0_21"`


### Install JBoss ###

JBoss is really easy to install on Debian. You download a compressed file from the JBoss site and unzip it somewhere reasonable (more on this later) then run it.

To unzip the compressed file,  we can't use tar like we did for Java, we have to use the zip and unzip utilities. Because we did only a minimal install of Debian, zip and unzip are not installed. Use the following command to install them:`sudo aptitude install zip unzip`.

Finally, we don't want to run JBoss as the user with which we normally log into appsvr1. We want to run it using a different, non-root user. Let's call it jbuser, for JBoss User. To create jbuser:

- Use putty to log into appsvr1
- Add the jbuser with the following command, `sudo adduser jbuser`. You'll be prompted to set the password and enter some basic details about jbuser.
- **Important** Once you successfully create jbuser, open a new putty window and log in as jbuser.

Assuming you're logged into appsv1 as jbuser,

- Create a directory to deploy JBoss. `cd; mkdir jboss` (FYI, the `cd` ensures you change to the jbuser home directory before making the directory.)
- Download the JBoss install file to the /tmp directory using wget: `wget -O /tmp/jboss-as-7.1.1.Final.zip http://download.jboss.org/jbossas/7.1/jboss-as-7.1.1.Final/jboss-as-7.1.1.Final.zip`. wget will download jboss-as-7.1.1.Final.zip from the JBoss website and place it in /tmp 
- Unzip the jboss-as-7.1.1.Final.zip file to the jboss directory you created in the home directory: ` unzip /tmp/jboss-as-7.1.1.Final.zip -d ~/jboss`
- Once unzipped, you should see a directory under jboss called jboss-as-7.1.1.Final. (`ls -l ~/jboss`)

Since JBoss needs Java to run, we need to tell it where it can find Java. The most convenient way to do this is to set the JAVA_HOME  environment variable. To do this, enter the following commands:

	JAVA_HOME=/usr/local/jre1.7.0_21
	export JAVA_HOME

To avoid having to do this every time you log in as jbuser to start/stop JBoss, enter these same commands in the .profile file in jbuser's home directory. I leave that as homework assignment.

To start JBoss,

	cd ~/jboss/jboss-as-7.1.1.Final/bin/
	./standalone.sh

You'll see lots of text scroll across the screen as JBoss starts up in standalone mode.

To stop JBoss,

- putty into appsvr1 as jbuser
- Go to the JBoss bin directory
- Run this command: `./jboss-cli.sh --connect controller=127.0.0.1:9999 command=:shutdown`.

You'll notice in the other putty window that JBoss stopped.
If you get an error message about java not found when you ran the shutdown command, it means you did not define JAVA_HOME (see above).

Okay. You've started and stopped JBoss. When JBoss is running, you can point a browser to http://hostname:8080 and if JBoss started properly, you should see the JBoss welcome page. (hostname in the URL is the IP address of appsvr1). Before we can do this test, though, we need to make a change to one of JBoss' configuration file. If we don't make the change, you won't be able to navigate to the welcome page because JBoss is not binding to all IPs. If you don't understand what this means now, ignore it for now and trust me.

- Change to the JBoss standalone config directory: `cd ~/jboss/jboss-as-7.1.1.Final/standalone/configuration`
- Use the vi editor to open the standalone.xml file: `vi standalone.xml`
- Search for "interfaces". You'll see something like this

        <interface name="management">
            <inet-address value="${jboss.bind.address.management:127.0.0.1}"/>
        </interface>
        <interface name="public">
            <inet-address value="${jboss.bind.address:127.0.0.1}"/>
        </interface>

- Change "127.0.0.1" to "0.0.0.0"
- Save the changes and exit vi
- Start JBoss like you did before. Give it some time to start. (On my system, it takes about 30 seconds)
- Point your browser to http://192.168.248.128:8080/. (On my laptop, appsvr1's IP is 192.168.248.128. Your system may be different.)
- You should see JBoss' welcome screen.
- There's an Administration Console link on the Welcome page as well. Click it, just for fun.

You're now running JBoss. Now, it's time to deploy a simple application.


