# 3) Ağ Temelleri (Networking)

Bu raporda ağ temelleri kapsamında IP, Port, DNS, TCP, UDP kavramları; paket yapısının nasıl çalıştığı; ping, traceroute ve nslookup komutlarının ne işe yaradığı detaylı olarak incelenmiştir. Bu konular, bir yazılımın internet üzerinden nasıl haberleşme kurduğunu anlamak açısından temel öneme sahiptir.

---

## IP - Port - DNS - TCP - UDP nedir?

Bir yazılımın başka bir cihazla internet üzerinden iletişim kurabilmesi için önce hedefin bulunması, sonra doğru uygulamaya ulaşılması ve verinin belirli kurallara göre taşınması gerekir. Bu süreçte IP, Port, DNS, TCP ve UDP kavramları birlikte çalışır.

### IP nedir?

IP adresi, ağ üzerindeki bir cihazın adresidir. Bir cihazın internette veya yerel ağda tanınabilmesi ve veri alabilmesi için bir IP adresine sahip olması gerekir. Bu adres sayesinde gönderilen veri doğru cihaza yönlendirilir.

Günlük hayatta bir eve mektup gönderebilmek için adres bilgisine ihtiyaç duyulması gibi, bilgisayar ağlarında da bir verinin hangi cihaza gideceğini belirlemek için IP adresi kullanılır.

Örneğin:

- `192.168.1.5` gibi adresler genellikle yerel ağlarda kullanılır.
- `8.8.8.8` gibi adresler ise internet üzerindeki genel IP adreslerine örnek olabilir.

IP adresinin temel görevi, verinin **hangi cihaza** gideceğini belirlemektir. Ancak bir cihazda birden fazla uygulama aynı anda çalışabileceği için, sadece IP adresi tek başına yeterli olmaz. Bu noktada port kavramı devreye girer.

---

### Port nedir?

Port, bir cihaz içindeki belirli bir uygulama veya servisin iletişim kapısıdır. Bunu bir apartmandaki daire numarası gibi düşünebiliriz.

- IP adresi binanın adresi ise,
- Port numarası da o binadaki daire numarasıdır.

Bir bilgisayar üzerinde aynı anda birden fazla servis çalışabilir. Örneğin:

- web sunucusu
- veritabanı sunucusu
- e-posta servisi
- uzaktan bağlantı servisi

Veri önce IP adresi sayesinde doğru cihaza gider, sonra port numarası sayesinde o cihaz içindeki doğru uygulamaya ulaşır. Yaygın port örnekleri şunlardır:

- `80` -> HTTP
- `443` -> HTTPS
- `21` -> FTP
- `22` -> SSH
- `25` -> SMTP
- `53` -> DNS
- `3306` -> MySQL
- `5432` -> PostgreSQL
- `8080` -> alternatif web uygulama portu

Bu nedenle bir ağ bağlantısında genellikle IP ve port birlikte düşünülür. Çünkü sistem sadece hedef cihazı değil, hedef servisi de bilmek zorundadır.

---

### DNS nedir?

DNS, alan adlarını IP adreslerine çeviren sistemdir. Açılımı **Domain Name System** şeklindedir. İnsanlar web sitelerine erişmek için genellikle `google.com`, `github.com` gibi alan adları kullanır. Ancak bilgisayarlar birbiriyle doğrudan alan adlarıyla değil, IP adresleriyle haberleşir. Bu nedenle alan adının hangi IP adresine karşılık geldiğini bulmak gerekir. Bu işlemi DNS yapar. DNS, bir nevi internetin telefon rehberi gibi çalışır:

- Kullanıcı isim bilir: `example.com`
- Sistem numarayı bulur: ilgili IP adresi

Bir kullanıcı tarayıcıya bir web sitesi yazdığında sistem şu adımları uygular:

1. Girilen alan adının IP adresi aranır.
2. DNS sunucusuna sorgu gönderilir.
3. DNS, ilgili IP adresini bulur ve geri döner.
4. Tarayıcı bu IP adresine bağlanmaya çalışır.

DNS olmasaydı insanlar web sitelerine erişmek için tüm IP adreslerini ezberlemek zorunda kalırdı. Bu da internet kullanımını son derece zorlaştırırdı.

