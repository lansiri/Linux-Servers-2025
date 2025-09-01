# H2 - Commander Penguin

## ToC

- [X - Command Line Basics](#x---command-line-basics)
- [A - Micro](#a---micro)
- [B - APT](#b---apt)
- [C - Important Directories](#c---important-directories)
  - [The root dir /](#the-root-dir-)
  - [Home directory](#home-directory)
  - [users home directory](#users-home-directory)
  - [/etc/ folder](#etc-folder)
  - [/media/ folder](#media-folder)
  - [/var/log/ the logs](#varlog-the-logs)
- [D - grep](#d---grep)
- [E - Pipes](#e---pipes)
- [F - lshw](#f---lshw)
- [G - Logs](#g---logs)
  - [apt logs](#apt-logs)
  - [journalctl](#journalctl)
- [H - micro addons / plugins](#h---micro-addons--plugins)
- [Tools used](#tools-used)
- [Resources](#resources)


## X - Command Line Basics

https://terokarvinen.com/2020/command-line-basics-revisited

An article with basic useful commands for linux and BSD

Some basic commands:

`pwd`
*shows current directory*

`ls`
*list files in current directory*

`cd foldeR/`
*enters foldeR/*

Updating the system with package manager

`sudo apt-get update`

`sudo apt-get upgrade`

---

## A - Micro

To install micro text editor I use the following command:

`sudo apt-get install micro`

![](assets/1756356986024.png)

To start micro

`micro`

or to open file or create file with micro:

`micro filename`

![](assets/1756748024174.png)

---

## B - APT

Install 3 apps with apt.

Im going to install irc client irssi, screen and lynx

`sudo apt-get install irssi screen lynx`

![](assets/1756748386602.png)

First ill try lynx, its a terminal browser

`lynx`

![](assets/1756748425187.png)

to open a page `g` and then type the url, for example terokarvinen.com

![](assets/1756748560666.png)

`Q` to quit.

Then ill open irssi with screen

`screen irssi`

![](assets/1756748599801.png)

screen starts a session that stays open even if we close the window, and we can later re-attach back to the screen with screen -r

irssi is just an IRC client.

---

## C - Important Directories

### The root dir /

this is the root for all folders.

to access it:
`cd /`

![](assets/1756748906824.png)

### Home directory

to access home directory, its the place where all users have their own home directories, for my instance, i just have my own user:

`cd /home/`

![](assets/1756749064188.png)


### users home directory 

to access the users home directory, the default area for new documents or downloaded files.

`cd ~`

or

`cd /home/username`

![](assets/1756748994115.png)

### /etc/ folder

/etc/ is the place for system settings, and other stuff such as passwords..

to enter:
`cd /etc/`

![](assets/1756749135693.png)

As an example, i will edit the "message of the day" file

`micro motd`



![](assets/1756750188401.png)

Added "Hello world!" to the motd

![](assets/1756750212669.png)


### /media/ folder

this is the place for removable media such as usb sticks

to access
`cd /media/`

![](assets/1756749206934.png)

we dont have any medias connected to the virtual machine, so this is empty.

I tested adding an sdcard/usb stick combo and it showed up.

![](assets/1756749834343.png)

### /var/log/ the logs

/var/log/ is the logs location

![](assets/1756749917477.png)

some logs require sudo, for example boot.log

`sudo cat boot.log`

![](assets/1756750089499.png)

---

## D - grep

grep is a tool to search for strings, some examples

Search for the string "Hello", recursively inside /etc

`sudo grep -r "Hello" /etc`

![](assets/1756750699935.png)


For a slightly cleaner view, only show the file names containgin "Hello" recursively on /etc, we can use:

`sudo grep -r -l "Hello" /etc`

![](assets/1756750891036.png)


---

## E - Pipes

For a very basic pipe command, we can combine cat with grep:


Ddo we find the line with "Hello" when using the command `cat motd`?

`cat motd | grep "Hello"`

![](assets/1756750393002.png)

another example, decode base64 with echo

![](assets/1756751277958.png)

---

## F - lshw

lshw shows system specs / components or virtual devices etc. It shows the H/W Path, device name, class and description fields.

example command:

`sudo lshw -short -sanitize`

![](assets/1756751437551.png)

it was not installed so we install it with the following command:

`sudo apt-get install lshw`

now we can use the command:

`sudo lshw -short -sanitize`

![](assets/1756751465040.png)

it shows that we are using VirtualBox, we have assigned 5632mb memory to the vm, our processor is amd 5900X.

---

## G - Logs

### apt logs

Our vm has not gathered much logs yet, but we know we used apt, so we can check the apt logs, to check the latest changes.

`cat /var/log/apt/history.log | tail`

![](assets/1756752024714.png)

We can confirm this is correct, since these apps we just installed. The logs show when the install was started, when it was completed, who initiated the install and what command was used, and what was installed.

### journalctl

To check the **journalctl** logs we can use the `journalctl` command, its similiar to the event viewer on windows systems.

some example parameters for `journalctl`

`-b ` shows logs since last boot

`-f` "follow" shows live log

we know we installed irssi recently, lets see if we can find a log in journalctl

`sudo journalctl -b | grep "irssi"`

![](assets/1756753770819.png)


---

## H - micro addons / plugins

I have previously also installed some of these, but to install i go back to previous guide / examples at:
 https://terokarvinen.com/2022/command-palette-cheatsheet-run-and-make-micro/

To install all the plugins in the guide:

```
micro --plugin install jump
cd .config/micro/plug/
git clone https://github.com/terokarvinen/palettero.git
git clone https://github.com/terokarvinen/micro-run.git
git clone https://github.com/terokarvinen/micro-cheat.git
```

testing the **run** plugin with python hello world

![](assets/1756753041479.png)


Pressing `F5` runs the app, and pressing `Enter` returns back to micro.

![](assets/1756753069736.png)

---

## Tools used

- micro
- virtualbox
- debian

---

## Resources

https://terokarvinen.com/2022/command-palette-cheatsheet-run-and-make-micro/
(tero karvinen 2022)


https://terokarvinen.com/linux-palvelimet/
(tero karvinen 2025)

https://terokarvinen.com/2020/command-line-basics-revisited
(tero karvinen 2020)