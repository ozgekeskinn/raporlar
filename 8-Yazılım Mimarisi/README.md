# 8. Yazılım Mimarisi Temelleri

Yazılım mimarisi, bir uygulamanın sadece “kod yazılmış hali” değil; o kodların **nasıl organize edildiğini**, parçaların **birbiriyle nasıl konuştuğunu**, verinin **nereden gelip nereye gittiğini**, sistemin **nasıl büyütülebileceğini**, **nasıl test edileceğini** ve **nasıl sürdürülebilir kalacağını** belirleyen genel yapıdır. Yani mimari, projenin omurgasıdır. Bir projede küçükken her şeyi tek dosyaya yazmak kolay görünebilir. Ama proje büyüdükçe şu sorunlar başlar:

* Kodlar birbirine karışır.
* Hata bulmak zorlaşır.
* Yeni özellik eklemek riskli hale gelir.
* Aynı kod tekrar tekrar yazılır.
* Test yazmak zorlaşır.
* Takım halinde çalışmak karmaşıklaşır.
* Bir yerde yapılan değişiklik başka bir yeri bozabilir.

İşte yazılım mimarisi bu sorunları azaltmak için vardır.

---

## İçindekiler

- [1. Yazılım Mimarisi Nedir?](#1-yazılım-mimarisi-nedir)
- [2. Neden Yazılım Mimarisi Öğrenmeliyiz?](#2-neden-yazılım-mimarisi-öğrenmeliyiz)

- [3. Monolith vs Microservice](#3-monolith-vs-microservice)
  - [3.1. Monolith Nedir?](#31-monolith-nedir)
  - [3.2. Monolith Mimariye Günlük Hayattan Benzetme](#32-monolith-mimariye-günlük-hayattan-benzetme)
  - [3.3. Monolith Mimarisinin Avantajları](#33-monolith-mimarisinin-avantajları)
  - [3.4. Monolith Mimarisinin Dezavantajları](#34-monolith-mimarisinin-dezavantajları)
  - [3.5. Microservice Nedir?](#35-microservice-nedir)
  - [3.6. Microservice Mimarisine Günlük Hayattan Benzetme](#36-microservice-mimarisine-günlük-hayattan-benzetme)
  - [3.7. Microservice Mimarisinin Avantajları](#37-microservice-mimarisinin-avantajları)
  - [3.8. Microservice Mimarisinin Dezavantajları](#38-microservice-mimarisinin-dezavantajları)
  - [3.9. Monolith ve Microservice Karşılaştırması](#39-monolith-ve-microservice-karşılaştırması)
  - [3.10. Hangisi Daha İyi?](#310-hangisi-daha-iyi)

- [4. Mimari Desenler: MVC, MVVM ve Diğer Mimari Yaklaşımlar](#4-mimari-desenler-mvc-mvvm-ve-diğer-mimari-yaklaşımlar)
  - [4.1. MVC Nedir?](#41-mvc-nedir)
    - [4.1.1. Model Nedir?](#411-model-nedir)
    - [4.1.2. View Nedir?](#412-view-nedir)
    - [4.1.3. Controller Nedir?](#413-controller-nedir)
    - [4.1.4. MVC Akışı](#414-mvc-akışı)
    - [4.1.5. MVC Örneği](#415-mvc-örneği)
    - [4.1.6. MVC’nin Avantajları](#416-mvcnin-avantajları)
    - [4.1.7. MVC’nin Dezavantajları](#417-mvcnin-dezavantajları)
  - [4.2. MVVM Nedir?](#42-mvvm-nedir)
    - [4.2.1. Model](#421-model)
    - [4.2.2. View](#422-view)
    - [4.2.3. ViewModel](#423-viewmodel)
    - [4.2.4. MVVM Akışı](#424-mvvm-akışı)
    - [4.2.5. MVVM Örneği](#425-mvvm-örneği)
    - [4.2.6. MVVM’nin Avantajları](#426-mvvmnin-avantajları)
    - [4.2.7. MVVM’nin Dezavantajları](#427-mvvmnin-dezavantajları)
  - [4.3. MVC ve MVVM Farkı](#43-mvc-ve-mvvm-farkı)
  - [4.4. MVP Mimarisi](#44-mvp-mimarisi)
  - [4.5. Layered Architecture](#45-layered-architecture)
  - [4.6. Clean Architecture](#46-clean-architecture)
  - [4.7. Repository Pattern](#47-repository-pattern)
  - [4.8. Service-Oriented Architecture](#48-service-oriented-architecture)
  - [4.9. Microservices Architecture](#49-microservices-architecture)
  - [4.10. Mimari Desenlerin Yazılım Geliştirmedeki Önemi](#410-mimari-desenlerin-yazılım-geliştirmedeki-önemi)

- [5. State Management Nedir?](#5-state-management-nedir)
  - [5.1. State’e Basit Örnek](#51-statee-basit-örnek)
  - [5.2. State Management Neden Gereklidir?](#52-state-management-neden-gereklidir)
  - [5.3. Local State Nedir?](#53-local-state-nedir)
  - [5.4. Global State Nedir?](#54-global-state-nedir)
  - [5.5. Server State Nedir?](#55-server-state-nedir)
  - [5.6. UI State Nedir?](#56-ui-state-nedir)
  - [5.7. State Management Araçları](#57-state-management-araçları)
  - [5.8. State Management Olmazsa Ne Olur?](#58-state-management-olmazsa-ne-olur)

- [6. Katmanlı Mimari Nedir?](#6-katmanlı-mimari-nedir)
  - [6.1. Katmanlı Mimariye Neden İhtiyaç Duyulur?](#61-katmanlı-mimariye-neden-ihtiyaç-duyulur)
  - [6.2. Controller Katmanı](#62-controller-katmanı)
    - [6.2.1. Controller Ne Yapmalı?](#621-controller-ne-yapmalı)
    - [6.2.2. Controller Ne Yapmamalı?](#622-controller-ne-yapmamalı)
  - [6.3. Service Katmanı](#63-service-katmanı)
    - [6.3.1. Service Katmanı Ne İşe Yarar?](#631-service-katmanı-ne-işe-yarar)
    - [6.3.2. Service Katmanına Örnek](#632-service-katmanına-örnek)
  - [6.4. Repository Katmanı](#64-repository-katmanı)
    - [6.4.1. Repository Neden Kullanılır?](#641-repository-neden-kullanılır)
    - [6.4.2. Repository Katmanının Avantajları](#642-repository-katmanının-avantajları)
  - [6.5. Entity, DTO ve Mapper Kavramları](#65-entity-dto-ve-mapper-kavramları)
    - [6.5.1. Entity Nedir?](#651-entity-nedir)
    - [6.5.2. DTO Nedir?](#652-dto-nedir)
    - [6.5.3. DTO Neden Önemlidir?](#653-dto-neden-önemlidir)
    - [6.5.4. Mapper Nedir?](#654-mapper-nedir)
  - [6.6. Katmanlı Mimari Akışı](#66-katmanlı-mimari-akışı)
  - [6.7. Katmanlı Mimari Örneği](#67-katmanlı-mimari-örneği)
  - [6.8. Katmanlı Mimari Kullanmanın Avantajları](#68-katmanlı-mimari-kullanmanın-avantajları)
  - [6.9. Katmanlı Mimari Kullanırken Yapılan Hatalar](#69-katmanlı-mimari-kullanırken-yapılan-hatalar)
    - [6.9.1. Controller’a Çok Fazla Kod Yazmak](#691-controllera-çok-fazla-kod-yazmak)
    - [6.9.2. Service Katmanını Gereksiz Boş Bırakmak](#692-service-katmanını-gereksiz-boş-bırakmak)
    - [6.9.3. Repository İçine İş Mantığı Yazmak](#693-repository-içine-iş-mantığı-yazmak)
    - [6.9.4. Entity’yi Doğrudan API Cevabı Olarak Döndürmek](#694-entityyi-doğrudan-api-cevabı-olarak-döndürmek)

- [7. Clean Code ve Mimari İlişkisi](#7-clean-code-ve-mimari-ilişkisi)
- [8. Yazılım Mimarisinin Proje Geliştirmeye Katkısı](#8-yazılım-mimarisinin-proje-geliştirmeye-katkısı)
- [9. Basit Bir Proje Üzerinden Genel Mimari Örnek](#9-basit-bir-proje-üzerinden-genel-mimari-örnek)
- [10. Bu Konunun Kazandırdığı Yetkinlik](#10-bu-konunun-kazandırdığı-yetkinlik)
- [11. Kısa Özet](#11-kısa-özet)

---

## 1. Yazılım Mimarisi Nedir?

Yazılım mimarisi, bir yazılım sisteminin temel yapı taşlarını ve bu yapı taşları arasındaki ilişkileri belirleyen tasarım yaklaşımıdır. Bir uygulama geliştirirken genelde şu soruların cevabı mimariyle ilgilidir:

* Kullanıcı arayüzü nerede olacak?
* İş kuralları nerede yazılacak?
* Veritabanı işlemleri hangi katmanda yapılacak?
* API isteklerini kim karşılayacak?
* Kodlar hangi klasörlere ayrılacak?
* Bir modül diğer modülle nasıl iletişim kuracak?
* Sistem ileride büyürse nasıl yönetilecek?
* Test yazmak kolay olacak mı?
* Hatalar sistemin tamamını mı etkiler, yoksa sadece küçük bir bölümü mü?

Kısacası mimari, yazılımın sadece “çalışmasını” değil, **düzenli, anlaşılır, geliştirilebilir ve sürdürülebilir olmasını** sağlar.

---

## 2. Neden Yazılım Mimarisi Öğrenmeliyiz?

Başlangıç seviyesinde bir projede genelde amaç “kod çalışsın” olur. Bu gayet normaldir. Ama orta ve ileri seviyeye geçtikçe sadece çalışan kod yeterli olmaz. İyi bir yazılımda şu özellikler beklenir:

* Kod okunabilir olmalı.
* Yeni özellik eklemek kolay olmalı.
* Hatalar kolay bulunmalı.
* Kod tekrarından kaçınılmalı.
* Her bölümün görevi net olmalı.
* Test edilebilir bir yapı kurulmalı.
* Proje büyüyünce dağılmamalı.

Mesela bir e-ticaret sitesi düşünelim. Kullanıcı ürünleri listeler, sepete ekler, ödeme yapar, sipariş oluşturur. Eğer bütün işlemler tek dosyada yazılırsa, proje büyüdükçe kod tam bir çorbaya döner. Ama mimari doğru kurulursa:

* Ürün işlemleri ayrı yönetilir.
* Sepet işlemleri ayrı yönetilir.
* Ödeme işlemleri ayrı yönetilir.
* Sipariş işlemleri ayrı yönetilir.
* Veritabanı işlemleri ayrı katmanda tutulur.
* Kullanıcı arayüzü iş mantığından ayrılır.

Bu sayede proje hem daha profesyonel hem de daha sürdürülebilir olur.

---

## 3. Monolith vs Microservice

Yazılım mimarisinde en temel ayrımlardan biri **monolithic architecture** ve **microservice architecture** ayrımıdır. Bunlar, uygulamanın genel olarak nasıl parçalara ayrıldığını anlatır.

---

### 3.1. Monolith Nedir?

Monolith, uygulamanın tüm parçalarının tek bir bütün halinde geliştirildiği mimari yaklaşımdır. Yani uygulamanın kullanıcı yönetimi, ürün yönetimi, sipariş yönetimi, ödeme sistemi, raporlama sistemi gibi bütün modülleri aynı proje içinde bulunur. Örneğin bir e-ticaret uygulaması monolith yapıda şöyle olabilir:

```text
E-Ticaret Uygulaması
│
├── Kullanıcı İşlemleri
├── Ürün İşlemleri
├── Sepet İşlemleri
├── Sipariş İşlemleri
├── Ödeme İşlemleri
├── Raporlama
└── Veritabanı İşlemleri
```

Bunların hepsi aynı uygulamanın içinde yer alır. Uygulama tek parça olarak geliştirilir, tek parça olarak derlenir ve tek parça olarak sunucuya yüklenir.

---

### 3.2. Monolith Mimariye Günlük Hayattan Benzetme

Monolith mimariyi büyük bir okul binasına benzetebiliriz. Okulun içinde:

* Sınıflar,
* Müdür odası,
* Öğretmenler odası,
* Kantin,
* Kütüphane,
* Spor salonu

aynı bina içindedir. Her şey tek yerde olduğu için yönetmek kolaydır. Ama bina çok büyürse, bir bölümde çıkan sorun tüm binayı etkileyebilir. Yazılımda da monolith buna benzer. Tüm sistem tek uygulamanın içindedir.

---

### 3.3. Monolith Mimarisinin Avantajları

Monolith mimari özellikle küçük ve orta ölçekli projeler için oldukça mantıklıdır.

#### 1. Geliştirmesi daha kolaydır

Başlangıçta tüm proje tek yerde olduğu için geliştirme süreci daha basittir. Ayrı servisler, ayrı deployment süreçleri veya servisler arası iletişim gibi karmaşık konularla uğraşılmaz.

#### 2. Test etmesi daha basit olabilir

Tüm kod aynı proje içinde olduğu için küçük projelerde test yazmak ve sistemi çalıştırmak daha kolaydır.

#### 3. Dağıtımı daha kolaydır

Uygulama tek parça olduğu için canlı ortama almak daha basittir. Tek uygulama derlenir ve sunucuya yüklenir.

#### 4. Küçük ekipler için uygundur

Küçük ekiplerde veya bireysel projelerde monolith yapı daha pratik olabilir. Çünkü herkes aynı proje üzerinde çalışır.

#### 5. Başlangıç maliyeti düşüktür

Microservice mimaride gereken altyapı, izleme, servis iletişimi ve dağıtım süreçleri monolith’e göre daha karmaşıktır. Monolith bu açıdan daha ekonomik ve hızlıdır.

---

### 3.4. Monolith Mimarisinin Dezavantajları

Proje büyüdükçe monolith mimarinin bazı zorlukları ortaya çıkar.

#### 1. Kod karmaşıklaşabilir

Uygulamadaki modül sayısı arttıkça kodların birbirine karışma riski artar. Örneğin ürün işlemlerinde yapılan bir değişiklik yanlışlıkla sipariş işlemlerini etkileyebilir.

#### 2. Ölçeklendirme zordur

Diyelim ki uygulamada sadece ödeme sistemi çok yoğun kullanılıyor. Monolith mimaride sadece ödeme kısmını büyütmek zordur. Çünkü sistem tek parça olduğu için tüm uygulamanın ölçeklendirilmesi gerekir.

#### 3. Hata tüm sistemi etkileyebilir

Bir modülde çıkan kritik hata, uygulamanın tamamını etkileyebilir. Örneğin raporlama modülünde çıkan bir hata yüzünden tüm sistemin çökmesi istenmez. Ama kötü tasarlanmış bir monolith sistemde bu mümkün olabilir.

#### 4. Büyük ekiplerde yönetimi zorlaşır

Aynı proje üzerinde çok fazla geliştirici çalışıyorsa kod çakışmaları ve bağımlılık sorunları oluşabilir.

#### 5. Teknoloji esnekliği azdır

Tüm proje aynı teknolojiyle geliştirildiği için farklı modüllerde farklı teknolojiler kullanmak zordur.

---

### 3.5. Microservice Nedir?

Microservice mimarisi, büyük bir uygulamayı küçük, bağımsız servisler halinde geliştirme yaklaşımıdır. Her servis belirli bir işi yapar ve diğer servislerle genellikle API üzerinden iletişim kurar. Örneğin bir e-ticaret uygulaması microservice mimaride şöyle ayrılabilir:

```text
E-Ticaret Sistemi
│
├── User Service
├── Product Service
├── Cart Service
├── Order Service
├── Payment Service
├── Notification Service
└── Report Service
```

Burada her servis kendi görevinden sorumludur. Mesela:

* User Service kullanıcı işlemlerini yönetir.
* Product Service ürünleri yönetir.
* Cart Service sepet işlemlerini yönetir.
* Order Service siparişleri yönetir.
* Payment Service ödeme işlemlerini yönetir.
* Notification Service e-posta/SMS bildirimlerini yönetir.

Bu servisler birbirinden bağımsız geliştirilebilir, test edilebilir ve dağıtılabilir.

---

### 3.6. Microservice Mimarisine Günlük Hayattan Benzetme

Microservice mimariyi bir alışveriş merkezine benzetebiliriz. Alışveriş merkezinde:

* Market ayrı çalışır.
* Kafe ayrı çalışır.
* Sinema ayrı çalışır.
* Giyim mağazası ayrı çalışır.
* Teknoloji mağazası ayrı çalışır.

Hepsi aynı yapının parçasıdır ama her biri bağımsızdır. Bir mağazada sorun çıkması tüm alışveriş merkezinin kapanmasını gerektirmez. Yazılımda da microservice yapısı buna benzer. Her servis kendi başına çalışabilir.

---

### 3.7. Microservice Mimarisinin Avantajları

#### 1. Bağımsız geliştirme imkânı sağlar

Her servis ayrı geliştirilebilir. Örneğin ödeme servisi üzerinde çalışan ekip, ürün servisini etkilemeden geliştirme yapabilir.

#### 2. Bağımsız dağıtım yapılabilir

Bir serviste değişiklik yapıldığında tüm sistemi yeniden yayınlamak gerekmez. Sadece ilgili servis güncellenebilir.

#### 3. Ölçeklendirme daha kolaydır

Sistemde hangi servis yoğun kullanılıyorsa sadece o servis büyütülebilir. Örneğin kampanya döneminde ödeme ve sipariş servisleri yoğun kullanılıyorsa sadece bu servisler ölçeklendirilebilir.

#### 4. Hata izolasyonu sağlar

Bir serviste hata çıkması tüm sistemi doğrudan çökertmeyebilir. Örneğin bildirim servisi çalışmazsa sistem yine sipariş almaya devam edebilir.

#### 5. Farklı teknolojiler kullanılabilir

Her servis farklı teknolojiyle yazılabilir. Örneğin:

* User Service Java ile,
* Recommendation Service Python ile,
* Notification Service Node.js ile

geliştirilebilir. Bu, özellikle büyük ve uzmanlaşmış ekiplerde avantaj sağlar.

---

### 3.8. Microservice Mimarisinin Dezavantajları

Microservice kulağa çok profesyonel gelse de her proje için uygun değildir.

#### 1. Yönetimi zordur

Birden fazla servis olduğu için sistemin yönetimi karmaşıklaşır.

#### 2. Servisler arası iletişim gerekir

Servisler birbirleriyle API, message queue veya event sistemi üzerinden haberleşir. Bu da ekstra karmaşıklık getirir.

#### 3. Deployment süreci daha zordur

Her servisin ayrı ayrı yayınlanması gerekir. Bu nedenle CI/CD, Docker, Kubernetes gibi araçlara ihtiyaç duyulabilir.

#### 4. Debug yapmak zorlaşabilir

Bir işlem birden fazla servisten geçiyorsa hatanın hangi serviste olduğunu bulmak zor olabilir.

#### 5. Veritabanı yönetimi karmaşıklaşır

Microservice mimaride genellikle her servisin kendi veritabanı olabilir. Bu yapı veri tutarlılığı açısından dikkatli tasarlanmalıdır.

#### 6. Küçük projeler için gereksiz karmaşık olabilir

Basit bir blog sitesi veya küçük bir okul projesi için microservice kullanmak çoğu zaman gereksizdir. Bu durumda monolith daha mantıklı olur.

---

### 3.9. Monolith ve Microservice Karşılaştırması

| Özellik          | Monolith                     | Microservice                             |
| ---------------- | ---------------------------- | ---------------------------------------- |
| Yapı             | Tek parça uygulama           | Küçük bağımsız servisler                 |
| Geliştirme       | Başlangıçta kolay            | Başlangıçta daha zor                     |
| Deployment       | Tek seferde yapılır          | Her servis ayrı yayınlanır               |
| Ölçeklendirme    | Tüm uygulama ölçeklenir      | Sadece ihtiyaç duyulan servis ölçeklenir |
| Hata etkisi      | Tüm sistemi etkileyebilir    | Genelde ilgili servisle sınırlı kalır    |
| Teknoloji seçimi | Genelde tek teknoloji        | Servis bazlı farklı teknoloji olabilir   |
| Küçük projeler   | Uygundur                     | Genelde fazla karmaşıktır                |
| Büyük projeler   | Zamanla zorlaşabilir         | Daha uygun olabilir                      |
| Takım çalışması  | Büyük ekiplerde zorlaşabilir | Ekipler servis bazlı ayrılabilir         |

---

### 3.10. Hangisi Daha İyi?

Aslında “monolith kötü, microservice iyi” gibi bir durum yoktur. Doğru cevap şudur:

> Projenin büyüklüğüne, ekibin tecrübesine, sistemin ihtiyaçlarına ve bakım sürecine göre doğru mimari değişir.

Küçük ve orta ölçekli projelerde iyi tasarlanmış bir monolith gayet başarılı olabilir. Büyük, yoğun trafikli, farklı ekiplerin çalıştığı ve sürekli geliştirilen sistemlerde microservice daha avantajlı olabilir.

---

## 4. Mimari Desenler: MVC, MVVM ve Diğer Mimari Yaklaşımlar

Yazılım mimarisinde sadece uygulamanın tek parça mı yoksa servislerden mi oluşacağı değil, uygulama içindeki kodların nasıl düzenleneceği de önemlidir. Bu noktada karşımıza **mimari desenler** çıkar. Mimari desenler, yazılımda sık karşılaşılan yapısal problemler için kullanılan genel çözüm yaklaşımlarıdır. En bilinen mimari desenlerden bazıları:

* MVC
* MVVM
* MVP
* Layered Architecture
* Clean Architecture

---

### 4.1. MVC Nedir?

MVC, “Model - View - Controller” kelimelerinin kısaltmasıdır. MVC mimarisinde uygulama üç ana bölüme ayrılır:

```text
Model
View
Controller
```

Her bölümün ayrı bir görevi vardır.

---

#### 4.1.1. Model Nedir?

Model, uygulamanın veri ve iş kurallarıyla ilgili kısmıdır. Model genellikle:

* Veritabanından gelen verileri temsil eder.
* Veri yapısını tanımlar.
* İş kurallarını içerebilir.
* Uygulamanın temel nesnelerini temsil eder.

Örneğin bir kullanıcı sistemi düşünelim.

```text
User
- id
- name
- email
- password
```

Buradaki User yapısı bir modeldir. Bir ürün sistemi için:

```text
Product
- id
- name
- price
- stock
```

Buradaki Product da bir modeldir. Model, uygulamanın “hangi veriyle çalıştığını” temsil eder.

---

#### 4.1.2. View Nedir?

View, kullanıcının gördüğü arayüzdür. Web uygulamasında View şunlar olabilir:

* HTML sayfası
* CSS ile tasarlanmış görünüm
* Kullanıcı formu
* Butonlar
* Listeleme ekranları
* Tablo yapıları

Mobil uygulamada View:

* Ekran tasarımı
* Widget yapıları
* Butonlar
* Form alanları

olabilir. View’un temel görevi kullanıcıya bilgiyi göstermektir. Örneğin:

* Ürün listesini gösterir.
* Kullanıcı giriş formunu gösterir.
* Sepet ekranını gösterir.
* Hata mesajını gösterir.

View mümkün olduğunca iş mantığından uzak tutulmalıdır. Yani View içinde “ürün stokta mı, ödeme nasıl alınacak, kullanıcı yetkili mi” gibi karmaşık kuralların yazılması doğru değildir.

---

#### 4.1.3. Controller Nedir?

Controller, Model ve View arasında köprü görevi görür. Kullanıcıdan gelen istekleri alır, gerekli işlemleri başlatır ve sonucu View’a gönderir. Örneğin kullanıcı “Giriş Yap” butonuna bastığında:

1. View kullanıcı bilgilerini alır.
2. Controller bu isteği karşılar.
3. Controller gerekli kontrolü yapar veya service katmanına gönderir.
4. Model/veritabanı tarafında işlem yapılır.
5. Sonuç tekrar Controller’a gelir.
6. Controller sonucu View’a iletir.

Yani Controller, uygulamadaki istekleri yöneten bölümdür.

---

#### 4.1.4. MVC Akışı

Bir MVC yapısında genel akış şu şekildedir:

```text
Kullanıcı → View → Controller → Model → Controller → View → Kullanıcı
```

Örnek:

Kullanıcı ürün listesini görmek istiyor.

```text
1. Kullanıcı ürünler sayfasına girer.
2. View isteği başlatır.
3. Controller isteği karşılar.
4. Controller ürün verilerini Model veya Service üzerinden alır.
5. Gelen ürün listesi View’a gönderilir.
6. View ürünleri kullanıcıya gösterir.
```

---

#### 4.1.5. MVC Örneği

Bir blog uygulaması düşünelim.

### Model

```text
Post
- id
- title
- content
- createdDate
```

### View

```text
post-list.html
post-detail.html
create-post.html
```

### Controller

```text
PostController
- getAllPosts()
- getPostById()
- createPost()
- deletePost()
```

Burada PostController kullanıcının isteklerini karşılar. Post modeli veriyi temsil eder. View ise kullanıcıya blog yazılarını gösterir.

---

#### 4.1.6. MVC’nin Avantajları

#### 1. Kod düzeni sağlar

Model, View ve Controller ayrıldığı için kodlar daha düzenli hale gelir.

#### 2. Sorumluluklar ayrılır

Her bölümün görevi bellidir. View sadece görünümle, Controller isteklerle, Model verilerle ilgilenir.

#### 3. Bakım kolaylaşır

Arayüzde değişiklik yapmak istediğinde iş mantığını bozman gerekmez. Aynı şekilde veritabanı tarafında değişiklik yaparken View’a çok fazla dokunman gerekmez.

#### 4. Test edilebilirlik artar

Controller ve Model katmanları ayrı olduğu için test yazmak daha kolay hale gelir.

#### 5. Takım çalışmasına uygundur

Frontend tarafında çalışan biri View ile ilgilenirken, backend tarafında çalışan biri Controller ve Model tarafında çalışabilir.

---

#### 4.1.7. MVC’nin Dezavantajları

#### 1. Küçük projelerde fazla yapı gibi görünebilir

Çok basit projelerde MVC kullanmak başlangıçta gereksiz dosya ve klasör kalabalığı gibi hissedilebilir.

#### 2. Controller şişebilir

Eğer dikkat edilmezse Controller içine çok fazla iş mantığı yazılır. Buna “Fat Controller” denir. Fat Controller kötü bir durumdur çünkü Controller sadece yönlendirme yapması gerekirken tüm iş mantığını taşımaya başlar. Örneğin şu işler Controller içine yığılırsa yapı bozulur:

* Validasyonlar
* Hesaplamalar
* Veritabanı işlemleri
* Mail gönderme
* Yetki kontrolü
* Rapor hesaplama

Bu yüzden büyük projelerde MVC genellikle service ve repository katmanlarıyla desteklenir.

---

### 4.2. MVVM Nedir?

MVVM, “Model - View - ViewModel” kelimelerinin kısaltmasıdır. Özellikle modern frontend, mobil ve masaüstü uygulamalarda sık kullanılır. MVVM şu üç bölümden oluşur:

```text
Model
View
ViewModel
```

---

#### 4.2.1. Model

MVVM’de Model yine veriyi ve iş kurallarını temsil eder. Örneğin:

```text
User
Product
Order
Task
Message
```

gibi veri yapıları Model olabilir.

---

#### 4.2.2. View

View, kullanıcının gördüğü arayüzdür. Flutter, Android, WPF, Vue, Angular gibi yapılarda View, ekran tasarımını temsil eder. Örneğin:

* LoginScreen
* ProductListPage
* ProfileView
* CartPage

View katmanı kullanıcıyla etkileşime girer.

---

#### 4.2.3. ViewModel

ViewModel, View ile Model arasında bağlantı kuran yapıdır. ViewModel’in görevi:

* View için gerekli verileri hazırlamak,
* Kullanıcıdan gelen aksiyonları yönetmek,
* API veya repository katmanından veri almak,
* State’i yönetmek,
* View’a gösterilecek durumu hazırlamak.

ViewModel doğrudan arayüz çizmez. Ama arayüzün hangi veriyi göstereceğini belirler.

---

#### 4.2.4. MVVM Akışı

MVVM’de genel akış şu şekildedir:

```text
View → ViewModel → Model
Model → ViewModel → View
```

Örneğin kullanıcı giriş ekranında e-posta ve şifre girer.

```text
1. Kullanıcı View üzerinde giriş bilgilerini yazar.
2. View, bu bilgileri ViewModel’e gönderir.
3. ViewModel giriş işlemini başlatır.
4. ViewModel gerekli veriyi Model/Repository/API üzerinden kontrol eder.
5. Sonuç ViewModel’de state olarak güncellenir.
6. View bu state’e göre kendini yeniler.
```

---

#### 4.2.5. MVVM Örneği

Bir görev takip uygulaması düşünelim.

### Model

```text
Task
- id
- title
- isCompleted
```

### View

```text
TaskListPage
```

### ViewModel

```text
TaskViewModel
- tasks
- isLoading
- errorMessage
- getTasks()
- addTask()
- deleteTask()
- completeTask()
```

Burada View sadece ekranda görevleri gösterir. ViewModel ise görevleri alma, ekleme, silme ve durum yönetme işlemlerini yapar.

---

#### 4.2.6. MVVM’nin Avantajları

#### 1. UI ve iş mantığı ayrılır

View sadece görünümle ilgilenir. ViewModel ise verinin ve durumun yönetimini sağlar.

#### 2. Test yazmak kolaylaşır

ViewModel, View’dan bağımsız test edilebilir. Bu da özellikle mobil ve frontend projelerde büyük avantajdır.

#### 3. State yönetimi daha düzenli yapılır

ViewModel, ekranın durumunu tuttuğu için arayüzün hangi durumda ne göstereceği daha net olur. Örneğin:

```text
isLoading = true  → Yükleniyor göstergesi göster
errorMessage != null → Hata mesajı göster
data != null → Veriyi göster
```

#### 4. Büyük UI projelerinde düzen sağlar

Birden fazla ekran, form, liste ve API isteği olan uygulamalarda ViewModel kullanmak kodun dağılmasını engeller.

---

#### 4.2.7. MVVM’nin Dezavantajları

#### 1. Basit projelerde fazla gelebilir

Küçük bir uygulamada ViewModel yazmak başlangıçta gereksiz gibi görünebilir.

#### 2. ViewModel şişebilir

Tıpkı Controller gibi ViewModel de fazla sorumluluk alırsa karmaşıklaşır. Her şeyi ViewModel içine yazmak doğru değildir.

#### 3. State yönetimi yanlış yapılırsa karmaşa artar

MVVM genellikle state management ile birlikte kullanılır. State yönetimi doğru yapılmazsa View ve ViewModel ilişkisi karışabilir.

---

### 4.3. MVC ve MVVM Farkı

MVC ve MVVM birbirine benzer görünse de kullanım alanları ve mantıkları farklıdır.

| Özellik              | MVC                                     | MVVM                                    |
| -------------------- | --------------------------------------- | --------------------------------------- |
| Açılım               | Model - View - Controller               | Model - View - ViewModel                |
| Aracı Katman         | Controller                              | ViewModel                               |
| Sık Kullanıldığı Yer | Web backend, klasik web uygulamaları    | Mobil, frontend, modern UI uygulamaları |
| View ile İlişki      | Controller View’a veri gönderir         | View, ViewModel’deki state’i takip eder |
| State Yönetimi       | Genellikle Controller/Service tarafında | ViewModel üzerinde daha belirgindir     |
| Test Edilebilirlik   | İyi yapılandırılırsa kolaydır           | ViewModel sayesinde oldukça uygundur    |
| Risk                 | Controller şişebilir                    | ViewModel şişebilir                     |

Basitçe:

* MVC’de Controller istekleri yönetir.
* MVVM’de ViewModel ekranın verisini ve durumunu yönetir.

---

### 4.4. MVP Mimarisi

MVP, “Model - View - Presenter” kelimelerinin kısaltmasıdır. MVC’ye benzeyen bir mimari desendir ancak burada Controller yerine Presenter bulunur.

MVP mimarisinde View daha pasif bir yapıdadır. Kullanıcıdan gelen olayları Presenter’a iletir. Presenter ise Model ile iletişim kurar, verileri işler ve sonucu tekrar View’a gönderir. MVP’nin bileşenleri şunlardır:

#### Model

Veri ve iş mantığını temsil eder. Uygulamanın temel veri yapısı burada bulunur.

#### View

Kullanıcı arayüzüdür. Ancak MVP’de View genellikle daha pasiftir. Kendi başına iş mantığı yürütmez, Presenter’dan gelen verileri gösterir.

#### Presenter

* View ile Model arasında köprü görevi görür. Kullanıcı işlemlerini yönetir, Model’den veri alır ve View’a ne göstereceğini belirler.
* MVP özellikle test edilebilirliği artırmak için tercih edilir. Çünkü Presenter, View’dan ayrıldığı için bağımsız olarak test edilebilir.

MVP’nin avantajları şunlardır:

* View ile iş mantığını ayırır.
* Test edilebilirliği artırır.
* Kullanıcı arayüzünün daha sade kalmasını sağlar.
* Büyük arayüz projelerinde düzen sağlar.

MVP’nin dezavantajları ise şunlardır:

* Presenter sınıfları zamanla büyüyebilir.
* Fazladan kod yazmayı gerektirebilir.
* Küçük projeler için fazla detaylı olabilir.

### 4.5. Layered Architecture

Layered Architecture, yani Katmanlı Mimari, yazılımın farklı sorumluluklara sahip katmanlara ayrılması mantığına dayanır. Bu mimaride her katmanın belirli bir görevi vardır ve katmanlar genellikle yukarıdan aşağıya doğru iletişim kurar. En yaygın katmanlar şunlardır:

#### Presentation Layer

Kullanıcıya görünen arayüz katmanıdır. Web sayfaları, mobil ekranlar veya masaüstü arayüzleri bu katmanda yer alır.

#### Business Layer

İş kurallarının bulunduğu katmandır. Uygulamanın temel karar mekanizmaları burada yer alır. Örneğin bir banka uygulamasında para transferi yapılırken bakiye kontrolü, limit kontrolü ve işlem doğrulama gibi kurallar Business Layer’da bulunabilir.

#### Data Access Layer

Veritabanı işlemlerinin yapıldığı katmandır. Veri ekleme, silme, güncelleme ve listeleme işlemleri bu katmanda gerçekleştirilir.

#### Database Layer

Verilerin fiziksel olarak saklandığı katmandır. SQL veya NoSQL veritabanları bu katmanda yer alır. 

Katmanlı mimarinin temel amacı, uygulamadaki farklı sorumlulukları birbirinden ayırmaktır. Böylece bir katmanda yapılan değişiklik diğer katmanları minimum düzeyde etkiler.

Layered Architecture’ın avantajları şunlardır:

* Anlaşılması kolaydır.
* Kurumsal uygulamalarda yaygın kullanılır.
* Sorumluluk ayrımı sağlar.
* Bakım ve geliştirme süreçlerini kolaylaştırır.
* Ekip çalışmasına uygundur.

Dezavantajları ise şunlardır:

* Katmanlar arasında fazla bağımlılık oluşabilir.
* Gereksiz katman kullanımı performansı etkileyebilir.
* Çok basit projelerde fazla yapılandırma oluşturabilir.

### 4.6. Clean Architecture

Clean Architecture, yazılımın bağımlılıklarını daha kontrollü hale getirmeyi amaçlayan modern bir mimari yaklaşımdır. Bu mimaride temel hedef, iş kurallarını dış teknolojilerden bağımsız tutmaktır. 

Clean Architecture’a göre uygulamanın merkezinde iş kuralları bulunur. Veritabanı, framework, kullanıcı arayüzü veya dış servisler ise dış katmanlarda yer alır. Böylece uygulamanın temel mantığı, kullanılan teknolojiye bağımlı hale gelmez.

Clean Architecture genel olarak şu yapılardan oluşur:

#### Entities

Uygulamanın en temel iş nesneleridir. Sistemin ana kurallarını temsil eder.

#### Use Cases

Uygulamanın gerçekleştirdiği iş senaryolarıdır. Örneğin “kullanıcı kaydı oluşturma”, “sipariş verme” veya “ödeme alma” birer use case olabilir.

#### Interface Adapters

Dış dünyadan gelen verileri uygulamanın iç yapısına uygun hale getirir. Controller, presenter veya gateway gibi yapılar bu katmanda yer alabilir.

#### Frameworks and Drivers

Veritabanı, web framework, mobil framework veya dış API gibi teknolojiler bu katmanda bulunur.

Clean Architecture’ın avantajları şunlardır:

* İş kurallarını dış teknolojilerden bağımsız tutar.
* Test edilebilirliği artırır.
* Büyük ve uzun ömürlü projeler için uygundur.
* Framework değişikliklerinden daha az etkilenir.
* Bakımı ve geliştirilmesi daha kontrollüdür.

Dezavantajları ise şunlardır:

* Öğrenmesi ve uygulaması başlangıçta zordur.
* Küçük projeler için fazla karmaşık olabilir.
* Daha fazla dosya, sınıf ve yapı gerektirebilir.
* Yanlış uygulanırsa gereksiz soyutlama oluşturabilir.

### 4.7. Repository Pattern

Repository Pattern, veri erişim işlemlerini uygulamanın diğer bölümlerinden ayırmak için kullanılan bir tasarım yaklaşımıdır. Genellikle mimari desenlerle birlikte kullanılır. Bu desende uygulama doğrudan veritabanı sorguları ile uğraşmaz. Bunun yerine veri işlemleri Repository adı verilen sınıflar üzerinden yapılır. Örneğin bir kullanıcı sistemi için UserRepository adında bir yapı olabilir. Bu yapı kullanıcı ekleme, kullanıcı silme, kullanıcı güncelleme ve kullanıcı listeleme işlemlerini yönetir. 

Repository Pattern’in avantajları şunlardır:

* Veri erişim kodlarını tek yerde toplar.
* Kod tekrarını azaltır.
* Test yazmayı kolaylaştırır.
* Veritabanı değişikliklerinde uygulamanın diğer kısımlarını daha az etkiler.
* Service katmanı ile birlikte kullanıldığında düzenli bir yapı sağlar.

Dezavantajları ise şunlardır:

* Basit projelerde gereksiz soyutlama oluşturabilir.
* Çok fazla repository sınıfı oluşabilir.
* Yanlış kullanılırsa sadece veritabanı işlemlerini tekrar eden gereksiz sınıflara dönüşebilir.

### 4.8. Service-Oriented Architecture

Service-Oriented Architecture, yani Servis Odaklı Mimari, uygulamanın farklı işlevlerinin servisler şeklinde tasarlanmasına dayanır. Bu mimaride her servis belirli bir işlevi yerine getirir ve diğer servislerle iletişim kurabilir. Örneğin büyük bir e-ticaret sisteminde kullanıcı servisi, ödeme servisi, ürün servisi ve kargo servisi ayrı yapılar olarak tasarlanabilir. SOA’nın temel amacı, sistemdeki işlevleri bağımsız servisler haline getirerek yeniden kullanılabilirliği ve esnekliği artırmaktır.

SOA’nın avantajları şunlardır:

* Servislerin yeniden kullanılmasını sağlar.
* Büyük sistemlerde modülerlik sunar.
* Farklı teknolojilerle geliştirilen sistemlerin birlikte çalışmasını kolaylaştırır.
* Kurumsal sistemlerde entegrasyonu destekler.

Dezavantajları ise şunlardır:

* Servisler arası iletişim karmaşıklaşabilir.
* Ağ bağlantısına bağımlılık artar.
* İzleme, güvenlik ve hata yönetimi daha dikkatli yapılmalıdır.
* Küçük projeler için ağır bir yapı olabilir.

### 4.9. Microservices Architecture

Microservices Architecture, yani Mikroservis Mimarisi, uygulamanın küçük, bağımsız ve ayrı ayrı geliştirilebilen servislerden oluşmasını sağlayan bir mimari yaklaşımdır. Mikroservis mimarisinde her servis kendi sorumluluğuna sahiptir. Servisler birbirinden bağımsız olarak geliştirilebilir, test edilebilir, dağıtılabilir ve ölçeklendirilebilir. 

Örneğin bir yemek sipariş uygulamasında şu servisler ayrı ayrı bulunabilir:

* Kullanıcı servisi
* Restoran servisi
* Sipariş servisi
* Ödeme servisi
* Bildirim servisi
* Kurye takip servisi

Her servis kendi görevinden sorumludur. Örneğin ödeme servisi sadece ödeme işlemleriyle ilgilenirken, bildirim servisi kullanıcıya SMS veya e-posta gönderme görevini üstlenir. 

Mikroservis mimarisinin avantajları şunlardır:

* Servisler bağımsız geliştirilebilir.
* Büyük ekiplerde iş bölümü kolaylaşır.
* Her servis ihtiyaca göre ayrı ölçeklendirilebilir.
* Bir servisteki hata tüm sistemi doğrudan çökertmeyebilir.
* Farklı servislerde farklı teknolojiler kullanılabilir.

Dezavantajları ise şunlardır:

* Yönetimi monolitik yapılara göre daha zordur.
* Servisler arası iletişim karmaşık olabilir.
* Dağıtık sistem problemleri ortaya çıkabilir.
* Loglama, izleme, güvenlik ve hata yönetimi daha zor hale gelir.
* Küçük projeler için gereğinden fazla karmaşık olabilir.

### 4.10. Mimari Desenlerin Yazılım Geliştirmedeki Önemi

Mimari desenler, yazılım projelerinde düzenli ve sürdürülebilir bir yapı oluşturmak için büyük önem taşır. Özellikle proje büyüdükçe kodların plansız şekilde yazılması ciddi sorunlara yol açabilir. Mimari desenlerin yazılım geliştirmeye sağladığı katkılar şunlardır:

* Kodun daha okunabilir olmasını sağlar.
* Bakım ve geliştirme süreçlerini kolaylaştırır.
* Ekip üyeleri arasında görev paylaşımını destekler.
* Test yazmayı kolaylaştırır.
* Kod tekrarını azaltır.
* Hataların daha kolay bulunmasını sağlar.
* Projenin uzun vadede sürdürülebilir olmasına katkı sağlar.
* Yeni özellik eklemeyi daha kontrollü hale getirir.

Doğru mimari desen seçimi, projenin türüne, büyüklüğüne, ekip yapısına ve uzun vadeli hedeflerine göre yapılmalıdır. Her mimari desen her proje için uygun değildir. Örneğin küçük bir öğrenci projesinde Clean Architecture veya Microservices fazla karmaşık olabilirken, büyük ve uzun süre geliştirilecek kurumsal projelerde bu yapılar oldukça faydalı olabilir.

Bu nedenle mimari desenleri bilmek, bir yazılım geliştiricinin sadece kod yazmasını değil, aynı zamanda daha düzenli, ölçeklenebilir ve profesyonel sistemler tasarlamasını sağlar.

---

## 5. State Management Nedir?

State management, özellikle frontend ve mobil uygulamalarda çok önemli bir konudur. State, uygulamanın o anki durumudur. Bir uygulamada kullanıcıya gösterilen her şey aslında bir state’e bağlıdır. Örneğin:

* Kullanıcı giriş yaptı mı?
* Sepette kaç ürün var?
* Ürün listesi yüklendi mi?
* API’den veri geliyor mu?
* Hata oluştu mu?
* Tema açık mod mu koyu mod mu?
* Form alanlarına ne yazıldı?
* Seçili kategori hangisi?
* Kullanıcının favorileri neler?
* Bildirim sayısı kaç?

Bunların hepsi state örneğidir.

---

### 5.1. State’e Basit Örnek

Bir sayaç uygulaması düşünelim. Ekranda şöyle yazıyor:

```text
Sayaç: 0
```

Kullanıcı butona bastığında:

```text
Sayaç: 1
```

Buradaki sayı uygulamanın state’idir. State değiştiğinde ekran da değişir.

---

### 5.2. State Management Neden Gereklidir?

Küçük bir uygulamada state’i yönetmek kolaydır. Ama uygulama büyüdükçe state birçok farklı yerde kullanılmaya başlar. Örneğin bir e-ticaret uygulamasında sepet bilgisi:

* Ürün detay sayfasında,
* Sepet sayfasında,
* Header kısmındaki sepet ikonunda,
* Ödeme sayfasında,
* Sipariş özeti ekranında

kullanılabilir. Eğer bu bilgi her yerde ayrı ayrı tutulursa ciddi sorunlar oluşur. Mesela:

* Header’da sepet 3 ürün gösterir.
* Sepet sayfasında 2 ürün görünür.
* Ödeme ekranında toplam fiyat yanlış olur.

Bu yüzden state’in merkezi ve kontrollü yönetilmesi gerekir.

---

### 5.3. Local State Nedir?

Local state, sadece belirli bir bileşeni veya ekranı ilgilendiren durumdur. Örneğin:

* Bir form alanının içeriği,
* Bir dropdown menünün açık/kapalı olması,
* Bir modal penceresinin görünür olup olmaması,
* Bir butonun aktif/pasif durumu

local state olabilir. Bu state sadece ilgili ekranda kullanılıyorsa global hale getirmeye gerek yoktur.

---

### 5.4. Global State Nedir?

Global state, uygulamanın birçok yerinde kullanılan ortak durumdur. Örneğin:

* Giriş yapmış kullanıcı bilgisi,
* Kullanıcı token bilgisi,
* Sepet bilgisi,
* Tema tercihi,
* Dil seçimi,
* Bildirim sayısı

global state olabilir. Global state merkezi bir yerde tutulur ve ihtiyaç duyan bölümler buradan okur.

---

### 5.5. Server State Nedir?

Server state, sunucudan/API’den gelen veridir. Örneğin:

* Ürün listesi,
* Kullanıcı profili,
* Sipariş geçmişi,
* Blog yazıları,
* Bildirimler

server state olabilir. Bu state’in yönetiminde genellikle şu konular önemlidir:

* Veri yükleniyor mu?
* Veri geldi mi?
* Hata oluştu mu?
* Veri tekrar çekilmeli mi?
* Cache kullanılacak mı?

---

### 5.6. UI State Nedir?

UI state, arayüzün görünüm durumudur. Örneğin:

* Loading göstergesi açık mı?
* Hata mesajı gösterilecek mi?
* Sekme seçili mi?
* Modal açık mı?
* Menü açık mı?
* Sayfa boş durumda mı?

UI state doğrudan kullanıcının gördüğü ekranla ilgilidir.

---

### 5.7. State Management Araçları

Farklı teknolojilerde farklı state management çözümleri kullanılır.

#### React tarafında

* useState
* useReducer
* Context API
* Redux
* Zustand
* MobX
* React Query

#### Flutter tarafında

* setState
* Provider
* Riverpod
* Bloc/Cubit
* GetX
* MobX

#### Vue tarafında

* ref/reactive
* Vuex
* Pinia

#### Angular tarafında

* Services
* RxJS
* NgRx

Ama önemli olan araç ismi değil, mantıktır. State management’ın temel amacı şudur:

> Uygulamanın durumunu kontrollü, tutarlı ve yönetilebilir şekilde saklamak ve güncellemek.

---

### 5.8. State Management Olmazsa Ne Olur?

State yönetimi düzgün yapılmazsa:

* Ekranlar tutarsız veri gösterebilir.
* Aynı veri farklı yerlerde farklı görünebilir.
* Gereksiz API istekleri atılabilir.
* Kod tekrarı artar.
* Debug yapmak zorlaşır.
* Kullanıcı deneyimi bozulur.
* Büyük projelerde kod kontrol edilemez hale gelir.

Özellikle frontend ve mobil projelerde state management, mimarinin en kritik parçalarından biridir.

---

## 6. Katmanlı Mimari Nedir?

Katmanlı mimari, yazılımı farklı sorumluluklara sahip katmanlara ayıran mimari yaklaşımdır. En yaygın kullanılan yapılardan biri şudur:

```text
Controller
Service
Repository
Database
```

Bazı projelerde buna ek olarak DTO, Entity, Mapper, ViewModel gibi yapılar da bulunabilir.

---

### 6.1. Katmanlı Mimariye Neden İhtiyaç Duyulur?

Bir uygulamada genellikle şu işlemler yapılır:

* Kullanıcıdan istek alınır.
* İstek kontrol edilir.
* İş kuralları uygulanır.
* Veritabanından veri alınır veya veri kaydedilir.
* Sonuç kullanıcıya döndürülür.

Eğer bunların hepsi aynı dosyada yapılırsa kod karmaşıklaşır. Katmanlı mimari bu işlemleri farklı bölümlere ayırır. Her katmanın görevi bellidir.

---

### 6.2. Controller Katmanı

Controller, dış dünyadan gelen istekleri karşılayan katmandır. Web API örneğinde kullanıcı veya frontend uygulaması bir endpoint’e istek atar. Bu isteği ilk karşılayan yer Controller’dır. Controller’ın görevi:

* HTTP isteğini almak,
* Parametreleri okumak,
* Gerekli service metodunu çağırmak,
* Service’ten gelen sonucu kullanıcıya döndürmek.

Controller mümkün olduğunca ince olmalıdır. Yani Controller içine çok fazla iş mantığı yazmak doğru değildir.

---

#### 6.2.1. Controller Ne Yapmalı?

Controller şunları yapabilir:

* Request almak,
* Route yönetmek,
* Parametreleri almak,
* Service çağırmak,
* Response döndürmek.

Örneğin:

```text
GET /products
POST /products
DELETE /products/{id}
PUT /products/{id}
```

Bu endpointleri Controller karşılar.

---

#### 6.2.2. Controller Ne Yapmamalı?

Controller şunları yapmamalıdır:

* Karmaşık iş kuralları yazmamalı,
* SQL sorguları içermemeli,
* Veritabanına doğrudan erişmemeli,
* Mail gönderme gibi detaylarla dolmamalı,
* Büyük hesaplamaları kendi içinde yapmamalı.

Çünkü bunlar Controller’ı şişirir ve kodun bakımını zorlaştırır.

---

### 6.3. Service Katmanı

Service katmanı, uygulamanın iş mantığını barındıran katmandır. Yani sistemin “ne yapması gerektiği” burada belirlenir. Örneğin bir e-ticaret uygulamasında:

* Ürün stokta mı?
* Kullanıcı sipariş verebilir mi?
* İndirim uygulanacak mı?
* Sipariş toplam tutarı nasıl hesaplanacak?
* Ödeme başarılıysa sipariş durumu ne olacak?
* Kullanıcı yetkili mi?

gibi kurallar service katmanında yer alır.

---

#### 6.3.1. Service Katmanı Ne İşe Yarar?

Service katmanı:

* İş kurallarını yönetir.
* Controller ile Repository arasında köprü olur.
* Birden fazla repository’den veri alabilir.
* Validasyon işlemleri yapabilir.
* İşlem sonucunu Controller’a döndürür.

Örneğin:

```text
OrderService
- createOrder()
- cancelOrder()
- calculateTotalPrice()
- checkStock()
```

Bu metotlar siparişle ilgili iş kurallarını içerir.

---

#### 6.3.2. Service Katmanına Örnek

Bir sipariş oluşturma işlemini düşünelim. Sipariş oluştururken yapılması gerekenler:

1. Kullanıcı var mı kontrol edilir.
2. Sepette ürün var mı kontrol edilir.
3. Ürünlerin stok durumu kontrol edilir.
4. Toplam fiyat hesaplanır.
5. Sipariş oluşturulur.
6. Stok azaltılır.
7. Ödeme başlatılır.
8. Kullanıcıya sonuç döndürülür.

Bunların tamamını Controller’a yazmak yanlış olur. Bu işlem Service katmanında yönetilmelidir.

---

### 6.4. Repository Katmanı

Repository katmanı, veritabanı işlemlerinden sorumlu katmandır. Repository’nin görevi:

* Veritabanından veri almak,
* Veri kaydetmek,
* Veri güncellemek,
* Veri silmek,
* Sorguları yönetmek.

Repository, uygulama ile veritabanı arasında soyutlama sağlar.

---

#### 6.4.1. Repository Neden Kullanılır?

Repository kullanılmazsa Service veya Controller doğrudan veritabanıyla konuşmak zorunda kalır. Bu da kodun bağımlılığını artırır. Repository sayesinde veritabanı işlemleri tek bir yerde toplanır.

Örneğin:

```text
ProductRepository
- findAll()
- findById()
- save()
- delete()
- findByCategory()
```

Service katmanı bu metotları çağırır ama SQL detaylarını bilmez.

---

#### 6.4.2. Repository Katmanının Avantajları

#### 1. Veritabanı işlemleri düzenli olur

Sorgular ve veri erişimi tek yerde toplanır.

#### 2. Service katmanı sade kalır

Service iş kurallarına odaklanır, veritabanı detaylarıyla uğraşmaz.

#### 3. Test yazmak kolaylaşır

Repository mock’lanarak Service test edilebilir.

#### 4. Veritabanı değişikliği daha kolay olur

İleride veritabanı teknolojisi değişirse sadece repository katmanı etkilenir.

---

### 6.5. Entity, DTO ve Mapper Kavramları

Katmanlı mimaride sık duyulan bazı ek kavramlar da vardır.

---

#### 6.5.1. Entity Nedir?

Entity, veritabanındaki tabloyu temsil eden nesnedir. Örneğin veritabanında Product tablosu varsa uygulamada Product entity’si olabilir.

```text
Product
- id
- name
- price
- stock
```

Entity genellikle veritabanı yapısına yakındır.

---

#### 6.5.2. DTO Nedir?

DTO, “Data Transfer Object” kelimelerinin kısaltmasıdır. DTO, katmanlar arasında veya API üzerinden veri taşımak için kullanılan nesnedir. Entity ile DTO aynı olmak zorunda değildir. Örneğin User entity’sinde şu alanlar olabilir:

```text
User
- id
- name
- email
- password
- createdDate
```

Ama kullanıcıya API cevabı olarak password göndermek çok yanlış olur. Bu yüzden UserResponseDTO şöyle olabilir:

```text
UserResponseDTO
- id
- name
- email
```

Yani DTO, dışarıya hangi verinin gösterileceğini kontrol etmek için kullanılır.

---

#### 6.5.3. DTO Neden Önemlidir?

DTO kullanmak şu avantajları sağlar:

* Hassas bilgiler dışarı verilmez.
* API response yapısı kontrol altında olur.
* Entity doğrudan dış dünyaya açılmaz.
* Frontend’in ihtiyacına uygun veri döndürülür.
* Güvenlik artar.
* Kod daha düzenli olur.

---

#### 6.5.4. Mapper Nedir?

Mapper, Entity ile DTO arasında dönüşüm yapan yapıdır. Örneğin:

```text
Product Entity → ProductResponseDTO
ProductCreateDTO → Product Entity
```

Mapper sayesinde dönüşüm işlemleri tek yerde toplanır.

---

### 6.6. Katmanlı Mimari Akışı

Bir kullanıcı ürünleri listelemek istediğinde akış şöyle olabilir:

```text
Frontend / Kullanıcı
        ↓
Controller
        ↓
Service
        ↓
Repository
        ↓
Database
        ↓
Repository
        ↓
Service
        ↓
Controller
        ↓
Frontend / Kullanıcı
```

Bu akışta:

* Controller isteği alır.
* Service iş mantığını yürütür.
* Repository veritabanından veriyi alır.
* Database veriyi döndürür.
* Repository sonucu Service’e iletir.
* Service gerekirse işlem yapar.
* Controller sonucu kullanıcıya döndürür.

---

### 6.7. Katmanlı Mimari Örneği

Bir ürün listeleme işlemi düşünelim.

#### Controller

```text
ProductController
- getAllProducts()
```

Görevi:

* Kullanıcıdan gelen ürün listeleme isteğini almak,
* ProductService’i çağırmak,
* Gelen sonucu response olarak döndürmek.

#### Service

```text
ProductService
- getAllProducts()
```

Görevi:

* Ürünleri getirme iş mantığını yönetmek,
* Gerekirse stokta olan ürünleri filtrelemek,
* Repository’den veri almak,
* DTO’ya dönüştürmek.

#### Repository

```text
ProductRepository
- findAll()
```

Görevi:

* Veritabanından ürün kayıtlarını çekmek.

#### Database

```text
products table
```

Görevi:

* Ürün verilerini saklamak.

---

### 6.8. Katmanlı Mimari Kullanmanın Avantajları

#### 1. Kod düzenli olur

Her katmanın görevi net olduğu için kodlar daha okunabilir hale gelir.

#### 2. Bakım kolaylaşır

Bir hata olduğunda hangi katmana bakılacağı daha kolay anlaşılır.

#### 3. Test yazmak kolaylaşır

Service, Controller ve Repository ayrı ayrı test edilebilir.

#### 4. Kod tekrarını azaltır

Ortak işlemler ilgili katmanda toplanır.

#### 5. Büyük projelerde sürdürülebilirlik sağlar

Proje büyüdüğünde kodun dağılmasını engeller.

#### 6. Takım çalışmasını kolaylaştırır

Farklı geliştiriciler farklı katmanlar üzerinde çalışabilir.

#### 7. Değişikliklerin etkisi azalır

Bir katmandaki değişiklik diğer katmanları minimum etkiler.

---

### 6.9. Katmanlı Mimari Kullanırken Yapılan Hatalar

#### 6.9.1. Controller’a Çok Fazla Kod Yazmak

En yaygın hata Controller içine çok fazla iş mantığı yazmaktır.

Yanlış yaklaşım:

```text
Controller:
- request alır
- validasyon yapar
- stok kontrol eder
- fiyat hesaplar
- veritabanına gider
- mail gönderir
- response döndürür
```

Bu kötü bir yapıdır.

Doğru yaklaşım:

```text
Controller:
- request alır
- service çağırır
- response döndürür
```

---

#### 6.9.2. Service Katmanını Gereksiz Boş Bırakmak

Bazen geliştiriciler Service katmanı açar ama hiçbir iş mantığı koymadan sadece Repository metodunu çağırır. Bu küçük projelerde normal olabilir ama büyük projelerde Service katmanı iş kurallarının merkezi olmalıdır.

---

#### 6.9.3. Repository İçine İş Mantığı Yazmak

Repository sadece veri erişimiyle ilgilenmelidir. Örneğin “kullanıcı indirim hakkına sahip mi?” gibi bir kural Repository’de olmamalıdır. Bu Service katmanının işidir.

---

#### 6.9.4. Entity’yi Doğrudan API Cevabı Olarak Döndürmek

Entity doğrudan dışarı açılırsa güvenlik ve bağımlılık sorunları oluşabilir. Örneğin kullanıcı entity’sinde password alanı varsa ve bu doğrudan API response olarak dönerse ciddi güvenlik açığı oluşur. Bu yüzden DTO kullanmak daha doğrudur.

---

## 7. Clean Code ve Mimari İlişkisi

Yazılım mimarisi ile temiz kod birbirini tamamlar. İyi mimari kötü kodu tamamen kurtaramaz. Aynı şekilde temiz yazılmış ama mimarisiz bir proje de büyüdükçe zor yönetilir. İyi bir mimaride:

* Her sınıfın görevi bellidir.
* Her fonksiyon tek bir işe odaklanır.
* Bağımlılıklar kontrol altındadır.
* Kod tekrarından kaçınılır.
* İsimlendirme anlaşılırdır.
* Katmanlar birbirinin görevini çalmaz.

Mesela ProductService sadece ürün iş kurallarıyla ilgilenmelidir. UserService içinde ürün işlemleri yapmak doğru değildir.

---

## 8. Yazılım Mimarisinin Proje Geliştirmeye Katkısı

Yazılım mimarisi öğrenmek, geliştiricinin sadece kod yazmasını değil, sistemi bütün olarak düşünmesini sağlar. Bir geliştirici mimari bilgisi kazandığında şu konularda daha bilinçli olur:

* Projeyi klasörlere nasıl ayıracağını bilir.
* Hangi kodun nereye yazılacağını bilir.
* API yapısını daha düzenli kurar.
* Frontend ve backend ayrımını daha iyi anlar.
* Takım projelerinde daha rahat çalışır.
* Test edilebilir kod yazmaya başlar.
* Büyük projelerde neden belirli desenlerin kullanıldığını kavrar.
* Framework’lerin arkasındaki mantığı daha iyi anlar.

Özellikle orta ve ileri seviye projelerde mimari bilmek çok önemlidir. Çünkü büyük projelerde asıl zorluk sadece kod yazmak değil, kodu yönetilebilir tutmaktır.

---

## 9. Basit Bir Proje Üzerinden Genel Mimari Örnek

Bir “Görev Yönetim Sistemi” düşünelim.

Kullanıcı:

* Görev ekleyebiliyor.
* Görevleri listeleyebiliyor.
* Görev tamamlayabiliyor.
* Görev silebiliyor.

Bu sistem katmanlı olarak şöyle tasarlanabilir:

```text
TaskController
TaskService
TaskRepository
TaskEntity
TaskDTO
Database
```

Akış:

```text
Kullanıcı görev ekler.
        ↓
TaskController isteği alır.
        ↓
TaskService görev başlığını kontrol eder.
        ↓
TaskRepository veritabanına kaydeder.
        ↓
Database görevi saklar.
        ↓
Sonuç kullanıcıya döner.
```

Burada her katman kendi görevini yapar.

* Controller: İsteği alır.
* Service: İş kuralını uygular.
* Repository: Veritabanına kaydeder.
* Database: Veriyi saklar.
* DTO: Veriyi taşır.
* Entity: Veritabanı nesnesini temsil eder.

Bu yapı küçük görünse bile proje büyüdüğünde büyük kolaylık sağlar.

---

## 10. Bu Konunun Kazandırdığı Yetkinlik

Yazılım mimarisi temellerini öğrenmek, geliştiriciye şu becerileri kazandırır:

* Orta ve ileri seviye projelerin genel yapısını anlama,
* Kodları daha düzenli organize etme,
* Projelerde sürdürülebilir yapı kurma,
* MVC ve MVVM gibi mimari desenleri kavrama,
* Frontend ve backend mimarisini daha iyi yorumlama,
* State management mantığını anlama,
* Katmanlı mimari ile profesyonel proje geliştirme,
* Monolith ve microservice farkını bilerek doğru sistem tasarımı yapma,
* Takım projelerinde daha bilinçli çalışma,
* Framework’lerin neden belirli klasör ve yapı kullandığını anlama.

Bu yüzden yazılım mimarisi, sadece teorik bir konu değil; gerçek projelerde yazılım kalitesini doğrudan etkileyen temel bir beceridir.

---

## 11. Kısa Özet

* Yazılım mimarisi, bir uygulamanın temel yapısını belirleyen yaklaşımdır. Kodun düzenli, sürdürülebilir, test edilebilir ve geliştirilebilir olmasını sağlar. 
* Monolith mimaride uygulama tek parça halinde geliştirilir. Küçük ve orta ölçekli projeler için uygundur, fakat büyüdükçe yönetimi zorlaşabilir.
* Microservice mimaride uygulama küçük, bağımsız servislerden oluşur. Büyük ve karmaşık sistemlerde avantaj sağlar, fakat yönetimi ve altyapısı daha zordur.
* MVC mimarisi uygulamayı Model, View ve Controller olarak ayırır. Özellikle web uygulamalarında sık kullanılır.
* MVVM mimarisi Model, View ve ViewModel yapısından oluşur. Özellikle mobil ve modern frontend projelerde kullanılır.
* State management, uygulamanın durumunu kontrollü şekilde yönetme sürecidir. Kullanıcı bilgisi, sepet, tema, loading durumu ve API verileri state örnekleridir.
* Katmanlı mimari ise Controller, Service, Repository ve Database gibi katmanlarla kodu sorumluluklarına göre ayırır. Bu yapı büyük projelerde okunabilirlik, sürdürülebilirlik ve test edilebilirlik sağlar.
* Bu konuyu öğrendiğinde artık projelerde sadece “kod çalışıyor mu?” diye değil, “bu kod ileride büyüyünce yönetilebilir mi?” diye düşünmeye başlarsın. Asıl seviye atlama da tam burada başlıyor.