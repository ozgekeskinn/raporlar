# 5. Hafta Raporu: Linux Temelleri
## Giriş

Bu haftaki çalışmanın konusu **Linux temelleri**dir. Yazılım geliştirme sürecinde yalnızca programlama dillerini bilmek yeterli değildir. Bir yazılımcının kullandığı işletim sistemi altyapısını, komut satırı araçlarını, dosya izin mantığını, paket kurulum süreçlerini ve servis yönetimini de anlaması gerekir. Bu nedenle Linux temelleri, hem sistem bilgisi hem de günlük geliştirme süreçleri açısından oldukça önemlidir.

Linux, özellikle sunucu sistemlerinde, bulut altyapılarında, DevOps süreçlerinde, siber güvenlik alanında, gömülü sistemlerde ve yazılım geliştirme ortamlarında çok yaygın olarak kullanılmaktadır. Bu yüzden Linux üzerinde temel seviyede bile olsa hakimiyet kazanmak, bir yazılımcı için güçlü bir altyapı bilgisi sağlar.

Bu raporda Linux’un temel mantığı, terminal kullanımı, önemli komutlar, paket yöneticileri, dosya izin sistemi ve servis yönetimi ayrıntılı biçimde ele alınmıştır. Ayrıca Linux’un yazılım geliştirme süreçlerindeki yeri, pratik kullanım örnekleriyle birlikte açıklanmıştır.

---

## Linux Nedir ve Neden Önemlidir?

Linux, açık kaynak kodlu bir işletim sistemi çekirdeği etrafında gelişmiş sistemlerin genel adıdır. Günümüzde Ubuntu, Debian, Fedora, Arch Linux, CentOS gibi birçok Linux dağıtımı kullanılmaktadır. Her dağıtımın kullanım amacı, paket yönetim sistemi ve yapılandırma yaklaşımı farklı olabilir; ancak temel Linux mantığı büyük ölçüde ortaktır.

Linux’un önemli özellikleri şunlardır:

- Açık kaynaklıdır.
- Güvenli ve kararlı bir yapıya sahiptir.
- Özelleştirilebilir.
- Sunucu sistemlerinde çok yaygın kullanılır.
- Komut satırı kullanımı çok güçlüdür.
- Yazılım geliştirme ve otomasyon süreçleri için uygundur.

Linux’un önemli olmasının sebeplerinden biri, birçok teknolojik altyapının bu sistem üzerinde çalışmasıdır. Web sunucuları, veritabanları, container sistemleri, CI/CD ortamları, uzak sunucular ve bulut servisleri çoğunlukla Linux temellidir. Bu nedenle Linux bilgisi, yalnızca bir işletim sistemi bilgisi değil, aynı zamanda bir **altyapı okuryazarlığı**dır.

Bugün birçok yazılım geliştirici doğrudan Linux kullanmasa bile Docker container’ları, uzak sunucular, sanal makineler, Git tabanlı iş akışları, deployment süreçleri veya terminal araçları üzerinden dolaylı olarak Linux ekosistemiyle sürekli temas halindedir. Bu yüzden Linux bilmek yalnızca bir artı değil, çoğu zaman bir gereklilik haline gelmiştir.

---

## Terminal ve Komut Satırı Mantığı

Linux’ta grafiksel arayüz kullanılabilse de sistemle en güçlü iletişim yöntemi **terminal**dir. Terminal, kullanıcı ile işletim sistemi arasında komutlar aracılığıyla iletişim kurulmasını sağlar.

Komut satırı kullanımı şu açılardan önemlidir:

- İşlemleri hızlı yapmayı sağlar.
- Otomasyon için uygundur.
- Sunucu erişiminde gereklidir.
- Grafik arayüz bulunmayan sistemlerde temel çalışma aracıdır.
- Geliştiriciye sistem üzerinde daha fazla kontrol sağlar.

Bir terminal komutu genellikle şu yapıdadır:

```bash
komut seçenek hedef
```

Örneğin:

```bash
ls -l /home/ozge
```

Burada:

- `ls` komuttur.
- `-l` seçenektir.
- `/home/ozge` hedef dizindir.