---

### TCP nedir?

TCP, verinin güvenilir şekilde iletilmesini sağlayan bir taşıma protokolüdür. Açılımı **Transmission Control Protocol** şeklindedir. TCP kullanıldığında veri iletiminde şu özellikler sağlanır:

- Veri kaybolursa tekrar gönderilir.
- Paketler karışık sırada gelse bile düzgün şekilde sıralanır.
- Verinin eksiksiz ulaşması hedeflenir.
- İletişimden önce bağlantı kurulur.

Bu nedenle TCP, doğruluğun ve bütünlüğün önemli olduğu durumlarda tercih edilir. Örneğin:

- web sayfası yükleme
- dosya indirme
- e-posta gönderimi
- API haberleşmesi
- veritabanı işlemleri

TCP bağlantı yönelimli bir protokoldür. Yani veri iletiminden önce iki taraf arasında bir bağlantı kurulur. Bu süreç genellikle **three-way handshake** olarak bilinir:

1. İstemci bağlantı talebi gönderir.
2. Sunucu bu talebe cevap verir.
3. İstemci cevabı onaylar ve bağlantı kurulur.

Bu yapıdan dolayı TCP daha güvenlidir; ancak daha fazla kontrol mekanizması kullandığı için UDP'ye göre genellikle daha yavaş olabilir.

---

### UDP nedir?

UDP, daha hızlı fakat daha az kontrollü bir taşıma protokolüdür. Açılımı **User Datagram Protocol** şeklindedir. UDP'de:

- önce bağlantı kurulmaz
- veri teslim edildi mi kontrol edilmez
- kaybolan veri için tekrar gönderim yapılmaz
- paketlerin sıralı gelmesi garanti edilmez

Bu nedenle UDP, "veriyi hızlı gönder, teslim kontrolünü minimumda tut" mantığıyla çalışır.  UDP genellikle şu alanlarda kullanılır:

- canlı video ve ses iletimi
- online oyunlar
- DNS sorguları
- anlık veri akışı gereken sistemler
- bazı sensör ve IoT uygulamaları

Örneğin canlı görüşmelerde her verinin kusursuz şekilde ulaşmasındansa, iletişimin kesintisiz ve hızlı olması daha önemlidir. Bu nedenle bazen küçük veri kayıpları kabul edilerek UDP tercih edilir.

---

### TCP ve UDP farkı

TCP ve UDP arasındaki temel fark, güvenilirlik ve hız dengesi üzerindedir.

**TCP:**
- bağlantı kurar
- veri teslimini kontrol eder
- kayıp paketi tekrar gönderir
- sıralamayı korur
- daha güvenilir ama daha maliyetlidir

**UDP:**
- bağlantısızdır
- teslim garantisi vermez
- tekrar gönderim yapmaz
- daha hızlıdır
- gerçek zamanlı uygulamalarda uygundur

Bu nedenle hangi protokolün seçileceği, uygulamanın ihtiyacına göre belirlenir.

---

## Paket yapısı nasıl çalışır?

Ağ üzerinde veri genellikle tek parça halinde değil, **paketler** halinde taşınır. Paket, ağ üzerinde iletilen veri birimidir. Büyük boyutlu bir veri doğrudan tek parça halinde gönderilmez. Bunun yerine daha küçük parçalara ayrılır ve bu parçalar ayrı ayrı ağ üzerinden iletilir. Karşı taraf bu parçaları alır ve tekrar birleştirir. Bir paketin iki temel kısmı vardır:

### 1. Header (Başlık)

Header, paketin yönetim bilgisini taşır. Bu kısımda genellikle şu bilgiler bulunur:

- kaynak IP adresi
- hedef IP adresi
- kaynak port
- hedef port
- kullanılan protokol bilgisi
- sıra bilgisi
- kontrol ve doğrulama bilgileri

Bu alanlar sayesinde paket nereye gideceğini, nereden geldiğini ve nasıl işleneceğini bilir.

### 2. Payload (Yük)

Payload, paketin taşıdığı asıl veridir. Yani kullanıcı veya uygulama açısından asıl anlamlı içerik bu kısımdadır. Örneğin:

- bir mesajın metni
- bir web sayfasının bir parçası
- bir resim dosyasının bölümü
- bir API cevabının parçası

---

### Veri neden paketlere ayrılır?

Verinin paketlere ayrılmasının birden fazla nedeni vardır:

- Ağ kaynakları daha verimli kullanılır.
- Büyük veri parçası yerine küçük parçalı iletim daha kolay yönetilir.
- Kaybolan veri varsa sadece kayıp paket yeniden gönderilir.
- Paketler farklı ağ yollarından gidebilir.
- Yönlendirme işlemleri daha esnek hale gelir.

Örneğin bir kullanıcı büyük bir dosya indirirken bu dosya ağ üzerinden tek seferde değil, çok sayıda paket halinde gelir. Kullanıcı bu süreci tek parça gibi görür; ancak arka planda pek çok küçük veri parçası taşınmaktadır.

---

### Paket iletimi nasıl gerçekleşir?

Bir kullanıcı tarayıcısından bir web sitesine girdiğinde genel olarak şu süreç yaşanır:

1. Kullanıcı alan adını yazar.
2. DNS, bu alan adının IP adresini bulur.
3. Sistem hedef IP ve port bilgisine göre bağlantı başlatır.
4. Veri paketlere ayrılır.
5. Paketler router ve switch gibi ağ cihazları üzerinden iletilir.
6. Hedef sunucu paketleri alır.
7. Gerekirse paketler doğru sıraya konur.
8. Veri tekrar birleştirilir ve uygulama tarafından işlenir.

Bu süreç sayesinde internet üzerindeki haberleşme düzenli ve yönetilebilir hale gelir.

---

## Ping, traceroute, nslookup ne işe yarar?

Ağ problemlerini anlamak ve bağlantı durumunu kontrol etmek için farklı komutlar kullanılır. Bunlardan en yaygın olanları ping, traceroute ve nslookup'tur.

---

### Ping ne işe yarar?

`ping`, bir hedef cihaza ulaşılıp ulaşılamadığını test etmek için kullanılır. Ping komutu, hedefe test amaçlı veri gönderir ve cevap alıp almadığına bakar. Böylece şu bilgiler edinilebilir:

- hedef cihaz erişilebilir mi
- cevap süresi ne kadar
- gecikme var mı
- paket kaybı bulunuyor mu

Ping, genellikle ilk seviye bağlantı testi için kullanılır. Örneğin bir sunucuya erişilemiyorsa önce ping atılarak temel ağ bağlantısı kontrol edilir.  Ancak burada önemli bir nokta vardır: bir cihazın ping'e cevap vermemesi, onun kesin olarak kapalı olduğu anlamına gelmez. Bazı sistemler güvenlik nedeniyle ping isteklerini engelleyebilir. Yani ping, ağ testi için yararlı bir araç olsa da tek başına kesin sonuç vermeyebilir.

---

### Traceroute ne işe yarar?

`traceroute` komutu, bir paketin hedefe giderken hangi ağ cihazlarından geçtiğini gösterir. Windows sistemlerde bunun karşılığı genellikle `tracert` komutudur. Bu komut sayesinde kaynak cihaz ile hedef cihaz arasındaki yol adım adım görülebilir. Her adım bir **hop** olarak ifade edilir. Traceroute şu durumlarda çok faydalıdır:

- bağlantının hangi noktada koptuğunu anlamak
- sorun yerel ağda mı yoksa dış ağda mı tespit etmek
- ISS taraflı gecikmeleri incelemek
- hedefe kadar olan yolun nasıl ilerlediğini görmek

Ping sadece hedefe ulaşılıp ulaşılmadığını anlamaya yardım ederken, traceroute yol üzerindeki ara durakları da gösterir. Bu nedenle daha detaylı bağlantı analizi için kullanılır.

---

### nslookup ne işe yarar?

`nslookup`, bir alan adının hangi IP adresine karşılık geldiğini öğrenmek için kullanılan bir DNS sorgulama aracıdır. Örneğin bir web sitesi açılmıyorsa sorun bazen sitenin sunucusunda değil, DNS kaydında olabilir. Bu durumda nslookup ile alan adının doğru IP'ye çözülüp çözülmediği kontrol edilir. nslookup şu durumlarda işe yarar:

- alan adının IP adresini öğrenmek
- DNS sorgusunun doğru çalışıp çalışmadığını kontrol etmek
- hatalı DNS yönlendirmelerini tespit etmek
- farklı DNS sunucularından sonuç karşılaştırmak

Bu komut, özellikle web sitesi erişim sorunlarında ve DNS kaynaklı problemlerde oldukça önemlidir.

---

## Bu kavramlar birlikte nasıl çalışır?

Ağ temellerindeki bu kavramlar birbirinden bağımsız değildir. Hepsi aynı iletişim sürecinin farklı bir parçasıdır. Bir kullanıcı tarayıcıya bir web adresi yazdığında genel olarak şu akış gerçekleşir:

1. **DNS**, alan adını IP adresine çevirir.
2. **IP**, hedef cihazın bulunmasını sağlar.
3. **Port**, o cihaz içindeki doğru servisi belirler.
4. **TCP veya UDP**, verinin hangi yöntemle taşınacağını belirler.
5. **Paketler**, veriyi ağ üzerinde taşınabilir hale getirir.
6. Gerekirse **ping**, **traceroute** ve **nslookup** gibi araçlarla sorun analizi yapılır.

Bu yapının bütünü, bir yazılımın internet üzerinde "nasıl konuştuğunu" anlamamızı sağlar.

---

## Gerçek hayat benzetmesi

Konuyu daha iyi anlamak için bunu bir kargo sürecine benzetebiliriz:

- **DNS** = alıcının ismini adrese çeviren rehber
- **IP** = gidilecek bina adresi
- **Port** = binadaki daire numarası
- **TCP** = teslimatı imza karşılığında güvenli şekilde yapmak
- **UDP** = hızlı teslim etmek ama her adımı kontrol etmemek
- **Paket** = taşınan koli
- **ping** = "bu adreste biri var mı" diye yoklama yapmak
- **traceroute** = kolinin hangi güzergahlardan geçtiğini görmek
- **nslookup** = isimden adres bulmak

Bu benzetme birebir teknik karşılık olmasa da mantığı anlamayı kolaylaştırır.

---

## Yazılım açısından neden önemlidir?

Networking bilgisi sadece teori için değil, pratik yazılım geliştirme sürecinde de çok önemlidir. Çünkü gerçek projelerde şu problemlerle sıkça karşılaşılır:

- API neden cevap vermiyor?
- Sunucuya neden bağlanamıyorum?
- DNS doğru mu çalışıyor?
- Port kapalı olabilir mi?
- Firewall erişimi engelliyor mu?
- TCP timeout mu yaşanıyor?
- Paket kaybı mı var?
- Sunucu ayakta ama servis mi çalışmıyor?

Bu nedenle ağ temellerini bilmek, hem backend hem frontend hem de sistem tarafında çok ciddi avantaj sağlar. Sorunun ağ kaynaklı mı, uygulama kaynaklı mı olduğunu ayırt etmek için bu bilgiler gereklidir.

---

## Sonuç

Ağ temelleri, modern yazılım sistemlerinin internet üzerinde nasıl haberleştiğini anlamak için vazgeçilmezdir. IP adresi hedef cihazı, port hedef servisi belirler. DNS, alan adlarını IP adreslerine çevirir. TCP ve UDP, verinin nasıl taşınacağını belirleyen temel protokollerdir. Veri ise paketler halinde iletilir. Ping, traceroute ve nslookup gibi araçlar da bu iletişimin test edilmesi ve olası sorunların analiz edilmesi için kullanılır. Bu kavramlar birlikte değerlendirildiğinde, bir yazılımın internette nasıl konuştuğu daha net şekilde anlaşılır. Bu da hem teorik ağ bilgisini hem de pratik yazılım geliştirme becerisini güçlendirir.

---

## Kazanç

Bu konuyu öğrenerek, yazılımın internette nasıl konuştuğunu anlamış oluruz. Yani bir istemcinin bir sunucuyu nasıl bulduğu, hangi yolla bağlantı kurduğu, veriyi nasıl gönderdiği ve ağ üzerindeki problemlerin nasıl tespit edilebileceği konusunda temel fakat çok güçlü bir altyapı edinmiş oluruz.