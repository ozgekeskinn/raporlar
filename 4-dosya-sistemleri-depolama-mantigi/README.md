# 4) Dosya Sistemleri ve Depolama Mantığı

Bu raporda dosya sistemleri ve depolama mantığı kapsamında NTFS, ext4 ve APFS dosya sistemlerinin farkları; blok yapısı; HDD ve SSD çalışma prensipleri; veri okuma/yazma hızlarının nereden geldiği detaylı şekilde incelenmiştir.

Bilgisayarda bir dosya oluşturduğumuzda aslında sadece masaüstüne bir belge koymuş olmayız. İşletim sistemi bu dosyanın adını, konumunu, boyutunu, izinlerini, hangi disk bloklarında saklandığını ve ne zaman değiştirildiğini bir dosya sistemi aracılığıyla yönetir.

Yani dosya sistemi, diskin içindeki verileri düzenleyen ve işletim sistemine “bu dosya nerede, nasıl okunacak, kim erişebilir?” bilgisini veren yapıdır.

---

## Dosya Sistemi Nedir?

Dosya sistemi, depolama birimlerinde verilerin nasıl tutulacağını, düzenleneceğini, bulunacağını ve erişileceğini belirleyen yapıdır.

Bir HDD, SSD, USB bellek veya hafıza kartı tek başına sadece ham depolama alanıdır. Bu alanın anlamlı şekilde kullanılabilmesi için bir dosya sistemine ihtiyaç vardır.

Örneğin bir bilgisayarda klasör yapısı şu şekilde görünebilir:

```text
C:
 ├── Users
 │    └── Ozge
 │         ├── Desktop
 │         ├── Documents
 │         └── Downloads
 └── Program Files
```

Bu klasör yapısını bize gösteren şey işletim sistemidir. Ancak arka planda bu düzeni oluşturan temel mekanizma dosya sistemidir. Dosya sistemi genel olarak şu bilgileri yönetir:

```text
Dosya adı
Dosya boyutu
Dosyanın diskteki fiziksel konumu
Dosya izinleri
Oluşturulma tarihi
Değiştirilme tarihi
Klasör yapısı
Boş ve dolu alan bilgisi
```

Mesela `odev.pdf` adlı bir dosya masaüstünde duruyor gibi görünür. Ancak gerçekte bu dosya diskin farklı bloklarına parçalar halinde yazılmış olabilir. Dosya sistemi, bu parçaların nerede olduğunu bilir ve kullanıcı dosyayı açtığında parçaları birleştirip dosyayı düzgün şekilde gösterir.

Bu nedenle dosya sistemi, kullanıcı ile depolama donanımı arasında bir düzenleme katmanı gibi düşünülebilir. Kullanıcı dosyaları isimleriyle ve klasörleriyle görürken, bilgisayar arka planda bu dosyaları bloklar, adresler ve metadata bilgileriyle yönetir.

Dosya sistemi olmasaydı disk üzerinde bulunan veriler anlamlı dosya ve klasörler halinde görüntülenemezdi. Yani işletim sistemi hangi verinin hangi dosyaya ait olduğunu, hangi kullanıcının hangi dosyaya erişebileceğini ve dosyanın diskte nerede bulunduğunu bilemezdi.

---

## NTFS, ext4 ve APFS Farkları

Farklı işletim sistemleri farklı dosya sistemleri kullanır. Windows, Linux ve macOS kendi ihtiyaçlarına göre farklı dosya sistemleri geliştirmiştir. En çok kullanılan dosya sistemlerinden bazıları şunlardır:

```text
NTFS  → Windows
ext4  → Linux
APFS  → macOS
```

Bu dosya sistemlerinin temel amacı aynıdır: Verileri düzenli, güvenli ve erişilebilir şekilde depolamak. Ancak her biri farklı işletim sistemleri için geliştirilmiştir ve sundukları özellikler birbirinden farklıdır.

---

## NTFS Nedir?

NTFS, yani **New Technology File System**, Windows işletim sistemlerinde kullanılan modern dosya sistemidir.

Windows’ta C diski genellikle NTFS olarak biçimlendirilir. Günümüzde Windows işletim sistemlerinde en yaygın kullanılan dosya sistemlerinden biridir. NTFS’nin güçlü olduğu noktalar şunlardır:

```text
Dosya izinlerini destekler.
Büyük dosya boyutlarını destekler.
Journaling özelliği vardır.
Şifreleme desteği sunar.
Disk kotası kullanılabilir.
Windows ile yüksek uyumludur.
```

