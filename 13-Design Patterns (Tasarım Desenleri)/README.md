# 13. Design Patterns (Tasarım Desenleri)

## İçindekiler

- [1. Giriş](#1-giris)
  - [1.1. Design Pattern Nedir?](#11-design-pattern-nedir)
  - [1.2. Tasarım Desenleri Bir Kod Kütüphanesi midir?](#12-tasarim-desenleri-bir-kod-kutuphanesi-midir)
  - [1.3. Tasarım Desenleri Neden Ortaya Çıkmıştır?](#13-tasarim-desenleri-neden-ortaya-cikmistir)
- [2. Neden Design Pattern Kullanılır?](#2-neden-design-pattern-kullanilir)
  - [2.1. Kod Tekrarını Azaltmak](#21-kod-tekrarini-azaltmak)
  - [2.2. Bakımı Kolaylaştırmak](#22-bakimi-kolaylastirmak)
  - [2.3. Esnek ve Genişletilebilir Kod Yazmak](#23-esnek-ve-genisletilebilir-kod-yazmak)
  - [2.4. Bağımlılıkları Azaltmak](#24-bagimliliklari-azaltmak)
  - [2.5. Ekip İçinde Ortak Bir Dil Oluşturmak](#25-ekip-icinde-ortak-bir-dil-olusturmak)
  - [2.6. Test Edilebilirliği Artırmak](#26-test-edilebilirligi-artirmak)
- [3. Design Pattern Türleri](#3-design-pattern-turleri)
  - [3.1. Creational Patterns](#31-creational-patterns)
  - [3.2. Structural Patterns](#32-structural-patterns)
  - [3.3. Behavioral Patterns](#33-behavioral-patterns)
- [4. Singleton Pattern](#4-singleton-pattern)
  - [4.1. Singleton Nedir?](#41-singleton-nedir)
  - [4.2. Singleton Hangi Problemi Çözer?](#42-singleton-hangi-problemi-cozer)
  - [4.3. Singleton Yapısı](#43-singleton-yapisi)
  - [4.4. Java ile Singleton Örneği](#44-java-ile-singleton-ornegi)
  - [4.5. Thread-Safe Singleton](#45-thread-safe-singleton)
  - [4.6. Singleton Kullanım Alanları](#46-singleton-kullanim-alanlari)
  - [4.7. Singleton Avantajları](#47-singleton-avantajlari)
  - [4.8. Singleton Dezavantajları](#48-singleton-dezavantajlari)
  - [4.9. Singleton Ne Zaman Kullanılmamalı?](#49-singleton-ne-zaman-kullanilmamali)
- [5. Factory Pattern](#5-factory-pattern)
  - [5.1. Factory Nedir?](#51-factory-nedir)
  - [5.2. Factory Hangi Problemi Çözer?](#52-factory-hangi-problemi-cozer)
  - [5.3. Factory Mantığı](#53-factory-mantigi)
  - [5.4. Java ile Factory Örneği](#54-java-ile-factory-ornegi)
  - [5.5. Simple Factory ve Factory Method Farkı](#55-simple-factory-ve-factory-method-farki)
  - [5.6. Factory Kullanım Alanları](#56-factory-kullanim-alanlari)
  - [5.7. Factory Avantajları](#57-factory-avantajlari)
  - [5.8. Factory Dezavantajları](#58-factory-dezavantajlari)
- [6. Strategy Pattern](#6-strategy-pattern)
  - [6.1. Strategy Nedir?](#61-strategy-nedir)
  - [6.2. Strategy Hangi Problemi Çözer?](#62-strategy-hangi-problemi-cozer)
  - [6.3. Strategy Yapısı](#63-strategy-yapisi)
  - [6.4. Java ile Strategy Örneği](#64-java-ile-strategy-ornegi)
  - [6.5. if-else Yerine Strategy Kullanımı](#65-if-else-yerine-strategy-kullanimi)
  - [6.6. Strategy Kullanım Alanları](#66-strategy-kullanim-alanlari)
  - [6.7. Strategy Avantajları](#67-strategy-avantajlari)
  - [6.8. Strategy Dezavantajları](#68-strategy-dezavantajlari)
- [7. Observer Pattern](#7-observer-pattern)
  - [7.1. Observer Nedir?](#71-observer-nedir)
  - [7.2. Observer Hangi Problemi Çözer?](#72-observer-hangi-problemi-cozer)
  - [7.3. Publisher-Subscriber Mantığı](#73-publisher-subscriber-mantigi)
  - [7.4. Java ile Observer Örneği](#74-java-ile-observer-ornegi)
  - [7.5. Observer Kullanım Alanları](#75-observer-kullanim-alanlari)
  - [7.6. Observer Avantajları](#76-observer-avantajlari)
  - [7.7. Observer Dezavantajları](#77-observer-dezavantajlari)
- [8. Adapter Pattern](#8-adapter-pattern)
  - [8.1. Adapter Nedir?](#81-adapter-nedir)
  - [8.2. Adapter Hangi Problemi Çözer?](#82-adapter-hangi-problemi-cozer)
  - [8.3. Gerçek Hayat Benzetmesi](#83-gercek-hayat-benzetmesi)
  - [8.4. Java ile Adapter Örneği](#84-java-ile-adapter-ornegi)
  - [8.5. Object Adapter ve Class Adapter](#85-object-adapter-ve-class-adapter)
  - [8.6. Adapter Kullanım Alanları](#86-adapter-kullanim-alanlari)
  - [8.7. Adapter Avantajları](#87-adapter-avantajlari)
  - [8.8. Adapter Dezavantajları](#88-adapter-dezavantajlari)
- [9. Decorator Pattern](#9-decorator-pattern)
  - [9.1. Decorator Nedir?](#91-decorator-nedir)
  - [9.2. Decorator Hangi Problemi Çözer?](#92-decorator-hangi-problemi-cozer)
  - [9.3. Kalıtım Yerine Composition](#93-kalitim-yerine-composition)
  - [9.4. Java ile Decorator Örneği](#94-java-ile-decorator-ornegi)
  - [9.5. Decorator Kullanım Alanları](#95-decorator-kullanim-alanlari)
  - [9.6. Decorator Avantajları](#96-decorator-avantajlari)
  - [9.7. Decorator Dezavantajları](#97-decorator-dezavantajlari)
- [10. Pattern'lerin Karşılaştırılması](#10-patternlerin-karsilastirilmasi)
  - [10.1. Singleton vs Factory](#101-singleton-vs-factory)
  - [10.2. Strategy vs Factory](#102-strategy-vs-factory)
  - [10.3. Observer vs Strategy](#103-observer-vs-strategy)
  - [10.4. Adapter vs Decorator](#104-adapter-vs-decorator)
  - [10.5. Genel Karşılaştırma Tablosu](#105-genel-karsilastirma-tablosu)
- [11. Design Patterns ve SOLID İlişkisi](#11-design-patterns-ve-solid-iliskisi)
  - [11.1. Single Responsibility Principle](#111-single-responsibility-principle)
  - [11.2. Open-Closed Principle](#112-open-closed-principle)
  - [11.3. Liskov Substitution Principle](#113-liskov-substitution-principle)
  - [11.4. Interface Segregation Principle](#114-interface-segregation-principle)
  - [11.5. Dependency Inversion Principle](#115-dependency-inversion-principle)
- [12. Junior Kod ile Profesyonel Kod Arasındaki Fark](#12-junior-kod-ile-profesyonel-kod-arasindaki-fark)
  - [12.1. Büyük if-else Blokları](#121-buyuk-if-else-bloklari)
  - [12.2. Sıkı Bağımlılık](#122-siki-bagimlilik)
  - [12.3. Tek Sınıfta Çok Fazla Sorumluluk](#123-tek-sinifta-cok-fazla-sorumluluk)
  - [12.4. Tekrar Eden Kodlar](#124-tekrar-eden-kodlar)
  - [12.5. Profesyonel Kodun Özellikleri](#125-profesyonel-kodun-ozellikleri)
- [13. Design Pattern Kullanırken Yapılan Hatalar](#13-design-pattern-kullanirken-yapilan-hatalar)
  - [13.1. Her Yerde Pattern Kullanmak](#131-her-yerde-pattern-kullanmak)
  - [13.2. Pattern'i Ezberleyip Problemi Anlamamak](#132-patterni-ezberleyip-problemi-anlamamak)
  - [13.3. Gereksiz Soyutlama Yapmak](#133-gereksiz-soyutlama-yapmak)
  - [13.4. Overengineering](#134-overengineering)
- [14. Design Pattern Seçerken Nasıl Düşünülmeli?](#14-design-pattern-secerken-nasil-dusunulmeli)
- [15. Gerçek Projelerde Birlikte Kullanım Senaryosu](#15-gercek-projelerde-birlikte-kullanim-senaryosu)
- [16. Mülakatlarda Sorulabilecek Sorular](#16-mulakatlarda-sorulabilecek-sorular)
- [17. Kısa Özet](#17-kisa-ozet)
- [18. Genel Sonuç](#18-genel-sonuc)

---

<a id="1-giris"></a>
## 1. Giriş

Yazılım geliştirme yalnızca çalışan kod yazmaktan ibaret değildir. Küçük bir uygulamada birkaç sınıf, birkaç fonksiyon ve birkaç `if-else` bloğu yeterli olabilir. Ancak proje büyüdükçe kod tabanı karmaşıklaşır, yeni özellikler eklenir, farklı geliştiriciler aynı kod üzerinde çalışmaya başlar ve başlangıçta basit görünen çözümler zamanla yönetilmesi zor bir hale gelir. Bu noktada yazılım tasarımı önem kazanır.

**Design Patterns**, yani **Tasarım Desenleri**, yazılım geliştirmede tekrar tekrar karşılaşılan tasarım problemlerine yönelik, zaman içinde denenmiş ve kabul görmüş çözüm yaklaşımlarıdır. Tasarım desenleri belirli bir programlama diline bağlı değildir. Java, C#, Python, JavaScript, C++ veya başka bir nesne yönelimli dilde aynı tasarım fikri farklı sözdizimleriyle uygulanabilir.

<a id="11-design-pattern-nedir"></a>
### 1.1. Design Pattern Nedir?

Design Pattern, yazılım geliştirmede sık karşılaşılan bir probleme yönelik genel bir çözüm şablonudur. Örneğin:

- Uygulama boyunca bir sınıftan yalnızca tek bir nesne oluşturmak istiyorsak **Singleton**,
- Nesne oluşturma işlemini merkezi bir noktada yönetmek istiyorsak **Factory**,
- Aynı işlemin farklı algoritmalarla yapılmasını istiyorsak **Strategy**,
- Bir nesnedeki değişiklikten birçok nesnenin haberdar olmasını istiyorsak **Observer**,
- Uyumsuz iki yapının birlikte çalışmasını sağlamak istiyorsak **Adapter**,
- Bir nesneye çalışma zamanında yeni davranışlar eklemek istiyorsak **Decorator**

gibi tasarım desenleri kullanılabilir. Bir tasarım deseni genellikle şunları açıklar:

1. Hangi problem çözülmektedir?
2. Problem hangi koşullarda ortaya çıkar?
3. Çözümde hangi sınıflar veya bileşenler bulunur?
4. Bu bileşenler birbirleriyle nasıl iletişim kurar?
5. Çözümün avantajları ve dezavantajları nelerdir?

<a id="12-tasarim-desenleri-bir-kod-kutuphanesi-midir"></a>
### 1.2. Tasarım Desenleri Bir Kod Kütüphanesi midir?

Hayır. Design Pattern doğrudan kopyalanıp kullanılacak hazır bir kod paketi değildir. Daha çok bir **tasarım fikridir**. Örneğin Singleton Pattern şu fikri söyler:

> Bir sınıftan yalnızca tek bir nesne oluşturulmalı ve bu nesneye uygulamanın farklı yerlerinden erişilebilmelidir.

Ancak bunu Java'da farklı, Python'da farklı, JavaScript'te farklı şekilde uygulayabiliriz. Bu nedenle pattern öğrenirken yalnızca kodu ezberlemek doğru değildir. Asıl öğrenilmesi gereken şey:

- Hangi problemi çözdüğü,
- Problemin neden ortaya çıktığı,
- Pattern'in problemi nasıl çözdüğü,
- Hangi durumlarda kullanılmasının yanlış olabileceğidir.

<a id="13-tasarim-desenleri-neden-ortaya-cikmistir"></a>
### 1.3. Tasarım Desenleri Neden Ortaya Çıkmıştır?

Yazılım geliştiriciler uzun yıllar boyunca benzer tasarım problemleriyle tekrar tekrar karşılaşmıştır. Örneğin:

- Nesne oluşturma süreçlerinin karmaşıklaşması,
- Sınıfların birbirine aşırı bağımlı olması,
- Bir değişiklik yapıldığında birçok dosyanın etkilenmesi,
- Kod tekrarlarının oluşması,
- Yeni özellik eklemenin zorlaşması,
- Büyük `if-else` veya `switch-case` bloklarının oluşması.

Bu problemlere farklı projelerde benzer çözümler uygulanmış ve zamanla bu çözümler isimlendirilerek tasarım desenleri haline gelmiştir. Design Patterns kavramının yaygınlaşmasında 1994 yılında yayımlanan **Design Patterns: Elements of Reusable Object-Oriented Software** kitabının büyük etkisi vardır. Kitabın yazarları:

- Erich Gamma
- Richard Helm
- Ralph Johnson
- John Vlissides

birlikte **Gang of Four (GoF)** olarak bilinir. GoF kitabında toplam 23 temel tasarım deseni tanımlanmıştır.

---

<a id="2-neden-design-pattern-kullanilir"></a>
## 2. Neden Design Pattern Kullanılır?

Design Pattern kullanmanın temel amacı kodu daha karmaşık hale getirmek değil, tam tersine büyüyen yazılımları daha kontrollü ve sürdürülebilir hale getirmektir.

<a id="21-kod-tekrarini-azaltmak"></a>
### 2.1. Kod Tekrarını Azaltmak

Aynı veya benzer kodun farklı yerlerde tekrar edilmesi uzun vadede ciddi bir bakım problemine dönüşür. Örneğin aynı ödeme hesaplaması beş farklı sınıfta bulunuyorsa, kurallar değiştiğinde beş farklı yerde değişiklik yapmak gerekir. Pattern kullanılarak ortak davranış tek bir yapıda toplanabilir. Bu yaklaşım **DRY — Don't Repeat Yourself** prensibiyle de ilişkilidir.

<a id="22-bakimi-kolaylastirmak"></a>
### 2.2. Bakımı Kolaylaştırmak

İyi tasarlanmış bir sistemde belirli bir davranış belirli bir sınıf veya modül tarafından yönetilir. Böylece değişiklik gerektiğinde:

```text
Bir özelliği değiştirmek
        ↓
İlgili sınıfı değiştirmek
        ↓
Diğer modüller minimum düzeyde etkilenir
```

Kötü tasarlanmış sistemlerde ise küçük bir değişiklik zincirleme şekilde birçok dosyayı etkileyebilir.

<a id="23-esnek-ve-genisletilebilir-kod-yazmak"></a>
### 2.3. Esnek ve Genişletilebilir Kod Yazmak

Profesyonel yazılım geliştirmede sistemin yalnızca bugünkü ihtiyaçlara değil, gelecekteki olası değişikliklere de uyum sağlayabilmesi önemlidir. Örneğin bir ödeme sistemi başlangıçta yalnızca:

```text
Kredi Kartı
```

destekliyor olabilir. Daha sonra:

```text
Kredi Kartı
PayPal
Banka Havalesi
Kripto Para
```

gibi yeni yöntemler eklenebilir. Eğer sistem Strategy Pattern ile tasarlanmışsa yeni bir ödeme yöntemi mevcut kodun büyük bölümünü değiştirmeden eklenebilir.

<a id="24-bagimliliklari-azaltmak"></a>
### 2.4. Bağımlılıkları Azaltmak

Bir sınıf başka bir sınıfın detaylarını çok fazla biliyorsa bu sınıflar arasında **tight coupling**, yani sıkı bağımlılık oluşur. Örneğin:

```java
class OrderService {
    CreditCardPayment payment = new CreditCardPayment();
}
```

Burada `OrderService`, doğrudan `CreditCardPayment` sınıfına bağımlıdır. Daha iyi tasarım:

```java
class OrderService {
    PaymentStrategy paymentStrategy;
}
```

Bu durumda `OrderService` belirli bir ödeme sınıfına değil, soyut bir arayüze bağımlıdır. Bu yaklaşım sistemi daha esnek hale getirir.

<a id="25-ekip-icinde-ortak-bir-dil-olusturmak"></a>
### 2.5. Ekip İçinde Ortak Bir Dil Oluşturmak

Design Pattern isimleri geliştiriciler arasında ortak bir teknik dil oluşturur. Örneğin bir geliştirici:

> "Bu davranışı Strategy olarak ayıralım."

dediğinde deneyimli bir geliştirici ne kastedildiğini hemen anlayabilir. Uzun uzun mimari yapıyı anlatmak yerine bir pattern ismi birçok tasarım kararını özetleyebilir.

<a id="26-test-edilebilirligi-artirmak"></a>
### 2.6. Test Edilebilirliği Artırmak

Bağımlılıkların arayüzler üzerinden yönetilmesi ve sorumlulukların ayrı sınıflara bölünmesi, unit test yazmayı kolaylaştırır. Örneğin ödeme işlemini test ederken gerçek banka servisine bağlanmak yerine sahte bir Strategy kullanılabilir.

```java
class FakePaymentStrategy implements PaymentStrategy {

    @Override
    public void pay(double amount) {
        System.out.println("Test payment");
    }
}
```

Bu yaklaşım mock ve dependency injection teknikleriyle birlikte yaygın olarak kullanılır.

---

<a id="3-design-pattern-turleri"></a>
## 3. Design Pattern Türleri

GoF tasarım desenleri üç ana gruba ayrılır:

1. Creational Patterns
2. Structural Patterns
3. Behavioral Patterns

<a id="31-creational-patterns"></a>
### 3.1. Creational Patterns

**Creational Patterns**, nesnelerin nasıl oluşturulduğu ile ilgilenir. Amaç doğrudan `new` kullanımıyla oluşabilecek sıkı bağımlılıkları azaltmaktır. Başlıca örnekler:

- Singleton
- Factory Method
- Abstract Factory
- Builder
- Prototype

Bu raporda:

- **Singleton**
- **Factory**

detaylı olarak incelenecektir.

<a id="32-structural-patterns"></a>
### 3.2. Structural Patterns

**Structural Patterns**, sınıfların ve nesnelerin nasıl bir araya getirileceğini ele alır. Amaç karmaşık sistemleri daha küçük ve yönetilebilir parçalara ayırmaktır. Örnekler:

- Adapter
- Decorator
- Facade
- Composite
- Bridge
- Proxy
- Flyweight

Bu raporda:

- **Adapter**
- **Decorator**

incelenecektir.

<a id="33-behavioral-patterns"></a>
### 3.3. Behavioral Patterns

**Behavioral Patterns**, nesnelerin birbirleriyle nasıl iletişim kuracağını ve sorumlulukların nasıl dağıtılacağını ele alır. Örnekler:

- Strategy
- Observer
- Command
- State
- Iterator
- Mediator
- Template Method
- Chain of Responsibility

Bu raporda:

- **Strategy**
- **Observer**

detaylı olarak ele alınacaktır.

---

<a id="4-singleton-pattern"></a>
## 4. Singleton Pattern

Singleton, en bilinen tasarım desenlerinden biridir. Creational Design Pattern kategorisindedir.

<a id="41-singleton-nedir"></a>
### 4.1. Singleton Nedir?

Singleton Pattern, bir sınıftan uygulama boyunca yalnızca **bir tane nesne oluşturulmasını** garanti etmeyi amaçlar. Aynı zamanda bu nesneye merkezi bir erişim noktası sağlar. Örneğin uygulamada:

```text
ConfigurationManager
Logger
CacheManager
DatabaseConnectionManager
```

gibi bazı servislerin tek bir instance olarak çalışması istenebilir.

<a id="42-singleton-hangi-problemi-cozer"></a>
### 4.2. Singleton Hangi Problemi Çözer?

Normal durumda şu şekilde birden fazla nesne oluşturulabilir:

```java
Logger logger1 = new Logger();
Logger logger2 = new Logger();
Logger logger3 = new Logger();
```

Eğer Logger uygulama genelinde tek bir kayıt sistemi kullanmalıysa bu istenmeyen bir durum olabilir. Singleton şu yapıyı hedefler:

```text
Application
    |
    |---- Component A
    |       |
    |       └── Logger Instance
    |
    |---- Component B
    |       |
    |       └── Aynı Logger Instance
    |
    └---- Component C
            |
            └── Aynı Logger Instance
```

<a id="43-singleton-yapisi"></a>
### 4.3. Singleton Yapısı

Singleton sınıfının genellikle üç temel özelliği vardır:

1. Constructor `private` yapılır.
2. Sınıf kendi instance'ını saklar.
3. Instance'a erişmek için `getInstance()` gibi statik bir metot sağlanır.

<a id="44-java-ile-singleton-ornegi"></a>
### 4.4. Java ile Singleton Örneği

```java
public class DatabaseManager {

    private static DatabaseManager instance;

    private DatabaseManager() {
        System.out.println("Database connection created.");
    }

    public static DatabaseManager getInstance() {

        if (instance == null) {
            instance = new DatabaseManager();
        }

        return instance;
    }
}
```

Kullanım:

```java
DatabaseManager db1 = DatabaseManager.getInstance();
DatabaseManager db2 = DatabaseManager.getInstance();

System.out.println(db1 == db2);
```

Çıktı:

```text
true
```

Çünkü `db1` ve `db2` aynı nesneyi göstermektedir.

<a id="45-thread-safe-singleton"></a>
### 4.5. Thread-Safe Singleton

Çoklu thread çalışan uygulamalarda basit Singleton uygulaması problem oluşturabilir. Aynı anda iki thread:

```java
if (instance == null)
```

kontrolüne girerse iki farklı instance oluşturulabilir. Basit bir çözüm:

```java
public class DatabaseManager {

    private static DatabaseManager instance;

    private DatabaseManager() {}

    public static synchronized DatabaseManager getInstance() {

        if (instance == null) {
            instance = new DatabaseManager();
        }

        return instance;
    }
}
```

Buradaki:

```java
synchronized
```

anahtar kelimesi aynı anda yalnızca bir thread'in metodu çalıştırmasını sağlar. Java'da daha modern ve güvenli yöntemlerden biri static holder yaklaşımıdır:

```java
public class DatabaseManager {

    private DatabaseManager() {}

    private static class Holder {
        private static final DatabaseManager INSTANCE =
                new DatabaseManager();
    }

    public static DatabaseManager getInstance() {
        return Holder.INSTANCE;
    }
}
```

<a id="46-singleton-kullanim-alanlari"></a>
### 4.6. Singleton Kullanım Alanları

Singleton şu tür yapılarda kullanılabilir:

- Uygulama yapılandırma yöneticisi
- Merkezi logger
- Cache yöneticisi
- Tema yöneticisi
- Sistem ayarları
- Kaynak yöneticileri
- Bazı bağlantı veya servis yöneticileri

Ancak modern uygulamalarda Singleton ihtiyacı çoğu zaman **Dependency Injection Container** tarafından yönetilebilir. Örneğin Spring Framework'te bean'lerin varsayılan scope'u Singleton'dır.

<a id="47-singleton-avantajlari"></a>
### 4.7. Singleton Avantajları

- Tek instance oluşturulmasını sağlar.
- Kaynak kullanımını azaltabilir.
- Merkezi erişim sağlar.
- Bazı global servislerin yönetimini kolaylaştırabilir.

<a id="48-singleton-dezavantajlari"></a>
### 4.8. Singleton Dezavantajları

Singleton'ın yaygın eleştirileri vardır. Özellikle:

- Global state oluşturabilir.
- Unit test yazmayı zorlaştırabilir.
- Sınıflar arasında gizli bağımlılık oluşturabilir.
- Çoklu thread ortamlarında dikkat gerektirir.
- Gereğinden fazla kullanılırsa kodun esnekliğini azaltabilir.

<a id="49-singleton-ne-zaman-kullanilmamali"></a>
### 4.9. Singleton Ne Zaman Kullanılmamalı?

Bir sınıfın gerçekten yalnızca tek instance olması gerekmiyorsa Singleton kullanılmamalıdır. Ayrıca yalnızca:

> "Her yerden erişmek istiyorum."

düşüncesi Singleton kullanmak için yeterli değildir. Bu durum çoğu zaman kötü tasarım belirtisi olabilir.

---

<a id="5-factory-pattern"></a>
## 5. Factory Pattern

Factory Pattern de Creational Pattern kategorisindedir. Factory'nin temel amacı nesne oluşturma sorumluluğunu doğrudan istemci kodundan ayırmaktır.

<a id="51-factory-nedir"></a>
### 5.1. Factory Nedir?

Factory Pattern, hangi sınıftan nesne oluşturulacağı kararını merkezi bir yapıya taşır. Normal kullanım:

```java
Car car = new Car();
```

Factory kullanımı:

```java
Vehicle vehicle = VehicleFactory.createVehicle("car");
```

Bu şekilde istemci kodu nesnenin nasıl oluşturulduğunu bilmek zorunda değildir.

<a id="52-factory-hangi-problemi-cozer"></a>
### 5.2. Factory Hangi Problemi Çözer?

Şöyle bir kod düşünelim:

```java
if (type.equals("email")) {
    EmailNotification notification =
        new EmailNotification();
}
else if (type.equals("sms")) {
    SmsNotification notification =
        new SmsNotification();
}
else if (type.equals("push")) {
    PushNotification notification =
        new PushNotification();
}
```

Bu kod uygulamanın birçok yerinde bulunursa bakım zorlaşır. Factory ile nesne oluşturma işlemi merkezi hale getirilir.

<a id="53-factory-mantigi"></a>
### 5.3. Factory Mantığı

Yapı:

```text
Client
   |
   v
Factory
   |
   |------ EmailNotification
   |
   |------ SmsNotification
   |
   └------ PushNotification
```

Client doğrudan gerçek sınıfları oluşturmaz.

<a id="54-java-ile-factory-ornegi"></a>
### 5.4. Java ile Factory Örneği

Önce ortak interface:

```java
public interface Notification {

    void send(String message);
}
```

Email:

```java
public class EmailNotification
        implements Notification {

    @Override
    public void send(String message) {
        System.out.println(
            "Email sent: " + message
        );
    }
}
```

SMS:

```java
public class SmsNotification
        implements Notification {

    @Override
    public void send(String message) {
        System.out.println(
            "SMS sent: " + message
        );
    }
}
```

Factory:

```java
public class NotificationFactory {

    public static Notification createNotification(
            String type) {

        if (type.equalsIgnoreCase("email")) {
            return new EmailNotification();
        }

        if (type.equalsIgnoreCase("sms")) {
            return new SmsNotification();
        }

        throw new IllegalArgumentException(
            "Unknown notification type"
        );
    }
}
```

Kullanım:

```java
Notification notification =
        NotificationFactory
            .createNotification("email");

notification.send("Order created.");
```

Client şu detayı bilmez:

```text
EmailNotification nesnesi nasıl oluşturuluyor?
```

Yalnızca ortak interface ile çalışır.

<a id="55-simple-factory-ve-factory-method-farki"></a>
### 5.5. Simple Factory ve Factory Method Farkı

Günlük kullanımda "Factory Pattern" denildiğinde çoğu zaman Simple Factory yapısı gösterilir. Simple Factory:

```text
Tek bir factory sınıfı
        ↓
Tür bilgisine göre nesne oluşturur
```

Factory Method Pattern'de ise nesne oluşturma davranışı alt sınıflara bırakılır. Örneğin:

```java
abstract class Dialog {

    public abstract Button createButton();

}
```

Alt sınıf:

```java
class WindowsDialog extends Dialog {

    @Override
    public Button createButton() {
        return new WindowsButton();
    }
}
```

Burada nesne oluşturma kararı alt sınıf tarafından verilir.

<a id="56-factory-kullanim-alanlari"></a>
### 5.6. Factory Kullanım Alanları

- Notification sistemleri
- Dosya formatı okuyucuları
- Veritabanı sürücüleri
- UI bileşenleri
- Payment provider oluşturma
- Parser sistemleri
- Platforma özel nesneler

<a id="57-factory-avantajlari"></a>
### 5.7. Factory Avantajları

- Nesne oluşturma mantığını merkezileştirir.
- Client ile concrete class arasındaki bağımlılığı azaltır.
- Yeni nesne türleri eklemeyi kolaylaştırır.
- Test edilebilirliği artırabilir.
- Kodun okunabilirliğini iyileştirir.

<a id="58-factory-dezavantajlari"></a>
### 5.8. Factory Dezavantajları

- Küçük projelerde gereksiz sınıf sayısı oluşturabilir.
- Basit bir nesne oluşturma işlemini gereğinden fazla soyutlayabilir.
- Hatalı tasarlanmış Factory zamanla büyük bir `switch-case` merkezine dönüşebilir.

---

<a id="6-strategy-pattern"></a>
## 6. Strategy Pattern

Strategy, Behavioral Design Pattern kategorisindedir. Aynı problemi çözmek için farklı algoritmalar bulunduğunda oldukça kullanışlıdır.

<a id="61-strategy-nedir"></a>
### 6.1. Strategy Nedir?

Strategy Pattern, bir işlemin farklı algoritmalarını ayrı sınıflara ayırır ve çalışma zamanında uygun algoritmanın seçilmesini sağlar. Örneğin:

```text
Ödeme
   |
   |------ Credit Card
   |------ PayPal
   |------ Bank Transfer
   └------ Crypto
```

Hepsi ödeme işlemi yapar ancak çalışma şekilleri farklıdır.

<a id="62-strategy-hangi-problemi-cozer"></a>
### 6.2. Strategy Hangi Problemi Çözer?

Strategy kullanılmadan önce:

```java
if (paymentType.equals("card")) {
    // kredi kartı işlemleri
}
else if (paymentType.equals("paypal")) {
    // paypal işlemleri
}
else if (paymentType.equals("bank")) {
    // banka işlemleri
}
```

Yeni ödeme yöntemi geldikçe bu blok büyür. Bu durum:

- Kodun okunmasını zorlaştırır.
- Testleri zorlaştırır.
- Open/Closed Principle'ı ihlal edebilir.
- Yeni özellik eklerken mevcut kodun değiştirilmesine neden olur.

<a id="63-strategy-yapisi"></a>
### 6.3. Strategy Yapısı

Genellikle üç bileşen vardır:

```text
Strategy Interface
        |
        |----- ConcreteStrategyA
        |----- ConcreteStrategyB
        └----- ConcreteStrategyC

Context
   |
   └── Strategy kullanır
```

<a id="64-java-ile-strategy-ornegi"></a>
### 6.4. Java ile Strategy Örneği

Strategy interface:

```java
public interface PaymentStrategy {

    void pay(double amount);

}
```

Kredi kartı:

```java
public class CreditCardPayment
        implements PaymentStrategy {

    @Override
    public void pay(double amount) {

        System.out.println(
            amount + " TL credit card payment"
        );

    }
}
```

PayPal:

```java
public class PaypalPayment
        implements PaymentStrategy {

    @Override
    public void pay(double amount) {

        System.out.println(
            amount + " TL PayPal payment"
        );

    }
}
```

Context:

```java
public class PaymentService {

    private PaymentStrategy strategy;

    public PaymentService(
            PaymentStrategy strategy) {

        this.strategy = strategy;
    }

    public void checkout(double amount) {

        strategy.pay(amount);

    }
}
```

Kullanım:

```java
PaymentStrategy strategy =
        new CreditCardPayment();

PaymentService paymentService =
        new PaymentService(strategy);

paymentService.checkout(1500);
```

Başka bir strategy:

```java
PaymentService paymentService =
        new PaymentService(
            new PaypalPayment()
        );
```

`PaymentService` sınıfını değiştirmeden algoritmayı değiştirmiş olduk.

<a id="65-if-else-yerine-strategy-kullanimi"></a>
### 6.5. if-else Yerine Strategy Kullanımı

Her `if-else` bloğu Strategy gerektirmez. Ancak şu durumlarda Strategy düşünülebilir:

- Aynı işlemin birçok farklı algoritması varsa,
- `switch-case` giderek büyüyorsa,
- Algoritmalar sık değişiyorsa,
- Her algoritmayı bağımsız test etmek istiyorsak.

Örneğin:

```text
Shipping Calculation
    |
    |---- Standard Shipping
    |---- Express Shipping
    |---- International Shipping
    └---- Same-Day Shipping
```

Bu yapı Strategy için uygundur.

<a id="66-strategy-kullanim-alanlari"></a>
### 6.6. Strategy Kullanım Alanları

- Ödeme sistemleri
- Kargo hesaplama
- İndirim algoritmaları
- Authentication yöntemleri
- Sıralama algoritmaları
- Compression yöntemleri
- Dosya işleme stratejileri
- Fiyatlandırma sistemleri

<a id="67-strategy-avantajlari"></a>
### 6.7. Strategy Avantajları

- Büyük koşul bloklarını azaltır.
- Algoritmaları bağımsız sınıflara ayırır.
- Yeni algoritma eklemeyi kolaylaştırır.
- Open/Closed Principle'a uygundur.
- Unit test yazmayı kolaylaştırır.

<a id="68-strategy-dezavantajlari"></a>
### 6.8. Strategy Dezavantajları

- Çok fazla küçük sınıf oluşabilir.
- Basit problemlerde gereksiz olabilir.
- Client bazen hangi Strategy'nin seçileceğini bilmek zorunda kalabilir.

---

<a id="7-observer-pattern"></a>
## 7. Observer Pattern

Observer Pattern, bir nesnedeki değişikliklerin diğer nesnelere otomatik olarak bildirilmesini sağlar. Behavioral Pattern kategorisindedir.

<a id="71-observer-nedir"></a>
### 7.1. Observer Nedir?

Observer Pattern'de temel olarak iki rol vardır:

```text
Subject / Publisher
Observer / Subscriber
```

Publisher'da bir değişiklik olduğunda subscriber'lara bildirim gönderilir.

<a id="72-observer-hangi-problemi-cozer"></a>
### 7.2. Observer Hangi Problemi Çözer?

Bir e-ticaret sisteminde sipariş oluşturulduğunda:

- Email gönderilebilir.
- SMS gönderilebilir.
- Stok güncellenebilir.
- Analytics kaydı oluşturulabilir.
- Mobil push notification gönderilebilir.

Sipariş servisi bütün bunları doğrudan çağırırsa:

```java
emailService.send();
smsService.send();
stockService.update();
analyticsService.track();
pushService.send();
```

OrderService çok fazla servise bağımlı hale gelir. Observer ile OrderService yalnızca:

```text
OrderCreated event
```

yayınlar. Diğer servisler bu olayı dinler.

<a id="73-publisher-subscriber-mantigi"></a>
### 7.3. Publisher-Subscriber Mantığı

Yapı:

```text
                ┌── Email Observer
Publisher ──────┼── SMS Observer
                ├── Analytics Observer
                └── Stock Observer
```

Publisher observer'ların ne yaptığını bilmek zorunda değildir. Yalnızca bildirim gönderir.

<a id="74-java-ile-observer-ornegi"></a>
### 7.4. Java ile Observer Örneği

Observer interface:

```java
public interface Subscriber {

    void update(String message);

}
```

Email subscriber:

```java
public class EmailSubscriber
        implements Subscriber {

    @Override
    public void update(String message) {

        System.out.println(
            "Email received: " + message
        );

    }
}
```

SMS subscriber:

```java
public class SmsSubscriber
        implements Subscriber {

    @Override
    public void update(String message) {

        System.out.println(
            "SMS received: " + message
        );

    }
}
```

Publisher:

```java
import java.util.ArrayList;
import java.util.List;

public class NewsPublisher {

    private List<Subscriber> subscribers =
            new ArrayList<>();

    public void subscribe(
            Subscriber subscriber) {

        subscribers.add(subscriber);
    }

    public void unsubscribe(
            Subscriber subscriber) {

        subscribers.remove(subscriber);
    }

    public void publish(String news) {

        for (Subscriber subscriber
                : subscribers) {

            subscriber.update(news);
        }
    }
}
```

Kullanım:

```java
NewsPublisher publisher =
        new NewsPublisher();

publisher.subscribe(
        new EmailSubscriber());

publisher.subscribe(
        new SmsSubscriber());

publisher.publish(
        "New product released!");
```

<a id="75-observer-kullanim-alanlari"></a>
### 7.5. Observer Kullanım Alanları

- GUI event sistemleri
- Notification sistemleri
- Event-driven architecture
- Message queue mantıkları
- Frontend state yönetimi
- Domain event'leri
- Stock price updates
- Chat uygulamaları
- Gerçek zamanlı dashboard'lar

JavaScript dünyasında event listener mantığı Observer'a çok benzer. Örneğin:

```javascript
button.addEventListener("click", () => {
    console.log("Clicked");
});
```

Burada event sistemi gözlemci mantığıyla çalışır.

<a id="76-observer-avantajlari"></a>
### 7.6. Observer Avantajları

- Loose coupling sağlar.
- Publisher subscriber'ın detaylarını bilmez.
- Yeni observer eklemek kolaydır.
- Event-driven sistemlerde esneklik sağlar.

<a id="77-observer-dezavantajlari"></a>
### 7.7. Observer Dezavantajları

- Çok fazla observer olduğunda akışı takip etmek zorlaşabilir.
- Bildirim sırası karmaşık olabilir.
- Observer kaldırılmazsa memory leak oluşabilir.
- Debug işlemleri zorlaşabilir.
- Senkron bildirimlerde performans problemleri oluşabilir.

---

<a id="8-adapter-pattern"></a>
## 8. Adapter Pattern

Adapter Structural Pattern kategorisindedir. Uyumsuz interface'lere sahip iki yapının birlikte çalışmasını sağlar.

<a id="81-adapter-nedir"></a>
### 8.1. Adapter Nedir?

Adapter, mevcut bir sınıfın interface'ini istemcinin beklediği interface'e dönüştürür. Yani:

```text
Client
   |
   v
Expected Interface
   |
   v
Adapter
   |
   v
Existing / Legacy System
```

<a id="82-adapter-hangi-problemi-cozer"></a>
### 8.2. Adapter Hangi Problemi Çözer?

Örneğin uygulamamız şu interface'i kullanıyor olabilir:

```java
interface PaymentGateway {

    void pay(double amount);

}
```

Yeni eklenen üçüncü parti servis ise:

```java
class LegacyBankApi {

    void makePayment(int amountInCents) {
        // ...
    }

}
```

İki interface uyumsuzdur. Uygulamadaki bütün kodu değiştirmek yerine Adapter yazılır.

<a id="83-gercek-hayat-benzetmesi"></a>
### 8.3. Gerçek Hayat Benzetmesi

Seyahat adaptörü Adapter Pattern için en iyi benzetmelerden biridir. Örneğin:

```text
Laptop şarj cihazı
        ↓
Avrupa priz standardı
        ↓
Adaptör
        ↓
İngiltere priz standardı
```

Adaptör cihazı değiştirmez. Sadece iki uyumsuz interface arasında dönüşüm sağlar.

<a id="84-java-ile-adapter-ornegi"></a>
### 8.4. Java ile Adapter Örneği

Uygulamanın beklediği interface:

```java
public interface PaymentGateway {

    void pay(double amount);

}
```

Eski servis:

```java
public class LegacyBankApi {

    public void makePayment(
            int amountInCents) {

        System.out.println(
            "Payment: "
            + amountInCents
            + " cents"
        );
    }
}
```

Adapter:

```java
public class BankAdapter
        implements PaymentGateway {

    private LegacyBankApi bankApi;

    public BankAdapter(
            LegacyBankApi bankApi) {

        this.bankApi = bankApi;
    }

    @Override
    public void pay(double amount) {

        int cents =
            (int) (amount * 100);

        bankApi.makePayment(cents);
    }
}
```

Kullanım:

```java
LegacyBankApi legacyApi =
        new LegacyBankApi();

PaymentGateway gateway =
        new BankAdapter(legacyApi);

gateway.pay(100.50);
```

Client yalnızca `PaymentGateway` interface'ini bilir. Legacy sistemin detaylarını bilmez.

<a id="85-object-adapter-ve-class-adapter"></a>
### 8.5. Object Adapter ve Class Adapter

Adapter iki temel şekilde uygulanabilir.

#### Object Adapter

Composition kullanır.

```text
Adapter
   |
   └── LegacyObject
```

Java'da en yaygın yöntem budur.

#### Class Adapter

Inheritance kullanır. Bazı dillerde multiple inheritance desteği gerektiği için her dilde uygun olmayabilir. Genellikle composition tabanlı Object Adapter daha esnek kabul edilir.

<a id="86-adapter-kullanim-alanlari"></a>
### 8.6. Adapter Kullanım Alanları

- Legacy sistem entegrasyonları
- Third-party API entegrasyonları
- Eski kütüphaneleri yeni sistemlere bağlama
- Payment provider entegrasyonları
- Dosya formatı dönüştürme
- Veritabanı sürücüsü uyumluluğu

<a id="87-adapter-avantajlari"></a>
### 8.7. Adapter Avantajları

- Mevcut kodu değiştirmeden entegrasyon sağlar.
- Legacy sistemlerin kullanılmaya devam etmesini sağlar.
- Client kodunu üçüncü parti sistemden ayırır.
- Değişiklik etkisini sınırlar.

<a id="88-adapter-dezavantajlari"></a>
### 8.8. Adapter Dezavantajları

- Ek sınıf oluşturur.
- Çok fazla adapter mimariyi karmaşıklaştırabilir.
- Bazı durumlarda tamamen yeni bir interface tasarlamak daha doğru olabilir.

---

<a id="9-decorator-pattern"></a>
## 9. Decorator Pattern

Decorator Pattern de Structural Pattern kategorisindedir. Bir nesnenin davranışını çalışma zamanında genişletmeyi sağlar.

<a id="91-decorator-nedir"></a>
### 9.1. Decorator Nedir?

Decorator, bir nesneyi başka bir nesneyle sararak ona ek özellikler kazandırır. Örneğin kahve sistemi:

```text
Coffee
   |
   + Milk
   |
   + Caramel
   |
   + Chocolate
```

Her kombinasyon için ayrı sınıf yazmak yerine decorator kullanılabilir.

<a id="92-decorator-hangi-problemi-cozer"></a>
### 9.2. Decorator Hangi Problemi Çözer?

Kalıtımla şöyle sınıflar oluşturulabilir:

```text
Coffee
MilkCoffee
CaramelCoffee
ChocolateCoffee
MilkCaramelCoffee
MilkChocolateCoffee
CaramelChocolateCoffee
MilkCaramelChocolateCoffee
```

Yeni özellikler geldikçe sınıf sayısı patlar. Bu duruma bazen **class explosion** denir. Decorator bu problemi composition ile çözer.

<a id="93-kalitim-yerine-composition"></a>
### 9.3. Kalıtım Yerine Composition

Decorator Pattern şu prensibi destekler:

> Favor composition over inheritance.

Yani davranışı yalnızca kalıtım yoluyla genişletmek yerine nesneleri birleştirerek davranış eklemek tercih edilebilir.

<a id="94-java-ile-decorator-ornegi"></a>
### 9.4. Java ile Decorator Örneği

Component interface:

```java
public interface Coffee {

    double getCost();

    String getDescription();

}
```

Temel kahve:

```java
public class BasicCoffee
        implements Coffee {

    @Override
    public double getCost() {
        return 50;
    }

    @Override
    public String getDescription() {
        return "Coffee";
    }
}
```

Decorator base class:

```java
public abstract class CoffeeDecorator
        implements Coffee {

    protected Coffee coffee;

    public CoffeeDecorator(
            Coffee coffee) {

        this.coffee = coffee;
    }
}
```

Milk decorator:

```java
public class MilkDecorator
        extends CoffeeDecorator {

    public MilkDecorator(
            Coffee coffee) {

        super(coffee);
    }

    @Override
    public double getCost() {

        return coffee.getCost() + 10;
    }

    @Override
    public String getDescription() {

        return coffee.getDescription()
                + ", Milk";
    }
}
```

Chocolate decorator:

```java
public class ChocolateDecorator
        extends CoffeeDecorator {

    public ChocolateDecorator(
            Coffee coffee) {

        super(coffee);
    }

    @Override
    public double getCost() {

        return coffee.getCost() + 15;
    }

    @Override
    public String getDescription() {

        return coffee.getDescription()
                + ", Chocolate";
    }
}
```

Kullanım:

```java
Coffee coffee = new BasicCoffee();
coffee = new MilkDecorator(coffee);
coffee = new ChocolateDecorator(coffee);

System.out.println(coffee.getDescription());
System.out.println(coffee.getCost());
```

Sonuç:

```text
Coffee, Milk, Chocolate
75
```

<a id="95-decorator-kullanim-alanlari"></a>
### 9.5. Decorator Kullanım Alanları

- UI component özellikleri
- Logging
- Cache katmanları
- Security
- Compression
- Encryption
- Stream işlemleri
- Middleware yapıları

Java'nın I/O sistemi Decorator Pattern için klasik örneklerden biridir. Örneğin:

```java
BufferedInputStream
DataInputStream
FileInputStream
```

gibi sınıflar birbirini sarabilir.

<a id="96-decorator-avantajlari"></a>
### 9.6. Decorator Avantajları

- Çalışma zamanında davranış eklenebilir.
- Çok sayıda alt sınıf oluşturma ihtiyacını azaltır.
- Open/Closed Principle'a uygundur.
- Composition kullanımını destekler.
- Özellikler kombinasyon halinde kullanılabilir.

<a id="97-decorator-dezavantajlari"></a>
### 9.7. Decorator Dezavantajları

- Çok fazla küçük decorator sınıfı oluşabilir.
- Nesnenin hangi katmanlarla sarıldığını takip etmek zorlaşabilir.
- Debug işlemleri karmaşıklaşabilir.

---

<a id="10-patternlerin-karsilastirilmasi"></a>
## 10. Pattern'lerin Karşılaştırılması

Pattern'ler bazen birbirine benzer görünse de farklı problemlere odaklanırlar.

<a id="101-singleton-vs-factory"></a>
### 10.1. Singleton vs Factory

Singleton:

```text
Kaç nesne oluşturulacak?
```

sorusuna odaklanır. Factory:

```text
Hangi nesne nasıl oluşturulacak?
```

sorusuna odaklanır.

<a id="102-strategy-vs-factory"></a>
### 10.2. Strategy vs Factory

Factory nesne oluşturur. Strategy davranış seçer. Örneğin:

```text
Factory
   ↓
Doğru PaymentStrategy nesnesini oluşturabilir
```

Daha sonra:

```text
Strategy
   ↓
Ödeme davranışını gerçekleştirir
```

Bu nedenle iki pattern birlikte kullanılabilir.

<a id="103-observer-vs-strategy"></a>
### 10.3. Observer vs Strategy

Strategy:

```text
Bir işlemi hangi algoritmayla yapacağım?
```

Observer:

```text
Bir olay olduğunda kimlere haber vereceğim?
```

sorusunu çözer.

<a id="104-adapter-vs-decorator"></a>
### 10.4. Adapter vs Decorator

Adapter:

```text
Interface'i uyumlu hale getirir.
```

Decorator:

```text
Davranışı genişletir.
```

Adapter'ın amacı uyumluluktur. Decorator'ın amacı yeni özellik eklemektir.

<a id="105-genel-karsilastirma-tablosu"></a>
### 10.5. Genel Karşılaştırma Tablosu

| Pattern | Kategori | Temel Amaç | Tipik Kullanım |
|---|---|---|---|
| Singleton | Creational | Tek instance oluşturmak | Logger, config |
| Factory | Creational | Nesne oluşturmayı soyutlamak | Notification, payment |
| Strategy | Behavioral | Algoritmayı değiştirilebilir yapmak | Ödeme, indirim |
| Observer | Behavioral | Değişiklikleri abonelere bildirmek | Event, notification |
| Adapter | Structural | Uyumsuz interface'leri bağlamak | Legacy API |
| Decorator | Structural | Nesneye dinamik davranış eklemek | UI, logging, streams |

---

<a id="11-design-patterns-ve-solid-iliskisi"></a>
## 11. Design Patterns ve SOLID İlişkisi

Design Patterns ve SOLID prensipleri birbirinden farklı kavramlardır ancak güçlü şekilde ilişkilidir. SOLID yazılım tasarımı için prensipler sunar. Design Patterns ise belirli problemlere yönelik tasarım çözümleri sunar. 

<a id="111-single-responsibility-principle"></a>
### 11.1. Single Responsibility Principle

Bir sınıfın yalnızca bir temel sorumluluğu olmalıdır. Örneğin Strategy Pattern'de her Strategy belirli bir algoritmadan sorumludur.

```text
CreditCardStrategy
    ↓
Kredi kartı ödeme işlemi
```

```text
PaypalStrategy
    ↓
PayPal ödeme işlemi
```

<a id="112-open-closed-principle"></a>
### 11.2. Open-Closed Principle

Yazılım bileşenleri:

```text
Extension'a açık
Modification'a kapalı
```

olmalıdır. Strategy ve Decorator bu prensiple güçlü şekilde ilişkilidir. Yeni Strategy eklenebilir:

```java
class CryptoPayment
    implements PaymentStrategy
```

Mevcut `PaymentService` değiştirilmez.

<a id="113-liskov-substitution-principle"></a>
### 11.3. Liskov Substitution Principle

Alt sınıflar veya implementasyonlar, temel interface'in yerine sorunsuz şekilde kullanılabilmelidir. Örneğin:

```java
PaymentStrategy strategy;
```

değişkenine:

```java
CreditCardPayment
PaypalPayment
BankPayment
```

atanabilmelidir.

<a id="114-interface-segregation-principle"></a>
### 11.4. Interface Segregation Principle

Büyük ve gereksiz interface'ler yerine küçük ve amaca yönelik interface'ler tercih edilmelidir. Örneğin:

```java
interface PaymentStrategy {
    void pay(double amount);
}
```

yalnızca ödeme davranışını tanımlar.

<a id="115-dependency-inversion-principle"></a>
### 11.5. Dependency Inversion Principle

Yüksek seviyeli modüller concrete class'lara değil abstraction'lara bağımlı olmalıdır. Kötü:

```java
CreditCardPayment payment =
        new CreditCardPayment();
```

Daha iyi:

```java
PaymentStrategy payment;
```

Bu prensip Strategy, Factory ve Adapter Pattern ile sıkça birlikte kullanılır.

---

<a id="12-junior-kod-ile-profesyonel-kod-arasindaki-fark"></a>
## 12. Junior Kod ile Profesyonel Kod Arasındaki Fark

Burada "junior kodu" ifadesi kötü kod yazan geliştirici anlamına gelmez. Daha çok deneyim kazandıkça geliştiricinin:

```text
Sadece çalışan kod
        ↓
Bakımı yapılabilir kod
        ↓
Esnek ve ölçeklenebilir kod
```

yazmaya başlamasını ifade eder.

<a id="121-buyuk-if-else-bloklari"></a>
### 12.1. Büyük if-else Blokları

Başlangıç seviyesinde:

```java
if (payment.equals("card")) {
    // ...
}
else if (payment.equals("paypal")) {
    // ...
}
else if (payment.equals("bank")) {
    // ...
}
else if (payment.equals("crypto")) {
    // ...
}
```

Profesyonel tasarımda:

```text
PaymentStrategy
    |
    |----- CardStrategy
    |----- PaypalStrategy
    |----- BankStrategy
    └----- CryptoStrategy
```

kullanılabilir.

<a id="122-siki-bagimlilik"></a>
### 12.2. Sıkı Bağımlılık

Başlangıç yaklaşımı:

```java
class OrderService {

    EmailService email =
        new EmailService();

}
```

OrderService doğrudan EmailService'e bağlıdır. Daha esnek yaklaşım:

```java
class OrderService {

    NotificationService
        notificationService;

}
```

Bu durumda farklı implementasyonlar kullanılabilir.

<a id="123-tek-sinifta-cok-fazla-sorumluluk"></a>
### 12.3. Tek Sınıfta Çok Fazla Sorumluluk

Kötü tasarım:

```text
OrderService
   |
   |-- Order oluştur
   |-- Payment yap
   |-- Email gönder
   |-- Invoice oluştur
   |-- Log yaz
   |-- Stock düş
```

Bu sınıfa bazen **God Class** denir. Daha iyi tasarım:

```text
OrderService
PaymentService
NotificationService
InvoiceService
StockService
LoggingService
```

Her servis belirli bir sorumluluk üstlenir.

<a id="124-tekrar-eden-kodlar"></a>
### 12.4. Tekrar Eden Kodlar

Başlangıç seviyesinde aynı iş mantığı birçok yerde tekrar edebilir. Profesyonel tasarımda ortak davranış:

- Service
- Helper
- Strategy
- Decorator
- Component

gibi yapılarla ayrılabilir.

<a id="125-profesyonel-kodun-ozellikleri"></a>
### 12.5. Profesyonel Kodun Özellikleri

Profesyonel kod genellikle şu özelliklere sahiptir:

- Okunabilir
- Test edilebilir
- Modüler
- Loose coupled
- High cohesion
- Genişletilebilir
- Değişikliklere dayanıklı
- Gereksiz tekrar içermeyen
- Sorumlulukları ayrılmış
- Soyutlamaları dengeli kullanan

Ancak önemli bir nokta vardır:

> Profesyonel kod, mümkün olan en fazla pattern'in kullanıldığı kod değildir.

Asıl amaç problemi en sade ve sürdürülebilir şekilde çözmektir.

---

<a id="13-design-pattern-kullanirken-yapilan-hatalar"></a>
## 13. Design Pattern Kullanırken Yapılan Hatalar

<a id="131-her-yerde-pattern-kullanmak"></a>
### 13.1. Her Yerde Pattern Kullanmak

Yeni pattern öğrenen geliştiriciler bazen her probleme pattern uygulamaya çalışır. Örneğin:

```text
Basit bir sınıf oluşturmak
```

için bile:

```text
Factory
Abstract Factory
Builder
Dependency Injection
```

kullanmak gereksiz olabilir. Bu durum kodu gereksiz yere karmaşıklaştırır.

<a id="132-patterni-ezberleyip-problemi-anlamamak"></a>
### 13.2. Pattern'i Ezberleyip Problemi Anlamamak

Pattern öğrenirken şu sorular sorulmalıdır:

```text
- Bu pattern hangi problemi çözüyor?
- Bu problem benim sistemimde gerçekten var mı? 
- Pattern kullanmazsam ne olur?
- Daha basit bir çözüm mümkün mü?
```

Kod şablonunu ezberlemek tek başına yeterli değildir.

<a id="133-gereksiz-soyutlama-yapmak"></a>
### 13.3. Gereksiz Soyutlama Yapmak

Her sınıf için interface oluşturmak da her zaman doğru değildir. Örneğin:

```text
UserService
IUserService
UserServiceImpl
UserServiceFactory
UserServiceManager
```

gibi yapılar küçük bir uygulamada gereksiz olabilir. Soyutlama ihtiyaç oldukça yapılmalıdır.

<a id="134-overengineering"></a>
### 13.4. Overengineering

Overengineering, basit bir probleme gereğinden karmaşık bir çözüm üretmektir. Örneğin:

```text
Problem:
Bir butona tıklanınca mesaj göster.
```

Bunun için 10 sınıflı bir event architecture tasarlamak gereksiz olabilir. İyi yazılım tasarımının temel prensiplerinden biri:

> Gerektiği kadar karmaşıklık.

---

<a id="14-design-pattern-secerken-nasil-dusunulmeli"></a>
## 14. Design Pattern Seçerken Nasıl Düşünülmeli?

Pattern seçerken önce probleme bakılmalıdır.

### Problem 1

```text
Bir sınıftan yalnızca tek instance lazım.
```

Muhtemel pattern:

```text
Singleton
```

### Problem 2

```text
Hangi concrete object'in oluşturulacağını client bilmesin.
```

Muhtemel pattern:

```text
Factory
```

### Problem 3

```text
Aynı işlemin farklı algoritmaları var.
```

Muhtemel pattern:

```text
Strategy
```

### Problem 4

```text
Bir değişiklik olduğunda birçok sistem haberdar olmalı.
```

Muhtemel pattern:

```text
Observer
```

### Problem 5

```text
Third-party sistemin interface'i bizim sisteme uymuyor.
```

Muhtemel pattern:

```text
Adapter
```

### Problem 6

```text
Bir nesneye çalışma zamanında farklı özellikler eklemek istiyorum.
```

Muhtemel pattern:

```text
Decorator
```

Pattern seçiminde en önemli yaklaşım:

```text
Önce problem
    ↓
Sonra tasarım
    ↓
Sonra pattern
```

olmalıdır. Yanlış yaklaşım:

```text
Pattern öğrendim
    ↓
Nerede kullanabilirim?
```

---

<a id="15-gercek-projelerde-birlikte-kullanim-senaryosu"></a>
## 15. Gerçek Projelerde Birlikte Kullanım Senaryosu

Design Pattern'ler gerçek projelerde genellikle tek başına kullanılmaz. Bir e-ticaret uygulaması düşünelim.

### Factory

Kullanıcının ödeme seçimine göre uygun Strategy oluşturabilir.

```text
PaymentFactory
    |
    |---- CreditCardStrategy
    |---- PaypalStrategy
    └---- BankStrategy
```

### Strategy

Seçilen ödeme algoritmasını çalıştırır.

```text
PaymentService
     |
     └── PaymentStrategy
```

### Observer

Ödeme başarılı olduğunda:

```text
PaymentSuccessEvent
        |
        |---- EmailService
        |---- InvoiceService
        |---- AnalyticsService
        └---- StockService
```

çalışabilir.

### Adapter

Harici banka sistemi farklı interface kullanıyorsa:

```text
BankApiAdapter
```

kullanılabilir.

### Decorator

Payment işlemine ek davranışlar eklenebilir:

```text
Payment
   ↓
LoggingDecorator
   ↓
SecurityDecorator
   ↓
RetryDecorator
```

### Singleton

Uygulama genelindeki configuration yöneticisi tek instance olabilir.

```text
ConfigurationManager
```

Bu senaryoda farklı pattern'ler birlikte çalışarak sistemin daha esnek ve modüler hale gelmesini sağlar.

---

<a id="16-mulakatlarda-sorulabilecek-sorular"></a>
## 16. Mülakatlarda Sorulabilecek Sorular

### 1. Design Pattern nedir?

Tekrar eden yazılım tasarımı problemleri için kullanılan genel ve denenmiş çözüm yaklaşımlarıdır.

### 2. Design Pattern neden kullanılır?

Kodun:

- Bakımını kolaylaştırmak,
- Esnekliğini artırmak,
- Bağımlılıkları azaltmak,
- Yeniden kullanılabilirliği artırmak,
- Ortak tasarım dili oluşturmak

için kullanılır.

### 3. Singleton Pattern nedir?

Bir sınıftan yalnızca tek instance oluşturulmasını sağlayan Creational Pattern'dir.

### 4. Singleton'ın dezavantajları nelerdir?

- Global state oluşturabilir.
- Testleri zorlaştırabilir.
- Gizli bağımlılık oluşturabilir.
- Thread safety problemi oluşturabilir.

### 5. Factory Pattern nedir?

Nesne oluşturma sorumluluğunu client koddan ayıran Creational Pattern'dir.

### 6. Strategy Pattern ne zaman kullanılır?

Aynı işlemin birden fazla algoritması olduğunda ve bu algoritmalar çalışma zamanında değiştirilebildiğinde kullanılır.

### 7. Strategy Pattern'in avantajı nedir?

Büyük `if-else` bloklarını azaltır ve algoritmaları bağımsız sınıflara ayırır.

### 8. Observer Pattern nedir?

Bir nesnedeki değişikliğin birden fazla bağlı nesneye otomatik olarak bildirilmesini sağlayan Behavioral Pattern'dir.

### 9. Observer Pattern nerede kullanılır?

- Event sistemleri
- Notification sistemleri
- GUI
- State management
- Event-driven architecture

### 10. Adapter Pattern nedir?

Uyumsuz iki interface'in birlikte çalışmasını sağlayan Structural Pattern'dir.

### 11. Adapter ve Decorator farkı nedir?

- Adapter interface uyumluluğunu sağlar.
- Decorator nesneye yeni davranış ekler.

### 12. Decorator neden inheritance yerine kullanılabilir?

Çünkü çalışma zamanında dinamik özellik eklemeyi sağlar ve çok sayıda alt sınıf oluşmasını önler.

### 13. Strategy ve Factory birlikte kullanılabilir mi?

Evet. Factory doğru Strategy nesnesini oluşturabilir, Strategy ise davranışı gerçekleştirir.

### 14. Design Pattern kullanmak her zaman gerekli midir?

Hayır. Pattern yalnızca gerçek bir tasarım problemi varsa kullanılmalıdır.

### 15. Overengineering nedir?

Basit bir problemi gereğinden fazla sınıf, abstraction ve mimari katman kullanarak çözmeye çalışmaktır.

---

<a id="17-kisa-ozet"></a>
## 17. Kısa Özet

Bu raporda incelenen pattern'ler:

### Singleton

```text
Amaç: Tek instance oluşturmak.
```

### Factory

```text
Amaç: Nesne oluşturmayı soyutlamak.
```

### Strategy

```text
Amaç: Algoritmaları değiştirilebilir hale getirmek.
```

### Observer

```text
Amaç: Bir olaydan birçok nesneyi haberdar etmek.
```

### Adapter

```text
Amaç: Uyumsuz interface'leri birlikte çalıştırmak.
```

### Decorator

```text
Amaç: Nesneye dinamik davranış eklemek.
```

Akılda tutulabilecek kısa form:

```text
Singleton → Tek nesne
Factory → Nesne üretimi
Strategy → Algoritma seçimi
Observer → Olay bildirimi
Adapter → Uyumluluk
Decorator → Özellik ekleme
```

---

<a id="18-genel-sonuc"></a>
## 18. Genel Sonuç

Design Patterns, profesyonel yazılım geliştirmede önemli bir tasarım bilgisidir. Ancak tasarım desenlerini öğrenmenin amacı mümkün olduğunca fazla pattern kullanmak değildir. Asıl amaç:

```text
Problemi doğru tanımak
        ↓
Bağımlılıkları yönetmek
        ↓
Sorumlulukları ayırmak
        ↓
Değişikliklere dayanıklı kod yazmak
        ↓
Bakımı kolaylaştırmak
```

olmalıdır. Başlangıç seviyesinde geliştirici çoğu zaman:

```text
"Bu kod çalışıyor mu?"
```

sorusuna odaklanır. Deneyim arttıkça şu sorular da önem kazanır:

```text
Bu kod okunabilir mi?
- Yeni özellik kolay eklenebilir mi?
- Bir değişiklik kaç sınıfı etkiliyor?
- Bu sınıfın sorumluluğu gerçekten tek mi?
- Bu kod test edilebilir mi?
- Sınıflar birbirine gereğinden fazla bağlı mı?
- Altı ay sonra bu kodu değiştirmek kolay olacak mı?
```

İşte Design Patterns tam olarak bu noktada önem kazanır. Tasarım desenleri, geliştiricinin yalnızca **kod yazmasını** değil, aynı zamanda **yazılım tasarlamasını** sağlar. Bu nedenle Singleton, Factory, Strategy, Observer, Adapter ve Decorator gibi pattern'leri öğrenmek; yalnızca sınav veya mülakat açısından değil, gerçek projelerde sürdürülebilir ve profesyonel yazılım geliştirebilmek açısından da büyük önem taşır.
