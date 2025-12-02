
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

- curl
> [post](https://www.warp.dev/terminus/curl-post-request)
> [get](https://reqbin.com/req/c-1n4ljxb9/curl-get-request-example)
> [getFile](https://www.digitalocean.com/community/tutorials/workflow-downloading-files-curl)

- [wget](https://wiki.archlinux.org/title/Wget)
 
```bash
# boot setting in 
# cat /etc/default/grub
# after change save changes

grub2-mkconfig -o /boot/grub2/grub.cfg

man ls              # With / go to mode search

sudo shutdown now   # permission temporary

su -                # switch to root user

su - user           # switch to user


who                 # show who is logged on

whoami              # current user 

which tar           # /usr/bin/tar

whereis ping        # ping: /usr/bin/ping /usr/sbin/ping /usr/share/man/man8/ping.8.gz

w                   # 03:01:17 up 1 min,  1 user,  load average: 0.36, 0.17, 0.06
                    # USER     TTY        LOGIN@   IDLE   JCPU   PCPU WHAT
                    # root     pts/0     03:00    4.00s  0.04s  0.00s w

last                # show a listing of last logged in users

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

!?ps?               # last command contain ps and run it

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


    # d  r-x  r-x  ---.   3        root    root    4096 Nov 11 06:17 root
    
    # owner-group-other NumberOfLink owner group file-size create-date file-name 
    

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

hostname                 # show hostname
hostname -I              # ips use in linux


echo  $0                 # -bash
echo  $PATH              # /root/.local/bin:/root/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin
echo $SHELL              # /bin/bash
p=1
echo  $p                 # 1

echo -e "Hello\nWolrd"   # Hello
                         # Wolrd

awk '{print $1}'         # out first column
tail -n /etc/passwd  | awk '{print $1}' # first column number 

cat f.txt                # all line 

cat /etc/passwd > f.txt  # write to f

cat /etc/shadow >> f.txt # append to f 

cat -n /etc/shadow       # with line number

cat file | xargs -I x echo see this : x    # get var from file and out in echo

cat -n /etc/shadow | less 

less f.txt               # show with pages, move arrow key

ls | tee > ls.txt        # print ls and  write to ls.txt


nl f.txt                  # show line with content

sort f.txt                # sort content


tail f.txt                # show end of line 

tail p 5 f.txt            # last 5 line 


ls | grep f               # find all f

ls | egrep -i "[0-9]"     # use regex in grep 

sed  's/A/B/g'             # A replace to B

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

mkdir -v f                # create dir -v verbos
mkdir -p /home/dir1/dir2

rmdir dir                 # remove  dir
rmdir -p dir/dir2


cp source destination     # copy

mv source destination     # can rename


touch newfile new2file

touch -m file            # update date in file



file /etc/fstab          # /etc/fstab: ASCII text

dd if=n.txt of=o.txt     # just like copy file and devices

find . -iname "[a-j]*"   # find files in .

find /home/user -name "*.txt"          # Find all .txt files in /home/user

find /home/user -type d               # Find all directories in /home/user
find . -type f                        # find all file in .

find -size 20M

find /home/user -type d -u user

find /home/user -mtime -7             # Find files modified in the last 7 days

find /home/user -exec ls -l {} \;      # Execute 'ls -l' on each found file

find . -type f -iname "*.txt" -exec grep 'March' {} \;  # out March

# Hard link
ln f1 file.txt          # create hard link can rm original file link file exist 
                        # when change file.txt will change f1
 
ln -s file.txt f1       # soft link when remove original file soft link not work 

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

tar -cjvf f3.tar.bz2  file2      # compress bz2

tar -cJvf.tar.xz file            # compress with xz
         

tar -xvf f2.tar.gz -C /home/student/  # out in dir

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
# RedHat
systemctl list-units --type service  # show list of service

systemctl get-default    # multi-user.target

systemctl set-default graphical.target

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

yum module list                # list of packages
yum module info PackageName    # show info about package

# Respository in Redhat
# cd /etc/yum.repos.d


# r READ    w WRITE    e EXECUTE  s root user permission to another user to run this file

chmod +x file.sh          # exec file
chmod  u+x file.sh        # user can exec like /bin/passwd

chmod u+s filename               

chmod u+t /dir          # The last special permission has been dubbed the "sticky bit."
                        # This permission does not affect individual files. However, at the directory level,
                        # it restricts file deletion. Only the owner (and root) of a file can remove the file within that directory.
                        # A common example of this is the /tmp directory:
                          

chmod 754 file.sh         # user group other 

                          # user  =>   read(4) write(2) execute(1) 4+2+1= 7
                          # group =>   read(4) execute(1) 4+1= 5
                          # other =>   read(4) = 4 

#                        --- 0     --x 1       -w- 2     r-- 4 
#                        -wx 3     r-x 5       rw- 6     rwx 7

chmod -x file.sh
chmod u=rw,o=r file.txt   # user= read, write / other=r

chmod u=rw,g=-,o-rwx      # user= read,write / group=remove premission / other= remove read write execute

getfacl file             # show access control file : owner , permission , .... . 
setfacl file -d -m u:tom:rw files/ # set to files/ permissions 
 
chown username:groupname file.txt # change file owner and group 
chown 1001:1001 file.txt 
                                 
chgrp groupname file             # change only group name

umask                            # is the default permission values for files and directories.
                                 # default for root is 0022 


useradd username          # add user


useradd -u 1003 -s /bin/bash -e 2026-01-01 -c "Admin User"  # -u user id 
                                                            # -s what bash 
                                                            # -e date expire 
                                                            # -c Comment 


usermod -aG groupname username  # add user to group 
                                # -a append user to group without remove current group

usermod -d /new/home/user username # add dir home to user

                                   # -a append
                                   # -G group
                                   # -L lock
                                   # -u unlock
                                   # -c comment 
chage -l root 
                                    #Last password change                                    : Nov 10, 2025
                                    #Password expires                                        : never
                                    #Password inactive                                       : never
                                    #Account expires                                         : never
                                    #Minimum number of days between password change          : 0
                                    #Maximum number of days between password change          : 99999
                                    #Number of days of warning before password expires       : 7



sudo userdel username      # Remove the user
sudo userdel -r username   # Remove the user and their home directory

chage -d 0 root            # first login must change password

groupadd groupname 

groupadd -g 1004 groupname

groupdel groupname

groupmod -n newgroupname oldgroupname

groupmod -g 1003 groupname  # change GID

chattr +a filename        # change attr file
lsattr file               # show attr file


visudo                      # we can add user to run command root without or with password
                            # Allow root to run any commands anywhere
                            # root      ALL=(ALL)    ALL
                            # tom       ALL=(ALL)    NOPASSWD: /sbin/fdisk
                            # mary      ALL=(ALL)    NOPASS 

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



top                      # display Linux processes

lscpu                    # info about CPU

htop                     # graphical top

ps                  # Show processes for the current user
ps -e               # Show all running processes
ps -ef              # Show full format of running processes
ps -u user          # Show processes running by user


kill 796        # kill process ID
kill -l
                # 1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL       5) SIGTRAP
                # 6) SIGABRT      7) SIGBUS       8) SIGFPE       9) SIGKILL     10) SIGUSR1
                #11) SIGSEGV     12) SIGUSR2     13) SIGPIPE     14) SIGALRM     15) SIGTERM
                #16) SIGSTKFLT   17) SIGCHLD     18) SIGCONT     19) SIGSTOP     20) SIGTSTP
                #21) SIGTTIN     22) SIGTTOU     23) SIGURG      24) SIGXCPU     25) SIGXFSZ
                #26) SIGVTALRM   27) SIGPROF     28) SIGWINCH    29) SIGIO       30) SIGPWR
                #31) SIGSYS      34) SIGRTMIN    35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+3
                #38) SIGRTMIN+4  39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+8
                #43) SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12 47) SIGRTMIN+13
                #48) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-12
                #53) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-7
                #58) SIGRTMAX-6  59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-2
                #63) SIGRTMAX-1  64) SIGRTMAX


pgrep python    # find pid process name

pkill -9 pid    # kill pid 
kill 9 pid      # kill pid




free -V         # version 
free -h         # human readable
                #  -t, --total 

xclock &        # run in background

bg              # see apps run in background with &

jobs            # see jobs in bg or fg

fg %1           # %1 point to first job in background to foreground

nohub xclock    # run xclock and when finish shutdown

nohub python backup.py > f.txt  2> error.txt  # run in background and standard input in f.txt Error to error.txt

nice -n 19 apt install jcal       # nice means periority 
                                  # if -20 is important
                                  # if 19 is not important

renice -n 15 PID                  # down or up nice to use source PC


#  /etc/crontab 
crontab -e                      # we can schedule command 
# at 5 a.m every week run command
# m(minute)   h(hours)   dom(Day of month)   mon(what month)   dow(Day of week)  command
# *            5              *                  *                 1                 tar -zcf /var/backups/home.tgz /home/                                                                                        

crontab -l                      # list of crontab user

# RedHat
systemctl enable/disable/start/stop/restart firewalld

firewall-cmd  --get-default-zone     # public
firewall-cmd --list-all              # In safe list 
firewall-cmd --realod                # realod

firewall-cmd --permanent --add/--remove-service=ssh   # add ssh to safe zone
firewall-cmd --permanent --add/--remove-port=22/tcp


```

## systemd-tmpfiles
We can remove file with one command
```bash
systemctl start temfiles
# man tempfiles.d
cd /etc/tmpfiles.d/
vim tmp.conf
```
```text
d   /var/log/dir1   0777 root root
d   /var/log/dir2   0777 root root 30s 

f   /var/log/dir1/f1  0777 student student 

r   /var/log/dir1/f1

```
30s after run systemd.tmpfiles --clean remove files

run for create files
```bash
systemd-tmpfiles --create
```

run for remove
```bash
systemd-tmpfiles --remove   # remove fiels start with  r
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

