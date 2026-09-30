# Sistem Tasarımı (System Design Basics)

---

## İçindekiler

- [1. Sistem Tasarımı Nedir?](#1-sistem-tasarımı-nedir)
  - [1.1. Sistem Tasarımının Amacı](#11-sistem-tasarımının-amacı)
  - [1.2. Functional ve Non-Functional Requirements](#12-functional-ve-non-functional-requirements)
  - [1.3. High-Level Design ve Low-Level Design](#13-high-level-design-ve-low-level-design)
- [2. Büyük Ölçekli Sistemlerde Temel Problemler](#2-büyük-ölçekli-sistemlerde-temel-problemler)
- [3. Scalability Nedir?](#3-scalability-nedir)
  - [3.1. Vertical Scaling](#31-vertical-scaling)
  - [3.2. Horizontal Scaling](#32-horizontal-scaling)
  - [3.3. Vertical ve Horizontal Scaling Karşılaştırması](#33-vertical-ve-horizontal-scaling-karşılaştırması)
  - [3.4. Stateless ve Stateful Sistemler](#34-stateless-ve-stateful-sistemler)
  - [3.5. Auto Scaling](#35-auto-scaling)
  - [3.6. Scaling Yaparken Ortaya Çıkan Problemler](#36-scaling-yaparken-ortaya-çıkan-problemler)
- [4. Availability, Reliability ve Fault Tolerance](#4-availability-reliability-ve-fault-tolerance)
  - [4.1. High Availability](#41-high-availability)
  - [4.2. Reliability](#42-reliability)
  - [4.3. Fault Tolerance](#43-fault-tolerance)
  - [4.4. Redundancy](#44-redundancy)
  - [4.5. Single Point of Failure](#45-single-point-of-failure)
- [5. Load Balancer Nedir?](#5-load-balancer-nedir)
  - [5.1. Load Balancer Neden Kullanılır?](#51-load-balancer-neden-kullanılır)
  - [5.2. Load Balancer Nasıl Çalışır?](#52-load-balancer-nasıl-çalışır)
  - [5.3. Load Balancing Algoritmaları](#53-load-balancing-algoritmaları)
  - [5.4. Layer 4 ve Layer 7 Load Balancing](#54-layer-4-ve-layer-7-load-balancing)
  - [5.5. Health Check](#55-health-check)
  - [5.6. Session Persistence ve Sticky Session](#56-session-persistence-ve-sticky-session)
  - [5.7. Load Balancer ve Reverse Proxy Farkı](#57-load-balancer-ve-reverse-proxy-farkı)
  - [5.8. Load Balancer'ın Kendisi Çökerse Ne Olur?](#58-load-balancerın-kendisi-çökerse-ne-olur)
- [6. Cache Nedir?](#6-cache-nedir)
  - [6.1. Cache Neden Kullanılır?](#61-cache-neden-kullanılır)
  - [6.2. Cache Hit ve Cache Miss](#62-cache-hit-ve-cache-miss)
  - [6.3. Cache Katmanları](#63-cache-katmanları)
  - [6.4. Cache Stratejileri](#64-cache-stratejileri)
  - [6.5. Cache Invalidation](#65-cache-invalidation)
  - [6.6. TTL](#66-ttl)
  - [6.7. Cache Eviction Politikaları](#67-cache-eviction-politikaları)
  - [6.8. Cache Stampede](#68-cache-stampede)
  - [6.9. Distributed Cache](#69-distributed-cache)
  - [6.10. Redis ve Memcached](#610-redis-ve-memcached)
  - [6.11. Cache Kullanmanın Riskleri](#611-cache-kullanmanın-riskleri)
- [7. Queue Nedir?](#7-queue-nedir)
  - [7.1. Producer ve Consumer](#71-producer-ve-consumer)
  - [7.2. Queue Neden Kullanılır?](#72-queue-neden-kullanılır)
  - [7.3. Senkron ve Asenkron İşleme](#73-senkron-ve-asenkron-işleme)
  - [7.4. Queue Kullanım Senaryoları](#74-queue-kullanım-senaryoları)
  - [7.5. Retry Mantığı](#75-retry-mantığı)
  - [7.6. Dead Letter Queue](#76-dead-letter-queue)
  - [7.7. Idempotency](#77-idempotency)
  - [7.8. Backpressure](#78-backpressure)
  - [7.9. Message Ordering](#79-message-ordering)
- [8. Message Broker Nedir?](#8-message-broker-nedir)
  - [8.1. Message Broker'ın Görevi](#81-message-brokerın-görevi)
  - [8.2. Queue ile Message Broker Arasındaki Fark](#82-queue-ile-message-broker-arasındaki-fark)
  - [8.3. Point-to-Point Messaging](#83-point-to-point-messaging)
  - [8.4. PublishSubscribe](#84-publishsubscribe)
  - [8.5. Exchange, Topic ve Routing Mantığı](#85-exchange-topic-ve-routing-mantığı)
  - [8.6. Delivery Guarantees](#86-delivery-guarantees)
  - [8.7. RabbitMQ, Kafka ve Diğer Brokerlar](#87-rabbitmq-kafka-ve-diğer-brokerlar)
- [9. Queue ve Pub/Sub Arasındaki Fark](#9-queue-ve-pubsub-arasındaki-fark)
- [10. Database Scaling Mantığı](#10-database-scaling-mantığı)
  - [10.1. Read Replica](#101-read-replica)
  - [10.2. Replication](#102-replication)
  - [10.3. Sharding](#103-sharding)
  - [10.4. Partitioning](#104-partitioning)
  - [10.5. SQL ve NoSQL Seçimi](#105-sql-ve-nosql-seçimi)
- [11. CDN Nedir?](#11-cdn-nedir)
- [12. API Gateway Nedir?](#12-api-gateway-nedir)
- [13. Monolith ve Microservices](#13-monolith-ve-microservices)
  - [13.1. Monolithic Architecture](#131-monolithic-architecture)
  - [13.2. Microservice Architecture](#132-microservice-architecture)
  - [13.3. Monolith ve Microservices Karşılaştırması](#133-monolith-ve-microservices-karşılaştırması)
- [14. CAP Teoremi Temelleri](#14-cap-teoremi-temelleri)
- [15. Consistency Modelleri](#15-consistency-modelleri)
- [16. Rate Limiting](#16-rate-limiting)
- [17. Retry, Timeout ve Circuit Breaker](#17-retry-timeout-ve-circuit-breaker)
- [18. Observability ve Sistem Tasarımı](#18-observability-ve-sistem-tasarımı)
- [19. Büyük Ölçekli Bir Web Uygulamasının Örnek Mimarisi](#19-büyük-ölçekli-bir-web-uygulamasının-örnek-mimarisi)
- [20. Örnek Senaryo: E-Ticaret Sipariş Sistemi](#20-örnek-senaryo-e-ticaret-sipariş-sistemi)
- [21. Örnek Senaryo: Sosyal Medya Akışı](#21-örnek-senaryo-sosyal-medya-akışı)
- [22. Sistem Tasarımında Sık Yapılan Hatalar](#22-sistem-tasarımında-sık-yapılan-hatalar)
- [23. Sistem Tasarımı Yaparken İzlenebilecek Adımlar](#23-sistem-tasarımı-yaparken-izlenebilecek-adımlar)
- [24. Mülakatlarda Sistem Tasarımı Sorularına Yaklaşım](#24-mülakatlarda-sistem-tasarımı-sorularına-yaklaşım)
- [25. Sık Sorulan Mülakat Soruları](#25-sık-sorulan-mülakat-soruları)
- [26. Önemli Kavramların Genel Karşılaştırması](#26-önemli-kavramların-genel-karşılaştırması)
- [27. Kısa Özet](#27-kısa-özet)
- [28. Genel Sonuç](#28-genel-sonuç)

---

# 1. Sistem Tasarımı Nedir?

**System Design**, bir yazılım sisteminin hangi bileşenlerden oluşacağını, bu bileşenlerin birbirleriyle nasıl haberleşeceğini, verinin nasıl saklanacağını ve sistemin artan kullanıcı yükü altında nasıl çalışmaya devam edeceğini belirleme sürecidir. Bir sistemi tasarlarken yalnızca:

> “Bu özellik çalışıyor mu?”

sorusu sorulmaz. Aynı zamanda şu sorular da sorulur:

- Aynı anda 10 kullanıcı yerine 1 milyon kullanıcı geldiğinde ne olacak?
- Sunuculardan biri çökerse sistem çalışmaya devam edecek mi?
- Veritabanı çok fazla yük alırsa ne yapılacak?
- Bir isteğin cevap süresi nasıl düşürülecek?
- Kullanıcı sayısı arttıkça sistem nasıl büyütülecek?
- Yavaş çalışan işlemler kullanıcıyı bekletmeden nasıl yürütülecek?
- Bir servis geçici olarak çalışmazsa diğer servisler etkilenir mi?
- Veri kaybı nasıl önlenecek?
- Trafik farklı sunuculara nasıl dağıtılacak?
- Sık kullanılan veriler tekrar tekrar veritabanından mı okunacak?

İşte bu soruların tamamı sistem tasarımının konusudur.

---

## 1.1. Sistem Tasarımının Amacı

İyi bir sistem tasarımının amacı aşağıdaki özellikleri dengeli şekilde sağlayabilmektir:

- **Scalability**
- **Availability**
- **Reliability**
- **Performance**
- **Maintainability**
- **Security**
- **Fault tolerance**
- **Observability**
- **Cost efficiency**

Burada önemli nokta şudur:

> Her sistem için tek bir “mükemmel mimari” yoktur.

Bir bankacılık sistemi ile sosyal medya uygulamasının öncelikleri farklıdır. Örneğin:

- Bankacılık sisteminde veri tutarlılığı kritik olabilir.
- Video platformunda yüksek trafik ve içerik dağıtımı daha kritik olabilir.
- Mesajlaşma uygulamasında düşük gecikme önemli olabilir.
- Raporlama sisteminde birkaç saniyelik gecikme kabul edilebilir olabilir.

Bu nedenle sistem tasarımı aslında bir **trade-off yönetimidir**.

---

## 1.2. Functional ve Non-Functional Requirements

Bir sistem tasarlanırken gereksinimler iki gruba ayrılır.

### Functional Requirements

Sistemin **ne yapması gerektiğini** açıklar. Örneğin bir e-ticaret sistemi:

- kullanıcı kaydı oluşturabilmeli,
- ürün listeleyebilmeli,
- sepete ürün ekleyebilmeli,
- sipariş oluşturabilmeli,
- ödeme alabilmeli.

### Non-Functional Requirements

Sistemin **nasıl çalışması gerektiğini** açıklar. Örneğin:

- saniyede 100.000 istek karşılayabilmeli,
- %99.99 erişilebilir olmalı,
- ortalama cevap süresi 200 ms altında olmalı,
- veri kaybına tolerans çok düşük olmalı,
- servislerden biri çöktüğünde sistem tamamen durmamalı.

Sistem tasarımında asıl mimari kararların büyük bölümü non-functional requirement'lardan çıkar.

---

## 1.3. High-Level Design ve Low-Level Design

### High-Level Design — HLD

Sistemin genel mimarisini gösterir. Örneğin:

```text
Client
  |
  v
Load Balancer
  |
  +--------+--------+
  |        |        |
Server 1 Server 2 Server 3
  |        |        |
  +--------+--------+
           |
           v
        Database
```

HLD seviyesinde şunlarla ilgilenilir:

- servisler,
- veritabanları,
- load balancer,
- cache,
- queue,
- CDN,
- API Gateway,
- servisler arası iletişim.

### Low-Level Design — LLD

Daha çok kod seviyesindeki tasarımı ele alır. Örneğin:

- sınıflar,
- interface'ler,
- design pattern'ler,
- method ilişkileri,
- domain modelleri,
- object-oriented design.

---

# 2. Büyük Ölçekli Sistemlerde Temel Problemler

Bir uygulamanın küçük ölçekte çalışması kolaydır. Örneğin:

```text
100 kullanıcı
    |
    v
1 Backend
    |
    v
1 Database
```

Fakat kullanıcı sayısı arttığında aynı tasarım yetersiz hale gelebilir. Örneğin:

```text
1.000.000 kullanıcı
```

geldiğinde:

- backend CPU'su %100 olabilir,
- RAM bitebilir,
- veritabanı connection sayısı dolabilir,
- sorgular yavaşlayabilir,
- network darboğazı oluşabilir,
- sistem tamamen cevap veremez hale gelebilir.

Bu noktada şu kavramlar devreye girer:

```text
Scalability
Load Balancing
Caching
Replication
Sharding
Queue
Message Broker
CDN
Microservices
Rate Limiting
Fault Tolerance
Observability
```

---

# 3. Scalability Nedir?

**Scalability**, sistemin kullanıcı, trafik veya veri miktarı arttığında performansını kabul edilebilir seviyede koruyarak büyüyebilme yeteneğidir. Basitçe:

> Sisteme daha fazla yük geldiğinde sistemin bu yükü karşılayabilecek şekilde büyüyebilmesidir.

Örneğin bir uygulama:

```text
10.000 request / second
```

karşılayabiliyorsa fakat trafik:

```text
50.000 request / second
```

seviyesine çıktığında çöküyorsa sistem yeterince ölçeklenebilir değildir.

Scalability iki temel yöntemle sağlanır:

```text
Vertical Scaling
Horizontal Scaling
```

---

## 3.1. Vertical Scaling

Vertical Scaling:

> Mevcut sunucunun donanım kaynaklarını artırmaktır.

Örneğin:

```text
Önce:

4 CPU
8 GB RAM

Sonra:

16 CPU
64 GB RAM
```

Aynı sunucu güçlendirilmiştir. Bu yaklaşım:

```text
Scale Up
```

olarak da bilinir.

### Avantajları

- Uygulama mimarisini değiştirmek gerekmez.
- Kurulumu kolaydır.
- Küçük sistemler için hızlı çözüm sunar.
- Distributed system karmaşıklığı oluşturmaz.

### Dezavantajları

Her makinenin fiziksel bir sınırı vardır. Örneğin sürekli:

```text
8 GB → 16 GB → 32 GB → 64 GB → 128 GB
```

RAM eklenemez. Ayrıca güçlü makineler genellikle pahalıdır.

Bir diğer problem:

```text
Tek sunucu
```

hala **Single Point of Failure** olabilir.

---

## 3.2. Horizontal Scaling

Horizontal Scaling:

> Sisteme yeni sunucular eklemektir.

Örneğin:

```text
Önce:

Server 1
```

Daha sonra:

```text
Server 1
Server 2
Server 3
Server 4
```

Bu yaklaşım:

```text
Scale Out
```

olarak da bilinir. Örnek:

```text
             Load Balancer
                    |
        +-----------+-----------+
        |           |           |
        v           v           v
     Server 1    Server 2    Server 3
```

Kullanıcı istekleri load balancer tarafından bu sunucular arasında dağıtılır.

### Avantajları

- Teorik olarak çok büyük sistemlere ölçeklenebilir.
- Bir sunucu çökerse diğerleri çalışabilir.
- Yük dağıtılabilir.
- Cloud ortamlarında kolayca otomatikleştirilebilir.

### Dezavantajları

Distributed system problemleri ortaya çıkar. Örneğin:

- session yönetimi,
- cache tutarlılığı,
- servisler arası iletişim,
- distributed transaction,
- network latency,
- veri senkronizasyonu.

---

## 3.3. Vertical ve Horizontal Scaling Karşılaştırması

| Özellik              | Vertical Scaling         | Horizontal Scaling |
| -------------------- | ------------------------ | ------------------ |
| Yaklaşım             | Makineyi güçlendirme     | Yeni makine ekleme |
| Diğer adı            | Scale Up                 | Scale Out          |
| Uygulama değişikliği | Az                       | Gerekebilir        |
| Ölçek sınırı         | Donanım sınırı var       | Çok daha yüksek    |
| Maliyet              | Güçlü makinelerde yüksek | Dağıtılabilir      |
| Fault tolerance      | Düşük                    | Yüksek olabilir    |
| Karmaşıklık          | Düşük                    | Daha yüksek        |
| Büyük sistemler      | Sınırlı                  | Daha uygun         |

Modern büyük ölçekli web sistemlerinde çoğu zaman horizontal scaling tercih edilir.

---

## 3.4. Stateless ve Stateful Sistemler

Horizontal scaling yapılırken çok önemli bir konu ortaya çıkar.

### Stateful Server

Server kullanıcı state'ini kendi belleğinde saklar. Örneğin:

```text
User Login
    |
    v
Server 1

Session = Server 1 memory
```

Sonraki request:

```text
User
 |
 v
Server 2
```

üzerine giderse Server 2 kullanıcının session bilgisini bilmiyor olabilir. Bu durum horizontal scaling'i zorlaştırır.

### Stateless Server

Server request'ler arasında kullanıcı state'i saklamaz. State başka yerde tutulur. Örneğin:

```text
Client
  |
  v
Load Balancer
  |
  +--------+--------+
  |        |        |
Server1 Server2 Server3
  |        |        |
  +--------+--------+
           |
           v
         Redis
```

Bu durumda herhangi bir server isteği karşılayabilir. Bu nedenle:

> Stateless backend tasarımı horizontal scaling için daha uygundur.

---

## 3.5. Auto Scaling

Cloud ortamlarında sunucu sayısı otomatik olarak artırılıp azaltılabilir. Örneğin:

```text
Normal trafik:

3 server
```

```text
Yoğun trafik:

10 server
```

```text
Gece:

2 server
```

Bu sisteme **Auto Scaling** denir. Auto scaling trigger'ları şunlar olabilir:

```text
CPU > %70
Memory > %80
Request/sec > threshold
Queue length > threshold
```

Avantajları:

- gereksiz maliyet azalır,
- trafik artışlarında sistem otomatik büyür,
- manuel müdahale azalır.

---

## 3.6. Scaling Yaparken Ortaya Çıkan Problemler

Sisteme yalnızca daha fazla server eklemek her problemi çözmez. Yeni problemler ortaya çıkar:

### Database Bottleneck

Backend sayısı artırılsa bile tüm server'lar aynı database'e bağlanıyorsa:

```text
Server 1 \
Server 2  \
Server 3 ---> Database
Server 4  /
```

darboğaz database olabilir.

### Shared State

Session veya cache tek server'da tutulursa diğer server'lar state'e ulaşamaz.

### Distributed Lock

Aynı kaynağı birden fazla servis değiştirmeye çalışabilir.

### Network Latency

Servisler ayrı makinelerde çalıştığı için network maliyeti oluşur.

### Consistency

Birden fazla database veya cache varsa verilerin senkron olması gerekir. Bu nedenle gerçek scalability:

> Sadece sunucu sayısını artırmak değil, bütün sistemi ölçeklenebilir tasarlamaktır.

---

# 4. Availability, Reliability ve Fault Tolerance

Scalability tek başına yeterli değildir. Bir sistem aynı zamanda erişilebilir ve güvenilir olmalıdır.

---

## 4.1. High Availability

**Availability**, sistemin erişilebilir olduğu zaman oranıdır. Örneğin:

```text
99.9%
99.99%
99.999%
```

gibi ifadeler kullanılır. Yüksek availability için:

- redundant server,
- load balancer,
- database replication,
- failover,
- multi-zone deployment

kullanılabilir.

---

## 4.2. Reliability

Reliability:

> Sistemin doğru sonucu üretmeye devam etme yeteneğidir.

Bir sistem online olabilir fakat yanlış veri üretirse reliable değildir.

---

## 4.3. Fault Tolerance

Fault tolerance:

> Sistemin bazı bileşenleri arızalansa bile çalışmaya devam edebilmesidir.

Örneğin:

```text
Server 1 → DOWN
Server 2 → UP
Server 3 → UP
```

Load balancer Server 1'e request göndermeyi bırakır. Sistem çalışmaya devam eder.

---

## 4.4. Redundancy

Redundancy:

> Kritik bileşenlerden birden fazla bulundurmaktır.

Örneğin:

```text
1 database
```

yerine:

```text
Primary Database
Replica Database
```

kullanılabilir. Ama redundancy tek başına yeterli değildir. Failover mekanizması da gerekir.

---

## 4.5. Single Point of Failure

**Single Point of Failure — SPOF**, çöktüğünde tüm sistemi durduran bileşendir. Örneğin:

```text
Client
  |
  v
1 Load Balancer
  |
  v
10 Server
```

Burada load balancer tek ise:

```text
Load Balancer DOWN
```

olduğunda 10 server çalışsa bile kullanıcı sisteme ulaşamaz. Bu nedenle kritik komponentlerde redundancy gerekir.

---

# 5. Load Balancer Nedir?

**Load Balancer**, gelen network veya HTTP isteklerini birden fazla sunucu arasında dağıtan sistemdir. Örneğin:

```text
                Users
                  |
                  v
           +---------------+
           | Load Balancer |
           +---------------+
            /      |      \
           v       v       v
       Server 1 Server 2 Server 3
```

Kullanıcı doğrudan backend server'a bağlanmaz. Önce load balancer'a gelir.

---

## 5.1. Load Balancer Neden Kullanılır?

Load balancer'ın temel amaçları:

### 1. Trafiği Dağıtmak

Tek server'ın aşırı yüklenmesini önler.

### 2. High Availability Sağlamak

Bir server çökerse request diğer server'a gönderilir.

### 3. Horizontal Scaling Sağlamak

Yeni server sisteme kolayca eklenebilir.

### 4. Maintenance Kolaylığı

Bir server bakım için sistemden çıkarılabilir. Diğer server'lar çalışmaya devam eder.

### 5. Performans

Request'ler boş veya daha az yoğun server'lara yönlendirilebilir.

---

## 5.2. Load Balancer Nasıl Çalışır?

Örnek:

```text
Request 1 → Server A
Request 2 → Server B
Request 3 → Server C
Request 4 → Server A
```

Load balancer bu dağıtımı belirli algoritmalarla yapar.

---

## 5.3. Load Balancing Algoritmaları

### Round Robin

Request'ler sırayla server'lara gönderilir.

```text
Request 1 → Server A
Request 2 → Server B
Request 3 → Server C
Request 4 → Server A
```

Basit ve yaygın bir algoritmadır.

---

### Weighted Round Robin

Bazı server'lar daha güçlü olabilir. Örneğin:

```text
Server A → weight 5
Server B → weight 3
Server C → weight 1
```

Server A daha fazla request alır.

---

### Least Connections

En az aktif bağlantıya sahip server seçilir. Örnek:

```text
Server A → 100 connection
Server B → 20 connection
Server C → 60 connection
```

Yeni request:

```text
Server B
```

üzerine gönderilebilir.

---

### Least Response Time

Cevap süresi en düşük server tercih edilir.

---

### IP Hash

Kullanıcının IP adresinden hash üretilir. Aynı kullanıcı çoğu zaman aynı server'a yönlendirilir. Özellikle sticky session benzeri ihtiyaçlarda kullanılabilir.

---

### Random

Server rastgele seçilir. Bazı durumlarda yeterince büyük sistemlerde şaşırtıcı derecede iyi sonuç verebilir.

---

## 5.4. Layer 4 ve Layer 7 Load Balancing

### Layer 4 Load Balancer

Transport layer seviyesinde çalışır. Genellikle:

```text
TCP
UDP
IP
Port
```

bilgilerine göre yönlendirme yapar. Avantajları:

- hızlıdır,
- düşük overhead vardır.

---

### Layer 7 Load Balancer

Application layer seviyesinde çalışır. HTTP içeriğini anlayabilir. Örneğin:

```text
/api/users
```

isteğini:

```text
User Service
```

üzerine,

```text
/api/orders
```

isteğini:

```text
Order Service
```

üzerine yönlendirebilir. Ayrıca:

- header,
- cookie,
- hostname,
- URL path

gibi bilgileri kullanabilir.

---

## 5.5. Health Check

Load balancer server'ların çalışıp çalışmadığını düzenli olarak kontrol eder. Örneğin:

```http
GET /health
```

Server:

```http
200 OK
```

döndürüyorsa healthy kabul edilir. Server cevap vermezse:

```text
Server 2 → unhealthy
```

Load balancer request göndermeyi bırakır.

---

## 5.6. Session Persistence ve Sticky Session

Bazı uygulamalar kullanıcının sürekli aynı server'a yönlendirilmesini ister. Buna:

```text
Sticky Session
```

denir. Örneğin:

```text
User A → Server 1
User A → Server 1
User A → Server 1
```

Fakat bu yöntem horizontal scaling açısından ideal değildir. Daha iyi yaklaşım:

```text
Session → Redis
```

gibi merkezi bir store kullanmaktır.

---

## 5.7. Load Balancer ve Reverse Proxy Farkı

Bu iki kavram benzer görünür.

### Reverse Proxy

Client ile backend arasına girer. Görevleri:

- request forwarding,
- SSL termination,
- caching,
- compression,
- routing,
- security.

### Load Balancer

Temel amacı:

```text
yükü birden fazla backend arasında dağıtmaktır.
```

Birçok modern araç iki işi birden yapabilir. Örnek teknolojiler:

```text
Nginx
HAProxy
Envoy
AWS Application Load Balancer
Cloud Load Balancing
Azure Load Balancer
```

---

## 5.8. Load Balancer'ın Kendisi Çökerse Ne Olur?

Tek load balancer varsa:

```text
SPOF
```

oluşabilir. Çözüm:

```text
Load Balancer A
Load Balancer B
```

kullanmak ve failover mekanizması oluşturmaktır.

---

# 6. Cache Nedir?

**Cache**, sık kullanılan verilerin daha hızlı erişilebilen bir ortamda geçici olarak tutulmasıdır. Normal akış:

```text
Application
    |
    v
Database
```

Cache ile:

```text
Application
    |
    v
  Cache
    |
    v
Database
```

Application önce cache'e bakar.

---

## 6.1. Cache Neden Kullanılır?

Database sorgusu:

```text
50 ms
```

Cache erişimi:

```text
1-5 ms
```

olabilir. Aynı veri milyonlarca kez isteniyorsa database'i her defasında sorgulamak gereksizdir. Cache sayesinde:

- latency azalır,
- database yükü azalır,
- throughput artar,
- sistem daha fazla kullanıcı kaldırabilir.

---

## 6.2. Cache Hit ve Cache Miss

### Cache Hit

Aranan veri cache'de bulunur.

```text
Request
  |
  v
Cache
  |
  v
Data Found
```

Bu durumda database'e gidilmez.

### Cache Miss

Veri cache'de bulunmaz.

```text
Request
  |
  v
Cache
  |
  v
Not Found
  |
  v
Database
```

Database'den alınan veri daha sonra cache'e yazılabilir.

### Cache Hit Ratio

Önemli bir metric'tir.

```text
Cache Hit Ratio = Cache Hit / Total Cache Request
```

Hit ratio ne kadar yüksekse cache o kadar etkili çalışıyor olabilir.

---

## 6.3. Cache Katmanları

Cache yalnızca Redis anlamına gelmez. Bir sistemde birçok cache seviyesi olabilir.

### Browser Cache

Tarayıcı:

- CSS,
- JavaScript,
- image,
- font

gibi dosyaları cache'leyebilir.

---

### CDN Cache

Statik içerikler kullanıcıya yakın edge server'larda tutulabilir.

---

### Application Memory Cache

Uygulama kendi RAM'inde veri tutabilir. Örneğin:

```text
Dictionary
MemoryCache
ConcurrentHashMap
```

---

### Distributed Cache

Birden fazla backend'in ortak kullandığı cache. Örneğin:

```text
Redis
Memcached
```

---

### Database Cache

Database engine'lerinin kendi internal cache sistemleri bulunur.

---

## 6.4. Cache Stratejileri

### Cache-Aside

En yaygın modellerden biridir. Akış:

```text
1. Application cache'e bakar.
2. Veri varsa döndürür.
3. Veri yoksa database'e gider.
4. Database'den gelen veri cache'e yazılır.
5. Veri client'a döndürülür.
```

Pseudo flow:

```text
if cache.contains(key):
    return cache.get(key)

data = database.get(key)
cache.set(key, data)

return data
```

Avantajı:

- sadece gerçekten kullanılan veriler cache'e girer.

---

### Read-Through Cache

Application database'e doğrudan gitmez. Cache sistemi eksik veriyi database'den getirir.

```text
Application
    |
    v
Cache
    |
    +------> Database
```

---

### Write-Through Cache

Write işlemi:

```text
Application
    |
    v
Cache
    |
    v
Database
```

şeklinde yapılır. Cache ve database aynı anda güncel tutulur.

Avantaj:

- cache tutarlılığı yüksektir.

Dezavantaj:

- write latency artabilir.

---

### Write-Back / Write-Behind Cache

Önce cache güncellenir. Database daha sonra asenkron güncellenir.

```text
Application
    |
    v
Cache
    |
    | async
    v
Database
```

Avantaj:

- write çok hızlıdır.

Risk:

- cache çökerse henüz database'e yazılmamış veri kaybolabilir.

---

## 6.5. Cache Invalidation

Cache'in en zor problemlerinden biri:

```text
Cache Invalidation
```

yani eski verinin ne zaman silineceğini belirlemektir. Örneğin:

```text
Database:
Product Price = 100 TL

Cache:
Product Price = 100 TL
```

Database güncellenir:

```text
Product Price = 120 TL
```

ama cache hâlâ:

```text
100 TL
```

tutuyorsa kullanıcı stale data görür. Çözümler:

- cache delete,
- TTL,
- event-driven invalidation,
- versioning.

---

## 6.6. TTL

**TTL — Time To Live**

Cache verisinin ne kadar süre yaşayacağını belirtir. Örneğin:

```text
product:123
TTL = 5 dakika
```

5 dakika sonra kayıt cache'den silinir.

TTL seçimi önemlidir. Çok uzun TTL:

```text
stale data
```

riskini artırır. Çok kısa TTL:

```text
cache effectiveness
```

azaltabilir.

---

## 6.7. Cache Eviction Politikaları

Cache memory dolduğunda bazı kayıtların silinmesi gerekir.

### LRU

Least Recently Used. En uzun süredir kullanılmayan veri silinir.

### LFU

Least Frequently Used. En az kullanılan veri silinir.

### FIFO

İlk eklenen veri önce silinir.

### Random

Rastgele veri silinir.

---

## 6.8. Cache Stampede

Popüler bir cache kaydı aynı anda expire olabilir. Örneğin:

```text
product-list
```

cache'den silinir. Aynı anda:

```text
100.000 request
```

gelirse hepsi database'e gidebilir. Bu duruma:

```text
Cache Stampede
```

denir. Çözümler:

- distributed lock,
- request coalescing,
- stale-while-revalidate,
- randomized TTL,
- background refresh.

---

## 6.9. Distributed Cache

Birden fazla backend server varsa local cache problem oluşturabilir. Örneğin:

```text
Server 1 Cache → Price = 100
Server 2 Cache → Price = 120
```

Tutarsızlık oluşur. Distributed cache:

```text
Server 1 \
Server 2 ---> Redis
Server 3 /
```

şeklinde ortak cache sağlar.

---

## 6.10. Redis ve Memcached

### Redis

Redis yalnızca basit key-value cache değildir. Desteklediği yapılar:

```text
String
Hash
List
Set
Sorted Set
Stream
```

Ayrıca:

- TTL,
- pub/sub,
- distributed lock,
- persistence,
- counters

gibi özellikler sunabilir.

### Memcached

Daha basit bir distributed memory cache sistemidir. Genellikle basit key-value caching için kullanılır.

---

## 6.11. Cache Kullanmanın Riskleri

Cache performansı artırır fakat yeni problemler getirir.

### Stale Data

Cache eski veri döndürebilir.

### Cache Invalidation Complexity

Verinin ne zaman silineceği zor olabilir.

### Cache Stampede

Cache miss sonrası database aşırı yüklenebilir.

### Memory Cost

Büyük cache cluster'ları maliyetlidir.

### Hot Key

Tek bir cache key çok yoğun istek alabilir. Bu durumda tek node darboğaz olabilir.

---

# 7. Queue Nedir?

Queue:

> İşlerin veya mesajların sıraya alındığı veri yapısı veya messaging mekanizmasıdır.

Temel mantık:

```text
Producer
   |
   v
 Queue
   |
   v
Consumer
```

Producer işi queue'ya bırakır.

Consumer işi daha sonra işler.

---

## 7.1. Producer ve Consumer

### Producer

Mesajı veya işi üretir. Örneğin:

```text
Order Service
```

### Consumer

Queue'dan mesajı alıp işler. Örneğin:

```text
Email Worker
```

---

## 7.2. Queue Neden Kullanılır?

### 1. Asynchronous Processing

Kullanıcı uzun işlemleri beklemek zorunda kalmaz.

### 2. Load Smoothing

Ani trafik artışı doğrudan backend'i çökertmez.

### 3. Service Decoupling

Servisler birbirine doğrudan bağımlı olmaz.

### 4. Retry

Başarısız işler tekrar denenebilir.

### 5. Fault Isolation

Bir servis geçici olarak çalışmasa bile mesaj queue'da bekleyebilir.

---

## 7.3. Senkron ve Asenkron İşleme

### Senkron

```text
Client
  |
  v
API
  |
  v
Email Service
  |
  v
Response
```

Email servisi yavaşsa kullanıcı bekler.

### Asenkron

```text
Client
  |
  v
API
  |
  v
Queue
  |
  v
Response

Queue
  |
  v
Email Worker
```

API kullanıcıya hızlı cevap verebilir. Email daha sonra gönderilir.

---

## 7.4. Queue Kullanım Senaryoları

Queue yaygın olarak şu işlemlerde kullanılır:

- e-mail gönderme,
- SMS gönderme,
- image processing,
- video encoding,
- notification,
- log processing,
- payment workflows,
- report generation,
- background jobs,
- order processing.

---

## 7.5. Retry Mantığı

Consumer mesajı işlerken hata alabilir. Örneğin:

```text
Payment API timeout
```

Mesaj kaybolmak yerine tekrar denenebilir. Örneğin:

```text
Retry 1 → 5 saniye sonra
Retry 2 → 30 saniye sonra
Retry 3 → 5 dakika sonra
```

Buna exponential backoff uygulanabilir.

---

## 7.6. Dead Letter Queue

Bir mesaj birçok kez işlenemiyorsa sonsuza kadar retry yapmak doğru değildir. Bu mesaj:

```text
Dead Letter Queue
```

içine gönderilebilir. Örnek:

```text
Main Queue
   |
   v
Consumer
   |
   | failure x 5
   v
Dead Letter Queue
```

Developer daha sonra problemi analiz edebilir.

---

## 7.7. Idempotency

Distributed sistemlerde aynı mesaj bazen birden fazla kez gelebilir. Örneğin:

```text
Payment message
```

iki kez işlenirse müşteri iki kez ücretlendirilebilir. Bu nedenle consumer:

```text
idempotent
```

olmalıdır. Idempotency:

> Aynı işlemin birden fazla kez uygulanmasının sonucu değiştirmemesidir.

Örneğin:

```text
payment_id = abc123
```

daha önce işlendi mi kontrol edilir.

---

## 7.8. Backpressure

Producer mesajları consumer'dan daha hızlı üretiyorsa queue büyür. Örneğin:

```text
Producer → 10.000 msg/sec
Consumer → 2.000 msg/sec
```

Queue sürekli büyür. Bu duruma backpressure problemi denir.

Çözümler:

- consumer sayısını artırmak,
- producer rate limit,
- batch processing,
- autoscaling,
- queue partitioning.

---

## 7.9. Message Ordering

Bazı sistemlerde mesaj sırası önemlidir. Örneğin:

```text
1. Order Created
2. Order Paid
3. Order Shipped
```

Consumer:

```text
Order Shipped
```

mesajını önce işlerse sorun oluşabilir. Bazı queue sistemleri global ordering sağlamaz. Partition veya key bazlı ordering kullanılabilir.

---

# 8. Message Broker Nedir?

**Message Broker**, farklı servisler arasında mesajların güvenilir şekilde iletilmesini sağlayan ara katmandır. Örneğin:

```text
Order Service
     |
     v
Message Broker
   /   |    \
  v    v     v
Email Inventory Analytics
```

Order Service diğer servisleri doğrudan çağırmak zorunda değildir.

---

## 8.1. Message Broker'ın Görevi

Message broker şu görevleri yapabilir:

- mesaj kabul etmek,
- mesaj saklamak,
- queue oluşturmak,
- routing yapmak,
- subscriber'lara mesaj göndermek,
- retry yönetmek,
- acknowledgment mekanizması sağlamak,
- delivery guarantee sağlamak.

---

## 8.2. Queue ile Message Broker Arasındaki Fark

Queue bir kavramdır:

```text
mesajların sırada tutulduğu yapı
```

Message broker ise daha geniş bir sistemdir. Broker:

- birden fazla queue yönetebilir,
- routing yapabilir,
- publish/subscribe destekleyebilir,
- retry sağlayabilir,
- persistence sağlayabilir.

Yani:

> Queue, message broker'ın sunduğu yapılardan biri olabilir.

---

## 8.3. Point-to-Point Messaging

Bir mesaj yalnızca bir consumer tarafından işlenir.

```text
Producer
   |
   v
Queue
   |
   +------ Consumer 1
   +------ Consumer 2
```

Mesaj:

```text
Consumer 1
```

veya:

```text
Consumer 2
```

tarafından işlenir. İkisi tarafından aynı anda işlenmez. Bu yaklaşım job processing için uygundur.

---

## 8.4. Publish/Subscribe

Bir event birden fazla subscriber tarafından alınabilir. Örneğin:

```text
OrderCreated
```

event'i oluştu. Subscriber'lar:

```text
Inventory Service
Email Service
Analytics Service
Notification Service
```

hepsi bu event'i alabilir. Akış:

```text
              OrderCreated
                   |
                   v
              Message Broker
             /      |       \
            v       v        v
       Inventory  Email  Analytics
```

Bu yapı event-driven architecture'da çok yaygındır.

---

## 8.5. Exchange, Topic ve Routing Mantığı

Özellikle RabbitMQ benzeri sistemlerde producer mesajı doğrudan queue'ya değil bir exchange'e gönderebilir.

```text
Producer
   |
   v
Exchange
  /   \
 v     v
Q1     Q2
```

Exchange routing kurallarına göre mesajları queue'lara yönlendirir.

### Direct Routing

Belirli routing key ile eşleşen queue.

### Topic Routing

Pattern bazlı routing. Örneğin:

```text
order.created
order.cancelled
payment.completed
```

### Fanout

Mesaj tüm bağlı queue'lara gönderilir.

---

## 8.6. Delivery Guarantees

Messaging sistemlerinde üç temel teslim modeli vardır.

### At-Most-Once

Mesaj:

```text
0 veya 1 kez
```

işlenir. Duplicate olmaz fakat mesaj kaybolabilir.

### At-Least-Once

Mesaj:

```text
1 veya daha fazla kez
```

işlenebilir. Mesaj kaybı azaltılır fakat duplicate olabilir. Bu durumda idempotency gerekir.

### Exactly-Once

Mesajın tam olarak bir kez işlenmesi hedeflenir. Distributed sistemlerde uygulanması daha karmaşıktır ve çoğu sistem pratikte idempotent processing ile benzer iş garantisini kurar.

---

## 8.7. RabbitMQ, Kafka ve Diğer Brokerlar

### RabbitMQ

Klasik message broker yaklaşımına yakındır. Güçlü yönleri:

- queue,
- exchange,
- routing,
- acknowledgment,
- retry,
- dead letter queue.

Genellikle:

- task queue,
- background jobs,
- command messaging

için kullanılır.

### Apache Kafka

Kafka klasik queue'dan farklı olarak distributed event log yaklaşımına sahiptir. Mesajlar:

```text
Topic
```

içinde saklanır. Topic'ler:

```text
Partition
```

yapısına ayrılır. Consumer mesajı okuduğunda mesaj hemen silinmek zorunda değildir. Bu nedenle Kafka:

- event streaming,
- analytics,
- log processing,
- high-throughput data pipelines

için çok güçlüdür.

### Diğer Örnekler

```text
Apache Pulsar
AWS SQS
AWS SNS
Azure Service Bus
Google Pub/Sub
NATS
ActiveMQ
```

---

# 9. Queue ve Pub/Sub Arasındaki Fark

### Queue

Bir mesaj genellikle tek worker tarafından işlenir.

```text
Job
 |
 v
Queue
 |
 v
One Consumer
```

### Pub/Sub

Bir event birçok subscriber'a gider.

```text
Event
 |
 v
Topic
 |   |   |
 v   v   v
A   B   C
```

| Özellik        | Queue                   | Pub/Sub                   |
| -------------- | ----------------------- | ------------------------- |
| Amaç           | İş dağıtmak             | Event yaymak              |
| Mesaj tüketimi | Genellikle bir consumer | Birden fazla subscriber   |
| Örnek          | Email job               | OrderCreated event        |
| Kullanım       | Background processing   | Event-driven architecture |

---

# 10. Database Scaling Mantığı

Backend ölçeklense bile database darboğaz olabilir. Bu nedenle database de ölçeklenmelidir.

---

## 10.1. Read Replica

Okuma trafiği çok yüksekse read replica kullanılabilir.

```text
               Primary DB
                /      \
               v        v
         Read Replica  Read Replica
```

Write:

```text
Primary
```

üzerine yapılır. Read:

```text
Replica
```

üzerinden yapılabilir. Bu sayede read yükü dağıtılır.

---

## 10.2. Replication

Replication:

> Verinin bir database'den başka database'lere kopyalanmasıdır.

Faydaları:

- high availability,
- disaster recovery,
- read scaling.

Ancak replication lag oluşabilir. Yani replica primary'den birkaç milisaniye veya saniye geride olabilir.

---

## 10.3. Sharding

Sharding:

> Veriyi birden fazla database arasında bölmektir.

Örneğin:

```text
User ID 1 - 1M → DB1
User ID 1M - 2M → DB2
User ID 2M - 3M → DB3
```

Başka bir yöntem:

```text
hash(user_id) % shard_count
```

Avantaj:

- veri ve yük dağıtılır.

Dezavantaj:

- cross-shard query,
- shard rebalancing,
- distributed transaction

karmaşık hale gelir.

---

## 10.4. Partitioning

Partitioning aynı database içinde büyük tabloların bölümlere ayrılmasıdır. Örneğin log tablosu:

```text
2025 logs
2026 logs
2027 logs
```

şeklinde partition edilebilir. Partitioning ile sharding aynı şey değildir.

### Partitioning

Genellikle aynı database sistemi içerisinde veri bölme.

### Sharding

Veriyi farklı database instance'larına dağıtma.

---

## 10.5. SQL ve NoSQL Seçimi

### SQL

Avantajları:

- relational model,
- strong consistency,
- transaction,
- JOIN,
- schema.

Örnek:

```text
PostgreSQL
MySQL
SQL Server
Oracle
```

### NoSQL

Bazı use-case'lerde daha esnek veya daha kolay horizontal scaling sağlayabilir. Türleri:

```text
Document
Key-Value
Column Family
Graph
```

Örnek:

```text
MongoDB
Redis
Cassandra
DynamoDB
Neo4j
```

Seçim:

> “NoSQL daha hızlıdır” gibi tek cümlelik bir kuralla yapılmaz.

Access pattern, consistency ihtiyacı, veri modeli ve ölçek gereksinimi analiz edilmelidir.

---

# 11. CDN Nedir?

**CDN — Content Delivery Network**, içerikleri kullanıcıya coğrafi olarak yakın sunuculardan dağıtan sistemdir. Örneğin ana server Almanya'da olsun. Türkiye'deki kullanıcı:

```text
Germany Server
```

yerine İstanbul'a yakın edge server'dan dosyayı alabilir.

CDN genellikle:

- image,
- video,
- JavaScript,
- CSS,
- font,
- static file

için kullanılır. Akış:

```text
User
 |
 v
CDN Edge
 |
 | cache miss
 v
Origin Server
```

Avantajları:

- latency azalır,
- origin server yükü azalır,
- bandwidth maliyeti azalabilir,
- global kullanıcı deneyimi iyileşir.

---

# 12. API Gateway Nedir?

Microservice sistemlerinde client'ın onlarca servisi ayrı ayrı bilmesi istenmez. Bu nedenle API Gateway kullanılabilir.

```text
Client
  |
  v
API Gateway
  |
  +------ User Service
  |
  +------ Order Service
  |
  +------ Payment Service
```

API Gateway şu görevleri yapabilir:

- routing,
- authentication,
- rate limiting,
- logging,
- SSL termination,
- request aggregation,
- authorization,
- throttling.

Load balancer ile API Gateway aynı şey değildir. Load balancer daha çok:

```text
traffic distribution
```

odaklıdır.

API Gateway ise:

```text
API management
```

odaklıdır.

---

# 13. Monolith ve Microservices

## 13.1. Monolithic Architecture

Tüm uygulama tek deployable unit olabilir.

```text
Application
 |
 +-- User
 +-- Product
 +-- Order
 +-- Payment
```

Avantajları:

- geliştirmesi kolay,
- debug kolay,
- deployment kolay,
- transaction yönetimi kolay.

Dezavantajları:

- uygulama büyüdükçe karmaşıklık artabilir,
- tek modül değişikliği tüm uygulamanın deploy edilmesini gerektirebilir,
- bağımsız scaling zor olabilir.

---

## 13.2. Microservice Architecture

Sistem ayrı servislerden oluşur.

```text
User Service
Order Service
Payment Service
Inventory Service
Notification Service
```

Her servis:

- kendi deployment sürecine,
- kendi scaling politikasına,
- bazen kendi database'ine

sahip olabilir.

Avantajları:

- bağımsız deployment,
- bağımsız scaling,
- fault isolation,
- ekip bağımsızlığı.

Dezavantajları:

- distributed transactions,
- network failures,
- service discovery,
- observability,
- message delivery,
- data consistency

gibi problemler ortaya çıkar.

---

## 13.3. Monolith ve Microservices Karşılaştırması

| Özellik                | Monolith     | Microservices              |
| ---------------------- | ------------ | -------------------------- |
| Başlangıç karmaşıklığı | Düşük        | Yüksek                     |
| Deployment             | Tek parça    | Bağımsız                   |
| Scaling                | Tüm sistem   | Servis bazlı               |
| Debug                  | Daha kolay   | Daha zor                   |
| Network problemi       | Az           | Fazla                      |
| Data consistency       | Daha kolay   | Daha karmaşık              |
| Küçük ekip             | Çok uygun    | Gereksiz karmaşık olabilir |
| Büyük sistem           | Zorlaşabilir | Avantaj sağlayabilir       |

Önemli nokta:

> Her proje microservice olmak zorunda değildir.

Küçük ve orta projelerde iyi tasarlanmış modular monolith çoğu zaman daha mantıklı olabilir.

---

# 14. CAP Teoremi Temelleri

Distributed database sistemlerinde üç özellik önemlidir:

```text
Consistency
Availability
Partition Tolerance
```

### Consistency

Her node aynı anda aynı veriyi görür.

### Availability

Her request cevap alır.

### Partition Tolerance

Network partition oluşsa bile sistem çalışmaya devam eder. CAP teoremine göre gerçek bir network partition sırasında aynı anda hem tam consistency hem tam availability garanti edilemez. Sistem bir trade-off yapmak zorunda kalır.

---

# 15. Consistency Modelleri

### Strong Consistency

Write sonrası yapılan read güncel veriyi görür. Bankacılık işlemleri gibi sistemlerde önemli olabilir.

### Eventual Consistency

Tüm node'lar hemen aynı veriyi görmeyebilir. Ancak zamanla tutarlı hale gelir. Örneğin sosyal medya like sayısı birkaç saniye gecikmeli güncellenebilir. Bu yaklaşım yüksek ölçekli distributed sistemlerde sık görülür.

---

# 16. Rate Limiting

Rate limiting:

> Bir kullanıcının veya client'ın belirli sürede yapabileceği request sayısını sınırlar.

Örneğin:

```text
100 request / minute
```

Amaçlar:

- abuse önlemek,
- DDoS etkisini azaltmak,
- servisleri korumak,
- adil kaynak kullanımı.

Yaygın algoritmalar:

```text
Token Bucket
Leaky Bucket
Fixed Window
Sliding Window
```

Örnek cevap:

```http
HTTP 429 Too Many Requests
```

---

# 17. Retry, Timeout ve Circuit Breaker

Distributed sistemlerde network request'leri her zaman başarılı olmaz. Bu nedenle üç önemli pattern vardır.

---

## Timeout

Bir servisi sonsuza kadar beklemek doğru değildir. Örneğin:

```text
Payment Service timeout = 2 seconds
```

---

## Retry

Geçici hata varsa request tekrar denenebilir. Fakat her hata retry edilmemelidir. Örneğin:

```text
HTTP 500 → retry olabilir
HTTP 400 → çoğu zaman retry anlamsız
```

Retry kullanırken:

```text
exponential backoff
```

uygulanabilir.

---

## Circuit Breaker

Bir servis sürekli hata veriyorsa tekrar tekrar çağırmak sistemi daha da zorlayabilir. Circuit breaker:

```text
CLOSED
OPEN
HALF-OPEN
```

durumlarına sahip olabilir.

### Closed

Request'ler normal gönderilir.

### Open

Servise request gönderilmez.

### Half-Open

Servisin iyileşip iyileşmediğini test etmek için sınırlı request gönderilir.

---

# 18. Observability ve Sistem Tasarımı

Büyük sistem sadece çalışmakla kalmamalı, gözlemlenebilir olmalıdır. Observability üç temel parçadan oluşur:

```text
Logs
Metrics
Traces
```

### Logs

Sistemde gerçekleşen olayları gösterir.

### Metrics

Sayısal ölçümler. Örneğin:

```text
CPU
Memory
Request per second
Error rate
Latency
Queue length
Cache hit ratio
```

### Distributed Tracing

Bir request'in microservice sisteminde hangi servislerden geçtiğini gösterir. Örneğin:

```text
API Gateway
  |
  v
Order Service
  |
  v
Payment Service
  |
  v
Database
```

Her adımın latency'si takip edilebilir.

---

# 19. Büyük Ölçekli Bir Web Uygulamasının Örnek Mimarisi

Basit bir büyük ölçekli sistem:

```text
                   Users
                     |
                     v
                    CDN
                     |
                     v
               Load Balancer
                     |
        +------------+------------+
        |            |            |
        v            v            v
     Server 1     Server 2     Server 3
        |            |            |
        +------------+------------+
                     |
             +-------+-------+
             |               |
             v               v
           Cache          Database
          (Redis)            |
                             v
                          Replica
```

Daha gelişmiş mimari:

```text
                        Users
                          |
                          v
                         CDN
                          |
                          v
                    API Gateway
                          |
                          v
                    Load Balancer
                          |
         +----------------+----------------+
         |                |                |
         v                v                v
   User Service      Order Service    Product Service
         |                |                |
         v                v                v
      User DB          Order DB        Product DB
                          |
                          v
                    Message Broker
                     /     |      \
                    v      v       v
                Payment  Email  Analytics
```

Burada:

- CDN static content'i hızlandırır.
- API Gateway API giriş noktasıdır.
- Load Balancer request'leri dağıtır.
- Backend servisleri horizontal scale edilebilir.
- Redis cache database yükünü azaltır.
- Message broker servisleri decouple eder.
- Queue uzun işlemleri asynchronous hale getirir.
- Database replication read yükünü dağıtabilir.

---

# 20. Örnek Senaryo: E-Ticaret Sipariş Sistemi

Kullanıcı sipariş oluşturuyor. İlk yaklaşım:

```text
Client
  |
  v
Order API
  |
  +--> Payment
  |
  +--> Inventory
  |
  +--> Email
  |
  +--> Analytics
  |
  v
Response
```

Problem:

Email servisi yavaşlarsa kullanıcı bekler. Analytics servisi çökerse sipariş işlemi etkilenebilir.

Daha iyi yaklaşım:

```text
Client
  |
  v
Order API
  |
  v
Database
  |
  v
OrderCreated Event
  |
  v
Message Broker
 /     |       \
v      v        v
Email Inventory Analytics
```

Bu yapı:

```text
loose coupling
```

sağlar.

---

# 21. Örnek Senaryo: Sosyal Medya Akışı

Bir sosyal medya uygulamasında milyonlarca kullanıcı ana sayfasını açıyor. Her request'te:

```text
database JOIN
sort
filter
aggregation
```

yapmak çok pahalı olabilir.

Çözüm olarak:

- cache,
- precomputed feed,
- CDN,
- distributed storage,
- queue,
- event-driven processing

kullanılabilir.

Örneğin kullanıcı post paylaşır:

```text
User
 |
 v
Post Service
 |
 v
Database
 |
 v
PostCreated Event
 |
 v
Queue
 |
 v
Feed Worker
 |
 v
Feed Cache
```

Kullanıcı feed açtığında:

```text
Feed Cache
```

üzerinden hızlı cevap alabilir.

---

# 22. Sistem Tasarımında Sık Yapılan Hatalar

### 1. Gereksiz Microservice Kullanmak

Küçük bir uygulamayı onlarca servise bölmek gereksiz karmaşıklık yaratabilir.

### 2. Cache'i Her Probleme Çözüm Sanmak

Cache consistency problemi oluşturabilir.

### 3. Database'i Unutmak

Backend scale edilse bile database bottleneck olabilir.

### 4. Single Point of Failure Bırakmak

Tek:

```text
database
load balancer
message broker
```

kritik risk olabilir.

### 5. Retry Storm Oluşturmak

Bir servis çöktüğünde binlerce client sürekli retry yaparsa sistem daha da kötüleşir.

### 6. Timeout Koymamak

Bir servis sonsuza kadar cevap bekleyebilir.

### 7. Idempotency'yi Unutmak

Duplicate message finansal hatalara yol açabilir.

### 8. Queue'nun Sonsuz Olduğunu Sanmak

Consumer yavaşsa queue büyüyebilir.

### 9. Monitoring Yapmamak

Production'da problemi görmek çok zorlaşır.

### 10. Premature Optimization

Henüz 100 kullanıcısı olan sistemi 100 milyon kullanıcıya göre tasarlamak gereksiz maliyet ve karmaşıklık yaratabilir.

---

# 23. Sistem Tasarımı Yaparken İzlenebilecek Adımlar

Bir sistemi tasarlarken aşağıdaki sıra kullanılabilir.

### Aşama 1 — Requirements

Functional requirements belirlenir. Örnek:

```text
User post paylaşabilir.
User post görebilir.
User follow yapabilir.
```

---

### Aşama 2 — Non-Functional Requirements

Örnek:

```text
100M kullanıcı
10K request/sec
low latency
high availability
```

---

### Aşama 3 — Capacity Estimation

Yaklaşık hesaplar yapılabilir. Örneğin:

```text
1M daily active user
10 request/user/day
```

Toplam:

```text
10M request/day
```

Average RPS:

```text
10M / 86.400
≈ 116 request/sec
```

Peak traffic bunun birkaç katı olabilir.

---

### Aşama 4 — API Design

Örneğin:

```http
POST /posts
GET /posts/{id}
GET /feed
```

---

### Aşama 5 — Data Model

Örneğin:

```text
User
Post
Comment
Like
Follow
```

---

### Aşama 6 — High-Level Architecture

Örneğin:

```text
Client
 |
 v
Load Balancer
 |
 v
API Servers
 |
 +--> Cache
 |
 +--> Database
 |
 +--> Queue
```

---

### Aşama 7 — Bottleneck Analizi

Sor:

```text
En çok hangi component yük alıyor?
Database?
Cache?
Network?
CPU?
Storage?
```

---

### Aşama 8 — Scaling Strategy

Gerekirse:

```text
Read Replica
Sharding
Cache
CDN
Queue
Horizontal Scaling
```

eklenir.

---

### Aşama 9 — Failure Scenarios

Şu sorular sorulur:

```text
Server çökerse?
Database çökerse?
Redis çökerse?
Queue dolarsa?
Network partition olursa?
```

---

### Aşama 10 — Monitoring

Sistem gözlemlenebilir hale getirilir.

---

# 24. Mülakatlarda Sistem Tasarımı Sorularına Yaklaşım

Örnek soru:

> “Twitter benzeri bir sistem tasarla.”

Doğrudan mimari çizmeye başlamak yerine önce requirement soruları sorulmalıdır. Örneğin:

```text
Kaç kullanıcı var?
Read/write oranı nedir?
Post limiti var mı?
Media desteklenecek mi?
Real-time feed gerekiyor mu?
Consistency seviyesi nedir?
```

Daha sonra:

```text
API
Data Model
Architecture
Scaling
Caching
Database
Queue
Failure handling
```

adım adım ele alınabilir. Sistem tasarımı mülakatında amaç yalnızca “doğru cevap” bulmak değildir. Asıl amaç:

> Mimari kararların nedenlerini açıklayabilmektir.

---

# 25. Sık Sorulan Mülakat Soruları

## Scalability nedir?

Sistemin artan kullanıcı veya trafik yükünü performansı kabul edilebilir seviyede tutarak karşılayabilme yeteneğidir.

---

## Vertical scaling ve horizontal scaling farkı nedir?

Vertical scaling mevcut sunucuyu güçlendirir.
Horizontal scaling yeni sunucular ekler.

---

## Load balancer ne işe yarar?

Gelen request'leri birden fazla backend server arasında dağıtır. Ayrıca high availability ve fault tolerance sağlamaya yardımcı olur.

---

## Cache neden kullanılır?

Sık kullanılan verilerin hızlı erişilebilen memory sistemlerinde tutulmasını sağlayarak latency ve database yükünü azaltır.

---

## Cache hit nedir?

İstenen verinin cache'de bulunmasıdır.

---

## Cache miss nedir?

İstenen verinin cache'de bulunmamasıdır. Bu durumda veri genellikle ana data source'dan alınır.

---

## TTL nedir?

Cache kaydının ne kadar süre geçerli kalacağını belirleyen süredir.

---

## Queue neden kullanılır?

Uzun veya yoğun işleri asenkron işlemek, servisleri decouple etmek ve ani yükleri absorbe etmek için kullanılır.

---

## Message broker nedir?

Servisler arasında mesaj iletimini ve routing'i yöneten middleware sistemidir.

---

## Queue ve message broker farkı nedir?

Queue mesajların tutulduğu yapıdır. Message broker ise queue'ları, routing'i, pub/sub'ı ve delivery mekanizmalarını yönetebilen daha geniş sistemdir.

---

## RabbitMQ ve Kafka farkı nedir?

RabbitMQ klasik message broker ve task queue kullanımına çok uygundur. Kafka distributed event streaming ve yüksek throughput event log sistemidir.

---

## Dead Letter Queue nedir?

Belirli sayıda retry sonrası işlenemeyen mesajların gönderildiği özel queue'dur.

---

## Idempotency neden önemlidir?

Aynı mesajın tekrar işlenmesi durumunda duplicate operasyonların oluşmasını engeller. Özellikle payment sistemlerinde kritiktir.

---

## CDN neden kullanılır?

Static içerikleri kullanıcıya coğrafi olarak yakın server'lardan sunarak latency'i ve origin server yükünü azaltır.

---

## Database sharding nedir?

Verinin birden fazla database instance arasında bölünmesidir.

---

## Read replica nedir?

Ana database'in read-only kopyasıdır. Read trafiğini dağıtmak için kullanılabilir.

---

## Stateless backend neden önemlidir?

Her request herhangi bir server tarafından işlenebildiği için horizontal scaling'i kolaylaştırır.

---

## Single Point of Failure nedir?

Çöktüğünde bütün sistemi durdurabilecek tek bileşendir.

---

# 26. Önemli Kavramların Genel Karşılaştırması

| Kavram          | Temel Amaç                                       |
| --------------- | ------------------------------------------------ |
| Scalability     | Artan yükü karşılamak                            |
| Load Balancer   | Trafiği server'lara dağıtmak                     |
| Cache           | Veri erişimini hızlandırmak                      |
| Queue           | İşleri sıraya almak                              |
| Message Broker  | Servisler arasında mesaj iletmek                 |
| CDN             | İçeriği kullanıcıya yakın noktadan sunmak        |
| Read Replica    | Read trafiğini dağıtmak                          |
| Sharding        | Veriyi farklı database'lere bölmek               |
| API Gateway     | API trafiğini yönetmek                           |
| Rate Limiting   | Request sayısını sınırlamak                      |
| Circuit Breaker | Hatalı servise sürekli request gitmesini önlemek |
| Retry           | Geçici hatalarda tekrar denemek                  |
| Timeout         | Sonsuz beklemeyi önlemek                         |
| Replication     | Veriyi birden fazla node'a kopyalamak            |
| Observability   | Sistemin davranışını izlemek                     |
| Auto Scaling    | Server sayısını trafik durumuna göre değiştirmek |

---

# 27. Kısa Özet

Büyük ölçekli bir sistem düşünürken temel akış şu şekilde özetlenebilir:

```text
                USER
                  |
                  v
                 CDN
                  |
                  v
             Load Balancer
                  |
       +----------+----------+
       |          |          |
       v          v          v
    Server 1   Server 2   Server 3
       |
       +----------------------+
       |                      |
       v                      v
     Cache                 Database
    (Redis)                   |
                              v
                         Read Replica
```

Asenkron işlemler:

```text
Backend
   |
   v
Message Broker
   |
   +------ Email Worker
   |
   +------ Notification Worker
   |
   +------ Analytics Worker
```

Bu mimaride:

```text
Load Balancer
```

trafik dağıtır.

```text
Horizontal Scaling
```

sunucu kapasitesini artırır.

```text
Cache
```

database yükünü azaltır.

```text
Queue
```

uzun işleri kullanıcı request'inden ayırır.

```text
Message Broker
```

servislerin birbirine bağımlılığını azaltır.

```text
Read Replica
```

database read yükünü dağıtır.

```text
CDN
```

static içeriği hızlı sunar.

```text
Monitoring
```

problemlerin production ortamında tespit edilmesini sağlar.

---

# 28. Genel Sonuç

Sistem tasarımı, yalnızca diyagram çizmek değildir.

Asıl amaç:

> Sistemin yük arttığında, bazı bileşenler çöktüğünde veya kullanıcı sayısı milyonlara ulaştığında nasıl davranacağını düşünmektir.

Küçük bir uygulama başlangıçta şu şekilde olabilir:

```text
Client
  |
  v
Server
  |
  v
Database
```

Fakat sistem büyüdükçe mimari şu bileşenlere ihtiyaç duyabilir:

```text
CDN
Load Balancer
Multiple Application Servers
Distributed Cache
Message Queue
Message Broker
Database Replication
Read Replicas
Sharding
Rate Limiting
Monitoring
Fault Tolerance
Auto Scaling
```

Bu yapıların hiçbiri yalnızca “modern olduğu için” kullanılmamalıdır. Her bileşenin eklenmesinin bir nedeni olmalıdır.

Örneğin:

```text
Problem:
Database çok fazla read request alıyor.

Çözüm:
Cache veya read replica.
```

```text
Problem:
Tek server trafik altında çöküyor.

Çözüm:
Horizontal scaling + load balancer.
```

```text
Problem:
Email gönderimi request'i yavaşlatıyor.

Çözüm:
Queue + background worker.
```

```text
Problem:
Servisler birbirine aşırı bağımlı.

Çözüm:
Message broker + event-driven communication.
```

Bu nedenle iyi bir system designer'ın en önemli sorusu:

> “Hangi teknolojiyi kullanmalıyım?”

değil,

> “Sistemde hangi problemi çözmeye çalışıyorum?”

olmalıdır.

Bir mimari karar değerlendirirken şu zinciri kurabilmek gerekir:

```text
Problem
   |
   v
Requirement
   |
   v
Architecture Decision
   |
   v
Trade-off
```

Örneğin:

```text
Yüksek read trafiği
        |
        v
Database yükü
        |
        v
Cache
        |
        v
Daha düşük latency
        |
        v
Fakat cache invalidation problemi
```

İşte sistem tasarımının temel mantığı tam olarak budur:

> **Performans, ölçeklenebilirlik, tutarlılık, maliyet, güvenilirlik ve karmaşıklık arasında doğru dengeyi kurmak.**
