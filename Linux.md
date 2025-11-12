
# View on this page 👀
- [Install on VirtualBox](https://github.com/ussefT/Essential/blob/main/Linux.md#install-on-virtualbox)
- [OVA](https://github.com/ussefT/Essential/blob/main/Linux.md#ova)
- [About](https://github.com/ussefT/Essential/blob/main/Linux.md#about)
- [Bash](https://github.com/ussefT/Essential/blob/main/Linux.md#bash)
- [Command](https://github.com/ussefT/Essential/blob/main/Linux.md#command)

# Install on VirtualBox 📦

Download virtualBox

 - [Download](https://www.virtualbox.org/wiki/Downloads) 
   
 - [VirtualBox Image](https://www.linuxvmimages.com/images/) 🖼️

---
## OVA

An Open Virtual Appliance (OVA) is a single file package that allows for easy distribution and setup of virtual machines (VMs). VirtualBox is an open source virtualization platform that allows you to use OVA files to create and manage VMs.

---
# About ℹ️
Just like Windows, iOS, and Mac OS, Linux is an operating system. In fact, one of the most popular platforms on the planet, Android, is powered by the Linux operating system. An operating system is software that manages all of the hardware resources associated with your desktop or laptop. To put it simply, the operating system manages the communication between your software and your hardware. Without the operating system (OS), the software wouldn’t function.

 - [GNU/Linux](https://www.gnu.org/home.en.html)

 - Bootloader –  The software that manages the boot process of your computer. For most users, this will simply be a splash screen that pops up and eventually goes away to boot into the operating system.

 - Kernel – This is the one piece of the whole that is actually called ‘Linux’. The kernel is the core of the system and manages the CPU, memory, and peripheral devices. The kernel is the lowest level of the OS.

 - Init system – This is a sub-system that bootstraps the user space and is charged with controlling daemons. One of the most widely used init systems is systemd, which also happens to be one of the most controversial. It is the init system that manages the boot process, once the initial booting is handed over from the bootloader (i.e., GRUB or GRand Unified Bootloader).

- Daemons – These are background services (printing, sound, scheduling, etc.) that either start up during boot or after you log into the desktop.
---
# Command ⌨️

- [Lpic1](https://www.lpi.org/our-certifications/lpic-1-overview/)
> [ More learn Lpic1](https://linux1st.com/)

- [Lpic2](https://www.lpi.org/our-certifications/lpic-2-overview/)

Diffrent shell Dash, Bash, [Zsh](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH) ,[tmux](https://tmuxcheatsheet.com/)

Configure [vim]() for python

```bash
man ls              # With / go to mode search

who                 # show who is logged on

whoami              # current user 

which tar           # /usr/bin/tar

whereis ping        # ping: /usr/bin/ping /usr/sbin/ping /usr/share/man/man8/ping.8.gz

pwd                 # /home/raven/Desktop


whatis              # fdisk (8)            - manipulate disk partition table


type fdisk          # fdisk is hashed (/usr/sbin/fdisk)


history             # 513  parted -l
                    # 514  fdisk
                    # 515  fidik -l
                    # 516  fdisk -l
                    # 517  fdisk /dev/sda
                    # 518  history

history -c          # clear history

!516                # run command  number 516

!!                  # run last command

ls                  # afs  bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run    sbin  srv  sys  tmp  usr  var

ls -ltrh

ls  #  -l - Long listing format
    #  -a - Include hidden files
    #  -h - Human-readable sizes
    #  -t - Sort by modification time
    #  -r - Reverse order while sorting
    #  -R - List subdirectories recursively
    #  -S - Sort by file size
    #  -1 - List one file per line
    #  -d - List directories themselves, not their contents

    # dr-xr-x---.   3 root root 4096 Nov 11 06:17 root

    # ‘-’ regular file
    # ‘b’ block special file
    # ‘c’ character special file
    # ‘C’ high performance (“contiguous data”) file
    # ‘d’ directory
    # ‘D’ door (Solaris 2.5 and up)
    # ‘l’ symbolic link
    # ‘M’ off-line (“migrated”) file (Cray DMF)
    # ‘n’ network special file (HP-UX)
    # ‘p’ FIFO (named pipe)
    # ‘P’ port (Solaris 10 and up)
    # ‘s’ socket
    # ‘?’ some other file type

    # owner-group-other link owner group file-size create-date file-name 
    

cd              # move to base path user -> /home/user
                #                   root -> /root

cd /tmp         # move to main dir (absolute path)

cd project/py   # move to current place dir (relative path)

uname 

    #  Linux rocky9.linuxvmimages.local 5.14.0-427.13.1.el9_4.x86_64 #1 SMP PREEMPT_DYNAMIC Wed May 1 19:11:28 UTC 2024 x86_64 x86_64 x86_64 GNU/Linux

uname -a

uname -p

    # -a, --all

    #    -s, --kernel-name

    #    -n, --nodename

    #    -r, --kernel-release

    #    -v, --kernel-version

    #    -m, --machine

    #    -p, --processor

    #    -i, --hardware-platform

    #    -o, --operating-system

echo  $0                # -bash
echo  $PATH             # /root/.local/bin:/root/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin
echo $SHELL             # /bin/bash
p=1
echo  $p                 # 1

cat f.txt                # all line 

cat /etc/passwd > f.txt  # write to f

cat /etc/shadow >> f.txt # append to f 

cat -n /etc/shadow       # with line number

less f.txt               # show with pages, move arrow key
cat -n /etc/shadow | less 

nl f.txt                  # show line with content

sort f.txt                # sort content


tail f.txt                # show end of line 

tail p 5 f.txt            # last 5 line 


ls | grep f               # find all f

ls | egrep -i "[0-9]"     # use regex in grep 

sed  's/A/B/'             # A replace to B

wc f.txt                  # 598  5390 42683 f.txt
                          # lines words byte 

md5sum file 
sha256sum file
sha512sum file 

*                         # means any string
?                         # means any single character
[ABC]                     # matches A, B, or C               
[a-z]                     # matches a, b, c, ..., z (both lower-case and upper-case)                                 
[0-9a-z]                  # matches all digits and numbers                                                      
[!x]                      # means NOT X.                                         

rm *                      # remove all file in dir

mkdir f                   # create dir
rmdir                     # remove  dir

cp source destination     # copy

mv source destination     # can rename


touch newfile 

file /etc/fstab          # /etc/fstab: ASCII text

dd if=n.txt of=o.txt     # just like copy file and devices

find . -iname "[a-j]*"   # find files in .

find /home/user -name "*.txt"          # Find all .txt files in /home/user

find /home/user -type d               # Find all directories in /home/user

find /home/user -mtime -7             # Find files modified in the last 7 days

find /home/user -exec ls -l {} \;      # Execute 'ls -l' on each found file

ln

export CAN="yes"

vim t1.txt 
#  :command 
#  :w       ## write
#  :q       ## exit
#  :qw      ## write, exit
#  :q!      ## do nothing and exit
#  :w!      ## override write 


tar -cf test.tar t1.txt t2.txt # archive

tar -czfv test.tar.gz t1.txt    # archive,compress

tar -xf

gzip file
gunzip file.gz

bzip2 file
bzip2 file.bz2


passwd user # change passwrod user

runlevel  # Print previous and current SysV runlevel
          # 0 poweroff
          # 1 rescue / one user 
          # 2,3,4 multi user
          # 5 graphical
          # 6 reboot

init 6    # reboot

shutdown now 

shutdown +5 --no-wall    # power off 5 minute - no wall 

shutdown +1 bye bye      # wall all user

mesg n/y                 # disable/enable

systemctl list-units

systemctl start ssh
systemctl enable ssh

ssh user@ip

scp file user@ip:/home/user

# debian/ubuntu
apt install vim

# redhat
yum/dnf install vim
#               update	Updates the repositories and update the names of packages, or all if nothing is named
#               install	Install a package
#               reinstall	Reinstall a package
#               list	Show a list of packages
#               info	Show information about a package
#               remove	Removes an installed package
#               search	Searches repositories for packages
#               provides	Check which packages provide a specific file
#               upgrade	Upgrades packages and removes the obsolete ones
#               localinstall	Install from a local rpm file
#               localupdate	Updates from a local rpm file
#               check-update	Checks repositories for updates to the installed packages
#               deplist	Shows dependencies of a package
#               groupinstall	Install a group, say "KDE Plasma Workspaces"
#               history	Show history of the usage



curl 


chmod +x file.sh          # exec file
chmod  u+x file.sh        # user can exec

chmod 754 file.sh         # user group other 

                          # user  =>   read(4) write(2) execute(1) 4+2+1= 7
                          # group =>   read(4) execute(1) 4+1= 5
                          # other =>   read(4) = 4 
                          
chmod -x file.sh
chmod u=rw,o=r file.txt   # user= read, write / other=r

chown username:groupname file.txt # change file owner and group 
chown 1001:1001 file.txt 

useradd username          # add user

usermod -aG groupname username  # add user to group 
                                # -a append user to group without remove current group

usermod -d /new/home/user username # add dir home to user

sudo userdel username      # Remove the user
sudo userdel -r username   # Remove the user and their home directory

groupadd groupname 

groupdel groupname

groupmod -n newgroupname oldgroupname

groupmod -g 1003 groupname  # change GID

df                        # show disk    

df -Th                    # type with human readable


du -h /home/user          # show files use 


lsblk -f                  # sda
                          # ├─sda1             xfs                        bf995dd6-3d3e-4ba3-a18f-62eddcd4d06d    735.6M    23% /boot
                          # └─sda2             LVM2_member LVM2 001       VbL08y-HQub-hJX4-ZSR2-TO5f-egyA-QTwVzd
                          #   ├─rl_rocky9-root xfs                        63e1a051-977d-40a1-a1ad-321916bce66f     68.1G     3% /
                          #   ├─rl_rocky9-swap swap        1              def2c0f4-42d1-4550-9800-0d7279b12422                  [SWAP]
                          #   └─rl_rocky9-home xfs                        31806d02-38c4-4bf7-b38f-89e626fd6fed    435.6G     1% /home



parted -l                 # Model: ATA VBOX HARDDISK (scsi)
                          # Disk /dev/sda: 550GB
                          # Sector size (logical/physical): 512B/512B
                          # Partition Table: msdos
                          # Disk Flags:

                          # Number  Start   End     Size    Type     File system  Flags
                          # 1      1049kB  1075MB  1074MB  primary  xfs          boot
                          # 2      1075MB  550GB   549GB   primary               lvm   
            
parted                    # command mod help with p or ? 


fdisk -l              
                          # Disk /dev/mapper/rl_rocky9-home: 438.95 GiB, 471318134784 bytes, 920543232 sectors
                          # Units: sectors of 1 * 512 = 512 bytes
                          # Sector size (logical/physical): 512 bytes / 512 bytes
                          # I/O size (minimum/optimal): 512 bytes / 512 bytes


fdisk /dev/sda            # command mode

mount                     # show all mounted file 
mount /dev/sda /mnt       # mount /dev/sda to /mnt

umount /dev/sda           # unmount /dev/sda 
umount /mnt               # unmount /dev/sda 



top             # display Linux processes

lscpu           # info about CPU

htop            # graphical top

ps                  # Show processes for the current user
ps -e               # Show all running processes
ps -ef              # Show full format of running processes
ps -u user          # Show processes running by user


kill 796        # kill process ID

free -V         # version 
free -h         # human readable
                #  -t, --total 


```



# grub
```bash

```

# systemctl
```bash

```

# firewall
```bash

```


# process

```bash

```

## pmap
```bash

```
## w
```bash

```
## pstree
```bash

```

# memory
## free
```bash

```

# I/O
## iotop

```bash

```

## iostat
```bash

```

## lsof
```bash

```