NTFS özellikle güvenlik ve kararlılık açısından güçlü bir dosya sistemidir. Kullanıcı izinleri, dosya sahipliği ve erişim kontrolü gibi özellikler Windows ortamında çok önemlidir.

Örneğin bir bilgisayarda birden fazla kullanıcı hesabı varsa, bazı dosyalara sadece belirli kullanıcıların erişmesi istenebilir. NTFS bu tarz izinleri yönetebilir. Bu nedenle Windows sistemlerde hem kişisel kullanımda hem de kurumsal ortamlarda yaygın şekilde tercih edilir.

NTFS’nin önemli özelliklerinden biri **journaling** desteğidir.

Journaling, dosya sisteminin işlem günlüğü tutmasıdır. Mesela bir dosya kopyalanırken elektrik kesilirse ya da sistem aniden kapanırsa, dosya sistemi işlem günlüğüne bakarak hangi işlemin yarım kaldığını anlayabilir. Örneğin:

```text
Bir dosya taşınıyor.
İşlem yarıda kesiliyor.
NTFS işlem günlüğüne bakarak sistemi daha güvenli şekilde toparlıyor.
```

Bu özellik veri bozulmasını azaltır ve sistemin daha güvenilir çalışmasını sağlar. NTFS, özellikle Windows ortamında dosya güvenliği, büyük dosya desteği ve sistem kararlılığı açısından önemli avantajlar sunar.

---

## ext4 Nedir?

ext4, Linux sistemlerde en yaygın kullanılan dosya sistemlerinden biridir. Açılımı **Fourth Extended File System** şeklindedir.

Ubuntu, Debian, Fedora gibi birçok Linux dağıtımında yaygın olarak kullanılır. ext4’ün güçlü olduğu noktalar şunlardır:

```text
Linux ile yüksek uyumludur.
Kararlı ve güvenilir bir yapıya sahiptir.
Journaling desteği vardır.
Büyük diskleri ve büyük dosyaları destekler.
Performansı genellikle iyidir.
Fragmentation oranı düşüktür.
```

ext4, Linux ortamında sade, güvenilir ve hızlı çalışmasıyla bilinir. Özellikle sunucularda ve geliştirici makinelerinde sık tercih edilir.

NTFS daha çok Windows dünyasına uygunken, ext4 Linux dünyasına daha uygundur.

Örneğin bir Linux sunucuda web sitesi dosyaları, log dosyaları, kullanıcı dosyaları veya sistem dosyaları genellikle ext4 üzerinde tutulabilir.

ext4 dosya sistemi, Linux sistemlerde performans ve kararlılık açısından oldukça yaygın bir seçenektir. Özellikle sistem dosyaları, uygulama dosyaları ve kullanıcı dizinleri için güvenilir bir yapı sunar.

ext4 de journaling desteğine sahiptir. Bu sayede sistem beklenmedik şekilde kapansa bile dosya sistemi tutarlılığını korumaya yardımcı olur.

Linux sistemlerde dosya izinleri, kullanıcı sahipliği ve grup yapısı oldukça önemlidir. ext4 bu yapılarla uyumlu çalışır. Bu nedenle Linux sistemlerde hem kişisel bilgisayarlarda hem de sunucu ortamlarında yaygın şekilde kullanılır.

---

## APFS Nedir?

APFS, yani **Apple File System**, Apple tarafından geliştirilen modern dosya sistemidir. macOS, iOS ve iPadOS gibi Apple ekosistemindeki sistemlerde kullanılır. 

APFS özellikle SSD ve flash depolama için tasarlanmıştır. Bu yüzden modern Mac cihazlarda oldukça verimli çalışır. APFS’nin güçlü olduğu noktalar şunlardır:

```text
SSD odaklı tasarlanmıştır.
Snapshot desteği vardır.
Güçlü şifreleme desteği vardır.
Copy-on-write mantığı kullanır.
Alan paylaşımı yapabilir.
macOS ile yüksek uyumludur.
```

APFS’nin önemli özelliklerinden biri **snapshot** desteğidir. Snapshot, sistemin belirli bir andaki durumunun görüntüsünün alınmasıdır. Örneğin macOS güncelleme yapmadan önce sistemin anlık görüntüsü alınabilir. Bir sorun olursa sistem eski haline döndürülebilir.