Terminal mantığını anlamak, Linux öğrenmenin temelidir. Çünkü Linux’ta neredeyse her işlem komut satırından yapılabilir: dosya oluşturma, taşıma, silme, servis başlatma, kullanıcı yönetimi, izin değiştirme, paket kurma, log inceleme ve sistem izleme gibi.

Terminal aynı zamanda kullanıcıya zincirleme düşünme mantığı kazandırır. Bir komutun çıktısı başka bir komutla kullanılabilir, dosya ve klasörler sistematik biçimde yönetilebilir, tekrar eden işlemler komutlarla otomatikleştirilebilir. Bu durum, özellikle yazılım geliştirme ve sistem yönetimi açısından büyük avantaj sağlar.

---

## Temel Terminal Komutları

Bu bölümde Linux’ta en sık kullanılan temel komutlar ayrıntılı olarak açıklanmıştır.

---

## ls Komutu

`ls` komutu, bir dizin içeriğini listelemek için kullanılır. Linux’ta bir klasörün içinde hangi dosya ve klasörlerin bulunduğunu görmek için en temel araçlardan biridir.

### Temel kullanım

```bash
ls
```

Bu komut, bulunulan dizindeki dosya ve klasörleri listeler.

### Sık kullanılan seçenekler

#### 1. Ayrıntılı listeleme

```bash
ls -l
```

Bu kullanım dosyaları uzun formatta gösterir. Uzun formatta şu bilgiler yer alır:

- Dosya türü ve izinleri
- Bağlantı sayısı
- Dosya sahibi
- Grup bilgisi
- Dosya boyutu
- Son değiştirilme tarihi
- Dosya adı

Örnek çıktı:

```bash
-rw-r--r-- 1 ozge users 2048 May 10 14:30 rapor.txt
```

Bu satırda:

- İlk karakter olan `-`, bunun normal bir dosya olduğunu gösterir.
- `rw-r--r--` kısmı dosya izinleridir.
- `1` bağlantı sayısını gösterir.
- `ozge` dosya sahibidir.
- `users` dosyanın ait olduğu gruptur.
- `2048` dosya boyutudur.
- `May 10 14:30` son değiştirilme zamanıdır.
- `rapor.txt` dosya adıdır.

#### 2. Gizli dosyaları gösterme

```bash
ls -a
```

Linux’ta nokta (`.`) ile başlayan dosyalar gizli kabul edilir. Bu seçenek gizli dosyaları da gösterir.

Örnek gizli dosyalar:

- `.bashrc`
- `.profile`
- `.config`

#### 3. İnsan okunabilir boyutla listeleme

```bash
ls -lh
```

Bu kullanım dosya boyutlarını byte yerine daha anlaşılır biçimde gösterir:

- KB
- MB
- GB

#### 4. Alt dizinleri de listeleme

```bash
ls -R
```

Bu komut, dizin içindeki alt klasörlerin içeriklerini de gösterir.

#### 5. Dosyaları zamana göre sıralama

```bash
ls -lt
```

Bu komut, dosyaları en son değiştirilen en üstte olacak şekilde sıralar.

### Kullanım amacı

`ls` komutu özellikle şu durumlarda sık kullanılır:

- Bir klasörde hangi dosyaların olduğunu görmek
- Dosya izinlerini kontrol etmek
- Gizli dosyaları incelemek
- Dosya boyutlarını görmek
- Dizin yapısını anlamak

### Neden önemlidir?

Linux’ta çalışırken önce içinde bulunulan dizinin içeriğini görmek gerekir. Bu nedenle `ls`, en temel keşif komutlarından biridir. Sistemde ne bulunduğunu görmek, klasör yapısını anlamak ve işlem yapılacak dosyaları tanımak için sürekli kullanılır.

---

## cd Komutu

`cd` komutu, dizin değiştirmek için kullanılır. Linux’ta klasörler arasında geçiş yapmayı sağlar.

### Temel kullanım

```bash
cd klasor_adi
```

Örnek:

```bash
cd Belgeler
```

### Sık kullanılan kullanımlar

#### 1. Üst dizine çıkmak

