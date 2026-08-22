# 15) Logging, Monitoring & Debugging

## İçindekiler

- [1. Giriş](#1-giriş)
- [2. Logging Nedir?](#2-logging-nedir)
  - [2.1. Neden Log Tutulur?](#21-neden-log-tutulur)
  - [2.2. İyi Bir Log Kaydı Nasıl Olmalıdır?](#22-iyi-bir-log-kaydı-nasıl-olmalıdır)
  - [2.3. Log Seviyeleri](#23-log-seviyeleri)
    - [TRACE](#trace)
    - [DEBUG](#debug)
    - [INFO](#info)
    - [WARN](#warn)
    - [ERROR](#error)
    - [FATAL / CRITICAL](#fatal--critical)
  - [2.4. Log Seviyeleri Karşılaştırma Tablosu](#24-log-seviyeleri-karşılaştırma-tablosu)
  - [2.5. Structured Logging](#25-structured-logging)
  - [2.6. Loglara Neler Yazılmalı?](#26-loglara-neler-yazılmalı)
  - [2.7. Loglara Neler Yazılmamalı?](#27-loglara-neler-yazılmamalı)
  - [2.8. Correlation ID ve Request ID](#28-correlation-id-ve-request-id)
  - [2.9. Log Rotation ve Retention](#29-log-rotation-ve-retention)
- [3. Exception Handling](#3-exception-handling)
  - [3.1. Exception Nedir?](#31-exception-nedir)
  - [3.2. Exception Handling Neden Gereklidir?](#32-exception-handling-neden-gereklidir)
  - [3.3. try-catch-finally Mantığı](#33-try-catch-finally-mantığı)
  - [3.4. Exception Türleri](#34-exception-türleri)
  - [3.5. Hataları Yutmak Neden Yanlıştır?](#35-hataları-yutmak-neden-yanlıştır)
  - [3.6. Global Exception Handling](#36-global-exception-handling)
  - [3.7. Custom Exception Kullanımı](#37-custom-exception-kullanımı)
  - [3.8. Kullanıcıya Gösterilen Hata ile Loglanan Hata Aynı Olmamalıdır](#38-kullanıcıya-gösterilen-hata-ile-loglanan-hata-aynı-olmamalıdır)
- [4. Debugging Nedir?](#4-debugging-nedir)
  - [4.1. Debugging Süreci](#41-debugging-süreci)
  - [4.2. Breakpoint Nedir?](#42-breakpoint-nedir)
  - [4.3. Step Over, Step Into ve Step Out](#43-step-over-step-into-ve-step-out)
  - [4.4. Watch ve Call Stack](#44-watch-ve-call-stack)
  - [4.5. Console Debugging](#45-console-debugging)
  - [4.6. Rubber Duck Debugging](#46-rubber-duck-debugging)
  - [4.7. Binary Search Debugging](#47-binary-search-debugging)
- [5. Monitoring Nedir?](#5-monitoring-nedir)
  - [5.1. Monitoring Neden Şarttır?](#51-monitoring-neden-şarttır)
  - [5.2. Monitoring ile Logging Arasındaki Fark](#52-monitoring-ile-logging-arasındaki-fark)
  - [5.3. Monitoring Türleri](#53-monitoring-türleri)
    - [Application Monitoring](#application-monitoring)
    - [Infrastructure Monitoring](#infrastructure-monitoring)
    - [Database Monitoring](#database-monitoring)
    - [Network Monitoring](#network-monitoring)
    - [User Experience Monitoring](#user-experience-monitoring)
  - [5.4. Temel Monitoring Metrikleri](#54-temel-monitoring-metrikleri)
  - [5.5. Golden Signals](#55-golden-signals)
- [6. Observability Nedir?](#6-observability-nedir)
  - [6.1. Logs](#61-logs)
  - [6.2. Metrics](#62-metrics)
  - [6.3. Traces](#63-traces)
  - [6.4. Logs, Metrics ve Traces Birlikte Nasıl Kullanılır?](#64-logs-metrics-ve-traces-birlikte-nasıl-kullanılır)
- [7. Alerting Nedir?](#7-alerting-nedir)
  - [7.1. İyi Bir Alarm Nasıl Olmalıdır?](#71-iyi-bir-alarm-nasıl-olmalıdır)
  - [7.2. Alert Fatigue](#72-alert-fatigue)
- [8. Production Ortamında Hata Çözme Süreci](#8-production-ortamında-hata-çözme-süreci)
  - [8.1. Incident Nedir?](#81-incident-nedir)
  - [8.2. Adım Adım Incident Çözüm Süreci](#82-adım-adım-incident-çözüm-süreci)
  - [8.3. Root Cause Analysis](#83-root-cause-analysis)
  - [8.4. 5 Whys Tekniği](#84-5-whys-tekniği)
  - [8.5. Postmortem Nedir?](#85-postmortem-nedir)
- [9. Uygulama Katmanlarında Logging Örnekleri](#9-uygulama-katmanlarında-logging-örnekleri)
  - [9.1. Frontend Logging](#91-frontend-logging)
  - [9.2. Backend Logging](#92-backend-logging)
  - [9.3. Database Logging](#93-database-logging)
  - [9.4. API Logging](#94-api-logging)
- [10. Örnek Kodlar](#10-örnek-kodlar)
  - [10.1. JavaScript Logging Örneği](#101-javascript-logging-örneği)
  - [10.2. Python Logging Örneği](#102-python-logging-örneği)
  - [10.3. C# Exception Handling Örneği](#103-c-exception-handling-örneği)
- [11. Yaygın Hatalar ve Anti-Pattern'ler](#11-yaygın-hatalar-ve-anti-patternler)
- [12. Güvenlik Açısından Logging](#12-güvenlik-açısından-logging)
- [13. Performans Açısından Logging](#13-performans-açısından-logging)
- [14. Monitoring ve Logging Araçları](#14-monitoring-ve-logging-araçları)
- [15. Production Senaryosu](#15-production-senaryosu)
- [16. Mülakat Soruları ve Kısa Cevaplar](#16-mülakat-soruları-ve-kısa-cevaplar)
- [17. Özet Tablo](#17-özet-tablo)
- [18. Genel Sonuç](#18-genel-sonuç)

---

# 1. Giriş

Bir yazılımın geliştirme ortamında çalışması tek başına yeterli değildir. Gerçek dünyada uygulamalar:

- binlerce kullanıcı tarafından kullanılabilir,
- aynı anda yüzlerce veya binlerce istek alabilir,
- farklı servislerle haberleşebilir,
- veritabanı bağlantısı kurabilir,
- harici API'leri kullanabilir,
- ağ problemleri yaşayabilir,
- beklenmeyen kullanıcı girdileriyle karşılaşabilir,
- sunucu kaynaklarının tükenmesi gibi sorunlar yaşayabilir.

Bu nedenle profesyonel bir yazılım sisteminde yalnızca **kod yazmak** değil, sistem çalışırken sistemin ne yaptığını anlayabilmek de gerekir. Bu noktada üç temel kavram devreye girer:

1. **Logging**
2. **Monitoring**
3. **Debugging**

Bunlara ek olarak hataların kontrollü biçimde yönetilmesi için:

4. **Exception Handling**

kullanılır. Bu kavramlar birlikte kullanıldığında geliştirici şu sorulara cevap verebilir:

- Sistem neden hata verdi?
- Hata ne zaman başladı?
- Hangi kullanıcı veya istek hatayı tetikledi?
- Hangi servis çalışmadı?
- Veritabanı mı yavaşladı?
- API çağrısı mı başarısız oldu?
- Bellek mi doldu?
- CPU kullanımı mı yükseldi?
- Son deploy'dan sonra mı problem başladı?
- Problem yalnızca belirli kullanıcılarda mı oluşuyor?
- Hatanın gerçek kök nedeni nedir?

Production sistemlerini yönetebilmenin temel şartlarından biri bu sorulara hızlı cevap verebilmektir.

---

# 2. Logging Nedir?

**Logging**, bir uygulama çalışırken meydana gelen olayların kayıt altına alınması işlemidir. Bir uygulama çalışırken birçok olay meydana gelir. Örneğin:

```text
Kullanıcı giriş yaptı.
Sipariş oluşturuldu.
Ödeme işlemi başladı.
Veritabanı bağlantısı başarısız oldu.
API isteği 500 hatası döndürdü.
Dosya yükleme tamamlandı.
```

Bu olayların kayıt altına alınmasına **loglama** denir. Loglar genellikle şu bilgileri içerir:

```text
2026-08-22 14:25:10 INFO User login successful userId=123
```

Buradaki bilgiler:

```text
2026-08-22 14:25:10
```

olayın gerçekleştiği zamanı,

```text
INFO
```

log seviyesini,

```text
User login successful
```

olayın açıklamasını,

```text
userId=123
```

ise olaya ait bağlam bilgisini gösterir.

---

## 2.1. Neden Log Tutulur?

Logların temel amacı sistemde ne olduğunu anlayabilmektir. Örneğin kullanıcı şöyle bir hata bildirebilir:

> "Siparişimi oluşturamıyorum."

Eğer sistemde log yoksa geliştirici problemi tahmin etmek zorunda kalabilir. Ancak log varsa:

```text
INFO  Creating order userId=42
INFO  Checking stock productId=78
ERROR Database timeout while checking stock productId=78
```

gibi kayıtlar görülebilir. Bu durumda problemin sipariş ekranında değil, veritabanı sorgusunda olduğu anlaşılır. Logging şu amaçlarla kullanılır:

- hata analizi,
- sistem davranışını takip etme,
- production sorunlarını inceleme,
- güvenlik olaylarını takip etme,
- performans problemlerini tespit etme,
- kullanıcı işlemlerini izleme,
- sistem geçmişini inceleme,
- hata oluştuğunda kök nedeni bulma.

---

## 2.2. İyi Bir Log Kaydı Nasıl Olmalıdır?

İyi bir log kaydı:

- anlamlı olmalıdır,
- gerekli bağlamı içermelidir,
- doğru log seviyesini kullanmalıdır,
- zaman bilgisini içermelidir,
- mümkünse hangi kullanıcı veya request ile ilgili olduğunu belirtmelidir,
- hassas veri içermemelidir.

Kötü log:

```text
Error happened.
```

Bu log neredeyse hiçbir bilgi vermez. Daha iyi log:

```text
ERROR Payment processing failed orderId=7842 provider=Stripe error=Timeout
```

Bu log sayesinde:

- hangi işlemin başarısız olduğu,
- hangi siparişte olduğu,
- hangi servis kullanıldığı,
- hata türünün ne olduğu

anlaşılabilir.

---

## 2.3. Log Seviyeleri

Log seviyeleri bir log mesajının önem derecesini belirtir. Yaygın log seviyeleri şunlardır:

```text
TRACE
DEBUG
INFO
WARN
ERROR
FATAL / CRITICAL
```

Her uygulama bütün seviyeleri kullanmak zorunda değildir. Küçük uygulamalarda genellikle:

```text
DEBUG
INFO
WARN
ERROR
```

yeterlidir.

---

### TRACE

En detaylı log seviyesidir. Uygulamanın çok ayrıntılı çalışma akışını görmek için kullanılır. Örneğin:

```text
TRACE Entering calculatePrice()
TRACE Applying discount rule
TRACE Returning final price
```

Production ortamında çok fazla log oluşturabileceği için genellikle kapatılır.

---

### DEBUG

Geliştirme ve hata ayıklama sırasında kullanılan detaylı bilgilerdir. Örneğin:

```text
DEBUG Fetching user from database userId=42
```

veya:

```text
DEBUG Request payload validated successfully
```

Production ortamında DEBUG logları çoğu zaman devre dışı bırakılır veya yalnızca gerektiğinde açılır.

---

### INFO

Sistemin normal çalışma akışındaki önemli olayları gösterir. Örneğin:

```text
INFO User logged in userId=42
```

```text
INFO Order created orderId=987
```

```text
INFO Application started on port 8080
```

INFO seviyesi hata anlamına gelmez. Sistemde beklenen ve normal gerçekleşen olayları kaydetmek için kullanılır.

---

### WARN

Sistem çalışmaya devam etmektedir ancak dikkat edilmesi gereken bir durum vardır. Örneğin:

```text
WARN API response time is high duration=3200ms
```

veya:

```text
WARN User failed login attempt count=4
```

WARN genellikle ileride probleme dönüşebilecek durumlar için kullanılır.

---

### ERROR

Bir işlem başarısız olduğunda kullanılır. Örneğin:

```text
ERROR Payment failed orderId=321
```

veya:

```text
ERROR Database connection failed
```

ERROR seviyesinde uygulamanın tamamının çökmesi gerekmez. Belirli bir işlem başarısız olmuş olabilir.

---

### FATAL / CRITICAL

Sistemin çalışmasını ciddi şekilde etkileyen kritik hataları belirtir. Örneğin:

```text
FATAL Application cannot connect to database
```

veya:

```text
CRITICAL Out of memory
```

Bu tür hatalarda uygulama tamamen durabilir veya servis kullanılamaz hale gelebilir.

---

## 2.4. Log Seviyeleri Karşılaştırma Tablosu

| Seviye | Kullanım Amacı | Örnek |
|---|---|---|
| TRACE | Çok detaylı çalışma akışı | Fonksiyon içerisindeki her küçük adım |
| DEBUG | Geliştirme ve debugging | Değişken değerleri, sorgu detayları |
| INFO | Normal sistem olayları | Kullanıcı giriş yaptı |
| WARN | Potansiyel problem | API yavaş cevap verdi |
| ERROR | İşlem başarısız | Veritabanı sorgusu başarısız |
| FATAL / CRITICAL | Sistem çalışamaz durumda | Database tamamen erişilemez |

---

## 2.5. Structured Logging

Eski tip loglar genellikle düz metindir. Örneğin:

```text
User 42 created order 583
```

Modern sistemlerde ise **structured logging** kullanılır. Örneğin JSON formatında:

```json
{
  "level": "INFO",
  "message": "Order created",
  "userId": 42,
  "orderId": 583,
  "timestamp": "2026-08-22T14:30:00Z"
}
```

Structured logging sayesinde loglar daha kolay:

- filtrelenebilir,
- aranabilir,
- analiz edilebilir,
- dashboard üzerinde gösterilebilir.

Örneğin:

```text
orderId = 583
```

olan bütün loglar aranabilir. Ya da:

```text
level = ERROR
```

olan loglar filtrelenebilir.

---

## 2.6. Loglara Neler Yazılmalı?

Genellikle şu bilgiler loglanabilir:

- zaman bilgisi,
- log seviyesi,
- işlem adı,
- endpoint,
- HTTP method,
- response status,
- request süresi,
- kullanıcı ID'si,
- request ID,
- correlation ID,
- sipariş ID,
- işlem ID,
- servis adı,
- hata mesajı,
- stack trace.

Örneğin:

```text
INFO request_completed
method=POST
path=/api/orders
status=201
duration=145ms
requestId=a83f91
userId=42
```

---

## 2.7. Loglara Neler Yazılmamalı?

Loglara hassas bilgiler kesinlikle yazılmamalıdır. Örneğin:

```text
password
credit card number
CVV
access token
refresh token
API key
secret key
kişisel sağlık verileri
```

Kötü örnek:

```text
INFO User login password=123456
```

Bu ciddi bir güvenlik açığıdır. Bunun yerine:

```text
INFO User login attempt userId=42
```

gibi güvenli kayıtlar kullanılmalıdır.

---

## 2.8. Correlation ID ve Request ID

Modern sistemlerde tek bir kullanıcı isteği birden fazla servisten geçebilir. Örneğin:

```text
Frontend
   ↓
API Gateway
   ↓
Order Service
   ↓
Payment Service
   ↓
Database
```

Bir hata oluştuğunda bütün servislerin loglarını ilişkilendirmek zor olabilir. Bu nedenle isteğe benzersiz bir kimlik atanır:

```text
correlationId=abc123
```

Daha sonra bütün servisler aynı ID ile log üretir. Örneğin:

```text
INFO Order request received correlationId=abc123
INFO Payment started correlationId=abc123
ERROR Payment timeout correlationId=abc123
```

Böylece tek bir isteğin sistemdeki yolculuğu takip edilebilir.

---

## 2.9. Log Rotation ve Retention

Loglar sürekli büyüyebilir. Örneğin bir uygulama günde:

```text
5 GB
```

log üretiyorsa kısa sürede disk dolabilir. Bu nedenle iki önemli kavram vardır:

### Log Rotation

Log dosyalarının belirli aralıklarla bölünmesidir. Örneğin:

```text
app.log
app-2026-08-21.log
app-2026-08-20.log
```

### Log Retention

Logların ne kadar süre saklanacağını belirler. Örneğin:

```text
30 gün
90 gün
1 yıl
```

Saklama süresi:

- sistem ihtiyacına,
- yasal gerekliliklere,
- depolama maliyetine

göre belirlenir.

---

# 3. Exception Handling

## 3.1. Exception Nedir?

**Exception**, programın normal çalışma akışını bozan beklenmeyen durumdur. Örneğin:

```text
dosya bulunamadı
veritabanına bağlanılamadı
null değer kullanıldı
geçersiz kullanıcı girdisi
API cevap vermedi
```

Bu durumlarda program bir exception oluşturabilir.

---

## 3.2. Exception Handling Neden Gereklidir?

Exception handling kullanılmazsa küçük bir hata bütün uygulamayı durdurabilir. Örneğin:

```text
Payment API timeout
```

oluştuğunda uygulama tamamen çökmek yerine:

```text
Ödeme şu anda gerçekleştirilemiyor.
```

şeklinde kontrollü cevap verebilir. Exception handling sayesinde:

- uygulamanın tamamen çökmesi engellenebilir,
- kullanıcıya kontrollü hata mesajı gösterilebilir,
- hata loglanabilir,
- gerekli cleanup işlemleri yapılabilir,
- sistem belirli durumlarda tekrar deneyebilir.

---

## 3.3. try-catch-finally Mantığı

Birçok programlama dilinde hata yönetimi şu yapıya benzer:

```text
try
catch
finally
```

Mantık:

```text
try
```

riskli kod çalıştırılır.

```text
catch
```

exception oluşursa hata yakalanır.

```text
finally
```

hata olsa da olmasa da çalışması gereken kod çalıştırılır. Örneğin:

```csharp
try
{
    ProcessPayment();
}
catch (Exception ex)
{
    LogError(ex);
}
finally
{
    CloseConnection();
}
```

---

## 3.4. Exception Türleri

Exception'lar farklı kategorilere ayrılabilir.

### Validation Exception

Kullanıcı girdisi geçersizdir. Örneğin:

```text
Email formatı hatalı.
```

### Authentication Exception

Kullanıcı doğrulanamamıştır.

```text
Invalid username or password.
```

### Authorization Exception

Kullanıcının işlem yetkisi yoktur.

```text
Access denied.
```

### Database Exception

Veritabanı işlemi başarısızdır.

```text
Database connection timeout.
```

### Network Exception

Ağ veya servis erişim problemi vardır.

```text
External service unreachable.
```

### Business Exception

İş kuralı ihlal edilmiştir. Örneğin:

```text
Stokta olmayan ürün sipariş edilemez.
```

---

## 3.5. Hataları Yutmak Neden Yanlıştır?

Kötü exception handling örneği:

```javascript
try {
    await saveOrder();
} catch (error) {
}
```

Burada hata tamamen yok sayılmıştır. Bu duruma bazen:

> **swallowing exceptions**

denir. Bu yaklaşım tehlikelidir çünkü sistem hata vermiştir fakat geliştirici bunu göremez. Daha doğru yaklaşım:

```javascript
try {
    await saveOrder();
} catch (error) {
    logger.error("Order save failed", error);
    throw error;
}
```

veya uygulamanın mimarisine uygun kontrollü bir cevap dönmektir.

---

## 3.6. Global Exception Handling

Her controller veya fonksiyon içerisinde tekrar tekrar:

```text
try-catch
```

yazmak kod tekrarına neden olabilir. Bu nedenle modern backend sistemlerinde **global exception handler** kullanılır. Örneğin:

```text
Request
   ↓
Controller
   ↓
Service
   ↓
Exception
   ↓
Global Exception Handler
   ↓
Log Error
   ↓
HTTP Response
```

Örneğin hata:

```text
ProductNotFoundException
```

ise global handler:

```http
404 Not Found
```

dönebilir.

---

## 3.7. Custom Exception Kullanımı

Her hatayı:

```text
Exception
```

olarak kullanmak yerine özel exception sınıfları oluşturulabilir. Örneğin:

```text
ProductNotFoundException
InsufficientStockException
PaymentFailedException
UnauthorizedOperationException
```

Bu yaklaşım kodun daha anlamlı olmasını sağlar.

---

## 3.8. Kullanıcıya Gösterilen Hata ile Loglanan Hata Aynı Olmamalıdır

Production sistemlerinde kullanıcıya teknik detay göstermek doğru değildir. Kötü örnek:

```text
SQLSTATE[HY000] Connection refused 192.168.1.15:3306
```

Bu mesaj hem kullanıcı açısından anlamsızdır hem de güvenlik açısından sistem detaylarını ortaya çıkarabilir. Kullanıcıya:

```text
İşlem sırasında bir hata oluştu. Lütfen daha sonra tekrar deneyin.
```

gösterilebilir. Log tarafında ise:

```text
ERROR Database connection refused
host=192.168.1.15
port=3306
requestId=abc123
```

gibi detaylı kayıt tutulabilir.

---

# 4. Debugging Nedir?

**Debugging**, yazılımdaki hatanın kaynağını bulma ve düzeltme sürecidir. Bir bug görüldüğünde amaç yalnızca hatayı ortadan kaldırmak değildir. Asıl amaç:

> Hatanın neden oluştuğunu anlamaktır.

---

## 4.1. Debugging Süreci

Profesyonel debugging süreci genellikle şu adımlardan oluşur:

```text
1. Problemi yeniden üret
2. Hata koşullarını belirle
3. Logları incele
4. Hangi katmanda olduğunu belirle
5. İlgili kodu izole et
6. Değişkenleri kontrol et
7. Kök nedeni bul
8. Düzeltme yap
9. Test et
10. Regression oluşmadığını doğrula
```

---

## 4.2. Breakpoint Nedir?

Breakpoint, program çalışırken belirli bir satırda durmasını sağlar. Örneğin:

```javascript
const total = calculateTotal(items);
```

satırına breakpoint konulursa uygulama burada durur. Geliştirici:

- değişken değerlerini,
- fonksiyon parametrelerini,
- çalışma akışını

inceleyebilir.

---

## 4.3. Step Over, Step Into ve Step Out

Debug araçlarında sık kullanılan üç komut vardır.

### Step Over

Mevcut satırı çalıştırır fakat fonksiyonun içine girmez.

### Step Into

Çağrılan fonksiyonun içine girer.

### Step Out

Mevcut fonksiyondan çıkar ve çağıran fonksiyona geri döner.

---

## 4.4. Watch ve Call Stack

### Watch

Belirli değişkenlerin değerlerini sürekli takip etmeye yarar. Örneğin:

```text
userId
orderId
totalPrice
```

### Call Stack

Programın hangi fonksiyonlardan geçerek mevcut noktaya geldiğini gösterir. Örneğin:

```text
createOrder()
↓
validateOrder()
↓
checkStock()
↓
databaseQuery()
```

Bu bilgi özellikle karmaşık hatalarda oldukça değerlidir.

---

## 4.5. Console Debugging

Frontend geliştirmede sık kullanılan yöntemlerden biri console çıktılarıdır. Örneğin:

```javascript
console.log("User:", user);
```

Ancak production kodunda gereksiz:

```javascript
console.log()
```

ifadeleri bırakılmamalıdır. Daha profesyonel sistemlerde merkezi logging araçları kullanılır.

---

## 4.6. Rubber Duck Debugging

İlginç fakat etkili bir debugging tekniğidir. Programcı problemi birine veya sembolik olarak bir nesneye adım adım anlatır. Örneğin:

```text
Bu fonksiyon kullanıcıyı alıyor.
Sonra userId ile sorgu yapıyor.
Burada userId aslında undefined geliyor...
```

Problemi anlatırken geliştirici çoğu zaman hatayı kendisi fark eder.

---

## 4.7. Binary Search Debugging

Büyük bir sistemde hatanın yerini bulmak için problemi ikiye bölerek ilerleme yaklaşımıdır. Örneğin sistem:

```text
Frontend
↓
API
↓
Service
↓
Database
```

şeklinde çalışıyorsa önce:

```text
API'ye doğru veri geliyor mu?
```

kontrol edilir. Geliyorsa problem frontend değildir. Daha sonra:

```text
Service doğru veriyi üretiyor mu?
```

kontrol edilir. Bu şekilde hata alanı giderek daraltılır.

---

# 5. Monitoring Nedir?

**Monitoring**, çalışan bir sistemin sağlık durumunun sürekli takip edilmesidir. Logging geçmişte ne olduğunu anlatırken monitoring sistemin mevcut durumunu anlamaya yardımcı olur. Örneğin monitoring ile şunlar takip edilebilir:

```text
CPU kullanımı
RAM kullanımı
disk kullanımı
request sayısı
response süresi
error rate
database connection sayısı
aktif kullanıcı sayısı
```

---

## 5.1. Monitoring Neden Şarttır?

Production ortamında geliştirici sistemi sürekli manuel olarak kontrol edemez. Örneğin gece saat 03:00'te:

```text
API error rate %1 → %35
```

olabilir. Monitoring sistemi bunu otomatik olarak tespit edip alarm gönderebilir. Örneğin:

```text
ALERT
Payment Service error rate > 20%
```

Monitoring olmadığı durumda problem ancak kullanıcılar şikayet etmeye başladığında fark edilebilir. Profesyonel sistemlerde hedef:

> Kullanıcı fark etmeden problemi fark etmektir.

---

## 5.2. Monitoring ile Logging Arasındaki Fark

Logging:

```text
Tek tek olayları kaydeder.
```

Monitoring:

```text
Sistemin genel sağlık durumunu takip eder.
```

Örneğin log:

```text
ERROR Payment failed
```

Monitoring metriği:

```text
Payment failure rate = 18%
```

İkisi birlikte kullanıldığında güçlü bir gözlem sistemi oluşur.

---

## 5.3. Monitoring Türleri

### Application Monitoring

Uygulamanın davranışını takip eder. Örneğin:

```text
request count
response time
error rate
```

---

### Infrastructure Monitoring

Sunucu kaynaklarını takip eder. Örneğin:

```text
CPU
RAM
disk
network
```

---

### Database Monitoring

Veritabanı performansını takip eder. Örneğin:

```text
slow queries
connection count
query latency
deadlock
```

---

### Network Monitoring

Ağ bağlantılarını takip eder. Örneğin:

```text
latency
packet loss
network errors
```

---

### User Experience Monitoring

Gerçek kullanıcının uygulamada yaşadığı deneyimi takip eder. Örneğin:

```text
page load time
frontend crash
JavaScript error
API waiting time
```

---

## 5.4. Temel Monitoring Metrikleri

Yaygın uygulama metrikleri:

### Request Rate

Saniyede veya dakikada gelen istek sayısı.

```text
1200 requests/minute
```

### Error Rate

Başarısız isteklerin oranı.

```text
2.3%
```

### Latency

İsteğin cevaplanma süresi.

```text
250 ms
```

### CPU Usage

```text
72%
```

### Memory Usage

```text
4.2 GB / 8 GB
```

### Disk Usage

```text
85%
```

### Database Connections

```text
87 / 100 active connections
```

---

## 5.5. Golden Signals

Google SRE yaklaşımında sistem gözlemi için sık kullanılan dört temel sinyal vardır.

### Latency

İsteklerin ne kadar sürede cevaplandığı.

### Traffic

Sistemin ne kadar trafik aldığı. Örneğin:

```text
requests / second
```

### Errors

Başarısız isteklerin oranı.

### Saturation

Sistemin kapasitesinin ne kadarının kullanıldığı. Örneğin:

```text
CPU %95
RAM %90
DB connection pool %100
```

Bu dört metrik sistem sağlığını anlamak için oldukça değerlidir.

---

# 6. Observability Nedir?

**Observability**, bir sistemin iç durumunu dışarıdan ürettiği veriler üzerinden anlayabilme yeteneğidir. Monitoring:

> "Bir problem var mı?"

sorusuna cevap verir. Observability ise:

> "Problem neden oldu?"

sorusuna cevap vermeye yardımcı olur. Observability'nin üç temel bileşeni vardır:

```text
Logs
Metrics
Traces
```

Bunlara genellikle **Three Pillars of Observability** denir.

---

## 6.1. Logs

Belirli olayların kayıtlarıdır. Örneğin:

```text
ERROR Payment failed
```

---

## 6.2. Metrics

Sayısal sistem ölçümleridir. Örneğin:

```text
payment_error_rate = 12%
```

---

## 6.3. Traces

Bir request'in birden fazla servis boyunca izlediği yolu gösterir. Örneğin:

```text
Frontend
↓ 20ms
API Gateway
↓ 40ms
Order Service
↓ 1800ms
Payment Service
↓ 50ms
Database
```

Burada Order Service'in ciddi gecikme oluşturduğu görülebilir. Distributed sistemlerde tracing son derece önemlidir.

---

## 6.4. Logs, Metrics ve Traces Birlikte Nasıl Kullanılır?

Örneğin monitoring sistemi şunu gösterir:

```text
Error rate yükseldi.
```

Metrics:

```text
HTTP 500 rate %2 → %25
```

Daha sonra trace incelenir:

```text
Payment Service timeout
```

Ardından log aranır:

```text
ERROR Payment provider timeout
correlationId=abc123
```

Bu üç veri kaynağı birlikte kullanılarak problemin kök nedeni bulunabilir.

---

# 7. Alerting Nedir?

**Alerting**, belirli bir problem veya eşik oluştuğunda sistemin otomatik bildirim üretmesidir. Örneğin:

```text
CPU > 90%
```

olduğunda:

```text
Slack
Email
SMS
Pager
```

gibi kanallardan bildirim gönderilebilir.

---

## 7.1. İyi Bir Alarm Nasıl Olmalıdır?

İyi bir alarm:

- gerçekten önemli olmalıdır,
- aksiyon gerektirmelidir,
- doğru kişiye gönderilmelidir,
- problemi açıklamalıdır,
- gereksiz tekrar üretmemelidir.

Kötü alarm:

```text
CPU 71%
```

İyi alarm:

```text
CRITICAL
Payment API error rate > 20% for 5 minutes
```

---

## 7.2. Alert Fatigue

Çok fazla gereksiz alarm gönderildiğinde ekip zamanla alarm bildirimlerini görmezden gelmeye başlar. Bu duruma:

> **Alert Fatigue**

denir. Örneğin her küçük hata için alarm gönderilirse:

```text
1000 alarm / gün
```

oluşabilir. Bu durumda kritik alarm geldiğinde bile fark edilmeyebilir. Bu nedenle alarm kuralları dikkatli tasarlanmalıdır.

---

# 8. Production Ortamında Hata Çözme Süreci

Production ortamında hata oluştuğunda panik yapmak yerine sistematik ilerlemek gerekir.

---

## 8.1. Incident Nedir?

Bir servisin veya sistemin beklenen şekilde çalışmaması durumuna genellikle **incident** denir. Örneğin:

```text
Login servisi çalışmıyor.
Ödeme servisi cevap vermiyor.
Database bağlantıları tükenmiş.
Site çok yavaş.
```

---

## 8.2. Adım Adım Incident Çözüm Süreci

### 1. Problemi doğrula

Gerçekten problem var mı?

```text
HTTP 500 oranı yükseldi mi?
```

### 2. Etki alanını belirle

Problem:

```text
tüm kullanıcıları mı
belirli kullanıcıları mı
tek endpoint'i mi
tek servisi mi
```

etkiliyor?

### 3. Monitoring dashboard'una bak

Kontrol edilecekler:

```text
error rate
latency
CPU
memory
database
network
```

### 4. Son değişiklikleri kontrol et

Örneğin:

```text
Yeni deploy yapıldı mı?
Config değişti mi?
Database migration yapıldı mı?
```

### 5. Logları incele

Örneğin:

```text
ERROR
WARN
```

logları aranır.

### 6. Correlation ID kullan

Tek bir hatalı request'in bütün servislerdeki izleri takip edilir.

### 7. Sistemi stabilize et

Gerekirse:

```text
rollback
restart
traffic redirect
feature disable
```

gibi işlemler yapılabilir.

### 8. Root cause belirle

Problemin gerçek nedeni bulunur.

### 9. Kalıcı çözüm geliştir

Sadece sistemi yeniden başlatmak çoğu zaman kalıcı çözüm değildir.

### 10. Postmortem hazırla

Problem tekrar yaşanmasın diye olay analiz edilir.

---

## 8.3. Root Cause Analysis

**Root Cause Analysis (RCA)**, problemin görünen belirtisini değil gerçek temel nedenini bulma sürecidir. Örneğin:

```text
Site yavaş.
```

Bu yalnızca semptomdur. Asıl neden:

```text
Database index eksik.
```

olabilir.

---

## 8.4. 5 Whys Tekniği

Bir problemi sürekli "neden?" sorarak kök nedene ulaşmaya çalışan tekniktir. Örnek:

```text
Site neden çöktü? → Database connection sayısı doldu.
Connection sayısı neden doldu? → Connection'lar kapanmıyordu.
Neden kapanmıyordu? → Exception oluştuğunda dispose edilmiyordu.
Neden dispose edilmiyordu? → finally bloğu yoktu.
Neden testlerde fark edilmedi? → Connection leak testi yoktu.
```

Böylece problem yalnızca:

```text
Database çöktü.
```

seviyesinde bırakılmaz.

---

## 8.5. Postmortem Nedir?

Postmortem, ciddi production incident'larından sonra yapılan olay analizidir. İyi bir postmortem genellikle şunları içerir:

```text
Incident özeti
Başlangıç zamanı
Bitiş zamanı
Kullanıcı etkisi
Timeline
Root cause
Geçici çözüm
Kalıcı çözüm
Action items
```

Modern engineering kültüründe postmortem'in amacı:

> suçlu bulmak değil, sistemi iyileştirmektir.

---

# 9. Uygulama Katmanlarında Logging Örnekleri

## 9.1. Frontend Logging

Frontend tarafında takip edilebilecek olaylar:

```text
JavaScript exception
API request failure
page load error
UI crash
```

Örneğin:

```javascript
try {
    await loadProducts();
} catch (error) {
    console.error("Products could not be loaded", error);
}
```

Büyük sistemlerde bu hatalar merkezi hata izleme sistemlerine gönderilebilir.

---

## 9.2. Backend Logging

Backend tarafında genellikle:

```text
request
response
business operation
database query
external API request
exception
```

loglanır. Örneğin:

```text
INFO order_creation_started orderId=123
INFO inventory_checked productId=52
INFO payment_started orderId=123
ERROR payment_failed orderId=123
```

---

## 9.3. Database Logging

Database tarafında özellikle şu bilgiler takip edilir:

```text
slow query
connection failure
deadlock
query timeout
```

Örneğin:

```text
WARN Slow query detected duration=4300ms
```

---

## 9.4. API Logging

API loglarında şu bilgiler faydalıdır:

```text
HTTP method
endpoint
status code
request duration
request ID
user ID
```

Örneğin:

```text
INFO
method=POST
endpoint=/api/orders
status=201
duration=182ms
requestId=abc123
```

---

# 10. Örnek Kodlar

## 10.1. JavaScript Logging Örneği

Basit kullanım:

```javascript
console.info("Application started");
console.warn("API response is slow");
console.error("Request failed");
```

Daha profesyonel yaklaşımda merkezi logger kullanılabilir:

```javascript
logger.info("Order created", {
    orderId: order.id,
    userId: user.id
});

logger.error("Payment failed", {
    orderId: order.id,
    error: error.message
});
```

---

## 10.2. Python Logging Örneği

Python'ın standart `logging` modülü kullanılabilir.

```python
import logging

logging.basicConfig(level=logging.INFO)
logging.info("Application started")
logging.warning("API response is slow")
logging.error("Database connection failed")
```

Exception loglamak için:

```python
try:
    result = 10 / 0
except Exception:
    logging.exception("Unexpected error occurred")
```

`logging.exception()` stack trace bilgisini de loglayabilir.

---

## 10.3. C# Exception Handling Örneği

```csharp
try
{
    var user = GetUser(userId);

    if (user == null)
    {
        throw new UserNotFoundException();
    }
}
catch (UserNotFoundException ex)
{
    logger.LogWarning(ex, "User not found. UserId: {UserId}", userId);
}
catch (Exception ex)
{
    logger.LogError(ex, "Unexpected error occurred.");
    throw;
}
finally
{
    // Gerekli kaynak temizleme işlemleri
}
```

Burada:

```text
UserNotFoundException
```

beklenen iş hatası olarak ele alınırken,

```text
Exception
```

beklenmeyen hataları yakalar.

---

# 11. Yaygın Hatalar ve Anti-Pattern'ler

Logging ve debugging sırasında sık yapılan yanlışlar vardır.

### Her şeyi INFO olarak loglamak

Yanlış:

```text
INFO Database failed
INFO Payment failed
INFO Application crashed
```

Doğrusu uygun log seviyesini kullanmaktır.

---

### Gereksiz yere çok fazla log üretmek

Örneğin loop içinde:

```javascript
for (const item of items) {
    logger.info(item);
}
```

milyonlarca log üretebilir.

---

### Hassas verileri loglamak

Örneğin:

```text
password
token
credit card
API key
```

loglanmamalıdır.

---

### Exception'ı sessizce yok saymak

```javascript
catch (error) {}
```

tehlikelidir.

---

### Sadece hata mesajını loglamak

Örneğin:

```text
ERROR Something went wrong
```

yetersizdir. Context eklenmelidir.

---

### Kullanıcıya stack trace göstermek

Production ortamında:

```text
NullReferenceException at UserService.cs line 87
```

gibi teknik detaylar kullanıcıya gösterilmemelidir.

---

### Monitoring olmadan production çalıştırmak

Kullanıcı şikayeti sistemin monitoring aracı olmamalıdır. Sistem problemleri kullanıcıdan önce fark edilmelidir.

---

### Her alarmı kritik yapmak

Her hata:

```text
CRITICAL
```

olarak tanımlanırsa kritik kavramının anlamı kalmaz.

---

# 12. Güvenlik Açısından Logging

Log sistemleri güvenlik açısından da önemlidir. Örneğin aşağıdaki olaylar loglanabilir:

```text
başarısız login girişimleri
şüpheli IP adresleri
yetkisiz erişim denemeleri
admin işlemleri
rol değişiklikleri
şifre sıfırlama talepleri
```

Örneğin:

```text
WARN Failed login attempt
userId=42
ip=192.168.1.10
attemptCount=5
```

Bu loglar saldırı tespitinde yardımcı olabilir. Ancak güvenlik açısından logların kendisi de korunmalıdır. Örneğin log dosyaları:

- yetkisiz kullanıcılar tarafından okunamamalı,
- değiştirilememeli,
- hassas veri içermemeli,
- belirli retention politikalarına göre saklanmalıdır.

---

# 13. Performans Açısından Logging

Logging faydalıdır ancak yanlış kullanıldığında performans problemi oluşturabilir. Örneğin saniyede:

```text
10000 request
```

alan bir sistem her request için onlarca log üretirse:

```text
disk I/O
network trafiği
storage maliyeti
CPU kullanımı
```

artabilir. Bu nedenle:

- doğru log seviyeleri kullanılmalı,
- gereksiz debug logları production'da kapatılmalı,
- async logging tercih edilebilmeli,
- log retention politikaları belirlenmeli,
- çok yüksek hacimli olaylarda sampling uygulanabilmelidir.

---

# 14. Monitoring ve Logging Araçları

Gerçek projelerde çeşitli araçlar kullanılabilir.

### Logging / Log Management

- ELK Stack
  - Elasticsearch
  - Logstash
  - Kibana
- Graylog
- Splunk
- Loki

### Monitoring

- Prometheus
- Grafana
- Datadog
- New Relic
- Zabbix

### Error Tracking

- Sentry
- Bugsnag
- Rollbar

### Distributed Tracing

- OpenTelemetry
- Jaeger
- Zipkin

Bu araçların temel amacı farklı olsa da modern sistemlerde genellikle birlikte kullanılırlar. Örneğin:

```text
Prometheus → Metrics
Grafana → Dashboard
Loki → Logs
OpenTelemetry → Traces
Sentry → Application Errors
```

---

# 15. Production Senaryosu

Bir e-ticaret sisteminde kullanıcılar ödeme yapamamaya başladı. Monitoring sistemi alarm gönderdi:

```text
Payment API error rate > 25%
```

İlk olarak dashboard kontrol edildi.

```text
CPU normal
RAM normal
Database normal
Payment latency yüksek
```

Trace incelendi:

```text
Order Service → 40ms
Payment Service → 6500ms
```

Payment Service logları incelendi:

```text
ERROR External payment provider timeout
correlationId=abc123
```

Harici ödeme sağlayıcısının timeout verdiği anlaşıldı. Geçici olarak retry mekanizması devreye alındı. Daha sonra sistem düzeldi. Ardından postmortem hazırlandı. Kalıcı iyileştirme olarak:

```text
timeout policy
retry
circuit breaker
monitoring alert
fallback
```

mekanizmaları geliştirildi. Bu örnek Logging + Monitoring + Tracing'in birlikte nasıl çalıştığını gösterir.

---

# 16. Mülakat Soruları ve Kısa Cevaplar

### Logging nedir?

Uygulama çalışırken meydana gelen olayların kayıt altına alınmasıdır.

---

### INFO ve ERROR arasındaki fark nedir?

INFO normal sistem olaylarını, ERROR ise başarısız işlemleri belirtir.

---

### WARN ne zaman kullanılır?

Sistem çalışmaya devam ederken dikkat edilmesi gereken potansiyel problem olduğunda kullanılır.

---

### Exception handling nedir?

Program çalışırken meydana gelen hataları kontrollü şekilde yakalama ve yönetme işlemidir.

---

### try-catch-finally nedir?

`try` riskli kodu çalıştırır, `catch` hatayı yakalar, `finally` ise hata olsa da olmasa da çalışması gereken kodları çalıştırır.

---

### Logging ile monitoring arasındaki fark nedir?

Logging tek tek olayları kaydeder. Monitoring ise sistemin genel sağlık durumunu sürekli takip eder.

---

### Observability nedir?

Sistemin iç durumunu logs, metrics ve traces gibi dışarı verdiği veriler üzerinden anlayabilme yeteneğidir.

---

### Observability'nin üç temel bileşeni nedir?

```text
Logs
Metrics
Traces
```

---

### Correlation ID nedir?

Bir request'in birden fazla servis boyunca takip edilmesini sağlayan benzersiz kimliktir.

---

### Root Cause Analysis nedir?

Bir problemin görünen belirtisini değil gerçek temel nedenini bulma sürecidir.

---

### Alert fatigue nedir?

Çok fazla gereksiz alarm nedeniyle ekiplerin alarm bildirimlerini görmezden gelmeye başlamasıdır.

---

### Production ortamında neden DEBUG log seviyesi genellikle kapatılır?

Çok fazla log üretip performans ve depolama maliyetini artırabileceği için.

---

### Loglara neden password veya token yazılmamalıdır?

Bu bilgiler ele geçirilirse ciddi güvenlik açığı oluşabilir.

---

### Monitoring neden production için önemlidir?

Sistem problemlerinin kullanıcı şikayetlerinden önce otomatik olarak fark edilmesini sağlar.

---

# 17. Özet Tablo

| Kavram | Amaç | Örnek |
|---|---|---|
| Logging | Olayları kayıt altına almak | "Order created" |
| INFO | Normal sistem olayı | Kullanıcı giriş yaptı |
| WARN | Potansiyel problem | API yavaşladı |
| ERROR | Başarısız işlem | Database timeout |
| Exception Handling | Hataları kontrollü yönetmek | try-catch |
| Debugging | Hatanın kaynağını bulmak | Breakpoint |
| Monitoring | Sistem sağlığını takip etmek | CPU, RAM, latency |
| Metrics | Sayısal sistem ölçümleri | Error rate |
| Tracing | Request akışını takip etmek | Service → Service |
| Observability | Sistemin iç durumunu anlamak | Logs + Metrics + Traces |
| Alerting | Problem olduğunda bildirim üretmek | CPU > %90 |
| Correlation ID | Dağıtık request'i takip etmek | abc123 |
| Root Cause Analysis | Gerçek hata nedenini bulmak | Eksik database index |
| Postmortem | Incident sonrası öğrenme ve iyileştirme | Timeline + action items |

---

# 18. Genel Sonuç

Logging, monitoring, debugging ve exception handling profesyonel yazılım geliştirmenin temel parçalarıdır. Bir uygulamanın yalnızca geliştirme ortamında çalışması yeterli değildir. Gerçek production ortamında sistemlerin:

```text
hata vermesi
yavaşlaması
harici servislerin çalışmaması
database bağlantılarının tükenmesi
network problemleri
beklenmeyen kullanıcı girdileri
kaynak problemleri
```

gibi birçok durumla karşılaşması mümkündür. Bu nedenle geliştiricinin sistemin davranışını gözlemleyebilmesi gerekir. Bu noktada:

```text
Logging → Ne oldu?
Monitoring → Sistem şu anda nasıl?
Tracing → Request nereden geçti?
Debugging → Hata kodun neresinde?
Exception Handling → Hata nasıl kontrollü yönetilir?
Root Cause Analysis → Gerçek neden ne?
```

sorularına cevap verir. Profesyonel bir production sisteminde ideal yaklaşım:

```text
Logs
+
Metrics
+
Traces
+
Alerting
+
Exception Handling
+
Monitoring
```

yapısının birlikte kullanılmasıdır. Bu sayede production ortamında bir problem meydana geldiğinde geliştirici tahmin yürütmek yerine veriye dayanarak problemi analiz edebilir. Sonuç olarak iyi tasarlanmış logging ve monitoring altyapısı:

- hata çözme süresini azaltır,
- sistem güvenilirliğini artırır,
- kullanıcı deneyimini iyileştirir,
- geliştirici ekibinin sistemi daha kolay yönetmesini sağlar,
- kritik production problemlerinde panik yerine sistematik hareket etmeyi mümkün kılar.

> **Temel fikir:** Production ortamında önemli olan hiç hata olmaması değil, hata olduğunda onu hızlı fark etmek, doğru şekilde analiz etmek ve güvenli biçimde çözebilmektir.
