# 1. Bilgisayar Bilimleri Temelleri ve Kod Yazma Süreci

<a id="icindekiler"></a>

## İçindekiler

1. [Giriş](#giris)
2. [Bilgisayar Sistemi Nedir?](#bilgisayar-sistemi)
3. [Donanım ve Yazılım Arasındaki Fark](#donanim-yazilim)
4. [Bilgisayar Veriyi Nasıl Temsil Eder?](#veri-temsili)
5. [CPU (Merkezi İşlem Birimi)](#cpu)
   - [CPU'nun Temel Görevi](#cpu-gorevi)
   - [CPU'nun Temel Bileşenleri](#cpu-bilesenleri)
   - [Fetch - Decode - Execute Döngüsü](#fetch-decode-execute)
   - [Çekirdek, Thread ve Saat Hızı](#cekirdek-thread)
   - [CPU Cache: L1, L2 ve L3](#cpu-cache)
6. [RAM (Ana Bellek)](#ram)
   - [RAM Neden Gereklidir?](#ram-neden)
   - [RAM ve Disk Arasındaki Fark](#ram-disk-farki)
   - [Stack ve Heap'e Kısa Bakış](#stack-heap)
   - [Sanal Bellek (Virtual Memory)](#sanal-bellek)
7. [Disk ve Kalıcı Depolama](#disk)
   - [HDD, SATA SSD ve NVMe SSD](#depolama-turleri)
   - [Dosya Sistemi](#dosya-sistemi)
8. [Anakart, Veri Yolları ve Diğer Temel Donanımlar](#anakart)
9. [Giriş ve Çıkış Birimleri](#giris-cikis)
10. [İşletim Sistemi](#isletim-sistemi)
    - [Kernel](#kernel)
    - [Process Yönetimi](#process-yonetimi)
    - [Bellek Yönetimi](#bellek-yonetimi)
    - [Dosya Sistemi Yönetimi](#dosya-yonetimi)
    - [Aygıt Sürücüleri](#suruculer)
    - [Kullanıcı ve Yetki Yönetimi](#yetki)
11. [Program, Process ve Thread Farkı](#program-process-thread)
12. [Kaynak Koddan Çalışan Programa Giden Yol](#kaynaktan-programa)
13. [Compiler, Interpreter ve JIT](#compiler-interpreter-jit)
14. [IDE, Kod Editörü, Terminal ve Shell](#ide-terminal)
15. [System Call Nedir?](#system-call)
16. [Bir Program Çalıştırıldığında Arka Planda Neler Olur?](#program-calistirma)
17. [VS Code'da Kod Yazarken Bilgisayarda Neler Olur?](#vscode-sureci)
18. [Basit Bir Kod Örneğinin Bilgisayar Açısından İncelenmesi](#kod-ornegi)
19. [Programlama Hataları: Syntax, Runtime ve Logic Error](#hatalar)
20. [Performans Darboğazları](#performans)
21. [CPU-Bound, Memory-Bound ve I/O-Bound İşlemler](#bound)
22. [Temel Kavramların Birbirleriyle İlişkisi](#iliski)
23. [Özet Karşılaştırma Tablosu](#ozet-tablo)
24. [Mülakat İçin Önemli Sorular ve Kısa Cevaplar](#mulakat)
25. [Genel Sonuç](#sonuc)

---

<a id="giris"></a>

## Giriş

Bilgisayar bilimi yalnızca programlama dili öğrenmekten veya ekrana kod yazmaktan ibaret değildir. Yazdığımız bir kodun gerçekten çalışabilmesi için donanım ve yazılım katmanlarının birlikte hareket etmesi gerekir.

Bir geliştirici olarak VS Code'u açıp birkaç satır kod yazdığımızda, aslında arka planda şu bileşenlerin tamamı birlikte çalışmaktadır:

- CPU komutları işler.
- RAM aktif programları ve verileri geçici olarak tutar.
- SSD/HDD dosyaları kalıcı olarak saklar.
- İşletim sistemi donanım kaynaklarını yönetir.
- Dosya sistemi kod dosyalarının nerede tutulacağını belirler.
- Derleyici veya yorumlayıcı kaynak kodu çalıştırılabilir hale getirir.
- Terminal ve shell, işletim sistemiyle komut tabanlı iletişim kurmamızı sağlar.
- Process ve thread yapıları çalışan programların yönetilmesini sağlar.

Bu nedenle bilgisayar bilimlerinin temelini anlamak, yalnızca teorik bilgi kazanmak anlamına gelmez. Bu bilgiler; performans sorunlarını anlamaktan hata ayıklamaya, backend geliştirmeden işletim sistemlerine, veri yapılarından dağıtık sistemlere kadar birçok ileri konunun temelini oluşturur.

Bu raporda bilgisayarın temel çalışma mantığını özellikle **"Bir geliştirici kod yazdığında bilgisayarda gerçekte ne olur?"** sorusu üzerinden inceleyeceğiz.

---

<a id="bilgisayar-sistemi"></a>

## Bilgisayar Sistemi Nedir?

Bilgisayar sistemi, verilen girdileri işleyen ve bir çıktı üreten donanım ve yazılım bileşenlerinin bütünüdür. En temel haliyle süreç şu şekilde düşünülebilir:

```text
Girdi → İşleme → Depolama → Çıktı
```

Örneğin klavyeden:

```text
5 + 3
```

işlemini yazdığımızı düşünelim. Bu durumda:

1. Klavye girdiyi bilgisayara gönderir.
2. İşletim sistemi bu girdiyi ilgili programa iletir.
3. Program gerekli işlemi CPU'ya yaptırır.
4. Gerekli veriler RAM'de tutulur.
5. Sonuç hesaplanır.
6. Sonuç ekrana gönderilir.

Yani bilgisayarın yaptığı temel işlem aslında:

```text
Veri al → İşle → Sonuç üret
```

mantığına dayanır.

---

<a id="donanim-yazilim"></a>

## Donanım ve Yazılım Arasındaki Fark

Bilgisayar sistemleri iki ana grupta incelenebilir:

### Donanım (Hardware)

Fiziksel olarak dokunabildiğimiz bilgisayar parçalarıdır. Örnekler:

- CPU
- RAM
- SSD
- HDD
- Anakart
- Ekran kartı
- Klavye
- Fare
- Monitör
- Ağ kartı

### Yazılım (Software)

Donanıma ne yapması gerektiğini söyleyen programlar ve komutlardır. Örnekler:

- Windows
- Linux
- macOS
- VS Code
- Chrome
- Python
- Java
- Git
- Bir geliştiricinin yazdığı uygulamalar

Donanım tek başına anlamlı bir iş yapamaz. Yazılım ise donanım olmadan çalışamaz. Aralarındaki ilişki kabaca şöyledir:

```text
Kullanıcı
   ↓
Uygulama
   ↓
İşletim Sistemi
   ↓
Donanım
```

Örneğin VS Code'da bir dosyayı kaydettiğimizde VS Code doğrudan SSD'nin elektronik devreleriyle konuşmaz. Bunun yerine işletim sisteminden dosyayı kaydetmesini ister. İşletim sistemi de ilgili donanım sürücülerini ve dosya sistemini kullanarak işlemi gerçekleştirir.

---

<a id="veri-temsili"></a>

## Bilgisayar Veriyi Nasıl Temsil Eder?

Bilgisayarın temel veri birimi **bit**tir. Bir bit yalnızca iki değer alabilir:

```text
0
1
```

Bu nedenle bilgisayarlar ikili sayı sistemi yani **binary system** kullanır.

### Bit ve Byte

```text
1 bit  = 0 veya 1
8 bit  = 1 byte
```

Örneğin:

```text
01000001
```

8 bitten oluşur ve 1 byte'tır. ASCII karakter kodlamasında bu değer `A` harfini temsil edebilir.

### Temel Veri Boyutları

Yaklaşık olarak:

```text
1 Byte = 8 bit
1 KB   ≈ 1024 Byte
1 MB   ≈ 1024 KB
1 GB   ≈ 1024 MB
1 TB   ≈ 1024 GB
```

Günlük kullanımda depolama üreticileri bazen 1000 tabanlı, işletim sistemleri ise bazı durumlarda 1024 tabanlı hesaplama kullandığı için görünen kapasite ile ürün üzerinde yazan kapasite arasında fark oluşabilir.

### Metinler Nasıl Saklanır?

Bilgisayar harfleri doğrudan "harf" olarak saklamaz. Karakterler sayısal kodlara dönüştürülür. Bunun için kullanılan sistemlerden bazıları:

- ASCII
- Unicode
- UTF-8
- UTF-16

Örneğin günümüzde web uygulamalarında en yaygın karakter kodlamalarından biri UTF-8'dir. Bu sayede:

```text
A
B
Ç
Ğ
😊
```

gibi farklı karakterler sayısal biçimde saklanabilir.

---

<a id="cpu"></a>

## CPU (Merkezi İşlem Birimi)

CPU yani **Central Processing Unit**, bilgisayarın komutları işleyen ana işlem birimidir. Genellikle "bilgisayarın beyni" olarak tanımlanır. Bu tanım basitleştirilmiş olsa da CPU'nun rolünü anlamak açısından kullanışlıdır.

CPU'nun temel görevi:

```text
Komutları almak → Anlamak → Çalıştırmak
```

şeklinde özetlenebilir. Burada önemli bir düzeltme yapmak gerekir:

> Yazdığımız kaynak kod her zaman CPU tarafından doğrudan "satır satır" okunmaz.

Örneğin C veya C++ kodu önce derlenerek makine koduna dönüştürülür. CPU daha sonra bu makine komutlarını çalıştırır.

Python gibi yorumlanan dillerde ise Python yorumlayıcısı kaynak kodu işler; CPU doğrudan Python sözdizimini değil, yorumlayıcının ve ilgili runtime'ın ürettiği düşük seviyeli komutları çalıştırır.

---

<a id="cpu-gorevi"></a>

### CPU'nun Temel Görevi

CPU aşağıdaki işlemleri gerçekleştirir:

- Matematiksel işlemler
- Mantıksal karşılaştırmalar
- Bellekten veri okuma
- Belleğe veri yazma
- Koşullu dallanmalar
- Döngüler
- Fonksiyon çağrıları
- Program akışının yürütülmesi

Örneğin:

```python
x = 10
y = 20
sonuc = x + y
```

kodunda toplama işleminin fiziksel olarak gerçekleştirilmesinde CPU görev alır.

---

<a id="cpu-bilesenleri"></a>

### CPU'nun Temel Bileşenleri

CPU'nun içinde birçok karmaşık yapı bulunur. Temel seviyede üç önemli yapı bilinmelidir.

#### ALU – Arithmetic Logic Unit

Aritmetik ve mantıksal işlemleri gerçekleştirir. Örneğin:

```text
5 + 3
10 - 4
7 > 2
x == y
```

gibi işlemler ALU ile ilişkilidir.

#### Control Unit – Kontrol Birimi

Komutların hangi sırayla çalışacağını yönetir. Örneğin:

```python
if yas >= 18:
    print("Yetiskin")
```

kodunda hangi komutun çalışacağına karar verilmesini sağlayan işlem akışı CPU kontrol mekanizmalarıyla yürütülür.

#### Registers – Register'lar

CPU'nun içinde bulunan son derece hızlı ve küçük bellek alanlarıdır. CPU bir işlemi gerçekleştirirken ihtiyaç duyduğu bazı değerleri kısa süreli olarak register'larda tutabilir. Genel hız sıralaması kabaca şöyledir:

```text
Register
↓
CPU Cache
↓
RAM
↓
SSD
↓
HDD
```

Yukarıdaki yapılar aşağı indikçe genellikle kapasite artar fakat erişim hızı düşer.

---

<a id="fetch-decode-execute"></a>

### Fetch - Decode - Execute Döngüsü

CPU'nun çalışma mantığını açıklayan en temel modellerden biri şu döngüdür:

```text
Fetch → Decode → Execute
```

#### 1. Fetch

CPU çalıştırılacak komutu bellekten alır.

#### 2. Decode

Komutun ne anlama geldiği çözülür. Örneğin:

```text
ADD
MOV
JMP
```

gibi düşük seviyeli komutların hangi işlemi istediği anlaşılır.

#### 3. Execute

Komut gerçekleştirilir. Örneğin iki sayı toplanır veya bir bellek adresindeki veri başka bir yere taşınır. Bu döngü saniyede milyarlarca kez gerçekleşebilir.

---

<a id="cekirdek-thread"></a>

### Çekirdek, Thread ve Saat Hızı

Modern CPU'lar genellikle birden fazla çekirdeğe sahiptir. Örneğin:

```text
4 Core
6 Core
8 Core
12 Core
```

Birden fazla çekirdek, uygun iş yüklerinde aynı anda daha fazla işlemin yürütülmesini sağlayabilir.

Ancak:

> "8 çekirdekli CPU, 4 çekirdekli CPU'dan her durumda iki kat hızlıdır."

demek doğru değildir.

Performansı etkileyen birçok faktör vardır:

- CPU mimarisi
- Saat hızı
- Çekirdek sayısı
- IPC (Instruction Per Clock)
- Cache boyutu
- Güç ve sıcaklık sınırları
- Programın paralel çalışmaya uygun olup olmaması

### Saat Hızı

CPU saat hızı genellikle GHz ile ifade edilir. Örneğin:

```text
3.5 GHz
4.2 GHz
```

Ancak yüksek GHz değeri tek başına daha yüksek performans anlamına gelmez. Farklı işlemci mimarileri aynı saat hızında farklı miktarda iş gerçekleştirebilir.

### Hardware Thread

Bazı işlemciler bir fiziksel çekirdeğin birden fazla mantıksal thread çalıştırabilmesine izin verir. Örneğin:

```text
8 Core / 16 Thread
```

ifadesi, 8 fiziksel çekirdek ve 16 mantıksal işlem akışı anlamına gelebilir.

---

<a id="cpu-cache"></a>

### CPU Cache: L1, L2 ve L3

CPU ile RAM arasında ciddi hız farkı vardır. CPU'nun sürekli RAM'i beklemesini azaltmak için **cache memory** kullanılır. Genellikle üç temel cache seviyesi vardır:

```text
L1 Cache
L2 Cache
L3 Cache
```

Genel olarak:

- L1 en küçük ve en hızlıdır.
- L2 daha büyüktür fakat L1'den biraz daha yavaştır.
- L3 daha büyüktür ve çoğu işlemcide çekirdekler arasında paylaşılabilir.

Örnek mantık:

```text
CPU veriye ihtiyaç duyar
        ↓
L1'de var mı?
        ↓
Yoksa L2
        ↓
Yoksa L3
        ↓
Yoksa RAM
```

Bu yapı performans açısından çok önemlidir.

---

<a id="ram"></a>

## RAM (Ana Bellek)

RAM, **Random Access Memory** ifadesinin kısaltmasıdır. Bilgisayarın aktif olarak kullandığı programların ve verilerin geçici olarak tutulduğu ana bellektir.

RAM'in temel özelliği:

```text
Hızlıdır fakat geçicidir.
```

Bilgisayar kapatıldığında RAM'deki veriler normal koşullarda korunmaz. Bu nedenle RAM, **volatile memory** olarak adlandırılır.

---

<a id="ram-neden"></a>

### RAM Neden Gereklidir?

SSD ve HDD kalıcı veri depolama için uygundur ancak CPU açısından RAM kadar hızlı değildir. Bu nedenle çalışan programlar diskten RAM'e yüklenir.

Örneğin VS Code açıldığında:

```text
SSD
 ↓
VS Code dosyaları okunur
 ↓
RAM
 ↓
CPU programı çalıştırır
```

Aynı durum Chrome, Spotify, terminal veya başka uygulamalar için de geçerlidir.

RAM üzerinde genellikle:

- Çalışan programların kodları
- Program verileri
- Değişkenler
- Nesneler
- Açık dosyaların bazı içerikleri
- İşletim sistemi verileri
- Cache verileri

bulunabilir.

---

<a id="ram-disk-farki"></a>

### RAM ve Disk Arasındaki Fark

| Özellik            | RAM                   | SSD/HDD                         |
| ------------------ | --------------------- | ------------------------------- |
| Amaç               | Aktif verileri tutmak | Kalıcı veri saklamak            |
| Hız                | Çok hızlı             | RAM'den daha yavaş              |
| Elektrik kesilince | Veri kaybolur         | Veri korunur                    |
| Kapasite           | Genellikle daha düşük | Genellikle daha yüksek          |
| Kullanım           | Çalışan programlar    | Dosyalar, projeler, uygulamalar |

Örneğin kod dosyamızı kaydetmeden yazıyorsak, içerik editörün çalışma belleğinde bulunabilir. `Ctrl + S` yaptığımızda dosya kalıcı depolamaya yazılır.

Modern editörlerin otomatik kurtarma mekanizmaları bulunabilse de temel mantık yine geçici bellek ve kalıcı depolama ayrımına dayanır.

---

<a id="stack-heap"></a>

### Stack ve Heap'e Kısa Bakış

Bir program çalışırken RAM içinde farklı amaçlarla kullanılan bellek bölgeleri oluşabilir. İki önemli kavram:

```text
Stack
Heap
```

#### Stack

Genellikle:

- Fonksiyon çağrıları
- Yerel değişkenler
- Fonksiyon parametreleri
- Dönüş adresleri

gibi bilgilerle ilişkilidir. Stack çoğunlukla hızlı ve düzenli bir şekilde yönetilir.

#### Heap

Çalışma zamanında dinamik olarak oluşturulan veriler için kullanılabilir. Örneğin nesneler ve dinamik veri yapıları heap üzerinde tutulabilir.

Bu konu bellek yönetimi açısından çok önemlidir ve ileri seviyede garbage collection, pointer, reference ve memory leak gibi konulara bağlanır.

---

<a id="sanal-bellek"></a>

### Sanal Bellek (Virtual Memory)

RAM kapasitesi sınırlıdır. İşletim sistemleri süreçlere gerçek fiziksel RAM'in doğrudan tamamını vermek yerine genellikle **virtual memory** adı verilen bir adresleme sistemi sağlar. Bir program kendisine ait büyük ve düzenli bir adres alanı varmış gibi davranabilir. İşletim sistemi bu sanal adresleri fiziksel RAM'e eşler. RAM baskısı arttığında bazı işletim sistemleri daha az kullanılan bellek sayfalarını diskteki özel bir alana taşıyabilir. Windows'ta bu kavram page file, Linux'ta swap ile ilişkilidir. Ancak disk RAM'den çok daha yavaş olduğu için yoğun swap/page file kullanımı sistem performansını ciddi biçimde düşürebilir.

---

<a id="disk"></a>

## Disk ve Kalıcı Depolama

Disk veya genel anlamıyla depolama birimleri verilerin kalıcı olarak saklandığı donanımlardır. Projelerimiz, fotoğraflarımız, işletim sistemi dosyaları ve uygulamalar burada bulunur. Örneğin bir yazılım projesinde disk üzerinde şunlar tutulabilir:

```text
src/
tests/
README.md
package.json
requirements.txt
pom.xml
bin/
dist/
.git/
```

Program kapatılsa veya bilgisayar yeniden başlatılsa bile bu dosyalar korunur.

---

<a id="depolama-turleri"></a>

### HDD, SATA SSD ve NVMe SSD

#### HDD

HDD, mekanik yapıya sahip geleneksel depolama teknolojisidir.

Avantajları:

- Genellikle daha düşük maliyet
- Büyük kapasite seçenekleri

Dezavantajları:

- Daha yavaş
- Mekanik parçalara sahip
- Darbeye daha hassas
- Erişim gecikmesi daha yüksek

#### SATA SSD

SSD'de hareketli mekanik parça bulunmaz.

Avantajları:

- HDD'den çok daha hızlıdır.
- Programlar daha hızlı açılır.
- Dosyalar daha hızlı okunur.
- İşletim sistemi daha hızlı tepki verir.

#### NVMe SSD

NVMe SSD'ler PCIe altyapısı üzerinden çok daha yüksek veri aktarım hızlarına ulaşabilir.

Özellikle:

- Büyük projelerin derlenmesi
- Çok sayıda küçük dosyanın okunması
- Docker image işlemleri
- Veritabanı işlemleri
- Büyük datasetlerle çalışma

gibi I/O ağırlıklı işlerde avantaj sağlayabilir. Ancak hızlı SSD, her programı otomatik olarak CPU açısından daha hızlı yapmaz. Program CPU-bound ise asıl darboğaz işlemci olabilir.

---

<a id="dosya-sistemi"></a>

### Dosya Sistemi

Depolama cihazında dosyaların nasıl organize edileceğini belirleyen yapıya **file system** denir. Örnekler:

- NTFS
- ext4
- APFS
- FAT32
- exFAT

Dosya sistemi şu bilgileri yönetir:

- Dosya adı
- Dosya boyutu
- Dosyanın diskte bulunduğu konum
- Klasör yapısı
- Dosya izinleri
- Oluşturulma ve değiştirilme zamanı
- Bazı sistemlerde ek metadata bilgileri

Örneğin:

```text
C:\Users\user\Desktop\project\main.py
```

veya Linux'ta:

```text
/home/user/project/main.py
```

bir dosyanın dosya sistemi içindeki konumunu ifade eder.

---

<a id="anakart"></a>

## Anakart, Veri Yolları ve Diğer Temel Donanımlar

Anakart, bilgisayarın temel donanım bileşenlerini birbirine bağlayan ana devre kartıdır. CPU, RAM, depolama cihazları, ekran kartı ve çevre birimleri anakart üzerinden haberleşir.

### Bus (Veri Yolu)

Bileşenler arasında veri aktarımı sağlayan iletişim yollarına genel olarak bus adı verilir. Örneğin:

- Memory bus
- PCI Express
- USB
- SATA

gibi bağlantılar farklı donanımlar arasında veri taşır. Bu nedenle bir bilgisayar yalnızca "CPU + RAM" değildir. Bu parçaların birbirleriyle hızlı ve doğru iletişim kurabilmesi de önemlidir.

---

<a id="giris-cikis"></a>

## Giriş ve Çıkış Birimleri

Bilgisayarın dış dünya ile iletişim kurmasını sağlayan aygıtlara giriş/çıkış birimleri denir.

### Giriş Birimleri

Bilgisayara veri gönderir. Örnek:

- Klavye
- Fare
- Mikrofon
- Kamera
- Dokunmatik ekran

### Çıkış Birimleri

Bilgisayardan kullanıcıya veri iletir. Örnek:

- Monitör
- Hoparlör
- Yazıcı

Kod yazarken klavyeden bastığımız her tuş bir giriş olayıdır. Örneğin:

```text
p
r
i
n
t
```

tuşlarına bastığımızda klavye sinyalleri işletim sistemi tarafından algılanır ve aktif uygulamaya iletilir.

---

<a id="isletim-sistemi"></a>

## İşletim Sistemi

İşletim sistemi, uygulamalar ile donanım arasında yönetim katmanı görevi görür. Örnek işletim sistemleri:

- Windows
- Linux
- macOS
- Android
- iOS

Bir program çoğu durumda donanıma doğrudan erişmez. Bunun yerine işletim sisteminin sunduğu servisleri kullanır. Basitleştirilmiş yapı:

```text
Uygulama
   ↓
İşletim Sistemi
   ↓
Donanım
```

İşletim sisteminin temel görevleri şunlardır:

- CPU yönetimi
- RAM yönetimi
- Process yönetimi
- Dosya sistemi yönetimi
- Aygıt yönetimi
- Kullanıcı ve yetki yönetimi
- Ağ yönetimi
- Güvenlik
- Giriş/çıkış işlemleri

---

<a id="kernel"></a>

### Kernel

Kernel, işletim sisteminin en temel çekirdek bileşenidir. Donanım kaynakları ile kullanıcı uygulamaları arasında kritik bir yönetim katmanı oluşturur. Kernel şu konularla ilgilenir:

- CPU zamanlama
- Bellek yönetimi
- Process yönetimi
- Donanım erişimi
- Dosya sistemi işlemleri
- System call işlemleri

Kullanıcı uygulamaları genellikle doğrudan kernel kodunu çalıştırmaz. İşletim sistemi güvenlik ve kararlılık amacıyla kullanıcı modu ve kernel modu gibi ayrımlar kullanır.

---

<a id="process-yonetimi"></a>

### Process Yönetimi

Bir program çalıştırıldığında işletim sistemi onun için bir process oluşturur. Örneğin:

```text
VS Code
Chrome
Spotify
Python script
Node.js server
```

çalıştığında sistemde bir veya daha fazla process oluşabilir. İşletim sistemi:

- Process oluşturur.
- Process sonlandırır.
- CPU zamanını dağıtır.
- Process durumlarını takip eder.
- Process'ler arası izolasyon sağlar.

---

<a id="bellek-yonetimi"></a>

### Bellek Yönetimi

İşletim sistemi RAM'in hangi bölümünün hangi process tarafından kullanıldığını takip eder. Amaçlardan biri process'lerin birbirlerinin belleğine kontrolsüz şekilde erişmesini engellemektir. Bu hem güvenlik hem sistem kararlılığı açısından önemlidir.

---

<a id="dosya-yonetimi"></a>

### Dosya Sistemi Yönetimi

Bir program:

```python
open("data.txt")
```

gibi bir işlem yaptığında, dosyaya erişim işletim sistemi üzerinden gerçekleştirilir. İşletim sistemi:

- Dosyanın var olup olmadığını kontrol eder.
- Erişim iznini kontrol eder.
- Dosya sisteminde ilgili konumu bulur.
- Depolama cihazından veriyi okur.
- Veriyi programa iletir.

---

<a id="suruculer"></a>

### Aygıt Sürücüleri

Driver, işletim sisteminin donanımla iletişim kurmasını sağlayan yazılım bileşenidir. Örneğin:

- Ekran kartı sürücüsü
- Ses sürücüsü
- Ağ kartı sürücüsü
- Yazıcı sürücüsü

İşletim sistemi her donanımın elektronik ayrıntılarını uygulamalara bırakmak yerine driver katmanını kullanır.

---

<a id="yetki"></a>

### Kullanıcı ve Yetki Yönetimi

İşletim sistemi hangi kullanıcının hangi kaynağa erişebileceğini kontrol eder. Örneğin:

- Dosya okuma
- Dosya yazma
- Program çalıştırma
- Yönetici yetkisi
- Sistem klasörlerine erişim

Linux'ta:

```bash
sudo
chmod
chown
```

gibi komutlar bu konularla ilişkilidir. Windows'ta ise administrator yetkileri ve NTFS izinleri benzer amaçlarla kullanılır.

---

<a id="program-process-thread"></a>

## Program, Process ve Thread Farkı

Bu üç kavram sık karıştırılır.

### Program

Disk üzerinde bulunan çalıştırılabilir kod veya uygulamadır. Örneğin:

```text
chrome.exe
python.exe
app.jar
myprogram.exe
```

Henüz çalışmıyorsa yalnızca bir program dosyasıdır.

### Process

Program çalıştırıldığında oluşan aktif çalışma örneğidir. Yani:

```text
Program + çalışma zamanı kaynakları = Process
```

Bir process'in:

- Bellek alanı
- Process ID
- Açık dosyaları
- CPU durumu
- Yetkileri

gibi bilgileri vardır.

### Thread

Thread, process içindeki yürütme akışıdır. Bir process bir veya birden fazla thread içerebilir.

Örnek:

```text
Process
 ├── Thread 1
 ├── Thread 2
 └── Thread 3
```

Thread'ler aynı process içinde bazı kaynakları paylaşabilir.

---

<a id="kaynaktan-programa"></a>

## Kaynak Koddan Çalışan Programa Giden Yol

Bir geliştiricinin yazdığı kod doğrudan donanımın anlayacağı formatta değildir. Örneğin:

```c
int sonuc = 5 + 3;
```

CPU bu C sözdizimini doğrudan anlamaz. Kaynak kodun çalıştırılabilir hale gelmesi programlama diline göre farklı süreçlerden geçebilir. Basitleştirilmiş derlenen dil süreci:

```text
Source Code
   ↓
Compiler
   ↓
Object Code
   ↓
Linker
   ↓
Executable
   ↓
Loader
   ↓
RAM
   ↓
CPU
```

### Source Code

Geliştiricinin yazdığı insan tarafından okunabilir koddur.

### Compiler

Kaynak kodu daha düşük seviyeli bir forma dönüştürür.

### Object Code

Derleme sonucunda oluşan ara makine kodu parçalarıdır.

### Linker

Programın farklı parçalarını ve gerekli kütüphaneleri birleştirir.

### Executable

Çalıştırılabilir program dosyasıdır.

### Loader

İşletim sistemi çalıştırılabilir dosyayı RAM'e yükler ve process oluşturur.

---

<a id="compiler-interpreter-jit"></a>

## Compiler, Interpreter ve JIT

Programlama dillerinin çalışma modeli aynı değildir.

### Compiler

Kaynak kodu çalıştırmadan önce başka bir forma çevirir. Örnek diller:

- C
- C++
- Rust
- Go

Örnek:

```text
C Source Code
     ↓
Compiler
     ↓
Machine Code
```

### Interpreter

Kaynak kod veya ara temsil çalışma zamanında yorumlanır. Python buna klasik örneklerden biridir. Basitleştirilmiş anlatımla:

```text
Python Code
    ↓
Python Interpreter
    ↓
Runtime işlemleri
    ↓
CPU
```

Gerçek uygulama detayları Python implementasyonuna göre daha karmaşıktır; örneğin CPython kaynak kodu bytecode'a dönüştürür ve Python sanal makinesi bu bytecode'u yürütür.

### JIT – Just In Time Compilation

Bazı çalışma ortamlarında kodun belirli bölümleri çalışma sırasında makine koduna derlenebilir. Örneğin:

- Java JVM
- .NET CLR
- Modern JavaScript motorları

JIT, yorumlama esnekliği ile derlenmiş kod performansı arasında avantaj sağlamayı hedefler.

---

<a id="ide-terminal"></a>

## IDE, Kod Editörü, Terminal ve Shell

Bu kavramlar da sık karıştırılır.

### Kod Editörü

Kod yazmak için kullanılan uygulamadır. Örnek:

- Visual Studio Code
- Sublime Text
- Notepad++

### IDE

Integrated Development Environment yani tümleşik geliştirme ortamıdır. Genellikle:

- Kod editörü
- Debugger
- Build araçları
- Proje yönetimi
- Test araçları
- Refactoring özellikleri

gibi birçok özelliği tek ortamda sunar. Örnek:

- Visual Studio
- IntelliJ IDEA
- PyCharm
- Android Studio

VS Code teknik olarak güçlü bir kod editörüdür; eklentiler sayesinde IDE benzeri özellikler kazanabilir.

### Terminal

Komut satırı arayüzünü kullandığımız pencere veya uygulamadır.

### Shell

Terminal içinde komutları yorumlayan programdır. Örnekler:

- Bash
- Zsh
- PowerShell
- Command Prompt

Örneğin:

```bash
python app.py
```

komutunu yazdığımızda shell komutu yorumlar, işletim sisteminden ilgili programı başlatmasını ister.

---

<a id="system-call"></a>

## System Call Nedir?

Uygulamalar işletim sisteminin kernel servislerinden yararlanmak için system call mekanizmasını kullanır. Örneğin bir program:

- Dosya açmak
- Dosya okumak
- Ağ bağlantısı kurmak
- Yeni process oluşturmak
- Bellek istemek

istediğinde işletim sistemine başvurur. Basitleştirilmiş yapı:

```text
Uygulama
   ↓
System Call
   ↓
Kernel
   ↓
Donanım / Sistem Kaynağı
```

Örneğin:

```python
with open("data.txt", "r") as file:
    data = file.read()
```

kodunda Python bize yüksek seviyeli bir API sunar. Fakat en alt seviyede dosya okuma işlemi işletim sistemi servislerine dayanır.

---

<a id="program-calistirma"></a>

## Bir Program Çalıştırıldığında Arka Planda Neler Olur?

Bir uygulamayı çift tıklayıp açtığımızda veya terminalden çalıştırdığımızda basitleştirilmiş süreç şöyledir:

### 1. İşletim sistemi program dosyasını bulur

Örneğin:

```text
python.exe
node.exe
myapp.exe
```

### 2. Programın gerekli dosyaları diskten okunur

SSD veya HDD üzerinden program verileri alınır.

### 3. RAM'de alan ayrılır

Programın çalışabilmesi için gerekli kod ve veriler belleğe yüklenir.

### 4. Process oluşturulur

İşletim sistemi yeni bir process kaydı oluşturur.

### 5. Gerekli kütüphaneler yüklenir

Programın ihtiyaç duyduğu dinamik kütüphaneler belleğe alınabilir. Örneğin Windows'ta:

```text
.dll
```

Linux'ta:

```text
.so
```

dosyaları kullanılabilir.

### 6. CPU programın instruction'larını çalıştırmaya başlar

CPU scheduler tarafından zaman verildiğinde process'in thread'leri yürütülür.

### 7. Program gerektiğinde I/O işlemleri yapar

Örneğin:

- Dosya okur.
- Ağ isteği gönderir.
- Ekrana çıktı verir.
- Kullanıcı girdisi bekler.

### 8. Program kapanınca kaynaklar serbest bırakılır

İşletim sistemi process'in kullandığı kaynakları temizler.

---

<a id="vscode-sureci"></a>

## VS Code'da Kod Yazarken Bilgisayarda Neler Olur?

Şimdi tüm kavramları gerçek bir geliştirme senaryosunda birleştirelim.

### 1. Bilgisayar açılır

Firmware ve boot sürecinden sonra işletim sistemi yüklenir. İşletim sisteminin önemli parçaları diskten RAM'e alınır.

### 2. VS Code açılır

VS Code'a ait dosyalar SSD'den okunur. Gerekli kod ve veriler RAM'e yüklenir. İşletim sistemi VS Code için process'ler oluşturur. VS Code bazı işlemleri birden fazla process ile yönetebilir.

### 3. Proje klasörü açılır

Örneğin:

```text
my-project/
```

İşletim sistemi klasördeki dosyaları dosya sistemi üzerinden okur.

VS Code:

- Dosya adlarını
- Proje yapısını
- Extension bilgilerini
- Git durumunu
- Bazı kaynak kod içeriklerini

RAM'de tutabilir.

### 4. Kod yazılır

Klavye girişleri işletim sistemi üzerinden VS Code'a gelir. Editördeki açık dosyanın güncel hali bellekte tutulur.

### 5. IntelliSense çalışır

VS Code veya ilgili language server:

- Değişkenleri analiz eder.
- Fonksiyonları tarar.
- Tür bilgilerini çıkarır.
- Otomatik tamamlama önerileri üretir.

Bu işlemler CPU ve RAM kullanır.

### 6. Dosya kaydedilir

`Ctrl + S` yaptığımızda:

```text
RAM'deki güncel içerik
        ↓
İşletim sistemi
        ↓
Dosya sistemi
        ↓
SSD/HDD
```

şeklinde kalıcı depolamaya yazılır.

### 7. Program çalıştırılır

Örneğin terminalde:

```bash
python main.py
```

yazdığımızı düşünelim. Shell komutu yorumlar ve işletim sisteminden `python` process'ini başlatmasını ister. Python yorumlayıcısı `main.py` dosyasını okur ve çalıştırır.

### 8. CPU komutları yürütür

Python runtime'ın oluşturduğu düşük seviyeli işlemler CPU tarafından yürütülür.

### 9. Değişkenler RAM'de tutulur

Örneğin:

```python
name = "Ozge"
age = 23
```

gibi çalışma zamanı verileri bellekte tutulur.

### 10. Program çıktı üretir

Örneğin:

```python
print("Hello")
```

komutu terminale çıktı verir. İşletim sistemi bu çıktının ilgili terminal penceresinde görüntülenmesini sağlar.

---

<a id="kod-ornegi"></a>

## Basit Bir Kod Örneğinin Bilgisayar Açısından İncelenmesi

Aşağıdaki Python kodunu düşünelim:

```python
numbers = [10, 20, 30, 40]

total = 0

for number in numbers:
    total += number

print(total)
```

Program çıktısı:

```text
100
```

Bu kodu bilgisayar açısından inceleyelim.

### `numbers` listesi oluşturulur

Listeye ait veriler RAM'de tutulur.

### `total` değişkeni oluşturulur

Başlangıç değeri:

```text
0
```

olarak bellekte temsil edilir.

### `for` döngüsü çalışır

Program listedeki elemanları sırayla işler. CPU her iterasyonda gerekli komutları yürütür. Mantıksal olarak:

```text
0 + 10  = 10
10 + 20 = 30
30 + 30 = 60
60 + 40 = 100
```

### Sonuç ekrana yazdırılır

`print()` fonksiyonu ilgili runtime ve işletim sistemi servisleri üzerinden terminale çıktı gönderir. Bu küçük programda bile:

```text
CPU
RAM
Python Runtime
İşletim Sistemi
Terminal
```

birlikte çalışmaktadır.

---

<a id="hatalar"></a>

## Programlama Hataları: Syntax, Runtime ve Logic Error

Kod yazarken karşılaşılan hatalar bilgisayarın çalışma modelini anlamak açısından önemlidir.

### Syntax Error

Programlama dilinin yazım kurallarına uyulmamasıdır. Örneğin Python'da:

```python
if x > 10
    print(x)
```

Burada `:` eksik olduğu için syntax error oluşur.

### Runtime Error

Program başlar ancak çalışma sırasında hata meydana gelir. Örneğin:

```python
x = 10 / 0
```

Sıfıra bölme nedeniyle çalışma zamanı hatası oluşur.

### Logic Error

Program hata vermeden çalışabilir fakat yanlış sonuç üretir. Örneğin:

```python
ortalama = toplam / (adet - 1)
```

ifadesinde aslında `toplam / adet` yazılması gerekiyorsa program çalışabilir fakat sonuç yanlış olur. Bu tür hatalar debugger, test ve log mekanizmalarıyla bulunabilir.

---

<a id="performans"></a>

## Performans Darboğazları

Bir programın yavaş olması her zaman "CPU yavaş" anlamına gelmez. Performans sorunları farklı kaynaklardan oluşabilir. Örneğin:

- CPU yetersiz olabilir.
- RAM yetersiz olabilir.
- Disk işlemleri yavaş olabilir.
- Ağ bağlantısı gecikmeli olabilir.
- Veritabanı sorgusu kötü tasarlanmış olabilir.
- Algoritmanın zaman karmaşıklığı kötü olabilir.
- Gereksiz dosya okuma/yazma yapılabilir.
- Bellek erişim düzeni verimsiz olabilir.
- Çok fazla process veya thread çalışıyor olabilir.

Bu nedenle performans analizi yaparken darboğazın nerede olduğunu ölçmek gerekir.

---

<a id="bound"></a>

## CPU-Bound, Memory-Bound ve I/O-Bound İşlemler

### CPU-Bound

Programın süresinin büyük kısmı hesaplama yapmakla geçiyorsa CPU-bound olabilir. Örnek:

- Görüntü işleme
- Video encoding
- Büyük matematiksel hesaplamalar
- Bazı makine öğrenmesi işlemleri

Bu durumda daha güçlü CPU veya paralelleştirme performansı artırabilir.

### Memory-Bound

Programın performansı belleğe veri erişim hızından etkileniyorsa memory-bound olabilir. Örneğin çok büyük veri yapıları üzerinde yoğun bellek erişimi yapan uygulamalar bu kategoriye yaklaşabilir.

### I/O-Bound

Program çoğunlukla veri bekliyorsa I/O-bound olabilir. Örnek:

- Dosya okuma
- Veritabanı sorgusu bekleme
- API isteği bekleme
- Ağ üzerinden veri indirme

Örneğin:

```python
response = requests.get(url)
```

satırında CPU çoğu zaman ağdan cevap gelmesini bekler. Bu nedenle I/O-bound işlemlerde asynchronous programming veya concurrency gibi teknikler önemli hale gelir.

---

<a id="iliski"></a>

## Temel Kavramların Birbirleriyle İlişkisi

Bir bilgisayar sistemini tek bir parça üzerinden anlamak mümkün değildir. Genel ilişkiyi şu şekilde düşünebiliriz:

```text
                KULLANICI
                    │
                    ▼
             UYGULAMA / IDE
                    │
                    ▼
            PROGRAMMING RUNTIME
                    │
                    ▼
             İŞLETİM SİSTEMİ
          ┌─────────┼─────────┐
          │         │         │
          ▼         ▼         ▼
         CPU       RAM       DISK
          │         │         │
          └─────────┴─────────┘
                    │
                    ▼
                 DONANIM
```

Bir programın çalışabilmesi için:

1. Kod kalıcı depolamada bulunur.
2. Gerekli veriler RAM'e yüklenir.
3. İşletim sistemi process oluşturur.
4. CPU komutları yürütür.
5. Program gerektiğinde disk, ağ veya diğer aygıtlarla I/O işlemleri yapar.
6. İşletim sistemi kaynakların kullanımını kontrol eder.

Bu katmanların herhangi birinde oluşan problem uygulamanın performansını veya davranışını etkileyebilir.

---

<a id="ozet-tablo"></a>

## Özet Karşılaştırma Tablosu

| Kavram          | Temel Görev                                          | Geçici / Kalıcı | Örnek                                 |
| --------------- | ---------------------------------------------------- | --------------- | ------------------------------------- |
| CPU             | Komutları çalıştırır                                 | -               | Toplama, karşılaştırma, program akışı |
| Register        | CPU'nun çok hızlı küçük belleği                      | Geçici          | İşlem sırasında kullanılan değer      |
| CPU Cache       | Sık kullanılan verileri CPU'ya yakın tutar           | Geçici          | L1, L2, L3                            |
| RAM             | Aktif program ve verileri tutar                      | Geçici          | Çalışan uygulamalar                   |
| SSD/HDD         | Dosyaları saklar                                     | Kalıcı          | Kod, fotoğraf, uygulama               |
| İşletim Sistemi | Donanım ve yazılım kaynaklarını yönetir              | -               | Windows, Linux, macOS                 |
| Kernel          | İşletim sisteminin çekirdek katmanı                  | -               | Process, memory, driver yönetimi      |
| Program         | Diskte bulunan çalıştırılabilir kod                  | Kalıcı          | `python.exe`, `app.exe`               |
| Process         | Çalışan program örneği                               | Geçici          | Çalışan Python uygulaması             |
| Thread          | Process içindeki yürütme akışı                       | Geçici          | Worker thread                         |
| Compiler        | Kaynak kodu başka bir forma dönüştürür               | -               | GCC, Clang                            |
| Interpreter     | Kodu çalışma zamanında yorumlar                      | -               | Python interpreter                    |
| File System     | Dosyaları düzenler                                   | Kalıcı yapı     | NTFS, ext4                            |
| Driver          | İşletim sistemi ile donanım arasında iletişim sağlar | Kalıcı yazılım  | GPU driver                            |
| Shell           | Komutları yorumlar                                   | -               | Bash, PowerShell                      |
| Terminal        | Shell'e eriştiğimiz arayüz                           | -               | Windows Terminal                      |

---

<a id="mulakat"></a>

## Mülakat İçin Önemli Sorular ve Kısa Cevaplar

### 1. CPU nedir?

CPU, programların makine seviyesindeki komutlarını çalıştıran temel işlem birimidir. Matematiksel ve mantıksal işlemleri gerçekleştirir, program akışını yürütür.

### 2. RAM nedir?

RAM, çalışan programların ve aktif verilerin geçici olarak tutulduğu hızlı ana bellektir. Güç kesildiğinde normal koşullarda içerik kaybolur.

### 3. RAM ile SSD arasındaki fark nedir?

RAM aktif veriler için kullanılan çok hızlı fakat geçici bellektir. SSD ise dosyaların kalıcı olarak saklandığı daha yavaş depolama birimidir.

### 4. CPU doğrudan Python kodunu çalıştırır mı?

Doğrudan Python sözdizimini çalıştırmaz. Python interpreter/runtime kodu işler; CPU altta oluşan makine seviyesindeki instruction'ları yürütür.

### 5. Program ile process arasındaki fark nedir?

Program disk üzerinde bulunan pasif kod dosyasıdır. Process ise program çalıştırıldığında işletim sistemi tarafından oluşturulan aktif çalışma örneğidir.

### 6. Process ile thread arasındaki fark nedir?

Process kendi adres alanı ve kaynaklarına sahip çalışan program örneğidir. Thread ise process içindeki yürütme akışıdır. Aynı process içindeki thread'ler bazı kaynakları paylaşır.

### 7. Cache neden kullanılır?

CPU ile RAM arasındaki hız farkını azaltmak için sık kullanılan veriler CPU'ya daha yakın olan cache bellekte tutulur.

### 8. L1, L2 ve L3 cache arasındaki genel fark nedir?

L1 genellikle en küçük ve en hızlı cache'tir. L2 daha büyük, L3 ise daha da büyük fakat görece daha yavaştır.

### 9. İşletim sisteminin temel görevleri nelerdir?

CPU, RAM, process, dosya sistemi, aygıtlar, kullanıcılar, izinler ve I/O işlemlerini yönetir.

### 10. Kernel nedir?

Kernel, işletim sisteminin donanım kaynaklarını yöneten çekirdek katmanıdır.

### 11. Compiler ile interpreter arasındaki fark nedir?

Compiler kodu çalıştırılmadan önce başka bir forma dönüştürür. Interpreter ise kodu veya ara temsili çalışma zamanında işler. Modern runtime'lar bu iki yaklaşımın birleşimlerini de kullanabilir.

### 12. Virtual memory nedir?

Process'lere soyut bir bellek adres alanı sağlayan işletim sistemi mekanizmasıdır. Sanal adresler fiziksel RAM'e eşlenir; gerektiğinde bazı sistemlerde disk tabanlı swap/page file kullanılabilir.

### 13. System call nedir?

Bir uygulamanın kernel servislerinden yararlanmak için işletim sistemine yaptığı kontrollü çağrıdır.

### 14. SSD kullanmak programı her zaman hızlandırır mı?

Hayır. SSD özellikle dosya okuma/yazma gibi I/O işlemlerini hızlandırır. Eğer programın darboğazı CPU ise daha hızlı SSD sınırlı fayda sağlayabilir.

### 15. Yüksek GHz her zaman daha hızlı CPU anlamına gelir mi?

Hayır. CPU performansı mimari, IPC, çekirdek sayısı, cache, sıcaklık ve programın çalışma biçimi gibi birçok faktöre bağlıdır.

### 16. Bir program çalıştırıldığında ilk olarak ne olur?

İşletim sistemi program dosyasını bulur, gerekli bölümleri RAM'e yükler, process oluşturur ve scheduler aracılığıyla CPU üzerinde çalıştırılmasını sağlar.

### 17. Ctrl + S yaptığımızda ne olur?

Editördeki güncel dosya içeriği işletim sistemi üzerinden dosya sistemine ve kalıcı depolamaya yazılır.

### 18. CPU-bound ve I/O-bound farkı nedir?

CPU-bound programlar zamanlarının büyük kısmını hesaplama yaparak geçirir. I/O-bound programlar ise dosya, ağ veya veritabanı gibi dış kaynaklardan veri bekleyerek zaman harcar.

---

<a id="sonuc"></a>

## Genel Sonuç

Bilgisayar üzerinde kod yazmak dışarıdan bakıldığında yalnızca bir editöre metin girmek gibi görünse de arka planda oldukça kapsamlı bir sistem birlikte çalışır.

Bir kod dosyasını açtığımız anda disk ve dosya sistemi devreye girer. Editör ve proje dosyaları RAM'e yüklenir. İşletim sistemi uygulamaları process'ler halinde yönetir. CPU gerekli komutları çalıştırır. Program dosya, ağ veya kullanıcı girdisine ihtiyaç duyduğunda işletim sistemi üzerinden I/O işlemleri gerçekleştirilir.

Bu nedenle şu dört temel kavramı birbirinden ayırmak özellikle önemlidir:

```text
CPU  → İşler
RAM  → Aktif veriyi geçici olarak tutar
Disk → Veriyi kalıcı olarak saklar
OS   → Tüm kaynakları yönetir
```

Ancak bilgisayar biliminin temelini gerçekten anlamak için bunun bir adım ötesine geçmek gerekir. CPU cache, register, process, thread, virtual memory, file system, compiler, interpreter, system call ve kernel gibi kavramlar da bu sistemin tamamlayıcı parçalarıdır.

Bir yazılım geliştirici için bu bilgilerin önemi yalnızca teorik değildir. Bu temel sayesinde:

- Programların neden yavaşladığını daha doğru analiz edebiliriz.
- RAM kullanımını ve bellek problemlerini daha iyi anlayabiliriz.
- Process ve thread mantığını kavrayabiliriz.
- Compiler ve interpreter farkını anlayabiliriz.
- İşletim sistemi ile uygulamalar arasındaki ilişkiyi görebiliriz.
- Dosya ve I/O işlemlerinin performans etkisini yorumlayabiliriz.
- İleride öğreneceğimiz veri yapıları, işletim sistemleri, concurrency, backend, veritabanı, networking ve system design konularını daha sağlam bir temel üzerine oturtabiliriz.

Kısacası yazılım geliştirme yalnızca "kod yazmak" değildir. Yazdığımız kodun bilgisayarın hangi katmanlarında, hangi kaynakları kullanarak ve hangi süreçlerden geçerek çalıştığını anlamak; daha bilinçli, performans odaklı ve profesyonel yazılım geliştirebilmenin temelidir.