```bash
cd ..
```

`..` ifadesi bir üst klasörü temsil eder.

#### 2. Ana dizine dönmek

```bash
cd ~
```

veya sadece:

```bash
cd
```

Bu komut kullanıcıya ait home dizinine döner.

#### 3. Bir önceki dizine dönmek

```bash
cd -
```

Bu komut son bulunulan dizine geri dönmeyi sağlar.

#### 4. Mutlak yol kullanmak

```bash
cd /home/ozge/projeler
```

Bu kullanımda kök dizinden itibaren tam yol belirtilir.

#### 5. Göreli yol kullanmak

```bash
cd proje1/kaynak
```

Bu kullanımda mevcut dizine göre geçiş yapılır.

### Kullanım amacı

`cd` komutu dosya sistemi içinde gezinmek için temel komuttur. Linux’ta birçok komut, bulunulan dizine göre çalıştığı için dizin kavramı çok önemlidir.

### Neden önemlidir?

Bir dosyayı düzenlemek, çalıştırmak, görüntülemek veya silmek için çoğu zaman önce doğru dizine geçmek gerekir. Bu yüzden `cd`, terminal kullanımının omurgasını oluşturur. Yanlış dizinde çalışmak, yanlış dosyaya işlem yapılmasına neden olabilir.

---

## grep Komutu

`grep`, metin içinde belirli bir ifadeyi aramak için kullanılır. Çok güçlü ve çok sık kullanılan bir komuttur. Yazılım geliştirme, log analizi ve dosya içeriği tarama işlemlerinde büyük kolaylık sağlar.

### Temel kullanım

```bash
grep "aranan_ifade" dosya_adi
```

Örnek:

```bash
grep "hata" log.txt
```

Bu komut `log.txt` dosyasında geçen `hata` kelimesini içeren satırları gösterir.

### Sık kullanılan seçenekler

#### 1. Büyük-küçük harf duyarsız arama

```bash
grep -i "error" log.txt
```

`Error`, `ERROR`, `error` gibi tüm eşleşmeleri bulur.

#### 2. Satır numarası ile gösterme

```bash
grep -n "main" app.py
```

Eşleşmenin hangi satırda olduğunu gösterir.

#### 3. Ters eşleşme

```bash
grep -v "debug" log.txt
```

`debug` içermeyen satırları gösterir.

#### 4. Klasör içinde tüm dosyalarda arama

```bash
grep -r "function" .
```

Bulunulan dizin ve alt dizinlerde `function` geçen tüm yerleri arar.

#### 5. Sadece eşleşen dosya adlarını gösterme

```bash
grep -l "import" *.py
```

Bu kullanım, ilgili ifadeyi içeren dosyaların sadece isimlerini listeler.

### Kullanım alanları

- Log dosyalarında hata aramak
- Kaynak kodda belirli bir kelimeyi bulmak
- Yapılandırma dosyalarını incelemek
- Belirli bir ayarın tanımlanıp tanımlanmadığını kontrol etmek
- Büyük dosyalarda hızlı metin taraması yapmak

### Neden önemlidir?

`grep`, Linux’un en güçlü arama araçlarından biridir. Özellikle binlerce satırlık log veya kod dosyalarında manuel arama yerine çok hızlı sonuç verir. Yazılımcılar için hata ayıklama, konfigürasyon kontrolü ve kod inceleme süreçlerinde çok değerlidir.

---

## mkdir Komutu

`mkdir`, yeni dizin oluşturmak için kullanılır.

### Temel kullanım

```bash
mkdir klasor_adi
```

Örnek:

```bash
mkdir proje_klasoru
```

Bu komut `proje_klasoru` adında yeni bir klasör oluşturur.

### Sık kullanılan seçenekler

#### 1. İç içe dizin oluşturma

```bash
mkdir -p proje/src/components
```

`-p` seçeneği ile eksik ara klasörler de otomatik oluşturulur.

#### 2. Birden fazla klasörü aynı anda oluşturma

```bash
mkdir logs backups temp
```

Bu kullanım tek komutla birden fazla klasör oluşturur.

### Kullanım alanları

