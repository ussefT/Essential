## Docker
داکر یک پلتفرمی که از هسته ی سیستم عامل استفاده میکند که میاد فایل های ایمیج را روی ماشین مجازی اجرا و تبدیل به کانتینر میشود.

### container
containerها یک محیط ایزوله و جدای از محیط بیرون هستند که میتوانند یک image را اجرا کنند.

- [Install on Linux]()
- [command]()


## Install on Linux

- [Install Linux]()

برای نصب روی لینوکس در هر ورژنی :
```bash

```


## command

- [pull]()
- [run]()
> -it
> -itd
- [images]()
- [ps]()
- [stats]()
- [tag]()
- [inspect]()
- [attach]()
- [exec]()
- [cp]()
- [log]()
- [event]()
- [volume]()
- [networking]()
- [port-mapping]()

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

میتونیم برنامه ی دیگری به غیر از bash را انجام دهیم .
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



---
## ps
کانیتر ها یک طول عمری دارند و مشغول انجام کاری هستند و وقتی تموم میشوند exit میشوند.
 با این دستور تمام کانتینر های up را میشه دید.
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


---
## inspect