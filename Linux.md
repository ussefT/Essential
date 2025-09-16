# Install on VirtualBox
 - [Download](https://www.virtualbox.org/wiki/Downloads)

## OVA
An Open Virtual Appliance (OVA) is a single file package that allows for easy distribution and setup of virtual machines (VMs). VirtualBox is an open source virtualization platform that allows you to use OVA files to create and manage VMs.

# About
Just like Windows, iOS, and Mac OS, Linux is an operating system. In fact, one of the most popular platforms on the planet, Android, is powered by the Linux operating system. An operating system is software that manages all of the hardware resources associated with your desktop or laptop. To put it simply, the operating system manages the communication between your software and your hardware. Without the operating system (OS), the software wouldn’t function.

 - [GNU/Linux](https://www.gnu.org/home.en.html)

 - Bootloader –  The software that manages the boot process of your computer. For most users, this will simply be a splash screen that pops up and eventually goes away to boot into the operating system.

 - Kernel – This is the one piece of the whole that is actually called ‘Linux’. The kernel is the core of the system and manages the CPU, memory, and peripheral devices. The kernel is the lowest level of the OS.

 - Init system – This is a sub-system that bootstraps the user space and is charged with controlling daemons. One of the most widely used init systems is systemd, which also happens to be one of the most controversial. It is the init system that manages the boot process, once the initial booting is handed over from the bootloader (i.e., GRUB or GRand Unified Bootloader).

- Daemons – These are background services (printing, sound, scheduling, etc.) that either start up during boot or after you log into the desktop.

# Bash 
The Bourne - Again Shell. default shell use in linux

# Command

Diffrent shell Dash, Bash, Zsh

```bash
        command [option] [args] 
```

```bash
    readlink /bin/sh # show default shell
````

```bash
echo $SHELL # show run current shell dir
echo $0 # show run current shell
```

we can use var in text
```bash 
echo i am $USER # i am root
```

this sign scape \ 
```bash 
echo i am \$USER # i am $USER
```

show date
```bash 
date 
var=`date`
echo $var
```

show process run in shell
```bash
ps # process run in shell
ps -a # all process 
```

show path file 
```bash 
which touch #/usr/bin/touch
 ```

search in history both key ctrl+r and type word, arrow key out in main 
```bash
history # show history command in bash
!1345 # reRun command in history with number
```

```bash
    root@look:/home
    # username @ hostname:/current dir
```
man show help command, in man with / can search
```bash
man ls
```
### Bash
variable is local, with reboot clear
```bash

echo $USER # show user current

var=foo

echo $var # foo

unset var

touch $var # touch foo 

```

### Directory
Files in Linux
![Files in Linux](url "Files in Linux")
```bash
  ll 
```
```bash
    ls -ltr
```
```bash
touch t.txt /tmp/T.txt tt.txt # create both
touch "new file" # space in name file
file t.txt # type of file 
```

