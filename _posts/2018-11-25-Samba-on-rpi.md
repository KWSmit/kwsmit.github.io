---
layout: post
title: "Robots & more"
subject: "Using Samba on RPi 3B+"
date: 2018-11-25
---

If you like to share your files and folders on your Raspberry Pi you
can use Samba. This way it's very easy to write programs on you rpi using 
your favorite code editor on your PC. In my case I use VS Code on my
Windows 10 computer.
On the Internet there are many tutorials explaining how to install and configure 
Samba on your Raspberry Pi, e.g. <a href="http://raspberrywebserver.com/serveradmin/share-your-raspberry-pis-files-and-folders-across-a-network.html" 
target="_blank">here</a>. This worked great for me on my RPi3B. But I found 
out that it's different on my brand new RPi3B+.

First lets start with the installation of Samba according the tutorial:

```python
sudo apt-get install samba samba-common-bin
```

This doesn't work. I got the message that both modules ar replaced. But I 
also found out Samba already seemed to be installed on my NOOBS SD-card. 
So you can edit the config file right away as described in the tutorial:

```python
sudo nano /etc/samba/smb.config
```

But creating a new user account by:

```python
sudo smbpasswd -a pi
```

didn't work. Running this command gives an error messages: unknown command 
smbpasswd. On the Samba webpage I found information on how 
<a href="https://wiki.samba.org/index.php/Distribution-specific_Package_Installation" 
target="_blank">to install Samba on Stretch</a>:

```python
sudo apt-get install samba attr
```

Now you can create a user by

```python
sudo smbpasswd -a pi
```

From now on you will see the Raspberry Pi in the network section of Windows 
Explorer. Double-click on it, enter your password and you're ready to go.

Summarizing:

- Run sudo apt-get install samba attr.
- Edit configuration file according the tutorial: sudo nano /etc/samba/smb.conf.
- Create user pi: sudo smbpasswd -a pi, enter the password twice.
- Start Windows Explorer on your PC and open your shared Pi-folder.