Bir diğer önemli kavram ise **copy-on-write** yapısıdır. Copy-on-write mantığında veri doğrudan eski verinin üzerine yazılmaz. Önce yeni veri farklı bir alana yazılır, sonra referans güncellenir. Bu yaklaşım veri güvenliği açısından avantaj sağlar.

APFS, modern Apple cihazlarında özellikle SSD performansını daha verimli kullanmak amacıyla geliştirilmiştir. Bu yüzden klasik mekanik disklerden çok flash tabanlı depolama birimleri için daha uygundur.

Ayrıca APFS güçlü şifreleme desteği sunar. Apple ekosisteminde güvenlik önemli olduğu için dosya sistemi seviyesinde şifreleme desteği büyük avantaj sağlar.

---

## NTFS, ext4 ve APFS Karşılaştırması

Aşağıdaki tabloda NTFS, ext4 ve APFS dosya sistemlerinin temel farkları gösterilmiştir:

| Özellik | NTFS | ext4 | APFS |
|---|---|---|---|
| Kullanıldığı sistem | Windows | Linux | macOS / iOS |
| Geliştirici | Microsoft | Linux topluluğu | Apple |
| Journaling | Var | Var | Farklı modern mekanizmalar var |
| SSD optimizasyonu | Orta / iyi | İyi | Çok iyi |
| Şifreleme | Var | Harici çözümlerle kullanılabilir | Güçlü yerleşik destek |
| Snapshot | Yerleşik olarak temel özellik değildir | Yerleşik olarak temel özellik değildir | Var |
| Dosya izinleri | Gelişmiş | Gelişmiş | Gelişmiş |
| En uygun kullanım | Windows bilgisayarlar | Linux sistemler | Apple cihazlar |

Ancak bu sadece uyumluluk meselesi değildir. Her dosya sistemi kendi işletim sisteminin ihtiyaçlarına göre optimize edilmiştir. Örneğin Windows ortamında NTFS, kullanıcı izinleri ve güvenlik yönetimi için güçlü bir yapı sunarken; Linux ortamında ext4 daha doğal ve kararlı bir çözüm sunar. Apple cihazlarında ise APFS, özellikle SSD ve şifreleme odaklı modern ihtiyaçlara göre tasarlanmıştır.

---

## Blok Yapısı Nedir?

Disklerde veriler tek parça halinde tutulmaz. Depolama birimleri küçük parçalara ayrılır. Bu parçalara genellikle **blok** denir. Bir blok, dosya sisteminin veri yazıp okurken kullandığı en küçük birimlerden biridir. 

Örneğin blok boyutu 4 KB olabilir. Bu durumda 10 KB’lık bir dosya kaydedildiğinde dosya bloklara şu şekilde yerleştirilebilir:

```text
1. blok → 4 KB
2. blok → 4 KB
3. blok → 2 KB veri + kalan boş alan
```

Yani 10 KB’lık dosya 3 blok kullanır. İşletim sistemi dosyaları byte byte değil, genellikle bloklar üzerinden yönetir. Bu yüzden dosyanın diskte kapladığı alan ile gerçek dosya boyutu her zaman birebir aynı olmayabilir.

---

## Blok Yapısı Neden Önemlidir?

Blok yapısı, dosya sisteminin veriyi nasıl organize ettiğini anlamak için çok önemlidir. Mesela kullanıcı `rapor.docx` dosyasını açmak istediğinde sistem şu adımları izler:

```text
1. Dosya sistemine sorar: Bu dosya nerede?
2. Dosya sistemi dosyanın hangi bloklarda olduğunu bulur.
3. Diskten ilgili bloklar okunur.
4. Dosya kullanıcıya gösterilir.
```

Dosya küçük bile olsa en az bir blok yer kaplar. Örneğin blok boyutu 4 KB ise ve dosya 1 KB ise:

```text
Dosya boyutu: 1 KB
Kapladığı alan: 4 KB
Boşa giden alan: 3 KB
```

Bu nedenle blok boyutu hem performans hem de disk alanı kullanımı açısından önemlidir. Eğer blok boyutu çok büyük olursa küçük dosyalar gereksiz yere fazla alan kaplayabilir. Eğer blok boyutu çok küçük olursa da büyük dosyalar çok fazla parçaya bölünebilir ve dosya sisteminin yönetmesi gereken blok sayısı artabilir.

---

## Büyük Blok ve Küçük Blok Farkı

