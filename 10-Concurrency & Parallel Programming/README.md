# 12) Concurrency & Parallel Programming

Concurrency ve parallel programming, bir yazılımın aynı anda birden fazla işle ilgilenebilmesini sağlayan programlama yaklaşımlarıdır. Özellikle çok çekirdekli işlemcilerde performansı artırmak, uzun süren işlemlerin uygulamayı dondurmasını önlemek ve ortak kaynakları güvenli biçimde kullanmak için önemlidir.

Bu konuyu anlayabilmek için önce **process**, **thread** ve **shared resource** kavramlarını bilmek gerekir.

## İçindekiler

- [1. Process ve Thread Kavramları](#1-process-ve-thread-kavramları)
- [2. Concurrency Nedir?](#2-concurrency-nedir)
- [3. Parallelism Nedir?](#3-parallelism-nedir)
- [4. Concurrency ve Parallelism Arasındaki Fark](#4-concurrency-ve-parallelism-arasındaki-fark)
- [5. I/O-Bound ve CPU-Bound İşlemler](#5-io-bound-ve-cpu-bound-işlemler)
- [6. Shared Resource Nedir?](#6-shared-resource-nedir)
- [7. Race Condition Nedir?](#7-race-condition-nedir)
- [8. Race Condition İçin Banka Hesabı Örneği](#8-race-condition-için-banka-hesabı-örneği)
- [9. Critical Section Nedir?](#9-critical-section-nedir)
- [10. Atomic İşlem Nedir?](#10-atomic-işlem-nedir)
- [11. Mutex Nedir?](#11-mutex-nedir)
- [12. Lock Nedir?](#12-lock-nedir)
- [13. Lock Türleri](#13-lock-türleri)
- [14. Semaphore Nedir?](#14-semaphore-nedir)
- [15. Semaphore Türleri](#15-semaphore-türleri)
- [16. Semaphore İçin Gerçek Hayat Örneği](#16-semaphore-için-gerçek-hayat-örneği)
- [17. Mutex ve Semaphore Arasındaki Fark](#17-mutex-ve-semaphore-arasındaki-fark)
- [18. Mutex, Semaphore ve Lock Karşılaştırması](#18-mutex-semaphore-ve-lock-karşılaştırması)
- [19. Synchronization Nedir?](#19-synchronization-nedir)
- [20. Thread-Safe Ne Demektir?](#20-thread-safe-ne-demektir)
- [21. Deadlock Nedir?](#21-deadlock-nedir)
- [22. Starvation Nedir?](#22-starvation-nedir)
- [23. Livelock Nedir?](#23-livelock-nedir)
- [24. Lock Kullanımının Performansa Etkisi](#24-lock-kullanımının-performansa-etkisi)
- [25. Fine-Grained ve Coarse-Grained Locking](#25-fine-grained-ve-coarse-grained-locking)
- [26. Producer–Consumer Problemi](#26-producerconsumer-problemi)
- [27. Concurrency Her Zaman Performansı Artırır mı?](#27-concurrency-her-zaman-performansı-artırır-mı)
- [28. Parallelism Her Programı Hızlandırır mı?](#28-parallelism-her-programı-hızlandırır-mı)
- [29. Concurrency Problemlerinin Bulunması Neden Zordur?](#29-concurrency-problemlerinin-bulunması-neden-zordur)
- [30. Güvenli Concurrency İçin Temel Kurallar](#30-güvenli-concurrency-için-temel-kurallar)
- [31. Thread Pool Nedir?](#31-thread-pool-nedir)
- [32. Concurrency Kullanım Alanları](#32-concurrency-kullanım-alanları)
- [33. Parallel Programming Kullanım Alanları](#33-parallel-programming-kullanım-alanları)
- [34. Sıralı, Concurrent ve Parallel Çalışma Karşılaştırması](#34-sıralı-concurrent-ve-parallel-çalışma-karşılaştırması)
- [35. Concurrency ile Asynchronous Programming Aynı Şey mi?](#35-concurrency-ile-asynchronous-programming-aynı-şey-mi)
- [36. Temel Kavramların Kısa Özeti](#36-temel-kavramların-kısa-özeti)
- [37. Genel Sonuç](#37-genel-sonuç)

---

## 1. Process ve Thread Kavramları

### Process nedir?

Process, çalışmakta olan bir programdır.

Örneğin bilgisayarda:

* Google Chrome
* Spotify
* Visual Studio Code
* Discord

uygulamalarını açtığında her biri işletim sistemi tarafından bir veya daha fazla process olarak çalıştırılır.

Her process genellikle kendisine ait:

* Bellek alanına
* Değişkenlere
* Dosya tanımlayıcılarına
* Sistem kaynaklarına

sahiptir.

Bir process başka bir processin belleğine doğrudan erişemez. Bu nedenle processler arasında veri paylaşımı threadlere göre daha güvenli, ancak daha maliyetlidir.

---

### Thread nedir?

Thread, bir process içerisinde çalışan en küçük yürütme birimidir.

Bir process içinde birden fazla thread bulunabilir.

Örneğin bir müzik uygulamasında:

* Bir thread müziği çalabilir.
* Bir thread kullanıcı arayüzünü yönetebilir.
* Bir thread internetten yeni şarkı bilgilerini indirebilir.
* Bir thread çalma listesini kaydedebilir.

Bu threadlerin tamamı aynı uygulamanın, yani aynı processin içinde çalışır.

Threadler aynı process içerisinde oldukları için şu kaynakları paylaşabilir:

* Global değişkenler
* Heap belleği
* Açık dosyalar
* Veritabanı bağlantıları
* Nesneler
* Koleksiyonlar

Bu paylaşım performans açısından avantaj sağlar. Ancak aynı veriye birden fazla thread aynı anda eriştiğinde ciddi hatalar ortaya çıkabilir.

İşte concurrency programming konusunun temel problemi budur:

> Birden fazla thread aynı kaynağı kullanırken verinin bozulmasını nasıl engelleriz?

---

# 2. Concurrency Nedir?

**Concurrency**, bir sistemin aynı zaman aralığında birden fazla işle ilgilenebilmesidir.

Burada işlemlerin tam olarak aynı anda çalışması zorunlu değildir. İşletim sistemi işlemler arasında çok hızlı geçiş yapabilir.

Örneğin tek çekirdekli bir işlemcide iki görev bulunduğunu düşünelim:

* Görev A
* Görev B

İşlemci şu şekilde çalışabilir:

```text
A çalışır
B çalışır
A çalışır
B çalışır
A çalışır
```

İşlemci görevler arasında çok hızlı geçiş yaptığı için kullanıcı iki işlem aynı anda çalışıyormuş gibi hisseder.

Bu geçiş işlemine **context switching** denir.

---

## Context Switching Nedir?

Context switching, işlemcinin bir thread veya processi geçici olarak durdurup başka bir thread veya processi çalıştırmasıdır.

İşletim sistemi bir threadi durdurduğunda o threade ait bazı bilgileri saklar:

* Program sayacı
* CPU register değerleri
* Çalışma durumu
* Stack bilgileri

Daha sonra thread tekrar çalıştırılacağı zaman bu bilgiler geri yüklenir.

Context switching concurrency sağlar. Ancak tamamen ücretsiz değildir. Her geçişte işlemci ek iş yapmak zorunda kalır.

Bu nedenle çok fazla thread oluşturmak her zaman performansı artırmaz. Tam tersine, aşırı thread kullanımı context switching maliyetini artırarak sistemi yavaşlatabilir.

---

## Günlük Hayattan Concurrency Örneği

Bir aşçının aynı anda birkaç yemek hazırladığını düşünelim.

Aşçı:

1. Çorbayı ocağa koyar.
2. Çorba kaynarken salatayı hazırlar.
3. Salatayı bırakıp fırındaki yemeği kontrol eder.
4. Tekrar çorbaya döner.

Burada tek bir aşçı vardır. Aşçı aynı anda fiziksel olarak iki işlem yapmaz, fakat görevler arasında geçiş yaparak birden fazla işi ilerletir.

Bu durum **concurrency** örneğidir.

---

# 3. Parallelism Nedir?

**Parallelism**, birden fazla işlemin gerçekten aynı anda çalışmasıdır.

Bunun gerçekleşebilmesi için genellikle birden fazla işlemci çekirdeği gerekir.

Örneğin dört çekirdekli bir işlemcide:

```text
Çekirdek 1 → Görev A
Çekirdek 2 → Görev B
Çekirdek 3 → Görev C
Çekirdek 4 → Görev D
```

Görevler aynı anda fiziksel olarak yürütülebilir.

---

## Günlük Hayattan Parallelism Örneği

Bir restoranda dört aşçı olduğunu düşünelim:

* Birinci aşçı çorbayı yapıyor.
* İkinci aşçı salatayı hazırlıyor.
* Üçüncü aşçı tatlıyı hazırlıyor.
* Dördüncü aşçı ana yemeği pişiriyor.

Burada görevler gerçekten aynı anda gerçekleştirilmektedir.

Bu durum **parallelism** örneğidir.

---

# 4. Concurrency ve Parallelism Arasındaki Fark

| Özellik                              | Concurrency                               | Parallelism                                  |
| ------------------------------------ | ----------------------------------------- | -------------------------------------------- |
| Temel amaç                           | Birden fazla görevi yönetmek              | Birden fazla görevi aynı anda çalıştırmak    |
| Aynı anda çalışma zorunlu mu?        | Hayır                                     | Evet                                         |
| Tek çekirdekte mümkün mü?            | Evet                                      | Gerçek anlamda hayır                         |
| Context switching kullanılabilir mi? | Evet                                      | Kullanılabilir ancak temel şart değildir     |
| Odak noktası                         | İşlerin organizasyonu                     | İşlerin hızlandırılması                      |
| Örnek                                | Tek aşçının farklı yemeklerle ilgilenmesi | Birden fazla aşçının aynı anda yemek yapması |

Concurrency şu soruya cevap verir:

> Birden fazla işi nasıl düzenli şekilde yürütebilirim?

Parallelism ise şu soruya cevap verir:

> Bir işi veya birden fazla işi birden fazla çekirdeğe dağıtarak nasıl hızlandırabilirim?

---

## Concurrency Var, Parallelism Yok Örneği

Tek çekirdekli bilgisayarda:

* Müzik çalıyor.
* Dosya indiriliyor.
* Kullanıcı arayüzü çalışıyor.

İşlemci görevler arasında geçiş yapar. Birden fazla görev ilerler ancak fiziksel olarak aynı anda yalnızca biri çalışır.

Bu concurrency'dir, fakat gerçek parallelism değildir.

---

## Hem Concurrency Hem Parallelism Örneği

Dört çekirdekli bir bilgisayarda:

* Bir çekirdek video işliyor.
* Bir çekirdek ses işliyor.
* Bir çekirdek kullanıcı arayüzünü çalıştırıyor.
* Bir çekirdek dosya kaydediyor.

Burada sistem hem birden fazla işi yönetmekte hem de görevleri aynı anda çalıştırmaktadır.

---

# 5. I/O-Bound ve CPU-Bound İşlemler

Concurrency ve parallelism kullanımını doğru seçebilmek için işlemlerin türünü bilmek önemlidir.

## I/O-Bound İşlem

I/O-bound işlemler, işlemciden çok dış kaynakları bekleyen işlemlerdir.

Örnekler:

* İnternetten veri indirmek
* API isteği göndermek
* Dosya okumak
* Veritabanı sorgusu yapmak
* Kullanıcı girişini beklemek

Bu işlemlerde thread çoğu zaman işlem yapmak yerine bekler.

Concurrency kullanıldığında bir görev beklerken diğer görev çalıştırılabilir.

Örneğin:

```text
Görev A → API cevabını bekliyor
Görev B → Dosya okuyor
Görev C → Kullanıcı arayüzünü güncelliyor
```

I/O-bound uygulamalarda concurrency genellikle oldukça faydalıdır.

---

## CPU-Bound İşlem

CPU-bound işlemler, işlemciyi yoğun şekilde kullanan işlemlerdir.

Örnekler:

* Görüntü işleme
* Video dönüştürme
* Makine öğrenmesi hesaplamaları
* Büyük matris işlemleri
* Şifreleme
* Karmaşık matematiksel hesaplamalar

Bu işlemlerde parallelism kullanılarak hesaplamalar birden fazla çekirdeğe dağıtılabilir.

Örneğin bir görüntünün dört parçaya ayrılıp her parçanın ayrı bir çekirdekte işlenmesi mümkündür.

---

# 6. Shared Resource Nedir?

**Shared resource**, birden fazla thread veya process tarafından kullanılan ortak kaynaktır.

Örnekler:

* Ortak değişken
* Dosya
* Veritabanı kaydı
* Yazıcı
* Bellekteki liste
* Banka hesabı bakiyesi
* Stok miktarı
* Sayaç

Örneğin iki thread aynı `counter` değişkenini artırmaya çalışabilir:

```text
counter = 10
```

Thread A:

```text
counter değerini oku
1 ekle
geri yaz
```

Thread B de aynı işlemi yapar.

Dışarıdan bakıldığında iki thread `counter` değerini artırdığı için sonucun `12` olması beklenir. Ancak bazı durumlarda sonuç `11` olabilir.

Bu durumun nedeni **race condition** problemidir.

---

# 7. Race Condition Nedir?

**Race condition**, bir programın sonucunun birden fazla thread veya processin çalışma sırasına bağlı olarak değişmesidir.

Başka bir ifadeyle:

> Birden fazla yürütme birimi aynı ortak veriye kontrolsüz şekilde eriştiğinde, sonucun hangi işlemin önce tamamlandığına bağlı hâle gelmesidir.

Race condition sonucunda:

* Veriler kaybolabilir.
* Sayaçlar yanlış hesaplanabilir.
* Para veya stok miktarı yanlış olabilir.
* Dosyalar bozulabilir.
* Program bazen doğru, bazen hatalı çalışabilir.
* Tekrar üretilmesi zor hatalar oluşabilir.

---

## Race Condition Örneği

Başlangıçta:

```text
counter = 10
```

İki thread şu işlemi gerçekleştirsin:

```text
counter = counter + 1
```

Bu ifade tek bir işlem gibi görünse de işlemci açısından genellikle üç aşamadan oluşur:

```text
1. counter değerini oku
2. Değere 1 ekle
3. Yeni değeri counter'a yaz
```

### Hatalı çalışma sırası

```text
Thread A counter değerini okur → 10
Thread B counter değerini okur → 10

Thread A 1 ekler → 11
Thread B 1 ekler → 11

Thread A counter'a 11 yazar
Thread B counter'a 11 yazar
```

Sonuç:

```text
counter = 11
```

Oysa iki artırma işlemi yapıldığı için doğru sonuç:

```text
counter = 12
```

olmalıydı.

Threadlerden birinin yaptığı güncelleme kaybolmuştur. Buna bazen **lost update**, yani kayıp güncelleme problemi denir.

---

# 8. Race Condition İçin Banka Hesabı Örneği

Bir banka hesabında `1000 TL` olduğunu düşünelim.

Aynı anda iki para çekme işlemi yapılsın:

* Thread A: 700 TL çekmek istiyor.
* Thread B: 500 TL çekmek istiyor.

İki thread de hesabı aynı anda okursa:

```text
Thread A bakiye = 1000 olarak okur.
Thread B bakiye = 1000 olarak okur.
```

İki thread de bakiyenin yeterli olduğunu düşünür.

Sonrasında:

```text
Thread A → 1000 - 700 = 300
Thread B → 1000 - 500 = 500
```

İşlemlerin sırasına göre son bakiye `300` veya `500` olabilir.

Gerçekte toplam `1200 TL` çekilmeye çalışılmıştır. Hesapta yalnızca `1000 TL` vardır. Buna rağmen kontrolsüz erişim nedeniyle iki işlem de başarılı olabilir.

Bu, finansal sistemlerde son derece ciddi bir race condition örneğidir.

---

# 9. Critical Section Nedir?

**Critical section**, ortak bir kaynağa erişen ve aynı anda yalnızca bir thread tarafından çalıştırılması gereken kod bölümüdür.

Örneğin:

```text
Bakiyeyi oku
Bakiyenin yeterli olup olmadığını kontrol et
Parayı bakiyeden düş
Yeni bakiyeyi kaydet
```

Bu dört işlem tek bir bütün olarak korunmalıdır.

Sadece parayı düşme işlemini korumak yeterli değildir. Çünkü kontrol ve güncelleme işlemlerinin tamamının atomik bir bütün gibi davranması gerekir.

---

## Critical Section İçin Temel Kural

Bir thread critical section içerisindeyken başka bir thread aynı critical sectiona girmemelidir.

Bu özelliğe **mutual exclusion**, yani karşılıklı dışlama denir.

Mutual exclusion sağlamak için çoğunlukla:

* Mutex
* Lock
* Semaphore
* Monitor
* Atomic işlemler

kullanılır.

---

# 10. Atomic İşlem Nedir?

**Atomic işlem**, bölünemeyen ve başka bir thread tarafından yarıda kesilmiş gibi gözlemlenemeyen işlemdir.

Atomic bir işlem ya tamamen gerçekleşir ya da hiç gerçekleşmez.

Örneğin teorik olarak aşağıdaki işlemin atomik olduğunu düşünelim:

```text
counter değerini 1 artır
```

Başka bir thread bu işlemin ortasında çalışamaz.

Ancak yüksek seviyeli programlama dillerinde yazılan basit bir ifade her zaman atomik değildir.

Örneğin:

```c
counter++;
```

tek satır olmasına rağmen arka planda okuma, artırma ve yazma adımlarından oluşabilir.

Bu nedenle:

> Kodun tek satır olması, işlemin atomik olduğu anlamına gelmez.

---

# 11. Mutex Nedir?

**Mutex**, “Mutual Exclusion” ifadesinden gelir.

Mutex, aynı ortak kaynağa aynı anda yalnızca bir threadin erişmesini sağlayan senkronizasyon aracıdır.

Bir mutex iki temel duruma sahiptir:

* Kilitli
* Kilitsiz

Bir thread ortak kaynağa erişmek istediğinde mutexi kilitler.

```text
lock mutex
critical section çalıştır
unlock mutex
```

Mutex başka bir thread tarafından kilitliyse, diğer thread genellikle beklemek zorunda kalır.

---

## Mutex Çalışma Mantığı

Başlangıçta mutex boştur:

```text
Mutex → Kilitsiz
```

Thread A gelir:

```text
Thread A mutexi kilitler.
Thread A critical sectiona girer.
```

Bu sırada Thread B gelir:

```text
Thread B mutexi kilitlemek ister.
Mutex Thread A'da olduğu için Thread B bekler.
```

Thread A işlemini bitirir:

```text
Thread A mutexin kilidini açar.
```

Daha sonra Thread B devam eder:

```text
Thread B mutexi kilitler.
Thread B critical sectiona girer.
```

Böylece iki thread aynı ortak veriyi aynı anda değiştiremez.

---

## Mutex ile Sayaç Örneği

Korumasız yapı:

```text
counter = counter + 1
```

Mutex ile korunan yapı:

```text
mutex.lock()

counter = counter + 1

mutex.unlock()
```

Bu durumda yalnızca bir thread sayaç değerini okuyup değiştirebilir.

---

## Mutexin Sahiplik Özelliği

Mutexin önemli bir özelliği **ownership**, yani sahipliktir.

Mutexi hangi thread kilitlediyse genellikle kilidi de o thread açmalıdır.

Örneğin:

```text
Thread A mutexi kilitledi.
Thread B mutexin kilidini açamaz.
```

Bu özellik mutexi semaphoredan ayıran önemli noktalardan biridir.

---

## Mutexin Avantajları

* Race condition problemini önler.
* Ortak veriyi güvenli hâle getirir.
* Critical sectiona tek thread girişini sağlar.
* Kullanımı ve mantığı görece kolaydır.

## Mutexin Dezavantajları

* Threadlerin beklemesine neden olabilir.
* Fazla kullanılırsa performansı düşürebilir.
* Yanlış sırada kilitleme deadlock oluşturabilir.
* Kilit açılmadan hata oluşursa diğer threadler sonsuza kadar bekleyebilir.

---

# 12. Lock Nedir?

**Lock**, ortak kaynaklara erişimi kontrol eden genel bir kilitleme mekanizmasıdır.

Mutex belirli bir senkronizasyon aracı iken lock daha genel bir kavramdır.

Programlama dillerinde lock farklı şekillerde karşımıza çıkabilir:

* `mutex.lock()`
* Java'da `synchronized`
* C#'ta `lock`
* Python'da `threading.Lock`
* C++'ta `std::mutex`
* Java'da `ReentrantLock`

Dolayısıyla şu ilişki kurulabilir:

> Mutex bir lock türüdür; fakat her lock yapısı mutlaka klasik mutex olmak zorunda değildir.

---

## Lock Kullanım Mantığı

Genel kullanım:

```text
lock.acquire()

critical section

lock.release()
```

Daha güvenli yapı:

```text
lock.acquire()

try:
    critical section
finally:
    lock.release()
```

`finally` kullanılmasının nedeni, critical section içinde hata oluşsa bile kilidin serbest bırakılmasını sağlamaktır.

Bazı diller otomatik kilit yönetimi sunar.

Python benzeri yapı:

```python
with lock:
    counter += 1
```

Bu yapı tamamlandığında lock otomatik olarak serbest bırakılır.

---

# 13. Lock Türleri

## 13.1. Exclusive Lock

Exclusive lock kullanıldığında aynı kaynağa yalnızca tek bir thread erişebilir.

Mutex mantığına benzer.

```text
Thread A → Yazma yapıyor
Thread B → Bekliyor
Thread C → Bekliyor
```

---

## 13.2. Read Lock

Birden fazla thread yalnızca okuma yapıyorsa aynı anda kaynağa erişebilir.

Çünkü okuma işlemleri veriyi değiştirmez.

```text
Thread A → Okuyor
Thread B → Okuyor
Thread C → Okuyor
```

Üç thread aynı anda çalışabilir.

---

## 13.3. Write Lock

Bir thread veri yazarken başka hiçbir threadin veriyi okumasına veya yazmasına izin verilmez.

```text
Thread A → Yazıyor
Thread B → Okumak için bekliyor
Thread C → Yazmak için bekliyor
```

Bu yapı genellikle **read-write lock** içerisinde kullanılır.

---

## 13.4. Reentrant Lock

Bir threadin aynı locku birden fazla kez almasına izin veren kilit türüdür.

Normal bir lockta thread aynı kilidi tekrar almaya çalışırsa kendisini beklemeye alabilir.

Reentrant lock, aynı threadin kilidi tekrar alabilmesini sağlar. Ancak kilit kaç kez alındıysa o kadar kez bırakılması gerekir.

---

## 13.5. Spinlock

Spinlock kullanan thread, kilit boşalana kadar uyumak yerine sürekli kontrol yapar:

```text
Kilit boş mu?
Hayır.
Kilit boş mu?
Hayır.
Kilit boş mu?
Evet.
```

Bu durum CPU tüketir.

Kritik bölüm çok kısa sürecekse spinlock faydalı olabilir. Ancak uzun süre bekleme varsa işlemciyi gereksiz yere meşgul eder.

---

# 14. Semaphore Nedir?

**Semaphore**, aynı anda belirli sayıda threadin bir kaynağa erişmesini sağlayan sayaç tabanlı senkronizasyon aracıdır.

Mutex yalnızca bir threadin girişine izin verirken semaphore birden fazla threadin girişine izin verebilir.

Semaphore içinde bir sayaç bulunur.

Örneğin:

```text
Semaphore değeri = 3
```

Bu, aynı anda en fazla üç threadin ilgili kaynağı kullanabileceği anlamına gelir.

---

## Semaphore Çalışma Mantığı

Semaphore değeri başlangıçta:

```text
3
```

Thread A kaynağa girer:

```text
Semaphore = 2
```

Thread B girer:

```text
Semaphore = 1
```

Thread C girer:

```text
Semaphore = 0
```

Thread D girmek ister:

```text
Semaphore 0 olduğu için Thread D bekler.
```

Thread A işini bitirip kaynağı bırakır:

```text
Semaphore = 1
```

Böylece Thread D kaynağa girebilir.

---

# 15. Semaphore Türleri

## 15.1. Binary Semaphore

Binary semaphore yalnızca iki değer alır:

```text
0 veya 1
```

Bir bakıma mutex gibi tek bir threadin erişimini kontrol edebilir.

Ancak binary semaphore ve mutex tamamen aynı değildir.

Temel fark:

* Mutexte sahiplik vardır.
* Semaphoreda genellikle sahiplik yoktur.

Yani bir thread semaphore değerini azaltabilir, başka bir thread artırabilir.

---

## 15.2. Counting Semaphore

Counting semaphore, sıfırdan büyük bir sayaçla çalışır.

Örneğin bir veritabanı bağlantı havuzunda beş bağlantı varsa:

```text
Semaphore = 5
```

Aynı anda en fazla beş thread veritabanı bağlantısı kullanabilir.

Altıncı thread bağlantılardan biri serbest kalana kadar bekler.

---

# 16. Semaphore İçin Gerçek Hayat Örneği

Bir otoparkta 50 araçlık yer olduğunu düşünelim.

Semaphore başlangıç değeri:

```text
50
```

Her araç girdiğinde değer azalır:

```text
49
48
47
...
```

Otopark dolduğunda:

```text
Semaphore = 0
```

Yeni araçlar beklemek zorunda kalır.

Bir araç çıktığında:

```text
Semaphore = 1
```

Bekleyen araçlardan biri içeri girebilir.

Bu durumda semaphore otoparktaki boş yer sayısını temsil etmektedir.

---

# 17. Mutex ve Semaphore Arasındaki Fark

| Özellik             | Mutex                               | Semaphore                                  |
| ------------------- | ----------------------------------- | ------------------------------------------ |
| Temel amaç          | Tek bir threadin erişimini sağlamak | Belirli sayıda threadin erişimini sağlamak |
| Sayaç değeri        | Genellikle kilitli/kilitsiz         | 0, 1, 2, 3 gibi değerler                   |
| Aynı anda giriş     | Genellikle 1 thread                 | Sayaç kadar thread                         |
| Sahiplik            | Vardır                              | Genellikle yoktur                          |
| Kilidi kim bırakır? | Kilitleyen thread                   | Başka bir thread de sinyal verebilir       |
| Kullanım örneği     | Ortak banka bakiyesi                | Veritabanı bağlantı havuzu                 |
| Temel kullanım      | Critical section korumak            | Sınırlı kaynak yönetmek                    |

---

# 18. Mutex, Semaphore ve Lock Karşılaştırması

| Kavram    | Açıklama                                                                                             |
| --------- | ---------------------------------------------------------------------------------------------------- |
| Lock      | Kaynağa erişimi kontrol eden genel kilitleme kavramıdır.                                             |
| Mutex     | Aynı anda yalnızca bir threadin critical sectiona girmesini sağlayan sahiplik tabanlı lock türüdür.  |
| Semaphore | Aynı anda belirli sayıda threadin kaynağa erişmesini sağlayan sayaç tabanlı senkronizasyon aracıdır. |

Kısaca:

```text
Lock → Genel kavram
Mutex → Tek kişi girebilir
Semaphore → Belirlenen sayıda kişi girebilir
```

Günlük hayat benzetmesi:

* **Mutex:** Tek anahtarlı bir tuvalet.
* **Semaphore:** Beş masalı bir kütüphane çalışma alanı.
* **Lock:** Kapıya erişimi kontrol eden genel kilit sistemi.

---

# 19. Synchronization Nedir?

**Synchronization**, birden fazla thread veya processin çalışmalarını belirli bir düzende yürütmesini sağlayan mekanizmalardır.

Synchronization iki temel amaçla kullanılır:

1. Ortak verinin güvenliğini sağlamak.
2. İşlemlerin doğru sırada çalışmasını sağlamak.

Örneğin:

```text
Veri indirilmeden veri işleme başlamamalıdır.
Dosya yazılmadan dosya okunmamalıdır.
Üretici veri üretmeden tüketici veriyi alamamalıdır.
```

Bu işlemler arasında koordinasyon gerekir.

Mutex, semaphore, lock ve condition variable gibi yapılar bu koordinasyonu sağlar.

---

# 20. Thread-Safe Ne Demektir?

Bir kod, fonksiyon veya veri yapısı aynı anda birden fazla thread tarafından kullanıldığında doğru çalışıyorsa **thread-safe** olarak adlandırılır.

Örneğin thread-safe bir sayaç:

* Güncellemeleri kaybetmez.
* Race condition oluşturmaz.
* Her çalıştırmada tutarlı sonuç verir.

Thread-safe olmayan bir listeye iki thread aynı anda eleman eklediğinde:

* Eleman kaybolabilir.
* Liste yapısı bozulabilir.
* Hata oluşabilir.

Bir kodun thread-safe olması için şu yöntemlerden biri kullanılabilir:

* Mutex veya lock
* Semaphore
* Atomic değişken
* Immutable veri
* Thread-local storage
* Mesajlaşma tabanlı yapı

---

# 21. Deadlock Nedir?

**Deadlock**, iki veya daha fazla threadin birbirinin tuttuğu kaynağı beklemesi ve hiçbirinin ilerleyememesi durumudur.

Örneğin iki lock bulunduğunu düşünelim:

```text
Lock A
Lock B
```

Thread 1:

```text
Lock A'yı aldı.
Lock B'yi bekliyor.
```

Thread 2:

```text
Lock B'yi aldı.
Lock A'yı bekliyor.
```

Sonuç:

```text
Thread 1, Thread 2'yi bekliyor.
Thread 2, Thread 1'i bekliyor.
```

Hiçbiri ilerleyemez.

---

## Deadlock İçin Günlük Hayat Örneği

Dar bir köprüde karşılıklı gelen iki araç düşünelim.

* Birinci araç ikinci aracın geri gitmesini bekliyor.
* İkinci araç birinci aracın geri gitmesini bekliyor.
* İkisi de hareket etmiyor.

Bu durum deadlock mantığına benzer.

---

## Deadlock Oluşmasının Dört Koşulu

Deadlock genellikle şu dört koşul aynı anda oluştuğunda meydana gelir:

### 1. Mutual Exclusion

Bir kaynak aynı anda yalnızca bir thread tarafından kullanılabilir.

### 2. Hold and Wait

Thread bir kaynağı tutarken başka bir kaynağı bekler.

### 3. No Preemption

Bir kaynağı threadin elinden zorla almak mümkün değildir.

### 4. Circular Wait

Threadler birbirlerinin tuttuğu kaynakları dairesel olarak bekler.

Bu koşullardan en az biri ortadan kaldırılırsa deadlock önlenebilir.

---

## Deadlock Nasıl Önlenir?

* Lockları her zaman aynı sırayla almak.
* Lock sayısını azaltmak.
* Locku mümkün olduğunca kısa süre tutmak.
* Timeout kullanmak.
* İç içe lock kullanımından kaçınmak.
* Birden fazla kaynağı tek lock altında yönetmek.
* Hata durumunda lockun kesinlikle bırakılmasını sağlamak.

Örneğin bütün threadler önce `Lock A`, sonra `Lock B` alırsa dairesel bekleme ihtimali azalır.

---

# 22. Starvation Nedir?

**Starvation**, bir threadin çalışmak için sürekli beklemesi ve ihtiyaç duyduğu kaynağa uzun süre erişememesidir.

Örneğin yüksek öncelikli threadler sürekli locku alıyorsa düşük öncelikli thread hiç sıra bulamayabilir.

Program tamamen kilitlenmez. Bazı threadler çalışmaya devam eder ancak belirli bir thread ilerleyemez.

Deadlock ile farkı:

* Deadlockta ilgili threadlerin hiçbiri ilerleyemez.
* Starvationda bazı threadler ilerlerken bir veya birkaç thread sürekli bekler.

---

# 23. Livelock Nedir?

**Livelock**, threadlerin bloke olmamasına rağmen birbirlerine sürekli tepki verdikleri için gerçek işi tamamlayamamasıdır.

Örneğin iki kişinin koridorda karşılaştığını düşünelim:

```text
İkisi de sağa geçer.
İkisi de sola geçer.
Tekrar sağa geçer.
Tekrar sola geçer.
```

İkisi de hareket etmektedir ama hiçbiri ilerleyememektedir.

Deadlockta threadler hareketsizdir. Livelockta threadler çalışır gibi görünür ancak sonuç üretemez.

---

# 24. Lock Kullanımının Performansa Etkisi

Locklar veri güvenliğini sağlar ancak ücretsiz değildir.

Bir lock kullanıldığında:

* Thread beklemek zorunda kalabilir.
* Context switching oluşabilir.
* CPU çekirdekleri boşta kalabilir.
* Paralel çalışma azalabilir.
* Lock yönetimi ek maliyet oluşturabilir.

Örneğin sekiz çekirdeğin bulunduğu bir sistemde bütün threadler aynı locku bekliyorsa uygulama pratikte tek thread gibi çalışabilir.

Bu duruma **lock contention**, yani kilit çekişmesi denir.

---

## Lock Contention Nedir?

Birden fazla thread aynı locku sık sık almaya çalışıyorsa contention oluşur.

Örnek:

```text
Thread A → Locku kullanıyor
Thread B → Bekliyor
Thread C → Bekliyor
Thread D → Bekliyor
```

Lock serbest kaldığında yalnızca bir thread devam eder.

Bu nedenle critical sectionlar mümkün olduğunca kısa tutulmalıdır.

Yanlış:

```text
lock al
uzun hesaplama yap
API isteği gönder
dosya oku
veriyi güncelle
lock bırak
```

Daha doğru:

```text
API isteğini lock dışında yap
uzun hesaplamayı lock dışında yap

lock al
yalnızca ortak veriyi güncelle
lock bırak
```

---

# 25. Fine-Grained ve Coarse-Grained Locking

## Coarse-Grained Locking

Büyük bir veri yapısının tamamını tek lock ile korumaktır.

Avantajı:

* Uygulaması kolaydır.
* Hata yapma ihtimali daha düşüktür.

Dezavantajı:

* Aynı anda daha az thread çalışabilir.
* Performans düşebilir.

Örneğin bütün banka hesaplarını tek lock ile korumak:

```text
GlobalBankLock
```

Bir hesaptaki işlem yüzünden diğer tüm hesaplar beklemek zorunda kalır.

---

## Fine-Grained Locking

Kaynakların daha küçük parçalarını ayrı locklarla korumaktır.

Örneğin her banka hesabının kendi locku olabilir:

```text
Account1Lock
Account2Lock
Account3Lock
```

Birinci hesapta işlem yapılırken ikinci hesapta başka bir işlem devam edebilir.

Avantajı:

* Paralellik artar.
* Bekleme azalır.

Dezavantajı:

* Yönetimi daha zordur.
* Deadlock riski artabilir.
* Kod karmaşıklaşabilir.

---

# 26. Producer–Consumer Problemi

Concurrency konusunda en bilinen problemlerden biri producer-consumer problemidir.

* Producer veri üretir.
* Consumer üretilen veriyi tüketir.
* Arada ortak bir buffer veya queue bulunur.

Örneğin:

```text
Producer → Dosyadan veri okur.
Queue → Veriyi geçici olarak saklar.
Consumer → Veriyi işler.
```

Sorunlar:

* Queue doluyken producer yeni veri eklememelidir.
* Queue boşken consumer veri almaya çalışmamalıdır.
* Producer ve consumer queueyu aynı anda bozacak şekilde değiştirmemelidir.

Bu yapıda:

* Mutex queueyu korumak için,
* Semaphore boş ve dolu alan sayısını takip etmek için

kullanılabilir.

Örneğin:

```text
emptySlots = 10
fullSlots = 0
```

Producer veri eklediğinde:

```text
emptySlots azalır
fullSlots artar
```

Consumer veri aldığında:

```text
fullSlots azalır
emptySlots artar
```

---

# 27. Concurrency Her Zaman Performansı Artırır mı?

Hayır.

Concurrency yanlış kullanıldığında uygulamayı daha yavaş ve daha karmaşık hâle getirebilir.

Ek maliyetler şunlardır:

* Thread oluşturma maliyeti
* Context switching maliyeti
* Lock bekleme süresi
* Cache tutarsızlıkları
* Senkronizasyon maliyeti
* Debug işlemlerinin zorlaşması

Örneğin çok küçük bir işi 1000 threade bölmek, işi tek threadde yapmaktan daha yavaş olabilir.

Çünkü thread yönetimi için harcanan süre gerçek hesaplama süresinden fazla olabilir.

---

# 28. Parallelism Her Programı Hızlandırır mı?

Hayır.

Bir programın yalnızca paralelleştirilebilen kısmı hızlandırılabilir.

Örneğin bir programın:

* %80'i paralelleştirilebiliyor,
* %20'si sırayla çalışmak zorunda

olsun.

Çekirdek sayısı ne kadar artırılırsa artırılsın, sıralı çalışan %20'lik bölüm toplam performansı sınırlar.

Bu düşünce **Amdahl Yasası** ile açıklanır.

Temel fikir şöyledir:

> Bir programın paralelleştirilemeyen kısmı, ulaşılabilecek en yüksek hızlanmayı sınırlar.

Bu nedenle daha fazla thread veya çekirdek her zaman aynı oranda hızlanma sağlamaz.

---

# 29. Concurrency Problemlerinin Bulunması Neden Zordur?

Concurrency hataları genellikle her çalıştırmada oluşmaz.

Örneğin program:

* 100 kez doğru çalışabilir.
* 101. çalıştırmada hata verebilir.
* Debug modunda doğru çalışıp gerçek ortamda bozulabilir.
* Hızlı bilgisayarda bozulup yavaş bilgisayarda çalışabilir.

Bunun nedeni threadlerin çalışma sırasının işletim sistemi tarafından belirlenmesidir.

Threadlerin sırası şu faktörlere göre değişebilir:

* CPU yükü
* İşletim sistemi zamanlayıcısı
* Çekirdek sayısı
* Network gecikmesi
* Disk hızı
* Diğer uygulamaların çalışması

Bu tür hatalara bazen **heisenbug** denir. Hata incelenmeye çalışıldığında zamanlama değiştiği için hata kaybolabilir.

---

# 30. Güvenli Concurrency İçin Temel Kurallar

## 1. Ortak veriyi mümkün olduğunca azalt

Her thread kendi verisi üzerinde çalışırsa senkronizasyon ihtiyacı azalır.

## 2. Immutable veriler kullan

Immutable veri oluşturulduktan sonra değiştirilemez. Değiştirilemediği için birden fazla thread tarafından güvenli biçimde okunabilir.

## 3. Critical sectionları kısa tut

Lock yalnızca gerçekten ortak verinin kullanıldığı bölümde alınmalıdır.

## 4. Lockları düzenli sırayla al

Bütün threadler lockları aynı sırada almalıdır.

## 5. Locku mutlaka serbest bırak

Hata oluşsa bile lockun bırakılacağı garanti edilmelidir.

## 6. Gereksiz thread oluşturma

Her işlem için yeni bir thread oluşturmak yerine thread pool kullanılabilir.

## 7. Hazır thread-safe veri yapılarını tercih et

Programlama dillerinin sunduğu:

* Concurrent queue
* Concurrent dictionary
* Atomic counter
* Blocking queue

gibi yapılar kullanılabilir.

## 8. Uzun I/O işlemlerini lock içinde yapma

API isteği, dosya okuma veya uzun hesaplama sırasında lock tutulmamalıdır.

## 9. Paylaşılan değişkenlerin erişim noktalarını sınırla

Bir ortak değişken ne kadar çok yerde değiştirilirse hata ihtimali o kadar artar.

## 10. Testleri yüksek yük altında çalıştır

Concurrency problemleri düşük yükte görünmeyebilir.

---

# 31. Thread Pool Nedir?

Thread pool, önceden oluşturulmuş belirli sayıda threadin görevleri sırayla çalıştırdığı yapıdır.

Her görev için yeni thread oluşturmak yerine görevler bir kuyruğa eklenir.

```text
Görev Kuyruğu
     ↓
Thread 1
Thread 2
Thread 3
Thread 4
```

Avantajları:

* Sürekli thread oluşturma maliyetini azaltır.
* Aynı anda çalışan thread sayısını sınırlar.
* Sistem kaynaklarının tükenmesini önler.
* Performansı daha kontrollü hâle getirir.

Örneğin bir web sunucusu her istek için sınırsız thread oluşturursa yoğun trafikte sistem çökebilir. Thread pool kullanıldığında aynı anda işlenecek görev sayısı kontrol edilir.

---

# 32. Concurrency Kullanım Alanları

Concurrency şu alanlarda yaygın olarak kullanılır:

* Web sunucuları
* Mobil uygulamalar
* Masaüstü uygulamaları
* Oyun motorları
* Veritabanı sistemleri
* İşletim sistemleri
* Dosya indirme uygulamaları
* Mesajlaşma sistemleri
* Mikroservis mimarileri
* Gerçek zamanlı uygulamalar
* Ağ programlama
* Kullanıcı arayüzleri

Örneğin bir mobil uygulamada API isteği ana thread üzerinde yapılırsa ekran donabilir. API işlemi farklı bir thread veya async görev üzerinde çalıştırıldığında kullanıcı arayüzü yanıt vermeye devam eder.

---

# 33. Parallel Programming Kullanım Alanları

Parallel programming özellikle hesaplama yoğun işlemlerde kullanılır:

* Yapay zekâ model eğitimi
* Görüntü işleme
* Video rendering
* Bilimsel simülasyonlar
* Büyük veri analizi
* Şifreleme
* Arama algoritmaları
* Matris hesaplamaları
* Oyun fizik motorları
* Hava durumu modellemeleri

Örneğin bir yapay zekâ modelinde binlerce matris işlemi GPU çekirdeklerine dağıtılarak paralel biçimde gerçekleştirilebilir.

---

# 34. Sıralı, Concurrent ve Parallel Çalışma Karşılaştırması

Üç görev olduğunu düşünelim:

```text
Görev A = 3 saniye
Görev B = 3 saniye
Görev C = 3 saniye
```

## Sequential çalışma

Görevler sırayla çalışır:

```text
A → B → C
```

Toplam süre yaklaşık:

```text
9 saniye
```

## Concurrent çalışma

Görevler arasında geçiş yapılır. Özellikle bekleme süreleri varsa toplam süre azalabilir.

```text
A biraz çalışır
B biraz çalışır
C biraz çalışır
A devam eder
```

## Parallel çalışma

Üç çekirdek varsa:

```text
Çekirdek 1 → A
Çekirdek 2 → B
Çekirdek 3 → C
```

Teorik toplam süre yaklaşık:

```text
3 saniye
```

Ancak pratikte thread oluşturma, veri paylaşımı ve senkronizasyon maliyetleri nedeniyle süre tam olarak üç saniye olmayabilir.

---

# 35. Concurrency ile Asynchronous Programming Aynı Şey mi?

Tam olarak aynı değildir.

**Concurrency**, birden fazla görevin aynı zaman aralığında yönetilmesidir.

**Asynchronous programming**, bir işlem tamamlanana kadar threadi gereksiz yere bekletmeden başka işlerin yapılmasına izin veren programlama modelidir.

Örneğin API isteği gönderilir:

```text
İstek gönder
Cevabı beklerken başka işlere devam et
Cevap gelince ilgili kodu çalıştır
```

Async yapı concurrency sağlamaya yardımcı olabilir. Ancak her async işlem ayrı bir thread üzerinde çalışmak zorunda değildir.

Özellikle I/O işlemlerinde tek bir thread çok sayıda async görevi yönetebilir.

---

# 36. Temel Kavramların Kısa Özeti

## Concurrency

Birden fazla görevin aynı zaman aralığında ilerletilmesidir. Gerçek anlamda aynı anda çalışmaları zorunlu değildir.

## Parallelism

Birden fazla görevin birden fazla çekirdekte gerçekten aynı anda çalışmasıdır.

## Race Condition

Program sonucunun threadlerin çalışma sırasına bağlı olarak hatalı veya tutarsız hâle gelmesidir.

## Critical Section

Ortak kaynağa erişen ve aynı anda yalnızca bir thread tarafından çalıştırılması gereken kod bölümüdür.

## Mutex

Aynı anda yalnızca bir threadin ortak kaynağa erişmesine izin veren, sahiplik tabanlı senkronizasyon aracıdır.

## Semaphore

Aynı anda belirli sayıda threadin bir kaynağa erişmesini sağlayan sayaç tabanlı yapıdır.

## Lock

Ortak kaynağa erişimi sınırlandıran genel kilitleme kavramıdır.

## Deadlock

Threadlerin birbirlerinin kaynaklarını beklemesi nedeniyle hiçbirinin ilerleyememesidir.

## Starvation

Bir threadin sürekli diğer threadler tarafından geride bırakılması ve uzun süre kaynağa erişememesidir.

## Thread-Safe

Bir kodun birden fazla thread tarafından aynı anda kullanıldığında doğru ve tutarlı şekilde çalışmasıdır.

---

# 37. Genel Sonuç

Concurrency ve parallel programming, modern yazılım sistemlerinin temel yapı taşlarındandır.

Concurrency sayesinde bir uygulama aynı zaman aralığında birden fazla görevle ilgilenebilir. Örneğin kullanıcı arayüzü çalışmaya devam ederken arka planda dosya indirilebilir veya API isteği yapılabilir.

Parallelism sayesinde hesaplama yoğun görevler birden fazla işlemci çekirdeğine dağıtılarak daha hızlı tamamlanabilir.

Ancak birden fazla thread aynı veriye kontrolsüz şekilde eriştiğinde race condition oluşabilir. Bu problemi önlemek için critical sectionlar mutex, semaphore ve lock mekanizmalarıyla korunur.

Bu yapıların yanlış kullanılması durumunda:

* Deadlock
* Starvation
* Livelock
* Performans kaybı
* Veri tutarsızlığı

gibi sorunlar ortaya çıkabilir.

Bu nedenle başarılı bir concurrent yazılımın amacı yalnızca çok sayıda thread çalıştırmak değildir. Asıl amaç şudur:

> Ortak kaynakları güvenli biçimde yönetmek, görevleri doğru şekilde koordine etmek ve donanım kaynaklarını gereksiz maliyet oluşturmadan verimli kullanmak.
