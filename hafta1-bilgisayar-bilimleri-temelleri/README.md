# Bilgisayar Bilimleri Temelleri ve Kod Yazma Sureci

## Giris

Bu raporda bilgisayar bilimlerinin temel kavramlarini, kendi deneyimim uzerinden yani bilgisayarda kod yazma surecine gore acikladim. Kod yazarken aslinda sadece metin yazmadigimi, arka planda bircok donanim ve yazilim bileseninin birlikte calistigini fark ettim.

VS Code gibi bir editor acip kod yazdigimda, kaydettigimde ve programi calistirdigimda CPU, RAM, disk ve isletim sistemi birlikte calisir. Bu nedenle bu kavramlari sadece teorik olarak degil, yazilim gelistirme surecindeki rollerine gore aciklamak daha anlamli hale gelmektedir.

---

## CPU (Merkezi Islem Birimi)

CPU, bilgisayarin en onemli parcalarindan biridir ve tum hesaplamalari gerceklestirir. Kod yazma surecinde CPU’nun rolu cok kritiktir.

Ben bir program yazip calistirdigimda, yazdigim kod aslinda CPU tarafindan satir satir islenir. Ornegin bir toplama islemi yaptigimda, bu islemi gercekte CPU gerceklestirir.

CPU:
- Komutlari sirayla isler
- Matematiksel islemleri yapar
- Kosullari kontrol eder (if-else)
- Donguleri calistirir (for, while)
- Program akisini yonetir

Yani ben kod yazarak bir mantik kuruyorum, ancak bu mantigin fiziksel olarak calistirilmasini CPU saglar. Bu nedenle CPU hizi ve performansi, yazdigim kodun calisma hizini dogrudan etkiler.

---

## RAM (Bellek)

RAM, bilgisayarin gecici veri depolama alanidir. Kod yazarken RAM’in onemi cok buyuktur.

Ben VS Code’u actigimda, bu program diskten okunur ve RAM’e yuklenir. Ayni sekilde yazdigim kodlar, acik dosyalar ve calisan programlar RAM uzerinde tutulur.

Kod yazarken RAM su islemlerde kullanilir:
- Acik olan editorler RAM’de tutulur
- Yazdigim kod gecici olarak RAM’de saklanir
- Program calisirken olusan degiskenler RAM’de tutulur
- Gecici hesaplamalar RAM uzerinde yapilir

RAM’in en onemli ozelligi gecici olmasidir. Bilgisayari kapattigimda RAM’deki veriler silinir. Bu nedenle kodumu kaydetmezsem kaybolabilir.

Ayrica RAM yetersiz oldugunda:
- Bilgisayar yavaslar
- Programlar gec acilir
- Kod calistirma performansi duser

Bu nedenle yazilim gelistirme surecinde yeterli RAM cok onemlidir.

---

## Disk (Depolama)

Disk, verilerin kalici olarak saklandigi yerdir. Kod yazma surecinde disk uzerinde tum projelerim bulunur.

Ben bir proje olusturdugumda:
- Kod dosyalarim (.py, .java, .cpp)
- README dosyalari
- Kutuphaneler
- Proje klasorleri

hepsi disk uzerinde saklanir.

Kod yazarken disk su durumlarda kullanilir:
- Editor programlari diskten acilir
- Dosyalar kaydedilir
- Projeler klasorler halinde tutulur
- Derlenen dosyalar diske yazilir

SSD ve HDD arasindaki fark da burada onemlidir:
- SSD daha hizlidir
- Programlar daha hizli acilir
- Dosya okuma/yazma daha hizlidir

Bu nedenle SSD kullanan bilgisayarlarda yazilim gelistirme sureci daha akici olur.

---

## Isletim Sistemi

Isletim sistemi, kullanici ile donanim arasindaki koprudur. Kod yazma surecinde tum islemler aslinda isletim sistemi uzerinden gerceklesir.

Ben:
- Dosya acarken
- Kod kaydederken
- Program calistirirken
- Terminal kullanirken

hep isletim sistemi araciligiyla bu islemleri yaparim.

Isletim sistemi:
- RAM kullanimini yonetir
- CPU’yu programlar arasinda paylastirir
- Dosya sistemini duzenler
- Programlarin calismasini kontrol eder

Ornegin ayni anda hem tarayici hem editor hem de terminal kullanabiliyorsam, bu isletim sisteminin yonetimi sayesinde mumkundur.

---

## Kod Yazma Surecinde Bu Kavramlarin Birlikte Calismasi

Bilgisayarda kod yazma sureci aslinda birden fazla bilesenin birlikte calismasini gerektirir.

Benim acimdan bu surec su sekilde ilerler:

1. Bilgisayari acarim → Isletim sistemi baslar  
2. VS Code’u acarim → Program diskten RAM’e yuklenir  
3. Kod yazmaya baslarim → Klavye girisleri isletim sistemi ile editore iletilir  
4. Kod gecici olarak RAM’de tutulur  
5. Ctrl + S yaparim → Kod diske kaydedilir  
6. Programi calistiririm → CPU komutlari isler  
7. Sonuclar ekrana yazdirilir  

Bu surecte:
- CPU islemleri yapar
- RAM aktif verileri tutar
- Disk kalici depolama saglar
- Isletim sistemi tum sureci yonetir

Yani yazilim gelistirme sadece kod yazmak degil, ayni zamanda bu bilesenlerin birlikte calismasini anlamaktir.

---

## Sonuc

Bu raporu hazirlarken bilgisayarda kod yazma surecinin aslinda ne kadar karmasik ama duzenli bir yapida ilerledigini daha iyi anladim.

CPU, RAM, disk ve isletim sistemi gibi temel kavramlar sadece teorik bilgiler degil, her gun aktif olarak kullandigim ve yazilim gelistirme surecimi dogrudan etkileyen bilesenlerdir.

Kod yazarken yasadigim performans, hiz ve deneyim bu bilesenlerin ne kadar verimli calistigina baglidir. Bu nedenle bu kavramlari anlamak, daha iyi bir yazilim gelistirici olmak icin onemlidir.