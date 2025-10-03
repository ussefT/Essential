
# View on this page
- [Install on VirtualBox](https://github.com/ussefT/Essential/blob/main/Linux.md#install-on-virtualbox)
- [OVA](https://github.com/ussefT/Essential/blob/main/Linux.md#ova)
- [About](https://github.com/ussefT/Essential/blob/main/Linux.md#about)
- [Bash](https://github.com/ussefT/Essential/blob/main/Linux.md#bash)
- [Command](https://github.com/ussefT/Essential/blob/main/Linux.md#command)
- [Directory](https://github.com/ussefT/Essential/blob/main/Linux.md#directory)
- [ssh](https://github.com/ussefT/Essential/blob/main/Linux.md#ssh)




---
# Install on VirtualBox
 - [Download](https://www.virtualbox.org/wiki/Downloads)
---
## OVA

An Open Virtual Appliance (OVA) is a single file package that allows for easy distribution and setup of virtual machines (VMs). VirtualBox is an open source virtualization platform that allows you to use OVA files to create and manage VMs.

---
# About
Just like Windows, iOS, and Mac OS, Linux is an operating system. In fact, one of the most popular platforms on the planet, Android, is powered by the Linux operating system. An operating system is software that manages all of the hardware resources associated with your desktop or laptop. To put it simply, the operating system manages the communication between your software and your hardware. Without the operating system (OS), the software wouldn’t function.

 - [GNU/Linux](https://www.gnu.org/home.en.html)

 - Bootloader –  The software that manages the boot process of your computer. For most users, this will simply be a splash screen that pops up and eventually goes away to boot into the operating system.

 - Kernel – This is the one piece of the whole that is actually called ‘Linux’. The kernel is the core of the system and manages the CPU, memory, and peripheral devices. The kernel is the lowest level of the OS.

 - Init system – This is a sub-system that bootstraps the user space and is charged with controlling daemons. One of the most widely used init systems is systemd, which also happens to be one of the most controversial. It is the init system that manages the boot process, once the initial booting is handed over from the bootloader (i.e., GRUB or GRand Unified Bootloader).

- Daemons – These are background services (printing, sound, scheduling, etc.) that either start up during boot or after you log into the desktop.
---
# Command
Diffrent shell Dash, Bash, Zsh

```bash
command [option] [args] 
```
 - [File](https://github.com/ussefT/Essential/blob/main/Linux.md#file)
    > work with file
 - [ls](https://github.com/ussefT/Essential/blob/main/Linux.md#ls)
   >  ls - list directory contents
 
 - [du](https://github.com/ussefT/Essential/blob/main/Linux.md#du)
   >  du - estimate file space usage
 - [specificSign](https://github.com/ussefT/Essential/blob/main/Linux.md#specifinSign)
   > . ? * [] {} 
 - [compress & archive](https://github.com/ussefT/Essential/blob/main/Linux.md#compress)
   > gzip
   > 
   > xz
   > 
   > bzip2
   > 
   > bzcat 
 - [grep](https://github.com/ussefT/Essential/blob/main/Linux.md#grep)
   > [regex](https://github.com/ussefT/Essential/blob/main/Linux.md#regexInGrep) 

 - [vim](https://github.com/ussefT/Essential/blob/main/Linux.md#vim)

---
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
---
## Bash
variable is local, with reboot clear
```bash

echo $USER # show user current

var=foo

echo $var # foo

unset var

touch $var # touch foo 

echo foo > file # foo in file and remove var

echo foo >> file # foo save file 

>file # create file  
```
---
### Directory
Files in Linux
![Files in Linux](https://github.com/ussefT/Essential/blob/main/linux_files.png "Files in Linux")
---
#### ls
```bash
  ll # -rwxrwxrwx 1 usef usef    181 Sep 15 03:42 Readme.md*
```
 - -l - Long listing format
 - -a - Include hidden files
 - -h - Human-readable sizes
 - -t - Sort by modification time
 - -r - Reverse order while sorting
 - -R - List subdirectories recursively
 - -S - Sort by file size
 - -1 - List one file per line
 - -d - List directories themselves, not their contents
 - -F - Append indicator (one of */=@|) to entries
#### -rwxrwxrwx 1 usef usef
#### - ---     ---    ---    1         usef   usef
####  t user  group  other  linkInDisk owner group
![ls](https://github.com/ussefT/Essential/blob/main/ls.png "ls")

```bash
ls -ltr # -rwxrwxrwx 1 usef usef   3767 Sep 16 02:26 Linux.md
ls -ltrh # -rwxrwxrwx 1 usef usef 3.8K Sep 16 02:27 Linux.md
```
---
### du 
```bash
du -sh /etc/* # du - estimate file space usage
```
---
### specificSign
```bash
rm -rf * # rm all file in folder
touch file{1..20} # create file1 ... file20
ls file? # show first name file 
ls file[3-5] # file3 file4 file5
ls bigfile?.* # all bigfile.tar or .gz or ....
```
---
### File
```bash
touch t.txt /tmp/T.txt tt.txt # create both
touch "new file" # space in name file
file t.txt # type of file 
```
```bash
cat /ect/* > bigfile #move all etc to big file
```
```bash
cat /etc/* | nl # line with number
```
---
## compress
only comress in linux => gz bz xz 
cross-platform (work any os)=> zip 

```bash 
#compress
bzip2 bigfile # bigfile.bz2
```
```bash 
#uncompress
bunzip2 bigfile.bz2
```
```bash 
bzcat bigfile.bz2 # without uncompress show files
```
---
```bash
gzip bigfile # bigfile.gz
```
```bash
gunzip bigfile.gz
```
---
```bash
xz bigfile # bigfile.xz
```
```bash
unxz bigfile.xz
```
attention do not compress gz to xz or any format data is lost

```bash
zip file.zip dir
unzip file.zip
```
---
### archive
archive & compress => tar
 - -c archive(tar)
 - -z compress(gz)
 - -v show detail in terminal(verboos)
 - -x extract
```bash
tar -czvf bigfile.tar.gz dir  # bigfile.tar
```
```bash
# uncompress
tar -xzvf bigfile.tar.gz  # bigfile.tar
```

## cat | grep
```bash
cat /etc/* | grep -i ROOT # every word match with root ROOT
```

```bash 
cat /etc/* | head # first 10 line
```
```bash 
cat /etc/* | tail # end 10 line
```
```bash
cat /etc/passwd | less # move a lot line with arrow key
cat /etc/passwd | more # move with enter key and end go out
```
### regexInGrep
```bash
cat text | grep 'a' # show only with a 

cat text | grep '[ab]' # show word a or b

cat text | grep 'a$' # word end with a

cat text | grep "a..a" # word 4 character contain a

cat text | grep "a..a*" # word 4 character contain a and after another
```

## Vim

shift+6 OR ^ => end line

shift+4 OR $ => first line

shift+g OR G => end first line


## ssh

SSH is a secure protocol used as the primary means of connecting to Linux servers remotely. It provides a text-based interface by spawning a remote shell. After connecting, all commands you type in your local terminal are sent to the remote server and executed there.

Install it:
```bash
sudo apt-get install openssh-server
```

Enable it

```bash
sudo systemctl enable ssh
```

Start it

```bash
sudo systemctl start ssh
```

Connect to linux server, In windows or mac or linux :
```bash
ssh userName@Your-server-name-IP
```

### moveFiles

Upload files:

```bash
scp Desktop/sample_example.txt root@136.183.142.28:/home/remote_dir
```

Download files:

```bash
scp 147.182.143.27:/home/remote_dir/sample_example.txt home/Desktop
```