- Proje klasörü hazırlamak
- Dizin yapısı oluşturmak
- Log, çıktı, yedek veya veri klasörleri açmak
- Uygulama klasör mimarisi oluşturmak

### Neden önemlidir?

Linux’ta düzenli dosya yapısı kurmak önemlidir. Yazılım projelerinde `src`, `assets`, `config`, `logs`, `scripts` gibi klasörler sıkça kullanılır. `mkdir`, bu yapının ilk adımıdır.

---

## chmod Komutu

`chmod`, dosya veya klasörlerin izinlerini değiştirmek için kullanılır. Linux’ta güvenlik ve erişim kontrolü açısından çok önemli bir komuttur.

### Temel kullanım

```bash
chmod izin dosya_adi
```

Örnek:

```bash
chmod 644 rapor.txt
```

veya

```bash
chmod +x script.sh
```

### Sayısal izin mantığı

Linux’ta izinler üç kullanıcı türü için tanımlanır:

- User (`u`): dosya sahibi
- Group (`g`): grup üyeleri
- Other (`o`): diğer kullanıcılar

Her biri için üç temel yetki vardır:

- Read (`r`) = 4
- Write (`w`) = 2
- Execute (`x`) = 1

Bu değerler toplanarak izin verilir.

#### Örnek: 755

```bash
chmod 755 script.sh
```

Bu durumda:

- Sahip: 7 = 4 + 2 + 1 = `rwx`
- Grup: 5 = 4 + 1 = `r-x`
- Diğerleri: 5 = 4 + 1 = `r-x`

Yani dosya sahibi okuyabilir, yazabilir, çalıştırabilir; diğerleri okuyabilir ve çalıştırabilir ama yazamaz.

#### Örnek: 644

```bash
chmod 644 rapor.txt
```

Bu durumda:

- Sahip: `rw-`
- Grup: `r--`
- Diğerleri: `r--`

Bu izin genelde normal metin dosyalarında kullanılır.

### Harf tabanlı kullanım

#### Çalıştırma izni ekleme

```bash
chmod +x script.sh
```

#### Grup yazma iznini kaldırma

```bash
chmod g-w dosya.txt
```

#### Diğer kullanıcılara okuma izni verme

```bash
chmod o+r dosya.txt
```

#### Sadece kullanıcıya tam yetki verme

```bash
chmod u+rwx dosya.sh
```

### Kullanım alanları

- Script dosyasını çalıştırılabilir yapmak
- Dosyaları yetkisiz erişime kapatmak
- Sunucuda güvenli erişim ayarlamak
- Yapılandırma dosyalarını korumak
- Proje dosyalarının erişim yapısını düzenlemek

### Neden önemlidir?

`chmod`, Linux güvenlik modelinin en temel parçalarından biridir. Yanlış izin vermek güvenlik açığına, fazla kısıtlama vermek ise erişim sorunlarına yol açabilir. Örneğin bir script çalışmıyorsa bunun sebebi çalıştırma izninin verilmemiş olması olabilir.

---

## top Komutu

`top`, sistemde çalışan işlemleri ve anlık kaynak kullanımını izlemek için kullanılır. Linux’ta görev yöneticisine benzer bir araçtır.

### Temel kullanım

```bash
top
```

Bu komut çalıştırıldığında ekranda dinamik olarak güncellenen bir süreç listesi görülür.

### Gösterdiği bilgiler

- CPU kullanımı
- Bellek kullanımı
- Çalışan işlemler
- İşlem kimliği (PID)
- Kullanıcı adı
- İşlem önceliği
- Sistem yükü
- Çalışma süresi

### Kullanım amacı

- Sistemi yavaşlatan işlemi bulmak
- Hangi uygulamanın fazla RAM kullandığını görmek
- CPU kullanımını izlemek
- Sistem sağlığını kontrol etmek
- Kaynak tüketen süreçleri fark etmek

### Önemli not

`top` canlı bir izleme aracıdır. Terminal açık kaldığı sürece verileri günceller. Çıkmak için genellikle `q` tuşuna basılır.

### Neden önemlidir?