Blok boyutu küçük olursa disk alanı daha verimli kullanılabilir. Çünkü küçük dosyalar gereksiz yere fazla alan kaplamaz. Ancak çok küçük blok boyutu da dosya yönetimini zorlaştırabilir. Büyük dosyalar çok fazla bloğa bölünür ve dosya sisteminin takip etmesi gereken blok sayısı artar.

Blok boyutu büyük olursa büyük dosyalar daha hızlı yönetilebilir. Ancak küçük dosyalarda alan israfı artabilir.

Özetle:

```text
Küçük blok → Daha az alan israfı, daha fazla yönetim yükü
Büyük blok → Daha hızlı büyük dosya erişimi, daha fazla alan israfı
```

Bu nedenle dosya sistemleri blok boyutunu seçerken performans ve alan kullanımı arasında denge kurmaya çalışır.

---

## HDD Çalışma Prensibi

HDD, yani **Hard Disk Drive**, mekanik yapıya sahip bir depolama birimidir. İçinde dönen manyetik plakalar ve bu plakalar üzerinde okuma/yazma yapan bir kafa bulunur. HDD’nin temel parçaları şunlardır:

```text
Platter → Manyetik disk plakası
Spindle → Plakaları döndüren motor
Read/Write Head → Okuma-yazma kafası
Actuator Arm → Kafayı hareket ettiren kol
```

HDD çalışırken plakalar döner, okuma-yazma kafası doğru konuma gider ve veri manyetik olarak okunur veya yazılır. HDD’lerde veri fiziksel olarak manyetik plakalar üzerinde saklanır. Bu plakalar yüksek hızda döner. Okuma/yazma kafası ise istenen verinin bulunduğu bölgeye hareket eder. Bu mekanik yapı nedeniyle HDD’lerde veri erişimi SSD’lere göre daha yavaştır. Çünkü veriye ulaşmak için fiziksel hareket gerekir.

---

## HDD’de Veri Okuma Nasıl Olur?

Bir dosya açıldığında HDD şu adımları izler:

```text
1. İşletim sistemi dosyanın hangi bloklarda olduğunu öğrenir.
2. HDD okuma kafasını ilgili bölgeye götürür.
3. Plaka dönerken doğru sektörün kafanın altına gelmesi beklenir.
4. Veri okunur.
```

Burada iki önemli gecikme vardır:

```text
Seek time → Kafanın doğru konuma gitme süresi
Rotational latency → Plakanın doğru noktaya dönmesini bekleme süresi
```

**Seek time**, okuma/yazma kafasının verinin bulunduğu konuma gitmesi için geçen süredir.

**Rotational latency** ise dönen plakanın doğru noktasının okuma kafasının altına gelmesini bekleme süresidir.

Bu iki mekanik gecikme HDD performansını ciddi şekilde etkiler. Özellikle küçük ve dağınık dosyalar okunurken HDD daha fazla zorlanır. Çünkü kafa sürekli farklı bölgelere gitmek zorunda kalır.

---

## HDD’nin Avantajları

HDD’lerin avantajları şunlardır:

```text
Daha ucuzdur.
Yüksek kapasiteyi daha uygun fiyatla sunar.
Arşivleme için uygundur.
Uzun süreli veri depolamada maliyet avantajı sağlar.
```

HDD’ler özellikle büyük boyutlu fotoğraf, video, yedek ve arşiv dosyalarını saklamak için tercih edilebilir. Örneğin çok fazla film, fotoğraf veya yedek dosyası saklanacaksa HDD fiyat/kapasite açısından avantajlıdır.

---

## HDD’nin Dezavantajları

HDD’lerin dezavantajları şunlardır:

```text
Mekanik olduğu için yavaştır.
Darbe ve düşmeye karşı hassastır.
Ses çıkarabilir.
Daha fazla enerji tüketebilir.
Rastgele erişim performansı düşüktür.
```

Özellikle işletim sistemi, oyunlar veya yazılım geliştirme ortamları HDD üzerinde çalışıyorsa sistem genel olarak daha yavaş hissedilir. Bilgisayarın geç açılması, programların yavaş başlaması veya dosya aramalarının uzun sürmesi HDD’nin mekanik yapısından kaynaklanabilir.

---

## SSD Çalışma Prensibi

SSD, yani **Solid State Drive**, mekanik parça içermeyen depolama birimidir.

Veriler NAND flash bellek hücrelerinde tutulur. SSD içinde dönen plaka veya hareket eden kafa yoktur. Bu yüzden SSD’ler HDD’lere göre çok daha hızlıdır. SSD’nin temel yapısı şunlardan oluşur:

```text
NAND flash bellek hücreleri
Controller
Cache
Firmware
```

SSD’de en önemli parçalardan biri **controller** yapısıdır.

Controller, verinin nereye yazılacağını, nereden okunacağını, boş alanların nasıl yönetileceğini ve hücrelerin nasıl dengeli kullanılacağını belirler. SSD’lerde veri elektronik olarak okunur ve yazılır. Bu nedenle mekanik gecikmeler yoktur. Veriye erişim süresi HDD’ye göre çok daha düşüktür.

---

## SSD’de Veri Okuma Nasıl Olur?

SSD’de okuma işlemi elektronik olarak yapılır. Bir dosya okunmak istendiğinde süreç genel olarak şu şekilde işler:

```text
1. İşletim sistemi dosyanın adresini ister.
2. SSD controller ilgili NAND hücrelerini bulur.
3. Veri elektronik olarak okunur.
```

Burada mekanik hareket olmadığı için bekleme süresi çok düşüktür. SSD’nin hızlı olmasının temel sebepleri şunlardır:

```text
Hareket eden parça yoktur.
Veriye elektronik olarak erişilir.
Rastgele erişim süresi çok düşüktür.
Küçük dosya erişimlerinde çok daha başarılıdır.
```

Bu nedenle SSD kullanılan bilgisayarlarda işletim sistemi daha hızlı açılır, programlar daha hızlı başlar ve genel sistem tepkileri daha akıcı olur.

---

## SSD’de Veri Yazma Mantığı

SSD’lerde veri yazma işlemi HDD’ye göre daha karmaşıktır. Çünkü SSD’lerde veri sayfa düzeyinde yazılır ama blok düzeyinde silinir.

Basitçe:

```text
Okuma → Hızlı
Yazma → Hızlı ama yönetim gerektirir
Silme → Blok düzeyinde yapılır
```

SSD’lerde veri yönetimi için bazı özel mekanizmalar kullanılır:

```text
Wear leveling
Garbage collection
TRIM
```

Bu mekanizmalar SSD’nin hem performansını korumak hem de ömrünü uzatmak için kullanılır.

---

## Wear Leveling Nedir?

SSD hücrelerinin sınırlı yazma ömrü vardır. Aynı hücreye sürekli veri yazılırsa o hücre daha hızlı yıpranır.

Wear leveling, yazma işlemlerini SSD hücrelerine dengeli dağıtarak hücrelerin eşit şekilde kullanılmasını sağlar. Yani SSD şunu yapmaya çalışır:

```text
Aynı yere sürekli yazma.
Tüm hücreleri dengeli kullan.
SSD ömrünü uzat.
```

Bu yapı sayesinde SSD içerisindeki bazı hücrelerin çok hızlı yıpranması engellenir. Wear leveling, SSD’nin uzun süre daha sağlıklı çalışmasına yardımcı olur.

---

## Garbage Collection Nedir?

SSD’de silinen dosyalar hemen fiziksel olarak tamamen temizlenmeyebilir. Garbage collection, artık kullanılmayan veri alanlarını arka planda temizleyerek yeni yazma işlemleri için hazır hale getirir. Bu işlem SSD performansını korumaya yardımcı olur. 

Eğer kullanılmayan alanlar düzenli temizlenmezse SSD yeni veri yazarken daha fazla işlem yapmak zorunda kalabilir. Bu da performans düşüşüne neden olabilir. Garbage collection sayesinde SSD, kullanılmayan alanları daha verimli yönetir.

---

## TRIM Nedir?

TRIM, işletim sisteminin SSD’ye “bu veri artık kullanılmıyor” bilgisini göndermesidir. Mesela kullanıcı bir dosyayı sildiğinde işletim sistemi SSD’ye bu alanın artık boş kabul edilebileceğini bildirir. Böylece SSD ileride veri yazarken daha verimli çalışır.

TRIM yoksa SSD zamanla yavaşlayabilir. Çünkü SSD hangi alanların gerçekten boş olduğunu anlamakta zorlanabilir. TRIM sayesinde SSD, silinen dosyaların kapladığı alanları daha doğru şekilde yönetir ve performansını uzun vadede koruyabilir.

---

## HDD ve SSD Karşılaştırması

Aşağıdaki tabloda HDD ve SSD arasındaki temel farklar gösterilmiştir:

| Özellik | HDD | SSD |
|---|---|---|
| Yapı | Mekanik | Elektronik |
| Veri saklama | Manyetik plaka | NAND flash bellek |
| Hareketli parça | Var | Yok |
| Hız | Daha yavaş | Daha hızlı |
| Rastgele erişim | Düşük | Çok yüksek |
| Ses | Ses çıkarabilir | Sessiz |
| Darbe dayanımı | Daha hassas | Daha dayanıklı |
| Enerji tüketimi | Daha fazla olabilir | Genellikle daha düşüktür |
| Fiyat/kapasite | Daha uygun | Daha pahalı |
| Kullanım alanı | Arşiv, yedekleme | İşletim sistemi, programlar, oyunlar |

Kısaca:

```text
HDD → Ucuz ve yüksek kapasite için mantıklı
SSD → Hız ve performans için mantıklı
```

En ideal kullanım genelde şu şekildedir:

```text
SSD → Windows/Linux/macOS, programlar, aktif projeler
HDD → Fotoğraf, video, arşiv, yedek
```

Modern bilgisayarlarda işletim sistemi için SSD tercih edilmesi sistem performansını ciddi şekilde artırır. HDD ise yüksek kapasiteli dosyaları saklamak için hâlâ kullanışlıdır.

---

## Veri Okuma/Yazma Hızları Nereden Gelir?

Bir depolama biriminin hızlı veya yavaş olması sadece “SSD mi HDD mi?” sorusuna bağlı değildir. Birden fazla faktör vardır. Veri okuma/yazma hızlarını etkileyen başlıca faktörler şunlardır:

```text
Depolama biriminin fiziksel yapısı
Sıralı okuma/yazma performansı
Rastgele okuma/yazma performansı
IOPS değeri
Bağlantı arayüzü
Cache kullanımı
Dosya sistemi yapısı
Fragmentation durumu
```

Bu faktörlerin her biri disk performansını farklı şekillerde etkiler.

---

## Fiziksel Yapı

HDD mekanik olduğu için veriye ulaşması zaman alır. Okuma kafasının hareket etmesi ve diskin dönmesi gerekir. 

SSD’de ise hareketli parça yoktur. Veriye elektronik olarak erişilir. Bu yüzden SSD’nin erişim süresi çok daha düşüktür.

```text
HDD → Milisaniye seviyesinde erişim
SSD → Mikrosaniye seviyesine yakın erişim
```

Bu fark özellikle bilgisayar açılışında, program başlatmada ve küçük dosyaları okurken çok hissedilir. Örneğin bir işletim sistemi açılırken çok sayıda küçük dosya okunur. HDD bu dosyalar için sürekli farklı fiziksel konumlara gitmek zorunda kalırken, SSD bu verilere elektronik olarak çok daha hızlı erişebilir.

---

## Sıralı Okuma/Yazma ve Rastgele Okuma/Yazma

Disk performansında iki temel hız türü vardır:

```text
Sequential read/write → Sıralı okuma/yazma
Random read/write → Rastgele okuma/yazma
```

Bu iki hız türü, depolama biriminin gerçek hayattaki performansını anlamak için çok önemlidir.

---

### Sıralı Okuma/Yazma Nedir?

Sıralı okuma/yazma, büyük bir dosyanın baştan sona okunması veya yazılmasıdır.

Örneğin:

```text
10 GB video dosyası kopyalamak
ISO dosyası taşımak
Büyük yedek dosyası oluşturmak
```

Bu durumda veri disk üzerinde ardışık şekilde okunur veya yazılır. HDD’ler sıralı işlemlerde fena değildir. Çünkü kafa bir noktaya gider ve veri ardışık okunur. Ancak yine de SSD’ler genel olarak daha hızlıdır.

Sıralı okuma/yazma değerleri genellikle disklerin tanıtımında “MB/s” veya “GB/s” olarak gösterilir.

---

### Rastgele Okuma/Yazma Nedir?

Rastgele okuma/yazma, küçük dosyaların veya parçalanmış verilerin diskin farklı yerlerinden okunmasıdır.

Örneğin:

```text
İşletim sistemi açılışı
Program başlatma
Tarayıcı cache dosyaları
Veritabanı işlemleri
Node_modules klasörü
IDE açılışı
```

Bu işlemlerde disk farklı konumlardaki çok sayıda küçük veriye erişmek zorundadır. SSD burada çok daha iyidir çünkü mekanik kafa bekleme süresi yoktur. Bu yüzden SSD’ye geçince bilgisayarın “uçuyor gibi” hissettirmesinin ana sebebi sadece yüksek MB/s değeri değildir. Asıl fark çoğu zaman rastgele erişim performansından gelir.

