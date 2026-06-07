# İşletim Sistemi Temelleri (OS Basics)

Bu çalışma, işletim sistemi temellerini anlamak amacıyla hazırlanmıştır. İşletim sistemi; bilgisayarın donanımı ile kullanıcı tarafından çalıştırılan programlar arasında yer alan, kaynakları yöneten ve düzen sağlayan temel yazılımdır. Bu konuyu öğrenmek, yazılımın yalnızca koddan ibaret olmadığını; aynı zamanda bellek, işlemci, süreçler ve çekirdek gibi yapılar üzerinde çalıştığını anlamayı sağlar.

## İşletim Sistemi Nedir?

İşletim sistemi, bilgisayarın donanımı ile uygulamalar arasında köprü görevi gören temel sistem yazılımıdır. Kullanıcı bir program çalıştırdığında, dosya açtığında, internete girdiğinde ya da bir çıktı aldığında tüm bu işlemler doğrudan donanım üzerinden değil, işletim sistemi aracılığıyla gerçekleşir.

İşletim sisteminin temel görevleri şunlardır:

- İşlemciyi yönetmek
- Belleği yönetmek
- Disk erişimini düzenlemek
- Klavye, fare, ekran gibi giriş/çıkış aygıtlarını kontrol etmek
- Çalışan programlar arasında düzen sağlamak
- Kaynakları adil ve güvenli şekilde paylaştırmak

Kısacası işletim sistemi, bilgisayarın düzenli çalışmasını sağlayan ana yöneticidir.

---

## Kernel Nedir?

Kernel, işletim sisteminin çekirdeğidir ve en temel parçasıdır. Donanıma en yakın çalışan yapı kernel’dir. Programlar, işlemciye, belleğe veya aygıtlara doğrudan erişemez; bu erişim kernel aracılığıyla gerçekleştirilir.

Kernel’in başlıca görevleri şunlardır:

- CPU kullanımını yönetmek
- Belleği yönetmek
- Dosya sistemlerini kontrol etmek
- Giriş/çıkış aygıtlarını yönetmek
- Süreçleri ve iş parçacıklarını düzenlemek
- Güvenlik ve erişim denetimlerini sağlamak

Örneğin bir program RAM talep ettiğinde, başka bir program diskten veri okumak istediğinde ya da yazıcıya çıktı gönderileceğinde bu işlemleri doğrudan uygulama değil, kernel düzenler.

Kernel’i anlamak için bir şirket benzetmesi yapılabilir:

- Donanım = şirketin fiziksel kaynakları
- Uygulamalar = çalışanlar
- Kernel = müdür

Çalışanlar nasıl doğrudan şirket kasasına veya depoya erişemiyorsa, uygulamalar da sistem kaynaklarına doğrudan ulaşamaz. Arada kernel bulunur.

Kernel’in önemi çok büyüktür. Çünkü kernel olmasaydı:

- Her program belleği kafasına göre kullanabilirdi
- Programlar birbirinin alanına müdahale edebilirdi
- Donanım kullanımı düzensiz olurdu
- Sistem çok daha kolay çökerdi

Bu nedenle kernel, işletim sistemindeki düzenin merkezidir.

---

## Süreç (Process) Nedir?

Bir program, diskte duran pasif bir dosyadır. Ancak çalıştırıldığı anda artık bir **process**, yani süreç haline gelir.

Örneğin bilgisayardaki bir `chrome.exe` dosyası yalnızca bir program dosyasıdır. Fakat Chrome açıldığında:

- Bellekte yer kaplar
- CPU kullanır
- Sekmeler çalıştırır
- Sistem kaynaklarını kullanır

Bu durumda artık o program bir **process** haline gelmiş olur. Bir process genellikle şunları içerir:

- Kendine ait bellek alanı
- Çalışma durumu
- Kendi değişkenleri
- Açık dosyaları
- Kullandığı sistem kaynakları

Yani process, çalışan bir program örneğidir. Aynı programdan birden fazla process de oluşturulabilir. Örneğin iki farklı uygulama penceresi açıldığında ya da aynı programdan birden çok örnek çalıştırıldığında bunlar ayrı süreçler olabilir.

---

## Thread Nedir?

Thread, bir process içindeki iş akışıdır. Başka bir deyişle thread, bir process’in içinde çalışan daha küçük yürütme birimidir. Her process’in en az bir thread’i vardır. Buna genellikle **ana thread** denir. Ancak ihtiyaç durumunda bir process içinde birden fazla thread bulunabilir. Bunu anlamak için şu benzetme yapılabilir:

Bir kafe düşünelim. Kafenin kendisi process olsun. Bu kafede çalışan kişiler ise thread olsun.

