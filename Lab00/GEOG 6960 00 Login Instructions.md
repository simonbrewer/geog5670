# GEOG 6960 Open Source Geospatial Tools
## Login instructions for the GRASS server (OSH 273)
#### Monday, January 6 2014

### Introduction
In this class we will be using GRASS GIS installed on the CSBS server [slap.csbs.utah.edu]. This server runs Ubuntu Linux, and we will be running GRASS virtually. This document describes the steps necessary to connect to this server. 

Format conventions:

- Filenames will be given in *italics*
- Programs will be referred to in  **bold**
- Any command that you should type will be given in a box, as follows:

		some command here

## Set-up
### Logging into the server
In the computer labs, GRASS is available on the CSBS server [slap.csbs.utah.edu]. We need three pieces of software to connect and start working on the server. 

- an SSH client (**putty**)
- an X server (**Xming**)
- software to transfer files (**WinSCP**) 

### WinSCP
First start **WinSCP** to allow transfer of files between your computer (the client) and the server. **WinSCP** will open with the following screen. 

<img src="/Users/sbrewer/Dropbox/GEOG6960/Day1/Lab01/images/winscp1.png" alt="WinSCP" style="width: 300px;"/>

Click on [New] to enter the server details, including your user name (don't enter your password here). The server's address is slap.csbs.utah.edu and the port number should be 22. 

<img src="/Users/sbrewer/Dropbox/GEOG6960/Day1/Lab01/images/winscp2.PNG" alt="WinSCP" style="width: 300px;"/>

When you have entered this, save the details, and login. Click [Yes] if it asks you about the key. It will ask you to enter your password. Do so, and a window will open showing your folders on your computer (left panel) and the server (right panel). You can now use this to copy and move files. 

<img src="/Users/sbrewer/Dropbox/GEOG6960/Day1/Lab01/images/winscp3.png" alt="WinSCP" style="width: 300px;"/>

### BASH setup
In order for your account to work correctly on the server, you need to add a '.profile' to your home directory on the server. This sets up your account to work with GRASS, BASH and some other programs that we will be using. Get the file *profileForLinux.zip* from Canvas, and unzip it. Now transfer the file it contained ".profile" to your home directory on the server "/home/xxxx/" with WinSCP.  

### Xming
Start by launching **Xming** from the programs menu. This will not open any windows, but instead launch a server. To check that it has started, an icon should appear in the tool tray (in the bottom right hand corner of the screen):

<img src="/Users/sbrewer/Dropbox/GEOG6960/Day1/Lab01/images/xming1.png" alt="XMing1" style="width: 200px;"/>

### putty
Now start **putty** from the programs menu. This will open a window with a large number of options. Fortunately, we only need to change a couple of these. In the first screen (the session window), add the name of the server to the 'Host Name' window, and make sure the Port is set to 22. 

<img src="/Users/sbrewer/Dropbox/GEOG6960/Day1/Lab01/images/putty1.png" alt="PUTTY" style="width: 300px;"/>

We need to set the connection so that it accepts "X forwarding", in other words, allows graphical windows from the server to be opened on the client computer. So go to the 'SSH' option on the left hand side, then the 'X11' option. On this window, check the tickbox labelled 'Enable X11 forwarding'. 

<img src="/Users/sbrewer/Dropbox/GEOG6960/Day1/Lab01/images/putty2.png" alt="PUTTY" style="width: 300px;"/>

Now return to the session window (left hand panel). As we are going to be using this several times during the semester, we will save the session details. Enter a name in the box 'Saved sessions', then click on [Save]. 

<img src="/Users/sbrewer/Dropbox/GEOG6960/Day1/Lab01/images/putty3.png" alt="PUTTY" style="width: 300px;"/>

Finally, click on [Open] to start the session.
Once the connection is established, **putty** will open a terminal and ask you to login. Enter here your uID and password when prompted. If prompted to save the
key, press yes.

If you've done all of this, you'll see a welcome screen, and a prompt:

This terminal opens automatically a bash shell, which allows you enter commands and run programs (we will go over this in a couple of weeks). For now, just try
running two commands:

	pwd
which prints the name of your home directory (where the terminal starts) and

	ls
which shows a list of the files in your home directory

### Logout
When you have finished working, you can logout of the terminal by simply typing 
	
	exit


------
Simon Brewer 01/21/14