Günlük kullanımda program açma, işletim sistemi başlatma, proje klasörü tarama gibi işlemler rastgele okuma/yazma performansından çok etkilenir.

---

## IOPS Nedir?

IOPS, **Input/Output Operations Per Second** ifadesinin kısaltmasıdır. Saniyede kaç tane okuma/yazma işlemi yapılabildiğini gösterir. Özellikle küçük dosya işlemlerinde önemlidir.

Örneğin:

```text
Bir işletim sistemi açılırken binlerce küçük dosya okunur.
Bir IDE proje açarken çok sayıda bağımlılığı tarar.
Bir veritabanı sürekli küçük okuma/yazma yapar.
```

Bu durumlarda MB/s hızından çok IOPS önem kazanır.

SSD’lerin IOPS değeri HDD’lere göre çok daha yüksektir. Bu yüzden işletim sistemleri SSD üzerinde çok daha hızlı çalışır. IOPS özellikle sunucular, veritabanları, sanal makineler ve yazılım geliştirme ortamları için çok önemlidir.

---

## Arayüz ve Bağlantı Türü Hızı Etkiler

Depolama biriminin kendisi hızlı olsa bile, bilgisayara bağlandığı arayüz de hızı sınırlar. Yaygın bağlantılar şunlardır:

```text
SATA
NVMe
PCIe
USB
```

Örneğin çok hızlı bir SSD, yavaş bir bağlantı arayüzüyle kullanılırsa tam performansını gösteremez. Bu nedenle sadece diskin SSD olması yeterli değildir. SSD’nin hangi bağlantı türüyle sisteme bağlı olduğu da önemlidir.

---

### SATA SSD

- SATA SSD’ler HDD’lerle aynı SATA arayüzünü kullanır. 
- Genellikle yaklaşık 500 MB/s civarında hızlara ulaşabilir.
- HDD’ye göre çok hızlıdır ama NVMe SSD’ye göre daha sınırlıdır.
- SATA SSD, eski bilgisayarlarda performans artışı sağlamak için oldukça mantıklı bir yükseltmedir. HDD’den SATA SSD’ye geçmek bilgisayarın açılış hızını, program başlatma süresini ve genel kullanım akıcılığını ciddi şekilde iyileştirebilir.

---

### NVMe SSD
- NVMe SSD’ler PCIe hattını kullanır. SATA’ya göre çok daha yüksek hız sunar.
- Modern NVMe SSD’ler birkaç GB/s okuma-yazma hızına ulaşabilir.
- Bu yüzden büyük dosya taşıma, video düzenleme, oyun yükleme, yazılım geliştirme ve sanal makine kullanımında ciddi avantaj sağlar.
- NVMe SSD’ler özellikle yüksek performans gerektiren işlemlerde büyük avantaj sağlar. Ancak günlük kullanımda SATA SSD bile HDD’ye göre çok büyük bir hız farkı oluşturur.

---

## Cache Kullanımı

Disklerde cache yani önbellek bulunabilir. Cache, sık kullanılan veya geçici olarak işlenen verilerin daha hızlı erişilen bir alanda tutulmasını sağlar.

Örneğin bir dosya kopyalanırken ilk başta hız çok yüksek görünüp sonra düşebilir. Bunun sebebi verinin önce cache’e yazılması, cache dolunca gerçek yazma hızının ortaya çıkmasıdır. Bu yüzden bazı disklerde kısa süreli hız çok yüksek görünür ama uzun süreli büyük dosya kopyalamada hız düşer.

Cache performansı özellikle büyük dosya transferlerinde fark edilebilir. İlk başta yüksek görünen hız, işlem uzadıkça düşebilir. Bu durum diskin gerçek sürekli yazma performansının cache dolduktan sonra ortaya çıkmasından kaynaklanır.

---

## Fragmentation Nedir?

Fragmentation, bir dosyanın diskte parçalı şekilde farklı yerlere dağılmasıdır. 

HDD’de bu büyük bir performans sorunu olabilir. Çünkü okuma kafası dosyanın parçalarını toplamak için farklı konumlara gitmek zorunda kalır. Örneğin:

```text
film.mp4 dosyasının parçaları diskin farklı bölgelerinde olabilir.
HDD kafası bu parçaları tek tek arar.
Okuma süresi uzar.
```

