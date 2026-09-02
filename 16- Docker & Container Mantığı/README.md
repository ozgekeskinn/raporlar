# Docker & Container Mantığı

## İçindekiler

1. [Docker Nedir?](#1-docker-nedir)
2. [Docker Neden Ortaya Çıktı?](#2-docker-neden-ortaya-cikti)
3. [Container Nedir?](#3-container-nedir)
4. [Container Nasıl Çalışır?](#4-container-nasil-calisir)
5. [Container İzolasyonu Nasıl Sağlanır?](#5-container-izolasyonu-nasil-saglanir)
6. [Container Yaşam Döngüsü](#6-container-yasam-dongusu)
7. [Docker Image Nedir?](#7-docker-image-nedir)
8. [Docker Image Katmanları](#8-docker-image-katmanlari)
9. [Image ve Container Arasındaki Fark](#9-image-ve-container-arasindaki-fark)
10. [Docker Mimarisi](#10-docker-mimarisi)
11. [Docker Client ve Docker Daemon](#11-docker-client-ve-docker-daemon)
12. [Docker Registry ve Docker Hub](#12-docker-registry-ve-docker-hub)
13. [Dockerfile Nedir?](#13-dockerfile-nedir)
14. [Dockerfile Komutları](#14-dockerfile-komutlari)
15. [Docker Build Mantığı](#15-docker-build-mantigi)
16. [Docker Build Cache](#16-docker-build-cache)
17. [Docker Port Mapping](#17-docker-port-mapping)
18. [Docker Networking](#18-docker-networking)
19. [Docker'da Veri Kalıcılığı](#19-dockerda-veri-kaliciligi)
20. [Volume, Bind Mount ve tmpfs](#20-volume-bind-mount-ve-tmpfs)
21. [Environment Variables](#21-environment-variables)
22. [Docker Compose Nedir?](#22-docker-compose-nedir)
23. [Gerçek Bir Full-Stack Projede Docker](#23-gercek-bir-full-stack-projede-docker)
24. [Docker ve Virtual Machine Farkı](#24-docker-ve-virtual-machine-farki)
25. [Docker Neden VM'den Daha Hafiftir?](#25-docker-neden-vmden-daha-hafiftir)
26. [Docker'ın Avantajları](#26-dockerin-avantajlari)
27. [Docker'ın Dezavantajları ve Sınırlamaları](#27-dockerin-dezavantajlari-ve-sinirlamalari)
28. [Docker ve Mikroservis Mimarisi](#28-docker-ve-mikroservis-mimarisi)
29. [Docker ve CI/CD](#29-docker-ve-cicd)
30. [Docker Güvenliği](#30-docker-guvenligi)
31. [Dockerfile Best Practices](#31-dockerfile-best-practices)
32. [Temel Docker Komutları](#32-temel-docker-komutlari)
33. [Docker Debugging ve Loglama](#33-docker-debugging-ve-loglama)
34. ["Benim Bilgisayarda Çalışıyordu" Problemi](#34-benim-bilgisayarda-calisiyordu-problemi)
35. [Sık Yapılan Docker Hataları](#35-sik-yapilan-docker-hatalari)
36. [Docker Hakkında Yanlış Bilinenler](#36-docker-hakkinda-yanlis-bilinenler)
37. [Mülakat Soruları ve Cevapları](#37-mulakat-sorulari-ve-cevaplari)
38. [Özet Karşılaştırma Tabloları](#38-ozet-karsilastirma-tablolari)
39. [Genel Sonuç](#39-genel-sonuc)

---

<a id="1-docker-nedir"></a>

# 1. Docker Nedir?
**Docker**, uygulamaların ihtiyaç duyduğu bağımlılıklarla birlikte paketlenmesini ve **container adı verilen izole çalışma ortamlarında** çalıştırılmasını sağlayan bir containerization platformudur. 
Bir uygulama yalnızca yazdığımız kaynak koddan oluşmaz. Örneğin bir ASP.NET Core uygulamasının çalışabilmesi için aşağıdakilerin doğru olması gerekebilir:

* .NET Runtime
* Belirli bir .NET sürümü
* İşletim sistemi kütüphaneleri
* Environment variable'lar
* Uygulama bağımlılıkları
* NuGet paketleri
* Belirli port ayarları
* Veritabanı bağlantıları

Benzer şekilde bir React uygulamasında:

* Node.js
* npm
* Belirli Node.js sürümü
* `package.json`
* npm paketleri

gereklidir. Normal şartlarda uygulamayı başka bilgisayara taşıdığımızda bütün bu ortamın yeniden hazırlanması gerekir. Docker'ın temel amacı şudur:

> **Uygulamayı yalnızca kaynak koduyla değil, çalışması için gereken ortamla birlikte paketlemek.**

Böylece geliştiricinin bilgisayarında çalışan uygulamanın test, staging veya production ortamında da mümkün olduğunca aynı şekilde çalışması sağlanır.

---

<a id="2-docker-neden-ortaya-cikti"></a>

# 2. Docker Neden Ortaya Çıktı?

Docker'ın çözdüğü en büyük problemlerden biri yazılım dünyasının meşhur cümlesidir:

> **"Ama benim bilgisayarımda çalışıyordu."**

Bir uygulamanın geliştiricinin bilgisayarında çalışmasına rağmen başka bir bilgisayarda çalışmamasının birçok sebebi olabilir.

### Örneğin

Developer A:

```text
Node.js 22
PostgreSQL 17
Ubuntu
```

kullanıyor olabilir. Developer B:

```text
Node.js 20
PostgreSQL 16
Windows
```

kullanıyor olabilir. Production sunucusunda ise:

```text
Node.js 22
PostgreSQL 17
Linux
```

bulunabilir. Kod aynı olsa bile environment farklı olduğu için uygulamanın davranışı değişebilir. Buna genel olarak:

```text
Environment inconsistency
```

yani **ortam tutarsızlığı** problemi denilebilir. Docker bu problemi şu yaklaşım ile çözer:

```text
Uygulama
   +
Runtime
   +
Dependencies
   +
Libraries
   +
Configuration
   ↓
Docker Image
```

Bu image nerede çalıştırılırsa çalıştırılsın aynı çalışma ortamının tekrar oluşturulması amaçlanır.

---

<a id="3-container-nedir"></a>

# 3. Container Nedir?

**Container**, bir uygulamanın ihtiyaç duyduğu dosyalar, bağımlılıklar ve çalışma ortamıyla birlikte izole edilmiş şekilde çalışan bir **process ortamıdır**. Container'ı küçük bir sanal bilgisayar gibi düşünmek başlangıçta yardımcı olabilir fakat teknik olarak container bir Virtual Machine değildir. Daha doğru tanım:

> Container, host işletim sisteminin kernel'ini paylaşarak çalışan izole edilmiş process veya process grubudur.

Örneğin bilgisayarımızda:

```text
Container 1
└── React Frontend

Container 2
└── ASP.NET Core API

Container 3
└── PostgreSQL

Container 4
└── Redis
```

çalışabilir. Her container kendi:

* Dosya sistemine
* Process alanına
* Network ortamına
* Environment variable'larına
* Kaynak sınırlarına

sahipmiş gibi davranabilir. Ancak tüm container'lar altta bulunan host işletim sisteminin kernel'ini paylaşabilir.

---

## Container'ın Temel Özellikleri

### İzolasyon

Bir container'daki process diğer container'lardan büyük ölçüde ayrılmıştır.

### Hafiflik

Her container kendi işletim sistemini çalıştırmadığı için VM'lere göre daha hafiftir.

### Taşınabilirlik

Image'ın çalıştırılabildiği uyumlu bir Docker ortamında aynı uygulama tekrar çalıştırılabilir.

### Hızlı Başlatma

Yeni bir işletim sistemi boot edilmediğinden container'lar genellikle hızlı başlatılır.

### Tekrarlanabilir Ortam

Development, testing ve production ortamları arasındaki fark azaltılır.

---

<a id="4-container-nasil-calisir"></a>

# 4. Container Nasıl Çalışır?

Bir Docker container oluşturulduğunda basitleştirilmiş süreç şöyledir:

```text
Docker Image
      ↓
docker run
      ↓
Container oluşturulur
      ↓
Writable Layer eklenir
      ↓
Container içerisindeki ana process başlatılır
      ↓
Uygulama çalışmaya başlar
```

Örneğin:

```bash
docker run nginx
```

komutu çalıştırıldığında Docker:

1. Bilgisayarda `nginx` image'ının bulunup bulunmadığını kontrol eder.
2. Yoksa registry'den image'ı indirir.
3. Image üzerinden yeni bir container oluşturur.
4. Container'a yazılabilir bir katman ekler.
5. Gerekli network yapılandırmasını hazırlar.
6. Image'ın tanımladığı başlangıç process'ini çalıştırır.

Böylece Nginx çalışmaya başlar.

---

## Container = Process

Docker öğrenirken anlaşılması gereken en önemli noktalardan biri budur:

```text
Container ≠ Tam işletim sistemi
```

Container'ın temelinde çalışan process vardır. Örneğin:

```text
Container
└── nginx process
```

veya:

```text
Container
└── dotnet RoomCraft.Api.dll
```

olabilir. Container'ın ana process'i sona ererse container da genellikle durur.

---

<a id="5-container-izolasyonu-nasil-saglanir"></a>

# 5. Container İzolasyonu Nasıl Sağlanır?

Docker özellikle Linux kernel'in sunduğu bazı mekanizmalardan yararlanır. Bunların en önemlileri:

```text
Namespaces
Cgroups
Capabilities
Filesystem isolation
```

---

## 5.1 Namespaces

**Namespace**, process'lerin sistem kaynaklarını farklı görmesini sağlayan kernel özelliğidir. Basitçe:

> Her container'a kendine ait küçük bir sistem görünümü verir.

Örneğin container kendi process listesini görür. Host'ta:

```text
PID 1000 → nginx
PID 1001 → postgres
PID 1002 → dotnet
```

olabilir. Ancak nginx container'ının içerisinden bakıldığında:

```text
PID 1 → nginx
```

görülebilir. Container host'taki bütün process'leri görmek zorunda değildir. Namespace türleri arasında:

* PID Namespace
* Network Namespace
* Mount Namespace
* IPC Namespace
* UTS Namespace
* User Namespace

gibi yapılar bulunur.

### PID Namespace

Process'leri birbirinden ayırır.

### Network Namespace

Container'a ayrı:

* Network interface
* IP
* Routing table

gibi network kaynakları sağlar.

### Mount Namespace

Dosya sistemi mount noktalarını birbirinden ayırır.

### UTS Namespace

Hostname gibi sistem bilgilerini izole eder.

---

## 5.2 Cgroups

**Control Groups (cgroups)** sistem kaynaklarının process'ler arasında kontrol edilmesini sağlar. Örneğin bir container'a:

```text
Maximum RAM: 512 MB
Maximum CPU: 1 Core
```

gibi sınırlar uygulanabilir. Böylece tek bir container'ın bütün sunucu kaynaklarını tüketmesinin önüne geçilebilir. Örneğin:

```bash
docker run --memory="512m" nginx
```

container'ın kullanabileceği belleği sınırlandırmak için kullanılabilir. Kısaca:

```text
Namespace → Ne görebiliyor?
Cgroup    → Ne kadar kullanabiliyor?
```

Bu ayrım oldukça önemlidir.

---

<a id="6-container-yasam-dongusu"></a>

# 6. Container Yaşam Döngüsü

Bir container farklı durumlarda bulunabilir.

```text
Created
   ↓
Running
   ↓
Paused
   ↓
Running
   ↓
Stopped
   ↓
Removed
```

### Created

Container oluşturulmuştur fakat henüz process çalıştırılmamıştır.

### Running

Container'ın ana process'i çalışmaktadır.

### Paused

Container process'leri geçici olarak durdurulmuştur.

### Stopped / Exited

Container bulunmaktadır fakat ana process artık çalışmamaktadır.

### Removed

Container tamamen silinmiştir.

---

## `docker stop` ve `docker rm` Farkı

```bash
docker stop my-container
```

container'ı durdurur fakat silmez.

```bash
docker rm my-container
```

container'ı siler. Bu nedenle:

```text
STOP ≠ DELETE
```

---

<a id="7-docker-image-nedir"></a>

# 7. Docker Image Nedir?

**Docker Image**, container oluşturmak için kullanılan değiştirilemez yani **immutable bir şablondur**. Image içerisinde uygulamanın çalışabilmesi için gereken:

* Uygulama kodu
* Runtime
* Kütüphaneler
* Bağımlılıklar
* Dosyalar
* Bazı environment/configuration değerleri
* Başlangıç komutu

bulunabilir. Örneğin:

```text
roomcraft-api:1.0
```

isimli image içerisinde:

```text
Linux kullanıcı alanı dosyaları
.NET Runtime
ASP.NET Core Runtime
RoomCraft API
NuGet bağımlılıkları
Başlangıç komutu
```

bulunabilir. Bu image kullanılarak:

```text
Container A
Container B
Container C
```

oluşturulabilir. Yani:

```text
Image
 ├── Container 1
 ├── Container 2
 └── Container 3
```

---

<a id="8-docker-image-katmanlari"></a>

# 8. Docker Image Katmanları

Docker image'ları tek büyük dosya şeklinde düşünülmemelidir. Image'lar **layer yani katmanlardan** oluşur.

Örneğin:

```dockerfile
FROM node:22
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
CMD ["npm", "start"]
```

için kavramsal olarak şöyle bir yapı oluşabilir:

```text
Layer 1 → Base Node.js image
Layer 2 → Working directory
Layer 3 → package.json
Layer 4 → npm dependencies
Layer 5 → Application source code
Layer 6 → Metadata
```

Katman yapısının önemli avantajlarından biri tekrar kullanımdır. Örneğin iki image da:

```dockerfile
FROM node:22
```

kullanıyorsa Docker aynı temel katmanları tekrar tekrar indirmek zorunda kalmayabilir. Bu:

* Disk kullanımını azaltır.
* Build işlemlerini hızlandırabilir.
* Image paylaşımını kolaylaştırır.

---

## Immutable Ne Demektir?

Image oluşturulduktan sonra mevcut image doğrudan değiştirilmez. Değişiklik gerekiyorsa:

```text
Eski Image
   ↓
Dockerfile değişir
   ↓
Yeni build
   ↓
Yeni Image
```

oluşturulur. Bu yaklaşım deployment'ların daha tahmin edilebilir olmasına yardımcı olur.

---

<a id="9-image-ve-container-arasindaki-fark"></a>

# 9. Image ve Container Arasındaki Fark

Docker'ın en önemli mülakat sorularından biridir.

### Kısa tanım

> **Image şablondur, container ise bu şablonun çalışan instance'ıdır.**

Programlama dünyasından benzetme yapılırsa:

```text
Class      → Image
Object     → Container
```

Tam anlamıyla aynı kavramlar olmasalar da başlangıç için oldukça faydalı bir benzetmedir.

---

| Image                                    | Container                          |
| ---------------------------------------- | ---------------------------------- |
| Şablondur                                | Image'ın çalışan instance'ıdır     |
| Çalışmaz                                 | Process çalıştırır                 |
| Immutable'dır                            | Yazılabilir runtime katmanı vardır |
| Container üretir                         | Image'dan üretilir                 |
| Bir image birçok container oluşturabilir | Belirli bir image'a dayanır        |
| Uygulama paketini temsil eder            | Çalışan uygulamayı temsil eder     |

---

## Örnek

Image:

```text
postgres:17
```

Bu image'dan:

```text
postgres-dev
postgres-test
postgres-local
```

isimli üç farklı container oluşturulabilir. Her biri aynı image'ı kullanabilir fakat farklı:

* Database verilerine
* Environment variable'larına
* Portlara
* Volume'lara

sahip olabilir.

---

<a id="10-docker-mimarisi"></a>

# 10. Docker Mimarisi

Docker genel olarak client-server mimarisine sahiptir. Basitleştirilmiş yapı:

```text
Developer
   │
   ▼
Docker CLI
   │
   ▼
Docker API
   │
   ▼
Docker Daemon
   │
   ├── Images
   ├── Containers
   ├── Networks
   └── Volumes
         │
         ▼
    Container Runtime
```

Registry tarafında ise:

```text
Docker Daemon
     │
     ├── pull
     ▼
Docker Registry

Docker Daemon
     │
     ├── push
     ▼
Docker Registry
```

yer alır.

---

<a id="11-docker-client-ve-docker-daemon"></a>

# 11. Docker Client ve Docker Daemon

## Docker Client

Terminalde kullandığımız:

```bash
docker build
docker run
docker pull
docker push
docker ps
```

gibi komutları sağlayan taraftır. Docker CLI doğrudan container oluşturmaz. İsteği Docker Engine'e iletir.

---

## Docker Daemon

Docker daemon genellikle:

```text
dockerd
```

olarak bilinir. Docker sisteminin arka planda çalışan temel servislerinden biridir. Şunları yönetir:

* Container'lar
* Image'lar
* Network'ler
* Volume'lar
* Build işlemleri
* Registry iletişimi

Örneğin:

```bash
docker run nginx
```

dediğimizde kabaca:

```text
Docker CLI
    ↓
Docker API
    ↓
Docker Daemon
    ↓
Image kontrolü
    ↓
Container oluşturma
    ↓
Process çalıştırma
```

gerçekleşir.

---

<a id="12-docker-registry-ve-docker-hub"></a>

# 12. Docker Registry ve Docker Hub

Docker image'larının saklandığı sisteme **container registry** denir. En bilinen örnek:

```text
Docker Hub
```

Ancak Docker Hub tek registry değildir. Kuruluşlar kendi private registry sistemlerini de kullanabilir.

---

## Registry Neden Gereklidir?

Bir developer image oluşturdu:

```text
roomcraft-api:1.0
```

Bunu yalnızca kendi bilgisayarında tutarsa diğer developer'lar veya production sunucusu image'a ulaşamaz. Bu nedenle image registry'ye gönderilir:

```text
Developer
   │
   │ docker push
   ▼
Registry
   │
   │ docker pull
   ▼
Production Server
```

---

## Pull

Image indirmek:

```bash
docker pull nginx
```

---

## Push

Image göndermek:

```bash
docker push username/roomcraft-api:1.0
```

---

## Tag Nedir?

Image sürümünü veya varyasyonunu belirtir.

```text
roomcraft-api:1.0
roomcraft-api:1.1
roomcraft-api:2.0
roomcraft-api:latest
```

Buradaki:

```text
1.0
1.1
2.0
latest
```

değerleri tag'dir. Production ortamlarında yalnızca `latest` kullanmak yerine kontrollü ve açık versiyonlama tercih edilmesi çoğu zaman daha güvenlidir.

---

<a id="13-dockerfile-nedir"></a>

# 13. Dockerfile Nedir?

**Dockerfile**, Docker image'ın nasıl oluşturulacağını açıklayan talimat dosyasıdır. Örneğin basit bir ASP.NET Core Dockerfile:

```dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY . .
EXPOSE 8080
ENTRYPOINT ["dotnet", "RoomCraft.Api.dll"]
```

Dockerfile şu sorunun cevabıdır:

> "Bu uygulamanın çalışabileceği image'ı nasıl oluşturmalıyım?"

---

## Dockerfile Neden Önemlidir?

Ortamın elle hazırlanması yerine ortamı kodla tanımlarız. Yani:

```text
Manuel kurulum
```

yerine:

```text
Dockerfile
```

kullanılır. Bu yaklaşım tekrarlanabilirliği artırır.

---

<a id="14-dockerfile-komutlari"></a>

# 14. Dockerfile Komutları

## FROM

Hangi base image'ın kullanılacağını belirler.

```dockerfile
FROM node:22
```

veya:

```dockerfile
FROM python:3.13
```

---

## WORKDIR

Container içerisindeki çalışma klasörünü belirler.

```dockerfile
WORKDIR /app
```

Bundan sonraki birçok komut `/app` içerisinde çalışır.

---

## COPY

Host'taki dosyaları image içerisine kopyalar.

```dockerfile
COPY package.json .
```

veya:

```dockerfile
COPY . .
```

---

## RUN

Image build edilirken komut çalıştırır.

```dockerfile
RUN npm install
```

Önemli nokta:

```text
RUN → Build time
```

çalışır. Container her başladığında tekrar çalışmaz.

---

## CMD

Container başlatıldığında çalışacak varsayılan komutu belirleyebilir.

```dockerfile
CMD ["npm", "start"]
```

---

## ENTRYPOINT

Container'ın temel executable'ını tanımlamak için kullanılabilir.

```dockerfile
ENTRYPOINT ["dotnet", "RoomCraft.Api.dll"]
```

---

## EXPOSE

Uygulamanın container içerisinde hangi portu dinlemesinin beklendiğini dokümante eder.

```dockerfile
EXPOSE 8080
```

Ancak çok önemli:

> `EXPOSE` tek başına portu host makineye açmaz.

Host'a port publish etmek için `docker run -p` gibi bir mekanizma gerekir.

---

## ENV

Environment variable tanımlar.

```dockerfile
ENV ASPNETCORE_ENVIRONMENT=Production
```

---

## ARG

Build sırasında kullanılabilecek değişkenler tanımlar.

```dockerfile
ARG VERSION=1.0
```

---

## USER

Container'ın hangi kullanıcıyla çalışacağını belirleyebilir.

```dockerfile
USER appuser
```

Güvenlik açısından uygulamaların gereksiz yere root olarak çalıştırılmaması iyi bir pratiktir.

---

## HEALTHCHECK

Container içindeki uygulamanın gerçekten sağlıklı çalışıp çalışmadığını kontrol etmek için kullanılabilir. Çünkü:

```text
Container running
```

olması:

```text
Application healthy
```

olduğu anlamına gelmeyebilir. Örneğin process çalışıyor olabilir fakat API cevap vermiyor olabilir.

---

<a id="15-docker-build-mantigi"></a>

# 15. Docker Build Mantığı

Dockerfile hazırlandıktan sonra:

```bash
docker build -t roomcraft-api:1.0 .
```

komutu kullanılabilir. Burada:

```text
docker build
```

image oluşturur.

```text
-t
```

image'a isim/tag verir.

```text
roomcraft-api:1.0
```

image ismidir.

```text
.
```

build context'i belirtir.

---

## Build Context Nedir?

Docker build sırasında Docker'a gönderilen dosya kümesidir. Örneğin:

```bash
docker build .
```

dediğimizde mevcut klasör build context olur. Bu nedenle gereksiz:

```text
node_modules
.git
logs
temporary files
build outputs
```

gibi dosyaların build context'e gönderilmemesi önemlidir. Bunun için:

```text
.dockerignore
```

dosyası kullanılır.

---

## .dockerignore

Örneğin:

```text
node_modules
.git
.env
logs
README.md
```

gibi dosyaların build context dışında bırakılmasını sağlayabilir. Bu:

* Build'i hızlandırabilir.
* Image'a gereksiz dosya girmesini engeller.
* Güvenlik açısından hassas dosyaların yanlışlıkla eklenme riskini azaltır.

---

<a id="16-docker-build-cache"></a>

# 16. Docker Build Cache

Docker, image build sırasında daha önce oluşturulmuş katmanları tekrar kullanabilir. Örneğin:

```dockerfile
COPY package.json .
RUN npm install
COPY . .
```

yapısının nedeni önemlidir. Eğer önce:

```dockerfile
COPY . .
RUN npm install
```

yazarsak source code'daki küçük bir değişiklik bile önceki katmanı değiştirebilir ve `npm install` tekrar çalışmak zorunda kalabilir. Ancak:

```dockerfile
COPY package.json .
RUN npm install
COPY . .
```

şeklinde yazıldığında `package.json` değişmemişse dependency katmanı cache'den kullanılabilir. Bu nedenle Dockerfile komutlarının sırası:

> **Build performansını ciddi şekilde etkileyebilir.**

---

<a id="17-docker-port-mapping"></a>

# 17. Docker Port Mapping

Container kendi izole network ortamına sahiptir. Örneğin uygulama container içinde:

```text
Port 80
```

üzerinden çalışıyor olabilir. Fakat bizim tarayıcıdan erişebilmemiz için host ile container arasında port mapping yapılabilir.

```bash
docker run -p 8080:80 nginx
```

Mantık:

```text
Host          Container
8080   ───►   80
```

Tarayıcı:

```text
localhost:8080
```

adresine istek gönderir. Docker bunu container'ın:

```text
80
```

portuna yönlendirir.

---

## Port Mapping Formatı

```text
HOST_PORT:CONTAINER_PORT
```

Örneğin:

```bash
-p 5000:8080
```

şu anlama gelir:

```text
localhost:5000
        ↓
container:8080
```

Bu konu özellikle backend geliştirirken çok önemlidir.

---

<a id="18-docker-networking"></a>

# 18. Docker Networking

Gerçek projelerde container'ların çoğu birbirleriyle iletişim kurmak zorundadır. Örneğin:

```text
Frontend
    ↓
Backend
    ↓
Database
```

Her biri farklı container olabilir. Docker bu container'ları network üzerinden birbirine bağlayabilir.

---

## Bridge Network

Docker'ın aynı host üzerindeki container'ları birbirine bağlamak için kullandığı yaygın network türlerinden biridir. Örneğin:

```text
roomcraft-network
        │
        ├── frontend
        ├── backend
        └── database
```

Bu container'lar aynı network üzerindeyse birbirleriyle iletişim kurabilir.

---

## Container İsmiyle İletişim

Compose gibi yapılarda backend:

```text
database
```

isimli PostgreSQL servisine:

```text
Host=database
```

üzerinden bağlanabilir. Bu nedenle container içerisinde:

```text
localhost
```

kavramına dikkat etmek gerekir.

---

## Çok Önemli: localhost

Bir backend container'ın içerisindeysen:

```text
localhost
```

backend container'ın kendisini ifade eder. Database farklı container'daysa:

```text
localhost
```

üzerinden database'e ulaşamazsın. Örneğin:

```text
backend container
localhost
     ↓
backend container
```

Database için ise:

```text
backend
   ↓
database:5432
```

kullanılabilir. Docker öğrenirken en çok hata yapılan yerlerden biridir.

---

<a id="19-dockerda-veri-kaliciligi"></a>

# 19. Docker'da Veri Kalıcılığı

Container'ın writable layer'ına kaydedilen veriler container'ın yaşam döngüsüne bağlıdır. Örneğin PostgreSQL'i container içinde çalıştırdığımızı düşünelim. Database verilerini yalnızca container filesystem'ine yazarsak:

```text
PostgreSQL Container
        │
        └── Database Data
```

container silindiğinde bu runtime katmanındaki veriler de kaybolabilir. Database için bu kabul edilemez. Bu nedenle kalıcı veriler container'ın yaşam döngüsünden ayrılmalıdır. Çözüm:

```text
Docker Volume
```

---

<a id="20-volume-bind-mount-ve-tmpfs"></a>

# 20. Volume, Bind Mount ve tmpfs

Docker'da veriyi container dışında yönetmek için farklı yöntemler vardır.

---

## 20.1 Volume

Docker tarafından yönetilen kalıcı depolama alanıdır.

```text
Container
    │
    ▼
Docker Volume
```

Container silinse bile volume kalabilir. Örneğin:

```bash
docker volume create postgres-data
```

Ardından:

```bash
docker run \
  -v postgres-data:/var/lib/postgresql/data \
  postgres
```

kullanılabilir.

---

## Volume Ne Zaman Kullanılır?

Özellikle:

* Database verileri
* Persistent application data
* Container'lar arasında paylaşılacak veriler

için uygundur.

---

## 20.2 Bind Mount

Host bilgisayardaki belirli bir klasör container'a bağlanır.

```text
Host

C:\project
     │
     ▼
Container

/app
```

Development ortamında source code paylaşımı için sık kullanılabilir.

---

## 20.3 tmpfs

Veriyi disk yerine geçici olarak memory'de tutmak için kullanılabilir. Container veya sistem yaşam döngüsüne bağlı geçici veriler için tercih edilebilir.

---

## Özet

| Yöntem     | Veri Nerede?                | Kullanım                          |
| ---------- | --------------------------- | --------------------------------- |
| Volume     | Docker tarafından yönetilir | Kalıcı uygulama/database verileri |
| Bind Mount | Host filesystem             | Development, source paylaşımı     |
| tmpfs      | Memory                      | Geçici veriler                    |

---

<a id="21-environment-variables"></a>

# 21. Environment Variables

Aynı Docker image farklı ortamlarda farklı configuration ile çalıştırılabilir. Örneğin:

```text
Development Database
Testing Database
Production Database
```

farklı olabilir. Image'ın içine bütün değerleri hard-code etmek yerine environment variable kullanılabilir. Örneğin:

```bash
docker run \
  -e ASPNETCORE_ENVIRONMENT=Production \
  roomcraft-api
```

Bu sayede:

```text
Aynı Image
   │
   ├── Development config
   ├── Test config
   └── Production config
```

ile çalıştırılabilir.

---

## Hassas Bilgiler

Şunların Dockerfile veya Git repository içerisinde düz metin olarak tutulması tehlikelidir:

```text
Database passwords
API keys
Access tokens
Private keys
```

Production ortamında secret yönetimi için uygun secret-management mekanizmaları tercih edilmelidir.

---

<a id="22-docker-compose-nedir"></a>

# 22. Docker Compose Nedir?

Gerçek uygulamalar çoğu zaman tek container'dan oluşmaz. Örneğin RoomCraft benzeri bir full-stack sistem:

```text
Frontend
Backend API
PostgreSQL
Redis
```

kullanıyor olabilir. Her container'ı ayrı ayrı:

```bash
docker run ...
docker run ...
docker run ...
docker run ...
```

ile yönetmek zorlaşır. Bu noktada **Docker Compose** kullanılır. Compose, çoklu container uygulamasını declarative şekilde tanımlamamızı sağlar.

---

## Örnek compose.yaml

```yaml
services:

  backend:
    build: ./backend
    ports:
      - "8080:8080"
    depends_on:
      - database

  database:
    image: postgres:17
    environment:
      POSTGRES_DB: roomcraft
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: example
    volumes:
      - postgres-data:/var/lib/postgresql/data

volumes:
  postgres-data:
```

Ardından:

```bash
docker compose up
```

komutuyla sistem ayağa kaldırılabilir.

---

## Docker Compose Neleri Tanımlayabilir?

* Services
* Images
* Build context
* Ports
* Volumes
* Networks
* Environment variables
* Service dependencies
* Restart davranışları
* Health checks

---

## Service Kavramı

Compose içinde:

```yaml
services:
```

altında tanımlanan her yapı çoğunlukla uygulamanın bir parçasını temsil eder. Örneğin:

```text
services

frontend
backend
database
redis
```

---

<a id="23-gercek-bir-full-stack-projede-docker"></a>

# 23. Gerçek Bir Full-Stack Projede Docker

Örneğin şöyle bir uygulamamız olduğunu düşünelim:

```text
React
ASP.NET Core Web API
PostgreSQL
```

Container mimarisi:

```text
┌─────────────────┐
│ React Frontend  │
│   Container     │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ ASP.NET Core    │
│ API Container   │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ PostgreSQL      │
│ DB Container    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Docker Volume   │
└─────────────────┘
```

Compose ile bütün proje:

```bash
docker compose up
```

ile ayağa kaldırılabilir. Yeni bir developer projeye geldiğinde artık:

```text
PostgreSQL hangi sürüm?
.NET hangi sürüm?
Node hangi sürüm?
Database nasıl kurulacak?
Portlar ne olacak?
```

gibi birçok kurulumu elle yapmak zorunda kalmayabilir. Gerekli container tanımları proje içerisinde bulunur.

---

<a id="24-docker-ve-virtual-machine-farki"></a>

# 24. Docker ve Virtual Machine Farkı

Docker ile VM arasındaki fark Docker'ın en önemli konularından biridir.

---

## Virtual Machine Mimarisi

```text
┌───────────────────────┐
│ Application           │
│ Libraries             │
│ Guest OS              │
├───────────────────────┤
│ Application           │
│ Libraries             │
│ Guest OS              │
├───────────────────────┤
│ Hypervisor            │
├───────────────────────┤
│ Host OS / Hardware    │
└───────────────────────┘
```

Her VM kendi:

```text
Guest Operating System
Kernel
Libraries
Application
```

yapısını taşıyabilir.

---

## Container Mimarisi

```text
┌───────────────────────┐
│ App A + Dependencies  │
├───────────────────────┤
│ App B + Dependencies  │
├───────────────────────┤
│ App C + Dependencies  │
├───────────────────────┤
│ Container Runtime     │
├───────────────────────┤
│ Host OS Kernel        │
├───────────────────────┤
│ Hardware              │
└───────────────────────┘
```

Container'lar kendi tam Guest OS kernel'lerini taşımak yerine host kernel'ini paylaşabilir.

---

## Karşılaştırma

| Özellik         | Virtual Machine                         | Container                              |
| --------------- | --------------------------------------- | -------------------------------------- |
| İşletim sistemi | Her VM kendi OS'ine sahip olabilir      | Host kernel paylaşılır                 |
| Boyut           | Genellikle daha büyük                   | Genellikle daha küçük                  |
| Başlatma        | OS boot gerektiği için daha ağır        | Process başlangıcına daha yakın        |
| Kaynak tüketimi | Daha yüksek olabilir                    | Daha düşüktür                          |
| İzolasyon       | Daha güçlü güvenlik sınırı sağlayabilir | Daha hafif izolasyon                   |
| Taşınabilirlik  | İyi                                     | Uygulama paketleme açısından çok güçlü |
| Deployment      | Daha ağır olabilir                      | Hızlı olabilir                         |
| Yoğunluk        | Aynı makinede daha az VM                | Genellikle daha fazla container        |

---

## Çok Önemli Bir Yanlış

Docker:

> "VM'nin geliştirilmiş hali"

değildir. Container ve VM birbirinin doğrudan alternatifi olmak zorunda değildir. Örneğin cloud ortamında şu yapı oldukça mümkündür:

```text
Physical Server
     ↓
Virtual Machine
     ↓
Docker
     ↓
Containers
```

Yani VM üzerinde Docker container çalıştırılabilir.

---

<a id="25-docker-neden-vmden-daha-hafiftir"></a>

# 25. Docker Neden VM'den Daha Hafiftir?

Çünkü her container için ayrı bir işletim sistemi kernel'i çalıştırılması gerekmez. VM:

```text
App
Libraries
Guest OS
Guest Kernel
```

taşıyabilir. Container:

```text
App
Libraries
```

taşırken host kernel'inden yararlanır. Bu nedenle container'lar:

* Daha az disk alanı kullanabilir.
* Daha az RAM tüketebilir.
* Daha hızlı başlayabilir.
* Aynı sunucuda daha yüksek uygulama yoğunluğu sağlayabilir.

Ancak bunun karşılığında container izolasyonu her durumda VM kadar güçlü bir güvenlik sınırı değildir. Bu nedenle:

```text
Container her zaman VM'den daha iyidir
```

demek yanlıştır. Doğru teknoloji ihtiyaca göre seçilir.

---

<a id="26-dockerin-avantajlari"></a>

# 26. Docker'ın Avantajları

## 26.1 Environment Tutarlılığı

Development:

```text
Docker Image X
```

Testing:

```text
Docker Image X
```

Production:

```text
Docker Image X
```

kullanabilir. Environment kaynaklı sorunları azaltır.

---

## 26.2 Kolay Deployment

Sunucuya onlarca dependency kurmak yerine image deploy edilebilir.

---

## 26.3 Taşınabilirlik

Container image farklı uyumlu Docker ortamlarında çalıştırılabilir.

---

## 26.4 İzolasyon

Uygulamaların dependency'leri birbirine karışmaz. Örneğin:

```text
Project A → Node 20
Project B → Node 22
```

aynı bilgisayarda farklı container'larda çalışabilir.

---

## 26.5 Hızlı Ortam Kurulumu

Yeni developer:

```bash
git clone
docker compose up
```

seviyesine yakın bir geliştirme deneyimi elde edebilir.

---

## 26.6 CI/CD Uyumluluğu

Build edilen image test edilebilir ve production'a taşınabilir.

---

## 26.7 Ölçeklenebilirlik

Aynı image'dan birden fazla container oluşturulabilir.

```text
API Image
   │
   ├── API Container 1
   ├── API Container 2
   ├── API Container 3
   └── API Container 4
```

Bu özellik orchestration sistemlerinde oldukça önemlidir.

---

<a id="27-dockerin-dezavantajlari-ve-sinirlamalari"></a>

# 27. Docker'ın Dezavantajları ve Sınırlamaları

Docker'ın çok güçlü olması her durumda doğru çözüm olduğu anlamına gelmez.

### Ek Karmaşıklık

Küçük projelerde:

```text
Dockerfile
Compose
Network
Volume
Registry
```

gibi yeni kavramların eklenmesi gereksiz karmaşıklık yaratabilir.

### Debugging

Container network ve filesystem problemleri geleneksel uygulamalara göre başlangıçta daha karmaşık olabilir.

### Güvenlik

Container'lar host kernel'ini paylaştığı için izolasyon sınırı VM'lerden farklıdır.

### Stateful Sistemler

Database gibi stateful uygulamalarda:

* Volume
* Backup
* Replication
* Persistence

stratejileri doğru tasarlanmalıdır.

---

<a id="28-docker-ve-mikroservis-mimarisi"></a>

# 28. Docker ve Mikroservis Mimarisi

Docker mikroservis mimarisinde çok yaygın kullanılır. Örneğin:

```text
User Service
Order Service
Payment Service
Notification Service
```

her biri farklı container olabilir.

```text
User Image
   ↓
User Container

Order Image
   ↓
Order Container

Payment Image
   ↓
Payment Container
```

Böylece her servis:

* Bağımsız deploy edilebilir.
* Bağımsız ölçeklenebilir.
* Kendi dependency'lerine sahip olabilir.

Ancak:

> Docker kullanmak uygulamayı otomatik olarak mikroservis yapmaz.

Monolitik bir uygulama da Docker container içerisinde çalıştırılabilir.

---

<a id="29-docker-ve-cicd"></a>

# 29. Docker ve CI/CD

Docker CI/CD pipeline'larında oldukça değerlidir. Tipik süreç:

```text
Developer Push
      ↓
Git Repository
      ↓
CI Pipeline
      ↓
Tests
      ↓
Docker Build
      ↓
Docker Image
      ↓
Registry
      ↓
Deployment
      ↓
Container
```

Örneğin:

```text
Commit
   ↓
Test
   ↓
Build image
   ↓
Tag image
   ↓
Push registry
   ↓
Production deploy
```

Bu yaklaşımın büyük avantajı:

> Test edilen artifact ile production'a gönderilen artifact'in aynı Docker image olmasıdır.

---

<a id="30-docker-guvenligi"></a>

# 30. Docker Güvenliği

Docker kullanmak uygulamayı otomatik olarak güvenli yapmaz. Docker güvenliğinde dikkat edilmesi gereken temel konular vardır.

---

## 30.1 Root Kullanıcısından Kaçınmak

Mümkünse uygulamayı container içinde root olmayan kullanıcıyla çalıştırmak tercih edilir.

---

## 30.2 Minimal Base Image

Gereksiz programlarla dolu image:

```text
Daha büyük attack surface
```

oluşturabilir. Bu nedenle ihtiyaca uygun minimal image tercih edilir.

---

## 30.3 Güncel Image Kullanımı

Base image'lar düzenli olarak güncellenmelidir. Eski image içerisinde güvenlik açıkları bulunabilir.

---

## 30.4 Secret'ları Image'a Gömmemek

Şunları Dockerfile içine yazmak tehlikelidir:

```dockerfile
ENV DB_PASSWORD=my-super-secret-password
```

çünkü image layer geçmişinde hassas bilgiler kalabilir.

---

## 30.5 Gereksiz Port Açmamak

Sadece gerçekten dış erişim gereken portlar publish edilmelidir. Örneğin:

```bash
-p 8080:80
```

ile publish edilen bir portun host dışından erişilebilir olup olmadığı ayrıca düşünülmelidir.

---

## 30.6 Resource Limitleri

Bir container'ın bütün sistemi tüketmesini engellemek için:

* CPU limit
* Memory limit

uygulanabilir.

---

## 30.7 Image Güvenliği

Production'a gönderilecek image'lar:

* Vulnerability scanning
* Dependency scanning
* Image signing

gibi güvenlik süreçlerinden geçirilebilir.

---

<a id="31-dockerfile-best-practices"></a>

# 31. Dockerfile Best Practices

Profesyonel Docker kullanımında aşağıdaki uygulamalar önemlidir.

---

## Küçük Base Image Kullan

Gereksiz büyük image'lardan kaçınılmalıdır.

---

## Gereksiz Dosyaları COPY Etme

`.dockerignore` kullanılmalıdır.

---

## Cache'i Düşünerek Dockerfile Yaz

Dependency dosyaları source code'dan önce copy edilebilir.

---

## Container'a Secret Koyma

Password ve token'lar image'a gömülmemelidir.

---

## Root Olmayan Kullanıcı Kullan

Mümkün olduğunda:

```dockerfile
USER appuser
```

gibi bir yaklaşım tercih edilebilir.

---

## Multi-Stage Build Kullan

Özellikle derlenen uygulamalarda build araçlarının production image içerisinde bulunması gerekmeyebilir. Örneğin:

```text
Stage 1
Build environment

        ↓

Stage 2
Runtime environment
```

Son image yalnızca çalışması gereken dosyaları içerebilir. Bu:

* Image boyutunu küçültür.
* Gereksiz build araçlarını kaldırır.
* Attack surface'i azaltabilir.

---

## Bir Container'a Her Şeyi Doldurma

Örneğin:

```text
React
API
PostgreSQL
Redis
Nginx
```

hepsini tek container'a koymak yerine mantıksal servisleri ayırmak genellikle daha yönetilebilir olur.

---

<a id="32-temel-docker-komutlari"></a>

# 32. Temel Docker Komutları

## Docker Versiyonu

```bash
docker --version
```

---

## Image İndirme

```bash
docker pull nginx
```

---

## Image Listeleme

```bash
docker images
```

---

## Container Çalıştırma

```bash
docker run nginx
```

---

## Container'a İsim Verme

```bash
docker run --name web-server nginx
```

---

## Detached Mode

```bash
docker run -d nginx
```

Container arka planda çalışır.

---

## Port Mapping

```bash
docker run -p 8080:80 nginx
```

---

## Çalışan Container'lar

```bash
docker ps
```

---

## Tüm Container'lar

```bash
docker ps -a
```

---

## Container Durdurma

```bash
docker stop web-server
```

---

## Container Başlatma

```bash
docker start web-server
```

---

## Container Silme

```bash
docker rm web-server
```

---

## Image Silme

```bash
docker rmi nginx
```

---

## Log Görüntüleme

```bash
docker logs web-server
```

---

## Logları Canlı Takip Etme

```bash
docker logs -f web-server
```

---

## Container İçinde Komut Çalıştırma

```bash
docker exec web-server ls
```

---

## Container İçine Terminal ile Girme

Image'da shell mevcutsa:

```bash
docker exec -it web-server bash
```

veya:

```bash
docker exec -it web-server sh
```

---

## Container Detayları

```bash
docker inspect web-server
```

---

## Resource Kullanımı

```bash
docker stats
```

CPU ve RAM kullanımını incelemek için kullanılabilir.

---

## Image Build Etme

```bash
docker build -t my-app:1.0 .
```

---

## Compose Başlatma

```bash
docker compose up
```

---

## Compose Arka Planda Başlatma

```bash
docker compose up -d
```

---

## Compose Durdurma

```bash
docker compose down
```

---

<a id="33-docker-debugging-ve-loglama"></a>

# 33. Docker Debugging ve Loglama

Container çalışmadığında ilk bakılacak yerlerden biri:

```bash
docker ps -a
```

olmalıdır. Container'ın:

```text
Exited
Restarting
Running
Created
```

durumu görülebilir.

---

## Log Kontrolü

```bash
docker logs container-name
```

Örneğin:

```text
Connection refused
Environment variable missing
Database unavailable
Port already in use
File not found
```

gibi sorunlar görülebilir.

---

## Inspect

```bash
docker inspect container-name
```

ile:

* Network bilgileri
* IP
* Mount'lar
* Environment
* Container configuration

gibi ayrıntılar incelenebilir.

---

## Container İçine Girme

```bash
docker exec -it container-name sh
```

ardından:

```bash
ls
pwd
env
cat ...
```

gibi komutlarla container ortamı incelenebilir.

---

## Resource Kontrolü

```bash
docker stats
```

ile:

```text
CPU
Memory
Network I/O
Block I/O
```

gözlemlenebilir.

---

<a id="34-benim-bilgisayarda-calisiyordu-problemi"></a>

# 34. "Benim Bilgisayarda Çalışıyordu" Problemi

Şimdi Docker'ın esas kazancını görelim. Docker olmadan:

```text
Developer PC

.NET 8
PostgreSQL 17
Library A v3
Environment X
```

Production:

```text
Server

.NET 7
PostgreSQL 16
Library A v2
Environment Y
```

Sonuç:

```text
Developer → Çalışıyor
Production → Çalışmıyor
```

---

Docker ile:

```text
Docker Image
├── Application
├── Runtime
├── Libraries
└── Configuration
```

Developer:

```text
Image v1
```

Test:

```text
Image v1
```

Production:

```text
Image v1
```

Böylece uygulamanın çalıştığı environment önemli ölçüde standartlaştırılmış olur. Docker'ın özeti aslında burada yatmaktadır:

> **Uygulamayı çalıştırmak için bilgisayarı uygulamaya uydurmak yerine, uygulamanın çalışma ortamını paketleriz.**

---

<a id="35-sik-yapilan-docker-hatalari"></a>

# 35. Sık Yapılan Docker Hataları

## 1. Image ile Container'ı Aynı Şey Sanmak

Yanlış:

```text
Image = Container
```

Doğru:

```text
Image → Template
Container → Running instance
```

---

## 2. EXPOSE ile Portun Açıldığını Sanmak

```dockerfile
EXPOSE 8080
```

portu otomatik olarak host makineye publish etmez. Genellikle:

```bash
-p 5000:8080
```

gibi mapping gerekir.

---

## 3. Container İçinde localhost Kullanmak

Backend ve DB farklı container'lardaysa:

```text
localhost
```

database container'ını ifade etmez.

---

## 4. Database Verisini Container İçinde Tutmak

Container silinince veri kaybına yol açabilir. Çözüm:

```text
Volume
```

---

## 5. Secret'ları Dockerfile'a Yazmak

Password ve API key'ler image'a gömülmemelidir.

---

## 6. Devasa Image Oluşturmak

Gereksiz:

* Build tools
* Cache files
* Source files
* Development dependencies

production image içerisinde bırakılmamalıdır.

---

## 7. Her Şeyi Tek Container'a Koymak

Docker'ın amacı:

```text
Bir container = Bir process
```

şeklinde katı bir kural değildir fakat container'ların belirli bir sorumluluğa odaklanması genellikle daha sağlıklı bir mimaridir.

---

## 8. Container'ı Kalıcı Sunucu Sanmak

Container'lar disposable yani gerektiğinde silinip yeniden oluşturulabilir yapılar olarak düşünülmelidir. State mümkün olduğunca container'ın kendisine bağımlı bırakılmamalıdır.

---

<a id="36-docker-hakkinda-yanlis-bilinenler"></a>

# 36. Docker Hakkında Yanlış Bilinenler

## "Docker bir Virtual Machine'dir."

Yanlış. Docker container'ları host kernel'ini paylaşabilir.

---

## "Her Container'ın Kendi İşletim Sistemi Vardır."

Tam anlamıyla yanlış bir ifadedir. Bir Linux image içerisinde Ubuntu user-space dosyaları bulunabilir fakat container'ın ayrı bir Ubuntu kernel'i boot ettiği anlamına gelmez.

---

## "Container Kapanırsa Image Silinir."

Yanlış.

```text
Image
   ↓
Container
```

Container silinse bile image kalabilir.

---

## "Image Silinirse Registry'deki Image da Silinir."

Yanlış. Local image silmek remote registry'deki image'ı otomatik silmez.

---

## "Running Demek Healthy Demektir."

Yanlış. Process çalışıyor olabilir fakat uygulama cevap vermiyor olabilir. Bu nedenle health check önemlidir.

---

## "Docker Kullanınca Uygulama Otomatik Ölçeklenir."

Yanlış. Docker container oluşturmayı sağlar. Çok sayıda container'ın:

* Scheduling
* Scaling
* Recovery
* Service discovery

gibi ihtiyaçlarının yönetilmesi için Kubernetes gibi orchestration sistemleri kullanılabilir.

---

<a id="37-mulakat-sorulari-ve-cevaplari"></a>

# 37. Mülakat Soruları ve Cevapları

## Soru 1: Docker nedir?

Docker, uygulamaların bağımlılıklarıyla birlikte image olarak paketlenmesini ve izole container ortamlarında çalıştırılmasını sağlayan containerization platformudur.

---

## Soru 2: Container nedir?

Container, uygulama process'inin bağımlılıklarıyla birlikte izole edilmiş bir ortamda çalışmasını sağlayan lightweight runtime yapısıdır.

---

## Soru 3: Image nedir?

Image, container oluşturmak için kullanılan immutable şablondur.

---

## Soru 4: Image ile Container farkı nedir?

Image çalıştırılabilir şablondur; container ise image'ın çalışan instance'ıdır.

---

## Soru 5: Docker ile VM arasındaki temel fark nedir?

VM kendi Guest OS ve kernel'ini çalıştırabilirken container host işletim sisteminin kernel'ini paylaşır. Bu nedenle container'lar genellikle daha hafiftir ve daha hızlı başlar.

---

## Soru 6: Dockerfile nedir?

Docker image'ın nasıl oluşturulacağını belirleyen talimat dosyasıdır.

---

## Soru 7: RUN ile CMD arasındaki fark nedir?

```text
RUN
```

image build edilirken çalışır.

```text
CMD
```

container runtime'da çalıştırılacak varsayılan komutu belirler.

---

## Soru 8: CMD ile ENTRYPOINT arasındaki fark nedir?

Her ikisi de container başlangıç komutuyla ilgilidir. Genel olarak:

```text
ENTRYPOINT
```

container'ın temel executable'ını tanımlamak,

```text
CMD
```

ise varsayılan komut veya argüman sağlamak için kullanılabilir.

---

## Soru 9: Docker Volume nedir?

Container'ın yaşam döngüsünden bağımsız kalıcı veri saklamak için kullanılan Docker-managed storage mekanizmasıdır.

---

## Soru 10: Container silinirse veriler silinir mi?

Container'ın writable layer'ındaki veriler container ile birlikte kaybolabilir. Volume üzerinde bulunan veriler ise container'dan bağımsız tutulabilir.

---

## Soru 11: Docker Compose nedir?

Birden fazla container'dan oluşan uygulamaların service, network, volume, environment ve diğer configuration bilgilerini tek bir YAML dosyasında tanımlayıp yönetmeye yarayan araçtır.

---

## Soru 12: `docker run` ve `docker start` farkı nedir?

```text
docker run
```

image'dan yeni container oluşturup çalıştırır.

```text
docker start
```

daha önce oluşturulmuş fakat durmuş container'ı tekrar çalıştırır.

---

## Soru 13: `docker stop` ve `docker rm` farkı nedir?

```text
docker stop
```

container'ı durdurur.

```text
docker rm
```

container'ı siler.

---

## Soru 14: `docker pull` ne yapar?

Registry'den Docker image indirir.

---

## Soru 15: `docker push` ne yapar?

Local image'ı registry'ye gönderir.

---

## Soru 16: Port mapping nedir?

Host makinedeki bir portun container içerisindeki porta yönlendirilmesidir. Örneğin:

```bash
docker run -p 8080:80 nginx
```

şu mapping'i oluşturur:

```text
Host 8080 → Container 80
```

---

## Soru 17: Container içinde `localhost` neyi ifade eder?

Container'ın kendisini ifade eder. Başka bir container'ı ifade etmez.

---

## Soru 18: Docker neden hızlıdır?

Container'lar her instance için ayrı işletim sistemi boot etmek yerine host kernel'ini paylaşabilir ve uygulama process'lerini izole eder.

---

## Soru 19: Docker image neden immutable'dır?

Image'ın değiştirilemez bir deployment artifact'i olması ortamların tekrar üretilebilir ve tutarlı olmasına yardımcı olur. Değişiklik gerektiğinde yeni image oluşturulur.

---

## Soru 20: Docker layer nedir?

Image filesystem'indeki değişiklikleri temsil eden katmanlardır. Docker image birden fazla layer'ın birleşiminden oluşur.

---

## Soru 21: Docker cache neden önemlidir?

Değişmemiş image layer'larının yeniden kullanılmasını sağlayarak build sürelerini azaltabilir.

---

## Soru 22: `.dockerignore` neden kullanılır?

Build context'e gönderilmemesi gereken dosyaları belirtmek için kullanılır. Örneğin:

```text
node_modules
.git
.env
```

---

## Soru 23: Docker güvenlik açısından VM'den daha mı güvenlidir?

Bu şekilde genelleme yapılamaz. VM'ler ayrı kernel ve OS sınırı nedeniyle genel olarak daha güçlü bir izolasyon sınırı sağlayabilir. Container güvenliği ise configuration, kernel güvenliği, capabilities, namespace'ler ve diğer mekanizmalara bağlıdır.

---

## Soru 24: Docker ile Kubernetes arasındaki fark nedir?

Docker container oluşturma ve çalıştırma teknolojileri sağlar. Kubernetes ise çok sayıda containerized uygulamanın:

* Deployment
* Scaling
* Scheduling
* Recovery
* Networking

gibi operasyonlarını yöneten orchestration platformudur.

---

<a id="38-ozet-karsilastirma-tablolari"></a>

# 38. Özet Karşılaştırma Tabloları

## Image vs Container

| Özellik         | Image           | Container                     |
| --------------- | --------------- | ----------------------------- |
| Ne?             | Şablon          | Çalışan instance              |
| Çalışır mı?     | Hayır           | Evet                          |
| Değişebilir mi? | Immutable       | Writable runtime layer vardır |
| Oluşturma       | `docker build`  | `docker run`                  |
| Listeleme       | `docker images` | `docker ps`                   |
| Silme           | `docker rmi`    | `docker rm`                   |

---

## Container vs VM

| Özellik   | Container              | VM                             |
| --------- | ---------------------- | ------------------------------ |
| Kernel    | Host kernel paylaşılır | Ayrı kernel                    |
| Guest OS  | Tam Guest OS gerekmez  | Guest OS vardır                |
| Boyut     | Daha küçük             | Daha büyük                     |
| Startup   | Daha hızlı             | Daha yavaş                     |
| Kaynak    | Daha az                | Daha fazla                     |
| İzolasyon | Process/OS düzeyi      | Donanım/OS düzeyine daha yakın |
| Kullanım  | Uygulama deployment    | Tam sistem izolasyonu          |

---

## Dockerfile Komutları

| Komut         | Amaç                             |
| ------------- | -------------------------------- |
| `FROM`        | Base image seçer                 |
| `WORKDIR`     | Çalışma klasörü belirler         |
| `COPY`        | Dosya kopyalar                   |
| `RUN`         | Build sırasında komut çalıştırır |
| `CMD`         | Varsayılan runtime komutu        |
| `ENTRYPOINT`  | Temel executable                 |
| `ENV`         | Environment variable             |
| `ARG`         | Build argument                   |
| `EXPOSE`      | Dinlenen portu belirtir          |
| `USER`        | Kullanıcı belirler               |
| `HEALTHCHECK` | Sağlık kontrolü tanımlar         |

---

## Temel Docker Akışı

```text
Source Code
     │
     ▼
Dockerfile
     │
     │ docker build
     ▼
Docker Image
     │
     ├──────── docker push ────────► Registry
     │
     │
     │ docker run
     ▼
Container
     │
     ▼
Running Application
```

Başka sistemde:

```text
Registry
    │
    │ docker pull
    ▼
Docker Image
    │
    │ docker run
    ▼
Container
```

---

## Docker Mantığını Tek Cümlelerle Hatırlama

```text
Dockerfile → Image'ın tarifi
Image → Uygulamanın paketlenmiş şablonu
Container → Image'ın çalışan hali
Registry → Image'ların saklandığı yer
Volume → Kalıcı veri
Network → Container'ların iletişimi
Docker Compose → Birden fazla container'ı birlikte yönetme
Docker Engine → Docker işlemlerini gerçekleştiren altyapı
```

---

<a id="39-genel-sonuc"></a>

# 39. Genel Sonuç

Docker'ın temel amacı yalnızca uygulamayı "bir kutunun içinde çalıştırmak" değildir. Asıl amaç:

```text
Uygulama
+
Runtime
+
Dependencies
+
Configuration
```

bileşenlerini standartlaştırılmış ve tekrar üretilebilir bir deployment ortamına dönüştürmektir. Docker öğrenirken özellikle şu zincirin çok iyi anlaşılması gerekir:

```text
Dockerfile
    ↓
docker build
    ↓
Image
    ↓
docker run
    ↓
Container
    ↓
Running Application
```

Image ile container ayrımı Docker'ın temelidir:

```text
Image = Şablon
Container = Çalışan instance
```

Container ile VM ayrımının temelinde ise kernel bulunur:

```text
VM → Kendi Guest OS'i ve kernel'i vardır.
Container → Host kernel'ini paylaşır.
```

Bu nedenle container'lar genellikle VM'lere göre daha:

* Hafif
* Hızlı
* Taşınabilir
* Kolay deploy edilebilir

yapılardır. Ancak gerçek projelerde yalnızca container oluşturmayı bilmek yeterli değildir. Profesyonel Docker bilgisi şu kavramları birlikte anlamayı gerektirir:

```text
Container
Image
Dockerfile
Layers
Build Cache
Registry
Port Mapping
Networking
Volumes
Environment Variables
Docker Compose
Logging
Security
CI/CD
```

Docker kullanmanın yazılım geliştirici açısından en büyük kazanımlarından biri ise development ile production ortamı arasındaki farkı azaltmasıdır. Eskiden:

```text
"Benim bilgisayarımda çalışıyordu."
```

denilen durumda sorun çoğu zaman kod değil, **environment** olabilirdi. Docker yaklaşımıyla:

```text
Aynı Kod
+
Aynı Runtime
+
Aynı Dependencies
+
Aynı Image
```

kullanılarak çok daha tutarlı bir çalışma ortamı oluşturulur. Bu nedenle Docker yalnızca bir DevOps aracı değildir. Backend, full-stack, cloud veya modern yazılım geliştirme alanlarında çalışan bir developer için Docker;

> **uygulamanın nasıl paketlendiğini, çalıştırıldığını, taşındığını ve production ortamına nasıl ulaştığını anlamanın temel parçalarından biridir.**