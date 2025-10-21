<div dir="rtl"></div>

## Docker
داکر یک پلتفرمی که از هسته ی سیستم عامل استفاده میکند که میاد فایل های ایمیج را روی ماشین مجازی اجرا و تبدیل به کانتینر میشود.

### container

کانتینر یک محیط ایزوله و جدای از محیط بیرون هستند که میتوانند یک ایمیج را اجرا کنند.

- [Install on Linux](https://github.com/ussefT/Essential/blob/main/Docker.md#install-on-linux)
- [command](https://github.com/ussefT/Essential/blob/main/Docker.md#command)


## Install on Linux

- [Install Linux](https://github.com/ussefT/Essential/blob/main/Linux.md)

برای نصب روی لینوکس در هر ورژنی :
- [Docker in linux](https://docs.docker.com/engine/install/ubuntu/)


## command

- [pull](https://github.com/ussefT/Essential/blob/main/Docker.md#pull)
- [run](https://github.com/ussefT/Essential/blob/main/Docker.md#pull)

> - -it
> - -itd

- [images]()
- [ps](https://github.com/ussefT/Essential/blob/main/Docker.md#ps)
- [stats](https://github.com/ussefT/Essential/blob/main/Docker.md#stats)
- [tag](https://github.com/ussefT/Essential/blob/main/Docker.md#tag)
- [inspect](https://github.com/ussefT/Essential/blob/main/Docker.md#inspect)
- [search](https://github.com/ussefT/Essential/blob/main/Docker.md#search)
- [rm](https://github.com/ussefT/Essential/blob/main/Docker.md#rm)
- [rmi](https://github.com/ussefT/Essential/blob/main/Docker.md#rmi)
- [attach](https://github.com/ussefT/Essential/blob/main/Docker.md#attach)
- [exec](https://github.com/ussefT/Essential/blob/main/Docker.md#exec)
- [cp](https://github.com/ussefT/Essential/blob/main/Docker.md#cp)
- [stop](https://github.com/ussefT/Essential/blob/main/Docker.md#stop)
- [restart](https://github.com/ussefT/Essential/blob/main/Docker.md#restart)
- [log](https://github.com/ussefT/Essential/blob/main/Docker.md#log)
- [event](https://github.com/ussefT/Essential/blob/main/Docker.md#event)
- [pause](https://github.com/ussefT/Essential/blob/main/Docker.md#pause)
- [commit](https://github.com/ussefT/Essential/blob/main/Docker.md#commit)
- [save](https://github.com/ussefT/Essential/blob/main/Docker.md#save)
- [load](https://github.com/ussefT/Essential/blob/main/Docker.md#load)
- [export](https://github.com/ussefT/Essential/blob/main/Docker.md#export)
- [import](https://github.com/ussefT/Essential/blob/main/Docker.md#import)
- [volume](https://github.com/ussefT/Essential/blob/main/Docker.md#volume)
- [networking](https://github.com/ussefT/Essential/blob/main/Docker.md#networking)
- [port-mapping](https://github.com/ussefT/Essential/blob/main/Docker.md#port-mapping)

version:
```bash
docker version
```

info:
```bash
docker  info
```


---
## pull

---
## run
اگر ایمیجی نباشد به صورت خودکار خودش آن ایمیج را دانلود میکند.
به ازای هر کانتینتر ما یک پراسس جدید در لینوکس داریم.

برای اجرا کردن یک ایمیج در داکر 
```bash
docker run hello-world
```
برای اجرای ایمیج ها به صورت تعاملی یعنی ترمینال یا  به صورت زنده بریم داخلش این دستور 

و برای اینکه  بک گراند اجرا بشه 
```bash
docker run -itd centos:lates
```

نکته برای ایمیج هایی که خودشان توانایی اجرا شدن در ترمینال مثل لینوکس ها را دارند نیاز نیست ولی برای بقیه ایمیج ها این دستور 
```bash
docker run -itd centos:lates /bin/bash
```

میتونیم برنامه ی دیگری به غیر از بش را انجام دهیم .
تا زمانی که این وظیفه را دارد کانتینر ما در حال اجرا است.

مثال : 
```bash
docker run -it centos:lates ping 8.8.8.8 
```

> ctrl+p+q -> exit container but run in background

> ctrl + D -> down container

نکته: اگر بخواهیم داکر هاست متوقف شود و لی کانتینتر در حال اجرا باقی بماند .
در این مسیر فایل deamon.json (/etc/docker)

```bash
cd /etc/docker
touch daemon.json
echo {"live_restor":true} > daemon.json
```

تغییر نام کانتینتر به نام دلخواه
```bash
docker -itd --name moon cnetos:lates
```
---
### memory
در  موقع اجرای یک ایمیج میتونیم مقدار memory, swap memory را مشخص کنیم .

```bash
docker run -itd --name moon -m 100M centos:lates 
# if -memory-swap=-1 unlimited 
docker run -itd --name moon -memory-swap 1G centos:lates 

```
---
### cpu
تعریف مقدا ر cpu 

```bash
# cpu start 0 to up
docker run -itd --name sun --cpuset-cpus="1,2"
docker run -itd --name sun --cpuset-cpus=1-6
docker run -itd --name sun --cpuset-cpus=5
```

### storage
برای تخصیص حافظه 
```bash
docker run -itd --name m  --storage-opt size=1G centos:lates
```
ممکنه ارور بده.
0000

### rm
بعد از اینکه کانتینر ما افتاد یا down شد پاک میشود.
```bash 
docker run -it --rm --name moon centos:latest
```

---
## ps
کانیتر ها یک طول عمری دارند و مشغول انجام کاری هستند و وقتی تموم میشوند خارج میشوند.
 با این دستور تمام کانتینر های بالا یا در حال اجرا را میشه دید.
```bash
docker ps 
# all container up or exit
docker ps -a
```
```bash
# just container with ID
docker ps -q
```
```bash
# show container with size
docker ps -s
```
```bash
# show container last run 
# -n=1 last container 
# -n=2 two last container 
docker ps -n=[int]
```
```bash
# filer container and show with filter exited
# -f status= created, running, paused, restarting, removing, exited, dead
docker ps -f status='exited'
```
```bash

```
---
## stats

دیدن وضعیت کانتینتر ها به صورت زنده

```bash
# show all container up
docker stats

# show moon container
docker stats moon

# show status and exit from that
docker stats --no-stream 
```


---
## tag
 هر ایمیج داکر دارای دو متغییر  < repository>:< tag> هست . 
در محیط پروداکشن ما از latest  استفاده میکنیم.

- dangling ایمیج چیه؟ ممکنه image باشه که tag,ID آن None خورده باشد مثلا اگر image هم اسم image دیگر بیلد شده باشد داکر iamge قبلی را dangel میکند.

پاک کردن ایمیج غیر قابل استفاده.
```bash
docker image prune # remove unused images 
```
 اگر بخواهیم ایمیج دنگل را نگه داریم میتونیم با این دستور اسم و تگ جدیدی برای آن انتخاب کنیم.
```bash
docer tag [source-tag] [target-tag]
```




---
## search
اگر بخواهیم ایمیجی را پیداکنیم. به طوری پیش فرض متصل به داکر هاب میشود.

```bash 
docker search [image]
```
>> ایمیج های که بعد از آنها / خورده و اسم امده رسمی نیستند nonofficed

---
## inspect
برای اطلاعات از ایمیج میتوانیم 
>> داکر با توجه به معماری manifest سیستم ایمیج ها را دانود میکند.
```bash
docker inspect [id] or [image]
```

---
## rm
با این دستور کانتینر پاک مشیود
```bash 
docker rm -f [name]
```

---
## rmi
 اسم و تگ ایمیج پاک میود با 
```bash
docker  rmi [name:tag]
```
> اگر کانتینری از ایمیج باشد آن ایمیج را پاک نمیکند.

 با این دستور ایمیج untag می شود
 برای پاک کردن ایمیج دنگل شده 
```bash
dcoker image prune # remove all images untag
```

## attch
با این دستور میتونیم به ورودی ها و خروجی ها و ارور ها را میتونیم ببینیم و بهش بچسبیم بعضی از ایمیج ها که بش دارن مثل ubuntu ,centos هستند میره داخل میتونیم دستور بزنیم 
```bash
docker attach moon ping google.com
```
میتوانیم در یک ترمینال که از قبل یا با دستور exec دستوری را اجرا کردیم با این دستور در ترمینالی دیگر ببینیم.


---
## exec
هر دستوری که قابل اجرا باشد در container را اجرا میکند 

در ا ینجا ما  بش را اجرا کردیم در حالی که بش اصلی در centos , ubuntu  ,etc بای ایدی 1 کار میکند اگر با ctrl+d برویم  بیرون همچنان دارد کار میکند.

```bash
docker exec -it 
```
اگر در conrainer هایی که بش دارند بزنیم میره داخل  و همچنان میتونیم دستوری را بدون رفتن در آن اجرا کنیم 

```bash
docker exec -itd centos ping google.com
```
با این روش میتوان متغییری را ست کنیم 

```bash 
docker exec -it -e myvalue=123 centos
```



---
## cp
میتوان فایلی را از روی سیستم بروی container کپی کنیم

```bash
docker cp ./foo/foo.txt centos2:/home/
```

---
## stop
میتوان container را down کرد 

```bash
docker stop -t (20) # after 20 sec is stop
```

---
## wait
وقتی داکر ما متوقف میشود یا down میشود کد خروج را به می گوید و ما را متوجه میکند.
```bash
docker wait centos2 
```

---
## start
کانتینتر را دوباره شروع میکند 
 > -a only out error and output not input
 > -i everything do
 
```bash
docker start -a/-i centos2
```


---
## restart

میتوان container را restart کنیم 
```bash
dcoker restart centos2
```


---
## logs
میتوان از container لاگ گرفت و لاگ ها در مسیر 
> root@xubuntu:/var/lib/docker/containers/2e81a80304d5a1a2d0fde78dc3bfc004b8e5a63b17170f6fd31143dc06b4f5ae#

```bash
docker logs -ft centos2
#   -f, --follow         Follow log output
#   -t, --timestamps     Show timestamps
```
---
## event
خروجی هایی که مانند event است را متوان با 

```bash
dcoker event --since='20m'
```
```bash
dcoker event --filter='event=stop'
```
```bash
dcoker event --filter='type=stop'
```
---
## pause
متوقف کردن container 

```bash
dcoker pause centos2
```

### unpause
از حالت متوقف در می آورد
```bash
dcoker uspause centos2
```

---
## commit 
برای مثال اگر conrainer را تغییر بدیم و بخواهیم از روی آن imageساخته شود
```bash
dcoker commit --name centos2 centos:v3
```
> not recommended for create new image
>> ممکنه دنگل ایمیج باشد که با دستور tag عوض میکنیم

---
## save
> best for create new image

یک ایمیج جدید میسازه و archive میکند

```bash
docker save -o centos.tar.gz
#   -o, --output string     Write to a file, instead of STDOUT
```

## load
یک فایل tar.gz میگیره و باز میکند
```bash
docker load -i centos.tar.gz
#   -i, --input string      Read from tar archive file, instead of STDIN
```
> ممکنه دنگل ایمیج باشد که با دستور tag عوض میکنیم


## export
از کانتینتر ما خروجی میگیرد
```bash
docker export centos2 > centos.tar
```

## import
وارد کردن کانتینتر با فرمت tar
```bash
docker import centos2.tar
```
> ممکنه دنگل ایمیج باشد که با دستور tag عوض میکنیم
>> مکنه با دستور run اجرا نشود

## volume
```bash

```

## networking
```bash

```

## port-mapping