SSD’de fragmentation etkisi çok daha azdır. Çünkü SSD’de mekanik kafa yoktur. Fakat yine de dosya sistemi düzeni performansı etkileyebilir.

HDD’lerde bu yüzden disk birleştirme, yani defragmentation yapılabilir. SSD’lerde klasik defrag önerilmez çünkü gereksiz yazma işlemi SSD ömrünü azaltabilir. Bu nedenle HDD ve SSD bakımında farklı yaklaşımlar vardır. HDD için disk birleştirme faydalı olabilirken, SSD için TRIM gibi mekanizmalar daha önemlidir.

---

## Günlük Hayattan Örnek

Dosya sistemi ve depolama mantığını bir kütüphane örneğiyle düşünebiliriz.

HDD şöyle çalışır:

```text
Görevli raflara fiziksel olarak gider.
Kitabı bulur.
Sayfaları alır.
Başka kitap gerekiyorsa başka rafa gider.
```

SSD şöyle çalışır:

```text
Kitapların konumu elektronik sistemde anında bulunur.
Fiziksel yürüyüş yoktur.
Veriye çok daha hızlı erişilir.
```

Dosya sistemi ise bu kütüphanenin katalog sistemidir.

```text
Dosya sistemi → Hangi kitap nerede?
HDD/SSD → Kitabın fiziksel olarak saklandığı yer
İşletim sistemi → Kullanıcının kitap istemesini yöneten yapı
```

Bu örnekte dosya sistemi, dosyaların nerede olduğunu bilen düzenleyici yapıdır. HDD veya SSD ise bu dosyaların fiziksel olarak tutulduğu depolama ortamıdır.

Kullanıcı bir dosyayı açmak istediğinde işletim sistemi dosya sisteminden dosyanın yerini öğrenir. Daha sonra depolama biriminden ilgili veriler okunur ve kullanıcıya gösterilir.

---

## Genel Özet

Dosya sistemleri, verilerin depolama birimlerinde düzenli şekilde tutulmasını sağlar. NTFS Windows sistemlerinde, ext4 Linux sistemlerinde, APFS ise Apple cihazlarında yaygın olarak kullanılır. Her dosya sistemi kendi işletim sisteminin ihtiyaçlarına göre güvenlik, performans, kararlılık ve uyumluluk sağlar.

Blok yapısı, dosyaların diskte küçük parçalara ayrılarak saklanmasıdır. İşletim sistemi dosyaları doğrudan tek parça halinde değil, bloklar üzerinden yönetir. Bu nedenle blok boyutu hem performansı hem de disk alanı kullanımını etkiler.

HDD’ler mekanik yapıya sahiptir ve verileri dönen manyetik plakalar üzerinden okur. Bu nedenle okuma-yazma sırasında kafa hareketi ve dönme gecikmesi oluşur. SSD’ler ise NAND flash bellek kullanır ve hareketli parça içermez. Bu yüzden erişim süreleri çok daha düşüktür.

Veri okuma/yazma hızları; depolama teknolojisi, bağlantı arayüzü, sıralı veya rastgele erişim tipi, cache kullanımı, dosya sistemi yapısı ve fragmentation gibi faktörlerden etkilenir. Özellikle SSD’lerin hızlı hissedilmesinin temel sebebi, küçük ve rastgele dosya erişimlerinde HDD’lere göre çok daha başarılı olmasıdır.

---

## Sonuç

Bu bölümde dosya sistemlerinin ve depolama birimlerinin bilgisayarda veriyi nasıl yönettiği incelenmiştir.

Dosya sistemleri verinin mantıksal düzeninden sorumluyken, HDD ve SSD gibi depolama birimleri verinin fiziksel olarak saklandığı yapılardır.

NTFS, ext4 ve APFS farklı işletim sistemlerine göre geliştirilmiş dosya sistemleridir. HDD ve SSD arasındaki temel fark ise veriye erişim yöntemlerinden kaynaklanır. HDD mekanik parçalara sahip olduğu için daha yavaş, SSD ise elektronik erişim sağladığı için daha hızlıdır.

Bu nedenle modern bilgisayarlarda işletim sistemi ve sık kullanılan programlar için SSD tercih edilirken, yüksek kapasiteli arşivleme ve yedekleme işlemlerinde HDD hâlâ kullanılabilir.

Dosya sistemleri ve depolama mantığını anlamak, bilgisayarın veriyi nasıl sakladığını, nasıl bulduğunu ve performans farklarının neden oluştuğunu kavramak açısından önemlidir.