- Biri sipariş alıyor
- Biri kahve hazırlıyor
- Biri kasaya bakıyor

Hepsi aynı işletmenin içinde, yani aynı process’te çalışır; fakat farklı görevler yürütürler. İşte thread mantığı da buna benzer.

---

## Process ile Thread Arasındaki Fark

Process ve thread kavramları birbirine benzese de aralarında çok önemli farklar vardır.

### Process

- Bağımsız çalışır
- Kendine ait bellek alanına sahiptir
- Daha izole yapıdadır
- Oluşturulması daha maliyetlidir

### Thread

- Bir process’in içinde çalışır
- Aynı process’in belleğini paylaşır
- Daha hafif yapıdadır
- Daha hızlı oluşturulabilir
- Ancak dikkat edilmezse veri çakışmalarına neden olabilir

En temel fark şudur:

**Process’ler birbirinden bağımsızdır, thread’ler ise aynı yapının içinde çalışan ve kaynak paylaşan birimlerdir.**

Bu nedenle thread’ler aynı veriye erişebilir. Bu hız avantajı sağlar; ancak aynı anda aynı veriyi değiştirmeye çalışırlarsa sorun çıkabilir. Bu tür sorunlar senkronizasyon problemleri olarak bilinir.

---

## Process mi Daha Ağırdır, Thread mi?

Process daha ağır bir yapıdır. Çünkü:

- Ayrı bellek alanı oluşturulur
- Sistem daha fazla kaynak ayırır
- Oluşturulması daha maliyetlidir
- Context switch maliyeti daha yüksek olabilir

Thread ise daha hafif yapıdadır. Çünkü:

- Aynı process içinde çalışır
- Kaynak paylaşır
- Daha hızlı oluşturulur
- Daha hızlı iletişim kurar

Ancak bu paylaşım beraberinde dikkat gerektirir. Özellikle çoklu thread kullanırken senkronizasyon çok önemlidir.

---

## Bellek Yönetimi Nedir?

İşletim sistemi, RAM’i yani ana belleği düzenli ve kontrollü şekilde yönetmek zorundadır. Çünkü aynı anda birçok program çalışabilir:

- Tarayıcı
- Kod editörü
- Müzik uygulaması
- Terminal
- Arka planda çalışan servisler

Bunların hepsi RAM kullanır. İşletim sistemi ise şu görevleri yerine getirir:

- Hangi programa ne kadar bellek verileceğini belirlemek
- Kullanılmayan alanları boşaltmak
- Bir programın belleğini diğer programdan korumak
- Gerekirse disk desteğiyle sanal bellek kullanmak

Bellek yönetimi olmazsa sistemde karmaşa olur, programlar birbirinin alanına müdahale edebilir ve sistem kararsız hale gelebilir.

---

## Bir Program Bellekte Neleri Kullanır?

Bir process’in belleği genellikle birkaç temel bölümden oluşur:

### Code / Text Segment

Programın çalıştırılabilir komutları burada bulunur. Yani yazılan kodun makine diline çevrilmiş hali burada yer alır.

### Data Segment

Global ve static değişkenler burada saklanır.

### Heap

Dinamik olarak ayrılan bellek alanıdır. Program çalışırken ihtiyaç oldukça büyüyebilir. Özellikle çalışma anında esnek veri yapıları oluşturmak için kullanılır.

### Stack

Fonksiyon çağrıları, yerel değişkenler ve dönüş adresleri burada tutulur. Fonksiyonlar çağrıldıkça stack kullanımı artar.

---

## Stack ve Heap Arasındaki Fark

### Stack

- Daha düzenlidir
- Otomatik yönetilir
- Fonksiyon bazlı çalışır
- Genellikle daha hızlıdır

### Heap

- Daha esnektir
- Dinamik bellek ayırmak için kullanılır
- Yönetimi daha karmaşıktır
- Bellek sızıntısı riski olabilir

Kısaca:

- Küçük, geçici ve düzenli yapılar için stack
- Dinamik ve esnek yapılar için heap kullanılır

---

## Sanal Bellek (Virtual Memory) Nedir?

RAM kapasitesi sınırlıdır. Ancak bazen çalışan programların toplam bellek ihtiyacı RAM miktarını aşabilir. İşletim sistemi bu durumda **sanal bellek** kullanır. Sanal belleğin mantığı şudur:

- Programlara sanki daha fazla bellek varmış gibi alan sunulur
- O anda aktif olarak kullanılmayan bazı veriler geçici olarak diske taşınabilir

Bu sayede sistem daha çok programı aynı anda çalıştırabilir. Ancak disk, RAM kadar hızlı olmadığı için sanal belleğin aşırı kullanılması sistemi yavaşlatabilir.

---