Özellikle sunucu yönetiminde ve performans sorunlarının incelenmesinde çok faydalıdır. Bir uygulama donmuş gibi görünüyorsa, CPU aşırı yükselmişse veya RAM tüketimi kontrol edilmek isteniyorsa ilk bakılan araçlardan biri `top` olur.

---

## Paket Yönetimi

Linux’ta yazılım kurma, güncelleme ve kaldırma işlemleri genellikle **paket yöneticileri** aracılığıyla yapılır. Her dağıtım farklı bir paket yöneticisi kullanabilir. Bu araçlar, yazılımların merkezi depolardan güvenli ve düzenli biçimde kurulmasını sağlar.

Paket yöneticilerinin temel görevleri şunlardır:

- Yazılım kurmak
- Kurulu paketleri güncellemek
- Paket kaldırmak
- Bağımlılıkları çözmek
- Paket veritabanını yenilemek
- Sürüm uyumluluğunu korumak

Bir programı internetten rastgele indirip kurmak yerine paket yöneticisi ile kurmak, hem güvenlik hem de sistem bütünlüğü açısından daha doğrudur.

---

## apt Paket Yöneticisi

`apt`, Debian ve Ubuntu tabanlı sistemlerde kullanılan paket yöneticisidir.

### Paket listelerini güncelleme

```bash
sudo apt update
```

Bu komut, depolardaki mevcut paket bilgilerini yeniler.

### Kurulu paketleri güncelleme

```bash
sudo apt upgrade
```

Sistemde kurulu paketlerin yeni sürümlerini yükler.

### Paket kurma

```bash
sudo apt install nginx
```

Bu komut `nginx` paketini kurar.

### Paket kaldırma

```bash
sudo apt remove nginx
```

Paketi kaldırır ancak bazı yapılandırma dosyaları kalabilir.

### Tam kaldırma

```bash
sudo apt purge nginx
```

Paketi ve yapılandırma dosyalarını kaldırır.

### Gereksiz bağımlılıkları temizleme

```bash
sudo apt autoremove
```

Artık kullanılmayan bağımlılıkları kaldırır.

### Paket arama

```bash
apt search git
```

Depolarda ilgili paketi arar.

### Neden önemlidir?

Ubuntu ve Debian çok yaygın olduğu için `apt` bilgisi pratikte oldukça değerlidir. Özellikle geliştirici ortamı hazırlarken Git, Python, Node.js, Nginx gibi araçlar çoğu zaman `apt` ile kurulur.

---

## pacman Paket Yöneticisi

`pacman`, Arch Linux ve türevlerinde kullanılan paket yöneticisidir.

### Paket veritabanını yenileme ve sistemi güncelleme

```bash
sudo pacman -Syu
```

Bu komut hem paket veritabanını günceller hem de sistemi yükseltir.

### Paket kurma

```bash
sudo pacman -S vim
```

### Paket kaldırma

```bash
sudo pacman -R vim
```

### Paket ve bağımlılıkları kaldırma

```bash
sudo pacman -Rs vim
```

### Paket arama

```bash
pacman -Ss firefox
```

### Yüklü paketi listeleme

```bash
pacman -Q
```

### Neden önemlidir?

Arch Linux daha çok ileri seviye kullanıcılar ve özelleştirme sevenler tarafından kullanılır. `pacman`, sade ve güçlü bir araçtır. Komutlarının kısa ve sistematik olmasıyla dikkat çeker.

---

## dnf Paket Yöneticisi

`dnf`, Fedora, RHEL tabanlı sistemler ve bazı diğer dağıtımlarda kullanılır.

### Paket güncelleme

```bash
sudo dnf update
```

### Paket kurma

```bash
sudo dnf install httpd
```

### Paket kaldırma

```bash
sudo dnf remove httpd
```

### Paket arama

```bash
dnf search python
```

### Paket bilgisi görüntüleme

```bash
dnf info nginx
```

### Neden önemlidir?

Kurumsal Linux sistemlerinde Fedora ve RHEL tabanlı yapılar görülebildiği için `dnf` bilgisi de önemlidir. Özellikle sistem yöneticiliği ve kurumsal altyapı süreçlerinde karşımıza çıkabilir.

