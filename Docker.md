<div dir="rtl"></div>

## Docker 🐋
داکر یک پلتفرمی که از هسته ی سیستم عامل استفاده میکند که میاد فایل های ایمیج را روی ماشین مجازی اجرا و تبدیل به کانتینر میشود.

### container

کانتینر یک محیط ایزوله و جدای از محیط بیرون هستند که میتوانند یک ایمیج را اجرا کنند.

- [Install on Linux](https://github.com/ussefT/Essential/blob/main/Docker.md#install-on-linux)
- [command](https://github.com/ussefT/Essential/blob/main/Docker.md#command)


## Install on Linux 🐧

- [Install Linux](https://github.com/ussefT/Essential/blob/main/Linux.md)

برای نصب روی لینوکس در هر ورژنی :
- [Docker in linux](https://docs.docker.com/engine/install/ubuntu/)


## command 💻

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
- [storage driver]()

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
## run 🏃‍♂️
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
### memory 📝
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
## search 🔍
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

اطلاعات container مخصوص
```bash
docker inspect --format="{{.Mounts}}" moon
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
## stop ⛔
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

متونیم لاگ بگیریم از کار کرد یک container 
```bash
docker run -it --log-opt centos2
```

در  حالت پیش فرض لاگ ها را به ما به صورت لایو نشون میده


دراین حالت لاگ ها را در بافر میریزد
```bash
docker run it --log-opt mode=none_blocking --log-opt max-buffer-size=4m centos:latest ping google.com
```
در این مسیر container 
> /var/docker/container/(id)_log

میتونیم 
```text
 {
    "log-driver":"syslog"
 }
```
در مسیر 
> /etc/docker/daemon.json
>> if not exist create 
or 
```text

{
    "log-driver":"json-file",
    "log-opts":
    {
        "max-size":"10m",
        "max-file":"3",
        "labels":"production_status",
        "env":"os,customer",
    }
}
```
عوض  کردن فرمت json به local و فایلی در مسیر 
> /var/lib/docker/containers/id_container
```bash
docker run -itd --name sun --log-driver local --log-opt max_size=10m --log-opt max-file=3 centos:latest echo Hi
```
و میتونیم به این صورت فایل خروجی log را به این صورت حروجی بگیریم

```bash
docker run --itd --name moon --log-opt tag="{{.ImageName}}{{.Name}}{{.ID}}" centos:latest
```
فایل در مسیر 
> /var/lib/docker/container/id_container/..

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

---
## volume
در داکر ما دونوع حافظه داریم 

- persistent storage (حافظه ی مهم)
- none-persistent storage (حافظه بی اهمیت)

به صورت پیش فرض اگر حافظه ای یا مکانی را برای ذخیره ی داده در container تعیین نکنیم بع داز اینکه container افتاد داده های ما از بین میرن.

- [bind mount]()
> save on disk (every space)
- [tmpfs]()
> save on ram (only use in linux)
- [volume]()
> save on disk but protect by Docker 

### volume
- در والیوم ها میتوان همزمان چند container از یک مسیر و در فایل اسفاده کنند
- اطلاعات در صورتی پاک میشود که دستور مستقیم بدیم پاک کنه
- بک اپ گرفتن و ذخیره کردن و منتقل کردن فایل های با والیوم

تفاوت volumes , bind mount
- دستورات cli در داکر با volume ها سریع تر و بهتر مدیریت میشود
- امنیت در volume ها بیشتر است 
- در volume اگر آدرس نباشد ایجاد میکند ولی bind mounts خطا میدهد.



وقتی ما مسیری را از روی دیسک بروی container مضخص میکنیم. داده به صورت خودکار بروی کانتینتر کپی مشود و قابل استفاده و در مسیر
> /var/lib/docker/volumes/(name)/....data

در اینجا فایل از هر دوطرف هاست داکر و container قابل رویت است.

ایجاد
```bash
docker volume create myvol
```
```bash
docker volume create --name myvol --label myval=123
```

همه ی volume
```bash
docker volume ls
```
اطلاعات از volume 
```bash
docker volume inspect myvol
```

برای یک container یک volume تعریف میکنیم که اگر پوشه ای نباشد خودش ایجاد میکنه
```bash
docker run --itd --name moon -v myvol:/app centos:latest
```
> یکی از مزیت های volume ها اینه container حذف شود و یکی دیگر بالا بیاد فایل های هم داخلش است


امکان تعریف کردن از مسیر داخل هاست به داخل container هم هست.
```bash
docker run -it -v /tmp/dir:/mydata centos:latest
# -v if volume dose not exist , will create it automatically
```
> اگر مسیر تعریفی برای container نباشد خودش ایجاد میکند.


پیداکردن containerاز روی volume 
```bash
docker ps -a --filter volume=myvol
```

اگر خواستیم فایل ما بروی سیستم روی هاست دیگر ذخیره بشه
```bash
docker volume create --drive local --opt type=nfs --opt o=add=192.168.56.106,rw --opt device=:/path myvol
```
> local : This means the volume was create with the default local driver, and is only available to containers on this Docker host 

#### rm volume
اگر volume در حال استاده باشد نمیتونیم پاک کنیم و این دستور پاک میشود

```bash
docker volume rm myvol
```

با این دستور او volume های بدون استفاده پاک میشوند
```bash
docker volume prune
```


میتوان دسترسی read , write تعیین کرد بروی volume
```bash
dcoker run -it -v myvol:/data:ro centos:latest
```

### tmpfs
اگه لخوایم از این ویژگی لینوکس استفاده کنیم 
```bash
docker run -itd --name mycent --tmpfs /tmp centos:lastes
```
or
```bash
docker run -itd --name mycent --mount type=tmpfs,destination=/tmp centos:latest
```


### bind mount

```bash
docker volume create myvol
```

```bash
docker volume create myvol
```
---
## storage drives
هر داکر containerمحیط ذخیره سازی خودشو داره. و این محیط توسط storage driver مدیریت میشود.
بعضی از storage drivers در داکر و موجود در linux:
- aufs(the original and oldest)
- overlay2(probably the best choise for the future)
- devicemapper
- btfrfs
- zfs

میتونیم در داکر لینوکس نوع این را تغییر بدیم و در مسیر 
> /etc/docker/daemon.json 
>> if not exist create that.

```text

{
    "storage-driver":"overlay2"
}

```
restart docker 
```bash
sudo systemctl restart docker
```




---
## networking

Dcoker networking comprises three major components:
- The Container Network Model
- Libnetwork
- Drivers

در مدل Container Network Model (CNM) سه مدل داریم:

- 1-sandbox (is an isolated network stack, It includes; Ethernet interface, ports , routing tables, adn DNS config)
- 2-endpoint (are virtal network interface. Like normal network interface, they re resposible for making connections)
- 3-network (are a software implementation of an 802.1d bridge (morecommonly known as a switch))

هر container sandboxخودشو داره.

وقتی داکر نصب میشود 

- 1-bridge (روی لایه 2 مجازی لوکال و روی سینگل هاست به صورت پیش فرض فعاله )
- 2-host (هر شخصی سازی در ماشین که شامل DNS ,... میشود با داکر یکی میشود و هیچ فضایی بین آنها نیست)
- 3-none (غیرفعال کردن شبکه داکر)

گرفتن network
```bash
docker network ls
```
### docker network driver
![network driver]()


گرفتن اطلاعات از network bridge
```bash
docker network inspect bridge
```

با این کد میتوان ethernet داکر هاست را دید و در این بازه containerهایی که بالا میآیند در محدوده هستند

![cnm_docker]()
![cnm_docker2]()

### create network

create network bridge/overlay
```bash
docker network create -d bridge/overlay mynet
```
> -d for bridge/overlay


for run 
```bash
docker run -it --name mycent --ntwork mynet centos:latest
```

If connect to container
```bash
docker network connect/disconnect mynet mycentos
```

for exmaples:
```bash
docker run -itd --name myn --network localhost -p 5000:80 nginx:latest
```
> -p 5000 enable own port 
>> 80 for container is up

نشان دادن پورت های container
```bash
docker port myn
```

---
## port-mapping




---
## Dockerfile
اسم این میتوان کوچک یا بزرگتر نوشت ولی به این صورت تعیین شده است.

میتوان ایمیج خودمان را درست کنیم.

در همون مسیر که فایلمان هست که تبدیل به docker image بشه 

- FROM
یعنی که از ایمیجی استفاده کنیم
```text
FROM centos:latest # use image centos
```
از هیچ ایمیج استفاده نکند 

```bash
FROM scratch
```

بخواهیم توضیحات یا ورژن یا هر چیز دیگه به عنوان متن بزاریم 

```text
LABEL description="this is a sample"
LABEL version="1.0.0"
LABEL maintainer="l"
```

بخواهیم فقط فایل را کپی کنیم که در مسیر داکر فایل اصلی هست و نه فایل دیگر یا آدرس وب
```text
COPY test.txt j.txt /app/
```
حتما در آخر مسر باید / بزاریم


اگر بخواهیم فایلی با فرمت tar, tar.gz, rar و ... بدیم با این دستور که خودش به صورت خودکار میاد untar میکند
```text
ADD t.tar /app2/
```


یک دستوری را اجرا کندو یا پکیجی را نصب کند
```text
RUN echo hi
```


متغییر گلوبالی تعریف کنیم که در container ما قایل دسترس است
```text
ENV myvar=123
```
in container
```text
echo $myvar # out: 123
```

با یوزری و یا با دسترسی ویژه ای این دستورات را انجام دهیم از اون خطی که تعریف میکنیم از اون دسترسی انجام میشود
```text
USER root
```

با این دستور مسیر از این خط به بعد اگر مسیر به آن معرفی نکنیم از این اجرا میکند
```text
ENV workpath=/home/sample
WORKDIR $workpath
```
وقتی بیلد میشه و container را بالا میاریم در این مسیر میاد بالا

مثال 

```text
FROM centos:centos7.9.2009
ENV myvar=123
ENV workpath=/home/sample
WORKDIR $workpath
COPY t1.txt .
```

استفاده از volume که میتونیم تعریف کنیم و مسیر آن را ایجاد میکند و تا زمانی که اجرا بشود و تا تعریف نکنیم براش مشخص نمیشود
- بیشتر برای داکیومنت دارد
این مسیر container ایجاد میشود
````text
VOLUME /myvol1 or ["/myvol1","myvol2"]
````
موقع اجرا
```bash
docker run -it --name mycent -v /home/test1:/myvol1 -v /home/test2:/myvol2 mycentos:v2
```

با این container ما بر روی این پورت در ال اجرا هست ولی هنوز از بیرون قابل استفاده نیست باید در هنگام اجرا پورت مپینگ انجام بدیم

```text
EXPOSE 80/tcp
```
زمانی که container ما میاد میتونه یک ماموریتی داشته باشه 
به سه شکل وجود داره 

```text
CMD ["/bin/bash"]
# CMD ["executablel", "param1", "param2"]
# CMD ["param1","param2"]
# CMD command1 command2
```
برای اینکه موقع اجرا کار دیگری انجام دهد 
```bash
docker run -it --name gg centos:latest /bin/bash
```
این هم مانند cmd است. Enterypoint 
```text
ENTRYPOINT ["executable","param1","param2"]

```
اگر هر دو entrypoint و cmd داشتیم. ماموریت داکر فایل مورد استفاده میشود. اگر دو مورد بود : 
- 1- هر دو باید به صورت exec باشد 
- 2- چیزی که جلوی cmd میاریم پاس داده میشود به entrypoint

exmaple

```text
FROM centos:latest
LABEL name="name"
ENTRYPOINT ["ping"]
CMD ["8.8.8.8"]
```

example2
```text

FROM centos:latest
RUN yum install -y httpd
EXPOSE 80/tcp
VOLUME /var/www/html
ENTRYPOINT /usr/sbin/httpd && /bin/bash 
```
/usr/sbin/httpd && /bin/bash 
> به معنی اینه که چون یه کاری انجام میده و بعد میوفته. بعدش به کارش ادامه بده با /bin/bash ادامه میدیم

### HealthCheck
برای بررسی درست کار کردن container باید چک کنیم دستوری را که تعریف میکنیم اجرا نکرده ولی container بالا است 

```text
FROM centos:centos7.9.2009

LABEL description="this is a sample"
LABEL version="1.0.0"
LABEL maintainer="l"

RUN echo salam

HEALTHCHECK --interval=2m --timeout=3s CMD curl 127.0.0.1 || exit 1
CMD /usr/sbin/httpd
```

بعد با این دستور میتوان دید که Health چه وضعیتی است.
```bash
docker inspect mycent
```