## Bellek Koruması Neden Önemlidir?

Her process’in kendi belleği korunur. Yani bir uygulama gidip başka bir uygulamanın belleğine doğrudan erişemez. Bu çok önemlidir çünkü aksi durumda:

- Güvenlik açıkları oluşur
- Uygulamalar birbirini bozabilir
- Sistem kararsız hale gelir

İşletim sistemi burada sınırlar koyar ve süreçlerin birbirine zarar vermesini engeller.

---

## CPU Zamanlayıcı (Scheduler) Nedir?

Bilgisayarda aynı anda birçok iş yapılıyor gibi görünür:

- Müzik çalıyor
- Tarayıcı açık
- Kod editörü çalışıyor
- Dosya indiriliyor

Bunu mümkün kılan temel yapılardan biri **CPU scheduling**, yani CPU zamanlamasıdır. İşletim sistemi, CPU’nun hangi process veya thread’e ne kadar süreyle verileceğini planlar. Böylece sistem hem hızlı hem de adil çalışır.

---

## Scheduler Ne İş Yapar?

Scheduler şu kararları verir:

- Sırada hangi iş çalışacak?
- Hangisi bekleyecek?
- Hangisi daha öncelikli?
- Hangisine ne kadar süre verilecek?

Bu yapı sayesinde çok sayıda iş, sınırlı işlemci kaynağı üzerinde düzenli biçimde çalıştırılabilir.

---

## CPU Zamanlayıcı Neden Gereklidir?

CPU sınırlı bir kaynaktır. Çok sayıda iş olduğu halde hepsine aynı anda tam erişim verilemez. Bu nedenle zamanlama gerekir. Scheduler olmazsa:

- Bazı işler hiç sıra alamaz
- Sistem takılıyor gibi görünür
- Bazı uygulamalar işlemciyi sömürür
- Kullanıcı deneyimi bozulur

Zamanlayıcı, sistemin dengeli çalışmasını sağlar.

---

## Temel Zamanlama Kavramları

### Burst Time

Bir işin CPU üzerinde ihtiyaç duyduğu çalışma süresidir.

### Waiting Time

Bir işin kuyrukta beklediği süredir.

### Turnaround Time

Bir işin sisteme geldiği andan tamamlanana kadar geçen toplam süredir.

### Response Time

Kullanıcının ilk tepkiyi aldığı süredir. Özellikle etkileşimli sistemlerde çok önemlidir.

---

## Yaygın CPU Zamanlama Algoritmaları

### FCFS – First Come First Served

İlk gelen iş ilk çalışır.

**Avantajları:**

- Basittir
- Uygulaması kolaydır

**Dezavantajları:**

- Uzun süren bir iş öne geçerse kısa işler çok bekleyebilir

Bu duruma bazen “convoy effect” denir.

---

### SJF – Shortest Job First

En kısa iş önce çalıştırılır.

**Avantajları:**

- Ortalama bekleme süresi azalabilir

**Dezavantajları:**

- Uzun işler çok bekleyebilir
- İşin ne kadar süreceğini önceden bilmek zordur

---

### Round Robin

Her işe belirli bir zaman dilimi verilir. Süre dolunca sıradaki işe geçilir.

Örneğin:

- A işlemi 2 ms çalışır
- Sonra B
- Sonra C
- Sonra tekrar A

**Avantajları:**

- Daha adildir
- Kullanıcıya sistem akıcı görünür

**Dezavantajları:**

- Zaman dilimi çok küçük olursa sürekli geçiş maliyeti artar
- Çok büyük olursa etkileşim hissi azalır

---

### Priority Scheduling

Önceliği yüksek olan iş önce çalıştırılır.

**Avantajları:**

- Önemli işler daha hızlı tamamlanır

**Dezavantajları:**

- Düşük öncelikli işler uzun süre bekleyebilir
- Bu durum starvation olarak adlandırılır

---

## Context Switch Nedir?

CPU bir işten başka bir işe geçtiğinde, o an çalışan işin durumu saklanır. Daha sonra tekrar o işe dönülebilmesi için gerekli bilgiler korunur. Örneğin:

- Hangi komutta olduğu
- Register değerleri
- Çalışma bağlamı

Bu geçiş işlemine **context switch** denir. Context switch faydalıdır çünkü çoklu görev çalışmasını mümkün kılar. Ancak bedava değildir; bu geçişin de bir zaman maliyeti vardır.

---

## İşletim Sistemi Tüm Bunları Nasıl Birlikte Yönetir?

Bir program çalıştırıldığında arka planda şu adımlar gerçekleşir:

1. Program diskte dosya olarak bulunur.
2. Çalıştırıldığında process oluşur.
3. İşletim sistemi bu process için bellekte alan ayırır.
4. Gerekirse thread’ler oluşturulur.
5. Scheduler CPU sırasını belirler.
6. Kernel donanım ve kaynak erişimini düzenler.
7. Bellek yönetimi sayesinde diğer programlarla çakışma önlenir.

Bu süreç, işletim sisteminin ne kadar büyük bir organizasyon yürüttüğünü gösterir.

---

## “Yazılımın Nerede Çalıştığını Anlamak” Şudur:

Bu ifade çok önemlidir. Çünkü çoğu zaman yazılım geliştirirken yalnızca “kod yazdım ve çalıştı” düşünülür. Oysa yazılım boşlukta çalışmaz. Her yazılım:

- RAM üzerinde yer kaplar
- CPU tarafından yürütülür
- İşletim sistemi tarafından planlanır
- Dosya sistemiyle iletişim kurar
- Thread’lerle paralel çalışabilir
- Kernel aracılığıyla kaynak kullanır

Yani yazılımın çalıştığı ortamı anlamak, sistemin nasıl işlediğini anlamak demektir.

Bu bilgi sayesinde:

- Performans sorunları daha iyi anlaşılır
- Bellek hataları yorumlanabilir
- Deadlock ve race condition gibi kavramlar daha anlaşılır hale gelir
- Sistem neden yavaşlıyor veya kilitleniyor daha rahat analiz edilebilir

---

## Bu Konuları Öğrenmenin Yazılımcıya Kazancı Nedir?

İşletim sistemi temellerini bilmek yazılımcıya çok önemli katkılar sağlar:

### Performansı Daha İyi Anlamayı Sağlar

Bir uygulama neden yavaş çalışıyor sorusu daha bilinçli şekilde analiz edilir. Sorun CPU’da mı, bellekte mi, disk erişiminde mi daha kolay anlaşılır.

### Hataları Daha Doğru Yorumlamayı Sağlar

Özellikle şu tür hatalar daha anlamlı hale gelir:

- Segmentation fault
- Out of memory
- Deadlock
- Race condition

---

## Gerçek Hayat Benzetmesi

Bilgisayar sistemi bir restoran gibi düşünülebilir:

- Kernel = restoran yöneticisi
- Process = ayrı siparişler
- Thread = siparişleri hazırlayan çalışanlar
- Memory = mutfaktaki çalışma alanı
- CPU scheduler = hangi siparişin önce hazırlanacağına karar veren düzen
- Context switch = bir çalışanın bir işi bırakıp başka bir işe geçmesi

Bu yapı düzgün işlemezse siparişler karışır, kaynaklar boşa harcanır ve sistem düzensiz hale gelir. Aynı mantık bilgisayar sistemleri için de geçerlidir.

---

## Kısa Özet

### Kernel

İşletim sisteminin çekirdeğidir. Donanım ile yazılım arasında köprü kurar ve CPU, bellek, aygıt, süreç yönetimi gibi temel görevleri yürütür.

### Process

Çalışmakta olan programdır. Kendi bellek alanına ve sistem kaynaklarına sahiptir.

### Thread

Bir process içindeki yürütme birimidir. Aynı process’in kaynaklarını paylaşır ve daha hafif yapıdadır.

### Bellek Yönetimi

İşletim sisteminin RAM’i düzenli biçimde paylaştırması, koruması ve gerektiğinde sanal bellek kullanarak sistemi verimli çalıştırmasıdır.

### CPU Scheduling

CPU’nun hangi süreç veya thread’e ne zaman verileceğini belirleyen mekanizmadır. Sistem performansı ve kullanıcı deneyimi açısından kritik öneme sahiptir.

---

## Temel Mantık Zinciri

İşletim sistemi konusunu anlamak için şu zincir çok önemlidir:

**Program çalışır → Process olur → Gerekirse thread’ler oluşur → Bellek ayrılır → Scheduler CPU verir → Kernel kaynakları yönetir**

Bu zincir kavrandığında işletim sistemi temelleri çok daha anlamlı hale gelir.

---

## Sonuç

İşletim sistemi temelleri, yazılım geliştirme sürecinde yalnızca teorik bir konu değildir. Bir programın nasıl çalıştığını, kaynaklara nasıl eriştiğini, neden bazen yavaşladığını veya neden hata verdiğini anlayabilmek için bu temel yapıların bilinmesi gerekir.

Kernel, process, thread, bellek yönetimi ve CPU zamanlayıcı gibi kavramlar; yazılımın arka planda nasıl çalıştığını anlamamızı sağlar. Bu nedenle işletim sistemi bilgisi, hem akademik hem de profesyonel yazılım geliştirme sürecinde çok değerli bir yere sahiptir.