---

## Dosya İzinleri

Linux’ta her dosya ve klasörün bir erişim izni yapısı vardır. Bu yapı sistem güvenliğinin temel taşlarından biridir. Kimlerin hangi dosyayı okuyabileceği, düzenleyebileceği veya çalıştırabileceği bu izinlerle belirlenir.

### Kullanıcı türleri

Linux’ta izinler üç farklı kullanıcı kategorisine göre tanımlanır:

- **User (u):** Dosyanın sahibi
- **Group (g):** Dosyanın ait olduğu grup
- **Other (o):** Bunların dışındaki tüm kullanıcılar

### Temel izin türleri

- **r (read):** Okuma izni
- **w (write):** Yazma izni
- **x (execute):** Çalıştırma izni

### Örnek izin gösterimi

```bash
-rwxr-xr--
```

Bu ifade parçalara ayrılırsa:

- İlk karakter: dosya türü
  - `-` normal dosya
  - `d` dizin
- Sonraki üç karakter: kullanıcı izinleri
- Sonraki üç karakter: grup izinleri
- Sonraki üç karakter: diğer kullanıcı izinleri

Bu örnekte:

- Sahip: `rwx`
- Grup: `r-x`
- Diğerleri: `r--`

### Dizinlerde izin mantığı

Dosyalarda ve dizinlerde izinlerin anlamı biraz farklı olabilir:

Bir dosyada:

- `r`: içeriği okuyabilmek
- `w`: içeriği değiştirebilmek
- `x`: dosyayı çalıştırabilmek

Bir dizinde ise:

- `r`: dizin içeriğini listeleyebilmek
- `w`: dizine dosya ekleyip silebilmek
- `x`: dizine girebilmek

### Neden önemlidir?

Dosya izinleri:

- Güvenlik sağlar
- Yetkisiz erişimi önler
- Sunucu yapılandırmalarında kritik rol oynar
- Çok kullanıcılı sistemlerde düzen sağlar
- Uygulamaların düzgün çalışmasını etkiler

Örneğin bir script çalışmıyorsa nedeni çoğu zaman çalıştırma izninin verilmemiş olmasıdır. Ya da bir yapılandırma dosyası değiştirilemiyorsa yazma izni olmayabilir.

### İzinleri görüntüleme

```bash
ls -l
```

Bu komutla dosya izinleri görülebilir. Linux’ta izin mantığını anlayabilmek için `ls -l` çıktısını yorumlayabilmek çok önemlidir.

---

## Servis Yönetimi

Linux sistemlerde birçok uygulama arka planda servis olarak çalışır. Örneğin:

- Web sunucuları
- Veritabanları
- SSH servisleri
- Zamanlanmış görev servisleri
- Ağ servisleri
- Mesaj kuyruk servisleri

Bu servisleri yönetmek için modern Linux sistemlerinde genellikle `systemd` kullanılır. `systemd` ile servis kontrolü yapmak için kullanılan temel araç `systemctl` komutudur.

Servis kavramı özellikle sunucu sistemlerinde çok önemlidir. Çünkü bir uygulamanın arka planda sürekli aktif kalması, belirli bir portu dinlemesi veya sistem açıldığında otomatik çalışması gerekebilir.

---

## systemctl Komutu

`systemctl`, servisleri başlatmak, durdurmak, yeniden başlatmak, durumunu kontrol etmek ve açılışta otomatik çalışmasını ayarlamak için kullanılır.

### Servis durumunu kontrol etme

```bash
systemctl status nginx
```

Bu komut servisin:

- Çalışıp çalışmadığını
- Son loglarını
- Hata verip vermediğini
- Başlangıç durumunu

gösterebilir.

### Servis başlatma

```bash
sudo systemctl start nginx
```

### Servis durdurma

```bash
sudo systemctl stop nginx
```

### Servisi yeniden başlatma

```bash
sudo systemctl restart nginx
```

### Yapılandırma değişikliğinden sonra yeniden yükleme

```bash
sudo systemctl reload nginx
```

Bu komut bazı servislerde kesinti olmadan yapılandırmayı yenileyebilir.

