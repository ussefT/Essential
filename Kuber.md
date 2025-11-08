
<div dir="auto">

## 🕸️ Kubernetes (K8s) 

- [Linux](https://github.com/ussefT/Essential/blob/main/Linux.md)
- [Docker](https://github.com/ussefT/Essential/blob/main/Linux.md)

More info in [kubernetes.io](https://kubernetes.io/docs/concepts/overview/)

About Bare Metal [this](https://www.ibm.com/think/topics/bare-metal-dedicated-servers)



#### Why you need Kubernetes and what it can do?
Containers are a good way to bundle and run your applications. In a production environment, you need to manage the containers that run the applications and ensure that there is no downtime. For example, if a container goes down, another container needs to start. Wouldn't it be easier if this behavior was handled by a system?

That's how Kubernetes comes to the rescue! Kubernetes provides you with a framework to run distributed systems resiliently. It takes care of scaling and failover for your application, provides deployment patterns, and more. For example: Kubernetes can easily manage a canary deployment for your system.

Kubernetes provides you with:

- Service discovery and load balancing Kubernetes can expose a container using the DNS name or using their own IP address. If traffic to a container is high, Kubernetes is able to load balance and distribute the network traffic so that the deployment is stable.


- Storage orchestration Kubernetes allows you to automatically mount a storage system of your choice, such as local storages, public cloud providers, and more.


- Automated rollouts and rollbacks You can describe the desired state for your deployed containers using Kubernetes, and it can change the actual state to the desired state at a controlled rate. For example, you can automate Kubernetes to create new containers for your deployment, remove existing containers and adopt all their resources to the new container.


- Automatic bin packing You provide Kubernetes with a cluster of nodes that it can use to run containerized tasks. You tell Kubernetes how much CPU and memory (RAM) each container needs. Kubernetes can fit containers onto your nodes to make the best use of your resources.


- Self-healing Kubernetes restarts containers that fail, replaces containers, kills containers that don't respond to your user-defined health check, and doesn't advertise them to clients until they are ready to serve.


- Secret and configuration management Kubernetes lets you store and manage sensitive information, such as passwords, OAuth tokens, and SSH keys. You can deploy and update secrets and application configuration without rebuilding your container images, and without exposing secrets in your stack configuration.


- Batch execution In addition to services, Kubernetes can manage your batch and CI workloads, replacing containers that fail, if desired.


- Horizontal scaling Scale your application up and down with a simple command, with a UI, or automatically based on CPU usage.


- IPv4/IPv6 dual-stack Allocation of IPv4 and IPv6 addresses to Pods and Services


- Designed for extensibility Add features to your Kubernetes cluster without changing upstream source code.

</div>

------
<div dir="auto">

### چرا Kubernetes وجود دارد؟
فرض کنید یک برنامه‌ی وب دارید که با Docker به صورت کانتینر اجرا می‌شود. در ابتدا روی یک سرور اجرا می‌کنید، ولی با رشد کاربران نیاز به:

اجرای همزمان چندین کپی از کانتینر (برای مقیاس‌پذیری)
 
مدیریت خودکار شکست (اگر یک کانتینر crash کرد، دوباره راه‌اندازی شود)

توزیع ترافیک بین نسخه‌ها (Load Balancing)

به‌روزرسانی بدون downtime (Rolling Updates) 

مدیریت ذخیره‌سازی، شبکه، امنیت، و ...
دارید. Kubernetes یک پلتفرم اورکستراتوری (Orchestration) است که این کارها را برای شما انجام می‌دهد.

به دلیل هزینه های زیاد سرور نمیتونیم برنامه ها را اجرا کنیم و تداخل وابستگی ها خیلی مشکل بود. 

🧩 کوبرنتیس (Kubernetes) چیه؟

به‌صورت ساده، Kubernetes (که بهش “کوبر” یا “کوبرنتیس” یا حتی “K8s” هم می‌گن)،
یه سیستم هوشمند برای مدیریت خودکار برنامه‌ها در کانتینرها (containers) هست.
</div>

----
## ⚙️ Install 
<div dir="ltr">

</div>

----

<div dir="rtl">

### Container Orchestration Engines
 مثلا اگر قرار باشه سرویس های زیادی اجرا کنیم از docker-compose استفاده میکنیم و تقریبا فایل هایشان یکی است.چون ارتباط بین container مقداری مشکل است ما به سمت orchestration میرویم. و به نوعی رهبر container ها حساب میشود و مدیریت میکنند. بین اناها هماهنگی برقرار میکنید با استفاده از kuber.

- Docker Swarm 
> برای سرویس های کوچک تر و محیط های آزمایشگاهی اجرا میکنیم 

![docker-swarm](https://github.com/ussefT/Essential/blob/kuber/res/docker-swarm.jpg)

در docker swarm ما دو تا node داریم.
- Leader
>
- Reachable
> گره‌های دیگر (به‌ویژه سایر managerها) می‌توانند با گره‌ی leader ارتباط شبکه‌ای برقرار کنند.

- no tag (هیچ نوعی ندارند)


---
#### 🚀 چرا بهش نیاز داریم؟


فرض کن یه برنامه‌ی وب داری که شامل چند بخشه:

- backend (مثلاً با Django یا Node.js)

- frontend (مثلاً React)

- database (مثلاً PostgreSQL)

می‌خوای اینا رو در محیط‌های مختلف (توسعه، تست، تولید) راحت اجرا و مدیریت کنی.
برای این کار معمولاً از Docker استفاده می‌کنی تا هر بخش رو داخل یه کانتینر بذاری.

اما... وقتی برنامه بزرگ شد چی؟ 😅
مثلاً:

باید ده‌ها یا صدها کانتینر رو اجرا کنی.

بعضیا crash می‌کنن و باید خودکار ری‌استارت شن.

باید لود بالانس بین چند سرور انجام بشه.

باید آپدیت بدون downtime داشته باشی.

اینجاست که Kubernetes وارد میشه. 🦾

---
#### ⚙️ کوبرنتیس چه کار می‌کنه؟ 

Kubernetes مثل یه مدیر کارخانه‌ی هوشمنده که همیشه وضعیت رو زیر نظر داره و کارها رو خودش تنظیم می‌کنه:

| وظیفه                           | توضیح                                                         |
| ------------------------------- | ------------------------------------------------------------- |
| 🚚 **Deployment خودکار**        | خودش برنامه‌هاتو در چند سرور اجرا می‌کنه.                     |
| 💪 **خوددرمانی (Self-healing)** | اگه یکی از پادها (Pods) خراب شه، خودکار دوباره ایجادش می‌کنه. |
| 📈 **Scaling خودکار**           | اگه فشار زیاد شد، خودش کانتینرهای بیشتری اجرا می‌کنه.         |
| 🔁 **Rolling Updates**          | آپدیت برنامه بدون قطعی انجام می‌ده.                           |
| ⚖️ **Load Balancing**           | درخواست‌ها رو بین نسخه‌های مختلف پخش می‌کنه.                  |

---
## node master
در Kubernetes (کوبرنتیس)، نودها (Nodes) به دو نوع اصلی تقسیم می‌شوند:

- Master Nodes (یا Control Plane Nodes)

- Worker Nodes

نود مستر در واقع مغز یا کنترل‌کننده‌ی کل خوشه (Cluster) کوبرنتیسه.
تمام تصمیم‌گیری‌ها، زمان‌بندی‌ها (scheduling)، و نظارت بر وضعیت (state management) توسط مستر انجام می‌شن.

می‌تونی بگی که:

> Master Node = بخش “مدیریتی” کوبرنتیس
Worker Node = بخش “اجرایی” که پادها (Pods) رویش اجرا می‌شن

![node-master-slave](https://github.com/ussefT/Essential/blob/kuber/res/kuber-master-slave.png)

####  اجزای اصلی مستر نود

هر مستر شامل چند جزء (Component) مهمه:

1. kube-apiserver

درگاه اصلی ارتباط با کل خوشه است (هم کاربران و هم سایر اجزا با آن صحبت می‌کنند).

هر دستوری که با kubectl می‌فرستی، اول به API Server می‌ره.

2. etcd
> یک دیتابیس no sql است که config های ما در اینجا ذخیره میشود. 

دیتابیس کل خوشه است.

تمام اطلاعات وضعیت (State) کوبرنتیس در etcd ذخیره می‌شه (مثل اینکه کدوم پادها در حال اجرا هستن و روی چه نودی).

3. kube-scheduler

تصمیم می‌گیره که هر پاد روی کدام Worker Node اجرا بشه، بر اساس منابع آزاد، محدودیت‌ها، و policyها.

4. kube-controller-manager

> الگوریتم ها در این قسمت قرار دارد 

شامل چندین کنترلر (Controller) است که وضعیت خوشه را همیشه با وضعیت مورد انتظار هماهنگ نگه می‌داره.
مثل:

- Node Controller (نظارت بر نودها)

- Replication Controller (مدیریت Replicaها)

- Endpoint Controller و غیره.

5. cloud-controller-manager (اختیاری)

در محیط‌های ابری (Cloud) مثل AWS، GCP یا Azure استفاده می‌شه برای ارتباط با APIهای آن پلتفرم.

![cluster architecture](https://github.com/ussefT/Essential/blob/kuber/res/kuber-cluster-architecture.jpg)

---
## 🧩 تعریف ساده‌ی Kubernetes Cluster

یک Kubernetes Cluster (خوشه) یعنی مجموعه‌ای از ماشین‌ها (Nodeها) که با هم کار می‌کنن تا برنامه‌های کانتینری تو رو به‌صورت خودکار و قابل‌اعتماد اجرا کنن.

یعنی به جای اینکه یه برنامه فقط روی یه سرور اجرا بشه، تو چندین سرور پخش می‌شه و کوبرنتیس همه‌ی اون‌ها رو مثل یک سیستم واحد کنترل می‌کنه.

⚙️ اجزای اصلی یک Cluster

یک خوشه از دو بخش اصلی ساخته شده 👇

1. 🧠 Control Plane (یا Master Node)

این مغز خوشه‌ست. وظیفه‌اش تصمیم‌گیری و مدیریت کل سیستم هست.

اجزای مهمش:

kube-apiserver → درگاه اصلی ارتباط با cluster

etcd → دیتابیس خوشه

kube-scheduler → تصمیم می‌گیره هر پاد کجا اجرا شه

controller-manager → بررسی می‌کنه همه‌چیز درست کار کنه

📘 در واقع Control Plane فقط “دستور” می‌ده و هیچ پاد (برنامه واقعی) رویش اجرا نمی‌شه.

2. 💪 Worker Nodes (نودهای کارگر)

اینا همون سرورهایی‌ان که برنامه‌ها (Pods) روشون اجرا می‌شن.
هر Worker Node شامل اجزای زیره:

kubelet → با مستر در ارتباطه و دستورات رو اجرا می‌کنه.

kube-proxy → شبکه بین پادها و سرویس‌ها رو مدیریت می‌کنه.

Pods → واحد اجرایی اصلی که برنامه‌ات داخلشه (مثلاً یه کانتینر Flask یا React).

### تصویر ذهنی (مثال واقعی) 

فرض کن یه فروشگاه زنجیره‌ای داری 🍕

مدیر مرکزی (Control Plane) فقط تصمیم می‌گیره کی چی بپزه، کی کمبود نیرو داره و کی زیاد.

شعبه‌ها (Worker Nodes) خودشون غذا درست می‌کنن (برنامه‌ها رو اجرا می‌کنن).

اگه یه شعبه خراب بشه (Crash)، مدیر می‌گه “خب یکی دیگه رو جایگزین کن”.

🧠 نکته مهم: ارتباط Master و Worker

ارتباط بینشون معمولاً از طریق پروتکل‌های امن (TLS/HTTPS) انجام می‌شه.
Master فقط دستورات مدیریتی می‌فرسته، Worker فقط گزارش وضعیت خودش رو می‌ده و پادها رو اجرا می‌کنه.


</div>






