### Sistem açıldığında otomatik başlatma

```bash
sudo systemctl enable nginx
```

### Açılışta otomatik başlamasını kapatma

```bash
sudo systemctl disable nginx
```

### Aktif mi kontrol etme

```bash
systemctl is-active nginx
```

### Etkin mi kontrol etme

```bash
systemctl is-enabled nginx
```

### Tüm servisleri listeleme

```bash
systemctl list-units --type=service
```

### Neden önemlidir?

Sunucu ortamlarında servis yönetimi temel iştir. Bir servis ayağa kalkmıyorsa uygulama çalışmaz, bir veritabanı durmuşsa sistem veri işleyemez, SSH servisi kapalıysa uzak bağlantı kurulamaz. Bu nedenle `systemctl`, Linux yönetiminin en kritik araçlarından biridir.

---

## Linux Dosya Sistemi Mantığı

Linux’ta her şey dosya mantığına yakın bir yapı ile ele alınır. Donanım aygıtları, yapılandırma dosyaları, kullanıcı dosyaları ve sistem kayıtları belirli dizin yapıları altında bulunur. Bu yapı Windows’tan farklıdır ve anlaşılması önemlidir.

### Bazı temel dizinler

- `/` : Kök dizindir. Tüm sistem buradan başlar.
- `/home` : Kullanıcıların kişisel dizinleri burada bulunur.
- `/etc` : Yapılandırma dosyaları burada tutulur.
- `/var` : Loglar, geçici veriler ve değişken sistem verileri burada bulunur.
- `/bin` : Temel komutlar burada bulunabilir.
- `/usr` : Kullanıcı programları ve ek sistem bileşenleri burada yer alır.
- `/tmp` : Geçici dosyalar için kullanılır.

### Neden önemlidir?

Linux’ta bir uygulamanın logu nerede, yapılandırma dosyası nerede, kullanıcı verisi nerede gibi soruların cevabı çoğu zaman bu dizin mantığına bağlıdır. Yazılımcı veya sistem yöneticisi için bu yapıyı bilmek, hata çözme ve sistem yönetiminde büyük kolaylık sağlar.

---

## Linux Temellerinin Yazılım Geliştirme Açısından Önemi

Linux temellerini öğrenmek yalnızca işletim sistemi bilgisi kazanmak değildir. Aynı zamanda bir yazılımcının profesyonel geliştirme ortamını daha iyi anlamasını sağlar.

### 1. Sunucu mantığını anlamayı sağlar

Birçok uygulama Linux sunucular üzerinde çalışır. Geliştirici, uygulamasının gerçek ortamda nasıl çalıştığını daha iyi kavrar.

### 2. Terminal hakimiyeti kazandırır

Kod klonlama, bağımlılık kurma, test çalıştırma, container yönetimi, log inceleme gibi birçok işlem terminal üzerinden yapılır.

### 3. Hata çözme becerisi geliştirir

Sistem logları, servis durumları, işlem kullanımları ve izin sorunları Linux araçlarıyla incelenebilir.

### 4. DevOps ve deployment süreçlerinde avantaj sağlar

CI/CD, Docker, Nginx, Apache, systemd, SSH ve uzak sunucu işlemleri Linux bilgisi gerektirir.

### 5. Güvenlik farkındalığı oluşturur

Dosya izinleri, kullanıcı yetkileri ve servis yönetimi sayesinde sistem güvenliği daha iyi anlaşılır.

### 6. Altyapı bağımsız düşünmeyi öğretir

Sadece IDE üzerinden değil, sistem düzeyinde de düşünebilen geliştirici daha güçlü olur.

### 7. Gerçek dünya yazılım ortamlarına hazırlık sağlar

Üniversite ortamında çoğu zaman sadece kod yazmaya odaklanılsa da gerçek iş hayatında sistemle etkileşim kurmak gerekir. Bu nedenle Linux bilgisi profesyonel gelişimde doğrudan katkı sağlar.

---

## Örnek Uygulama Senaryoları

Bu bölümde Linux temellerinin pratikte nasıl kullanıldığına dair örnekler verilmiştir.

### Senaryo 1: Yeni proje klasörü oluşturma

Bir geliştirici yeni bir çalışma alanı hazırlamak istediğinde şu komutları kullanabilir:

```bash
mkdir -p proje/src
cd proje
ls
```

Burada:

- Yeni klasör yapısı oluşturulmuştur.
- Proje dizinine geçilmiştir.
- İçerik kontrol edilmiştir.

### Senaryo 2: Bir script dosyasını çalıştırılabilir yapmak

```bash
chmod +x backup.sh
./backup.sh
```

Burada script dosyasına çalıştırma izni verilmiş ve ardından çalıştırılmıştır.

### Senaryo 3: Log dosyasında hata aramak

```bash
grep -i "error" app.log
```

Burada hata mesajları hızlıca bulunabilir.

### Senaryo 4: Sistemi yavaşlatan işlemi incelemek

```bash
top
```

Bu komut ile hangi işlemin fazla CPU veya RAM kullandığı görülebilir.

### Senaryo 5: Web servisinin durumunu kontrol etmek

```bash
systemctl status nginx
```

Servisin çalışıp çalışmadığı anlaşılır.

### Senaryo 6: Paket kurmak

Ubuntu tabanlı sistemde:

```bash
sudo apt install git
```

Bu komut ile Git kurulabilir.

### Senaryo 7: Gizli dosyaları görmek

```bash
ls -a
```

Bu komut özellikle terminal yapılandırma dosyalarını görmek için yararlıdır.

### Senaryo 8: Bir üst dizine dönmek

```bash
cd ..
```

Bu kullanım dizinler arasında hızlı gezinme sağlar.

---

## Sonuç

Bu haftaki çalışmada Linux’un temel bileşenleri detaylı olarak incelenmiştir. Terminal mantığı, temel komutlar, paket yönetim sistemleri, dosya izinleri ve servis yönetimi konuları Linux kullanımının temelini oluşturmaktadır. Bu bilgiler yalnızca sistem yöneticileri için değil, yazılım geliştiriciler için de kritik öneme sahiptir.

Özellikle `ls`, `cd`, `grep`, `mkdir`, `chmod` ve `top` gibi komutlar günlük kullanımda sıkça karşılaşılan araçlardır. Bunun yanında `apt`, `pacman` ve `dnf` gibi paket yöneticileri yazılım kurulumunu ve güncellemeyi kolaylaştırır. Dosya izinleri Linux güvenliğinin temelini oluştururken, `systemctl` ile servis yönetimi sistem kontrolünü mümkün hale getirir.

Linux bilgisi, yazılımcının yalnızca kod yazan biri değil, aynı zamanda uygulamanın çalıştığı sistemi anlayan bir geliştirici olmasını sağlar. Bu da hem teknik yeterliliği artırır hem de profesyonel hayatta büyük avantaj sağlar.

---

## Kazanım

Bu çalışma sonunda aşağıdaki kazanımlar elde edilmiştir:

- Linux işletim sistemi mantığı anlaşılmıştır.
- Terminal kullanımının önemi kavranmıştır.
- Temel Linux komutlarının işlevleri öğrenilmiştir.
- `ls`, `cd`, `grep`, `mkdir`, `chmod` ve `top` komutlarının kullanım mantığı anlaşılmıştır.
- Paket yönetim sistemlerinin mantığı öğrenilmiştir.
- `apt`, `pacman` ve `dnf` paket yöneticileri karşılaştırmalı olarak incelenmiştir.
- Dosya izin yapısı detaylı şekilde öğrenilmiştir.
- Linux’ta kullanıcı, grup ve diğer kullanıcı izinleri kavranmıştır.
- Servis yönetimi konusunda temel bilgi edinilmiştir.
- `systemctl` komutu ile servis kontrolünün mantığı öğrenilmiştir.
- Linux dosya sistemi yapısının genel mantığı anlaşılmıştır.
- Yazılım geliştirme süreçlerinde Linux bilgisinin neden önemli olduğu görülmüştür.
- Sunucu, terminal ve altyapı konularında temel farkındalık kazanılmıştır.
