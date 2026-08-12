# 6. API Mantığı (REST & JSON Temelleri)

## İçindekiler

- [1. API Nedir?](#1-api-nedir)
- [2. API Neden Kullanılır?](#2-api-neden-kullanılır)
- [3. API Mantığı Nasıl Çalışır?](#3-api-mantığı-nasıl-çalışır)
- [4. Frontend, Backend ve API İlişkisi](#4-frontend-backend-ve-api-ilişkisi)
- [5. REST Nedir?](#5-rest-nedir)
- [6. REST API Mantığı](#6-rest-api-mantığı)
- [7. HTTP Metotları](#7-http-metotları)
- [8. GET Metodu](#8-get-metodu)
- [9. POST Metodu](#9-post-metodu)
- [10. PUT Metodu](#10-put-metodu)
- [11. DELETE Metodu](#11-delete-metodu)
- [12. PATCH Metodu](#12-patch-metodu)
- [13. CRUD Mantığı](#13-crud-mantığı)
- [14. JSON Nedir?](#14-json-nedir)
- [15. JSON Yapısı](#15-json-yapısı)
- [16. Request ve Response Mantığı](#16-request-ve-response-mantığı)
- [17. Endpoint Nedir?](#17-endpoint-nedir)
- [18. Basit Bir Endpoint Nasıl Tasarlanır?](#18-basit-bir-endpoint-nasıl-tasarlanır)
- [19. Örnek Ürün API Tasarımı](#19-örnek-ürün-api-tasarımı)
- [20. API Testi Nasıl Yapılır?](#20-api-testi-nasıl-yapılır)
- [21. Kazanım](#21-kazanım)
- [22. Genel Özet](#22-genel-özet)

---

## 1. API Nedir?

API, İngilizce olarak **Application Programming Interface** ifadesinin kısaltmasıdır. Türkçeye **Uygulama Programlama Arayüzü** olarak çevrilebilir.
Daha anlaşılır bir ifadeyle API, farklı yazılımların, uygulamaların veya sistemlerin birbirleriyle iletişim kurmasını sağlayan yapıdır.
Bir uygulama başka bir uygulamadan veri almak, veri göndermek, işlem yaptırmak veya belirli bir servisi kullanmak istediğinde API kullanır.
Örneğin bir web sitesinde ürünleri listelemek istediğimizi düşünelim. Kullanıcı siteye girdiğinde ürünler ekranda görünür. Ancak bu ürünler genellikle doğrudan HTML dosyasının içine yazılmaz. Ürün bilgileri çoğunlukla bir veritabanında tutulur.
Frontend tarafı, yani kullanıcının gördüğü arayüz, backend tarafına bir istek gönderir. Backend bu isteği alır, veritabanından ürünleri çeker ve frontend’e geri gönderir. Bu iletişim API aracılığıyla gerçekleşir.Temel akış şu şekildedir:

```text
Frontend → API → Backend → Veritabanı
```

Cevap dönüşü ise şu şekildedir:

```text
Veritabanı → Backend → API → Frontend
```

Bu yapıda API, frontend ile backend arasında bir köprü görevi görür.

---

## 2. API Neden Kullanılır?

API kullanımı modern yazılım geliştirmede çok önemlidir. Günümüzde uygulamalar genellikle tek başına çalışmaz. Web uygulamaları, mobil uygulamalar, ödeme sistemleri, harita servisleri, yapay zeka servisleri ve veritabanları birbirleriyle sürekli iletişim halindedir.Bu iletişimi düzenli, güvenli ve kontrollü şekilde sağlayan yapı API’dir.

---

### 2.1. Sistemler Arası İletişim Sağlar

API, farklı sistemlerin birbirleriyle konuşmasını sağlar.Örneğin:

- Bir hava durumu uygulaması, hava durumu verilerini başka bir servisin API’sinden alır.
- Bir e-ticaret sitesi, ödeme almak için banka veya ödeme sistemi API’sini kullanır.
- Bir mobil uygulama, kullanıcı bilgilerini backend API’sinden çeker.
- Bir harita uygulaması, konum ve rota bilgilerini harita API’sinden alır.
- Bir yapay zeka uygulaması, modelden cevap almak için AI servisinin API’sine istek gönderir.

Yani API, uygulamaların birbirine bağlanmasını sağlar.

---

### 2.2. Frontend ve Backend Ayrımını Sağlar

Modern yazılım geliştirmede frontend ve backend genellikle ayrı geliştirilir.Frontend tarafı kullanıcının gördüğü arayüzdür. Örneğin:

- HTML
- CSS
- JavaScript
- React
- Vue
- Angular
- Flutter

gibi teknolojiler frontend tarafında kullanılabilir.Backend tarafı ise uygulamanın arka planda çalışan kısmıdır. Örneğin:

- Node.js
- Java Spring Boot
- Python Django
- Python Flask
- Python FastAPI
- C# ASP.NET Core
- PHP Laravel

gibi teknolojiler backend geliştirmede kullanılabilir.Frontend JavaScript ile, backend ise Python ile yazılmış olabilir. Bu iki taraf farklı teknolojilerle geliştirilse bile API sayesinde iletişim kurabilir.Çünkü frontend ve backend genellikle JSON gibi ortak bir veri formatı üzerinden haberleşir.

---

### 2.3. Veritabanını Doğrudan Dışarı Açmaz

Frontend tarafının doğrudan veritabanına bağlanması güvenli değildir. Çünkü frontend kodları kullanıcının tarayıcısında çalışır ve incelenebilir.Eğer frontend doğrudan veritabanına bağlanırsa:

- Veritabanı bağlantı bilgileri açığa çıkabilir.
- Kullanıcılar yetkisiz verilere ulaşabilir.
- Veri güvenliği tehlikeye girer.
- Sistemde ciddi güvenlik açıkları oluşabilir.
- Veri bütünlüğü bozulabilir.

Bu nedenle frontend doğrudan veritabanına gitmez. Bunun yerine backend API’ye istek gönderir.Backend tarafı:

- Kullanıcının yetkisini kontrol eder.
- Gönderilen veriyi doğrular.
- Gerekirse veritabanına gider.
- Uygun cevabı frontend’e döndürür.

Bu yapı sistemi daha güvenli hale getirir.

---

### 2.4. Aynı Backend’i Farklı Platformlar Kullanabilir

Bir API yalnızca web sitesi tarafından kullanılmak zorunda değildir. Aynı API farklı platformlar tarafından da kullanılabilir.Örneğin bir alışveriş uygulamasının backend API’si şu platformlar tarafından kullanılabilir:

- Web sitesi
- Android uygulaması
- iOS uygulaması
- Admin paneli
- Masaüstü uygulaması

Bu durumda her platform için ayrı backend yazmaya gerek kalmaz. Ortak bir backend API geliştirilir ve tüm istemciler bu API’yi kullanır.

Örnek yapı:

```text
Web Uygulaması     → 
Mobil Uygulama     →   Backend API
Admin Paneli       →
```

Bu yapı yazılım geliştirme sürecini daha düzenli ve sürdürülebilir hale getirir.

---

### 2.5. Güvenli ve Kontrollü Veri Paylaşımı Sağlar

API sayesinde sistem dış dünyaya tamamen açılmaz. Sadece belirlenen endpointler üzerinden belirli işlemlere izin verilir.Örneğin bir kullanıcı sadece kendi profil bilgilerini görebilir. Başka bir kullanıcının bilgilerine ulaşamaması gerekir.Bunun kontrolü backend API tarafında yapılır.Örneğin:

```http
GET /users/5
```

Bu istek geldiğinde backend şunu kontrol edebilir:

```text
Bu isteği atan kullanıcı, ID’si 5 olan kullanıcının bilgisine erişebilir mi?
```

Eğer erişim izni yoksa backend şu cevabı döndürebilir:

```http
403 Forbidden
```

Bu nedenle API yalnızca veri taşıyan bir yapı değildir. Aynı zamanda güvenlik, kontrol ve yetkilendirme mekanizmasının da önemli bir parçasıdır.

---

## 3. API Mantığı Nasıl Çalışır?

API mantığı temel olarak **request** ve **response** ilişkisine dayanır.

```text
Request  → İstek
Response → Cevap
```

Bir istemci yani client, API’ye bir request gönderir. API bu request’i backend tarafında işler ve client’a bir response döndürür.Client tarafı şunlar olabilir:

- Web tarayıcısı
- Mobil uygulama
- Masaüstü uygulaması
- Postman
- Swagger
- Başka bir backend servisi

Server tarafı ise isteği alan, işleyen ve cevap döndüren taraftır.Temel akış şu şekildedir:

```text
1. Kullanıcı bir işlem yapar.
2. Frontend API’ye request gönderir.
3. Backend request’i alır.
4. Backend gerekli kontrolleri yapar.
5. Gerekirse veritabanına gider.
6. Backend response oluşturur.
7. Frontend gelen response’u alır.
8. Kullanıcıya sonuç gösterilir.
```

Örneğin kullanıcı ürün listesini görmek istiyor olsun:

```text
Kullanıcı ürünler sayfasını açar.
Frontend GET /products isteği gönderir.
Backend isteği alır.
Backend ürünleri veritabanından çeker.
Backend ürünleri JSON formatında frontend’e döner.
Frontend ürünleri ekranda gösterir.
```

Bu, API mantığının en temel çalışma şeklidir.

---

## 4. Frontend, Backend ve API İlişkisi

Web uygulamalarında frontend, backend ve API birlikte çalışır.

---

### 4.1. Frontend Nedir?

Frontend, kullanıcının gördüğü ve etkileşime geçtiği kısımdır.Örneğin:

- Butonlar
- Formlar
- Menüler
- Ürün kartları
- Profil ekranı
- Sepet ekranı
- Giriş sayfası
- Kayıt ekranı

Frontend tarafında kullanıcı arayüzü oluşturulur.Örneğin kullanıcı giriş formuna email ve şifre yazdığında, frontend bu bilgileri alır ve backend’e göndermek için API isteği oluşturur.

---

### 4.2. Backend Nedir?

Backend, uygulamanın arka planda çalışan kısmıdır.Backend tarafında genellikle şu işlemler yapılır:

- Kullanıcı kaydı
- Kullanıcı girişi
- Yetki kontrolü
- Veritabanı işlemleri
- İş kuralları
- Veri doğrulama
- Dosya işlemleri
- Mail gönderme
- Ödeme işlemleri
- API response oluşturma

Kullanıcı backend’i doğrudan görmez. Ancak frontend’de yapılan birçok işlemin arkasında backend çalışır.

---

### 4.3. API Bu İlişkide Nerededir?

API, frontend ile backend arasındaki iletişim katmanıdır.Frontend, backend’e doğrudan kod seviyesinde ulaşmaz. Bunun yerine belirli URL’lere istek gönderir.Örneğin:

```http
GET /products
POST /users
POST /auth/login
DELETE /products/5
```

Bu endpointler backend tarafından tanımlanır. Frontend bu endpointlere istek göndererek backend ile iletişim kurar.

---

## 5. REST Nedir?

REST, web servisleri ve API tasarımında kullanılan yaygın bir mimari yaklaşımdır.REST’in açılımı:

```text
Representational State Transfer
```

REST temel olarak şunu söyler:

```text
Kaynaklara belirli URL’ler üzerinden erişilir ve bu kaynaklar üzerinde HTTP metotlarıyla işlem yapılır.
```

Buradaki **kaynak** kavramı çok önemlidir.Kaynak, sistemde üzerinde işlem yapılan veri türüdür.Örneğin bir e-ticaret sisteminde kaynaklar şunlar olabilir:

```text
products
users
orders
categories
comments
payments
cart-items
```

Bir okul sisteminde kaynaklar şunlar olabilir:

```text
students
teachers
courses
exams
grades
departments
```

Bir blog sisteminde kaynaklar şunlar olabilir:

```text
posts
comments
users
tags
categories
```

REST API’de her kaynak için belirli endpointler tasarlanır.Örneğin ürünler için:

```http
GET /products
POST /products
GET /products/5
PUT /products/5
PATCH /products/5
DELETE /products/5
```

Bu yapıda URL kaynakları, HTTP metotları ise yapılacak işlemi ifade eder.

---

## 6. REST API Mantığı

REST API’de temel mantık şudur:

```text
Kaynak + HTTP Metodu = Yapılacak İşlem
```

Örneğin:

```http
GET /products
```

Burada:

```text
GET       → Veri getir
/products → Ürünler kaynağı
```

Yani anlamı:

```text
Ürünleri getir.
```

Başka bir örnek:

```http
POST /products
```

Burada:

```text
POST      → Yeni veri oluştur
/products → Ürünler kaynağı
```

Yani anlamı:

```text
Yeni ürün oluştur.
```

Bir başka örnek:

```http
DELETE /products/5
```

Burada:

```text
DELETE      → Sil
/products/5 → ID’si 5 olan ürün
```

Yani anlamı:

```text
ID’si 5 olan ürünü sil.
```

REST API’de endpoint isimlerinde genellikle fiil kullanılmaz. Çünkü fiil görevini HTTP metodu yapar.Yanlış kullanım:

```http
GET /getProducts
POST /createProduct
DELETE /deleteProduct/5
```

Daha doğru REST kullanımı:

```http
GET /products
POST /products
DELETE /products/5
```

Burada işlem zaten HTTP metodundan anlaşılır.

---

## 7. HTTP Metotları

HTTP metotları, bir API isteğinin hangi amaçla yapıldığını belirtir.En temel HTTP metotları şunlardır:

```text
GET
POST
PUT
PATCH
DELETE
```

Bu metotlar REST API tasarımında CRUD işlemlerine karşılık gelir.CRUD şu kelimelerin kısaltmasıdır:

```text
Create → Oluşturma
Read   → Okuma
Update → Güncelleme
Delete → Silme
```

HTTP metotları ile CRUD ilişkisi genel olarak şöyledir:

| CRUD İşlemi | HTTP Metodu | Açıklama |
|---|---|---|
| Create | POST | Yeni veri oluşturur |
| Read | GET | Var olan veriyi okur/getirir |
| Update | PUT | Var olan veriyi tamamen günceller |
| Update | PATCH | Var olan verinin belirli alanlarını günceller |
| Delete | DELETE | Var olan veriyi siler |

Bu metotları bilmek API mantığını anlamanın temelidir.

---

## 8. GET Metodu

GET metodu, API’den veri almak için kullanılır.Bir veriyi okumak, listelemek veya görüntülemek istediğimizde GET kullanırız.Örneğin tüm ürünleri listelemek için:

```http
GET /products
```

Bu istek backend’e şu anlamı verir:

```text
Bana ürünleri getir.
```

Backend bu isteği alır, veritabanından ürünleri çeker ve genellikle JSON formatında geri döndürür.Örnek response:

```json
[
  {
    "id": 1,
    "name": "Laptop",
    "price": 25000,
    "stock": 10
  },
  {
    "id": 2,
    "name": "Mouse",
    "price": 500,
    "stock": 50
  }
]
```

Tek bir ürünü getirmek istersek endpoint şu şekilde olabilir:

```http
GET /products/1
```

Bu istek şu anlama gelir:

```text
ID’si 1 olan ürünü getir.
```

Örnek response:

```json
{
  "id": 1,
  "name": "Laptop",
  "price": 25000,
  "stock": 10
}
```

GET metodunun özellikleri:

- Veri okumak için kullanılır.
- Genellikle request body gönderilmez.
- URL üzerinden bilgi gönderilebilir.
- Filtreleme, arama ve sayfalama query parameter ile yapılabilir.
- Veri üzerinde değişiklik yapmamalıdır.
- Listeleme ve detay görüntüleme işlemlerinde kullanılır.

Örneğin kategoriye göre ürün listeleme:

```http
GET /products?category=electronics
```

Arama yapma:

```http
GET /products?search=laptop
```

Sayfalama:

```http
GET /products?page=1&limit=10
```

Fiyata göre filtreleme:

```http
GET /products?minPrice=1000&maxPrice=5000
```

GET isteği, sistemdeki verileri değiştirmeden sadece okumak için kullanılmalıdır.

---

## 9. POST Metodu

POST metodu, yeni veri oluşturmak için kullanılır.Bir kullanıcı sisteme kayıt olacaksa, yeni ürün eklenecekse, yeni sipariş oluşturulacaksa veya yeni yorum yazılacaksa genellikle POST metodu kullanılır.Örneğin yeni ürün eklemek için:

```http
POST /products
```

Bu istekte gönderilecek veri request body içinde yer alır.Örnek request body:

```json
{
  "name": "Keyboard",
  "price": 900,
  "stock": 25
}
```

Bu istek backend’e şu anlamı verir:

```text
Bu bilgilerle yeni bir ürün oluştur.
```

Backend bu veriyi alır, doğrular, veritabanına kaydeder ve cevap döndürür.Örnek response:

```json
{
  "success": true,
  "message": "Product created successfully",
  "data": {
    "id": 3,
    "name": "Keyboard",
    "price": 900,
    "stock": 25
  }
}
```

Burada dikkat edilmesi gereken nokta şudur:

Frontend ürün oluştururken genellikle `id` göndermez. Çünkü `id` değeri çoğunlukla backend veya veritabanı tarafından otomatik oluşturulur.POST metodunun özellikleri:

- Yeni veri oluşturmak için kullanılır.
- Request body ile veri gönderilir.
- Genellikle `201 Created` status code döner.
- Aynı POST isteği birden fazla kez gönderilirse birden fazla kayıt oluşturabilir.
- Kullanıcı kayıt, login, ürün ekleme, yorum ekleme gibi işlemlerde kullanılır.

Kullanıcı kayıt örneği:

```http
POST /users
```

Request body:

```json
{
  "name": "Özge",
  "email": "ozge@example.com",
  "password": "123456"
}
```

Login örneği:

```http
POST /auth/login
```

Request body:

```json
{
  "email": "ozge@example.com",
  "password": "123456"
}
```

Login işlemi teknik olarak yeni bir kullanıcı oluşturmaz. Ancak kullanıcıdan email ve şifre gibi bilgiler backend’e gönderildiği ve bir işlem başlatıldığı için genellikle POST kullanılır.

---

## 10. PUT Metodu

PUT metodu, var olan bir kaydı güncellemek için kullanılır.PUT genellikle bir kaydı tamamen güncelleme mantığıyla çalışır.Örneğin ID’si 5 olan ürünü güncellemek için:

```http
PUT /products/5
```

Request body:

```json
{
  "name": "Mechanical Keyboard",
  "price": 1500,
  "stock": 15
}
```

Bu istek backend’e şu anlamı verir:

```text
ID’si 5 olan ürünü bu bilgilerle güncelle.
```

Örneğin eski ürün bilgisi şöyle olsun:

```json
{
  "id": 5,
  "name": "Keyboard",
  "price": 900,
  "stock": 25
}
```

PUT isteği gönderildikten sonra ürün şöyle olabilir:

```json
{
  "id": 5,
  "name": "Mechanical Keyboard",
  "price": 1500,
  "stock": 15
}
```

PUT metodunun özellikleri:

- Var olan veriyi güncellemek için kullanılır.
- Güncellenecek kaydın `id` değeri genellikle URL içinde gönderilir.
- Request body içinde yeni bilgiler yer alır.
- Kaydın tamamının güncellenmesi beklenebilir.
- Eksik alan gönderilirse bazı backendlerde eksik alanlar `null` veya boş kabul edilebilir.
- Bu nedenle PUT kullanılırken güncellenecek kaydın tüm önemli alanları gönderilmelidir.

Örneğin mevcut ürün şu şekilde olsun:

```json
{
  "id": 5,
  "name": "Keyboard",
  "price": 900,
  "stock": 25,
  "category": "Electronics"
}
```

Eğer PUT ile sadece şu gönderilirse:

```json
{
  "stock": 35
}
```

bazı sistemlerde diğer alanlar korunabilir, bazı sistemlerde ise boş veya `null` olabilir. Bu durum backend’in nasıl yazıldığına bağlıdır.Ancak teorik olarak PUT, kaydın tamamını güncellemek için kullanılır.Bu yüzden PUT için daha doğru body örneği şudur:

```json
{
  "name": "Keyboard",
  "price": 900,
  "stock": 35,
  "category": "Electronics"
}
```

---

## 11. DELETE Metodu

DELETE metodu, var olan bir kaydı silmek için kullanılır.Örneğin ID’si 5 olan ürünü silmek için:

```http
DELETE /products/5
```

Bu istek backend’e şu anlamı verir:

```text
ID’si 5 olan ürünü sil.
```

DELETE isteğinde çoğu zaman body gönderilmez. Çünkü silinecek kayıt URL’deki id değerinden anlaşılır.Başarılı response örneği:

```json
{
  "success": true,
  "message": "Product deleted successfully"
}
```

Bazı API’lerde başarılı silme işleminden sonra response body dönülmez. Sadece status code döner:

```http
204 No Content
```

Bu şu anlama gelir:

```text
İşlem başarılı, fakat döndürülecek içerik yok.
```

DELETE metodunun özellikleri:

- Veri silmek için kullanılır.
- Silinecek kaydın `id` değeri genellikle URL içinde yer alır.
- Request body genellikle kullanılmaz.
- Başarılı olduğunda `200 OK` veya `204 No Content` dönebilir.
- Kayıt bulunamazsa `404 Not Found` dönebilir.

Örnek:

```http
DELETE /users/10
```

Anlamı:

```text
ID’si 10 olan kullanıcıyı sil.
```

---

## 12. PATCH Metodu

PATCH metodu, var olan bir kaydın sadece belirli alanlarını güncellemek için kullanılır.PUT ile PATCH arasındaki en önemli fark şudur:

```text
PUT   → Kaydın tamamını günceller.
PATCH → Kaydın sadece gönderilen alanlarını günceller.
```

Örneğin veritabanında şu ürün olsun:

```json
{
  "id": 5,
  "name": "Keyboard",
  "price": 900,
  "stock": 20,
  "category": "Electronics"
}
```

Bu ürünün sadece stok bilgisini 20’den 35’e çıkarmak istiyoruz.Bu durumda PATCH isteği şöyle olur:

```http
PATCH /products/5
Content-Type: application/json
```

Request body:

```json
{
  "stock": 35
}
```

Burada önemli nokta şudur:

```http
PATCH /products/5
```

satırı sadece hangi ürünün güncelleneceğini belirtir.

Yani:

```text
/products/5 → ID’si 5 olan ürünü bul.
```

Asıl değişiklik bilgisi body kısmındadır:

```json
{
  "stock": 35
}
```

Bu da şu anlama gelir:

```text
Bu ürünün stock alanını 35 yap.
```

Eski değer olan 20 request içinde gönderilmez. Çünkü backend eski değeri zaten veritabanından bilir. Frontend sadece yeni değeri gönderir.Son durumda ürün şu hale gelir:

```json
{
  "id": 5,
  "name": "Keyboard",
  "price": 900,
  "stock": 35,
  "category": "Electronics"
}
```

Burada sadece `stock` alanı değişmiştir. `name`, `price` ve `category` alanları aynı kalmıştır.PATCH şu durumlarda çok kullanışlıdır:

- Sadece stok güncellemek
- Sadece fiyat güncellemek
- Sadece profil fotoğrafı değiştirmek
- Sadece kullanıcı açıklamasını değiştirmek
- Sadece sipariş durumunu güncellemek
- Sadece aktif/pasif durumunu değiştirmek
- Sadece şifre değiştirmek

Örnek sipariş durumu güncelleme:

```http
PATCH /orders/12
```

Request body:

```json
{
  "status": "shipped"
}
```

Bu istek şu anlama gelir:

```text
ID’si 12 olan siparişin sadece status alanını shipped yap.
```

PATCH daha küçük, hedefli ve parçalı güncellemeler için kullanılır.

---

## 13. CRUD Mantığı

CRUD, yazılım geliştirmede en temel veri işlem mantıklarından biridir.CRUD kelimesi şu işlemleri ifade eder:

```text
Create → Oluştur
Read   → Oku
Update → Güncelle
Delete → Sil
```

Birçok uygulamanın temelinde CRUD işlemleri vardır.Örneğin bir ürün yönetim sisteminde:

- Ürün eklemek → Create
- Ürünleri listelemek → Read
- Ürün bilgilerini güncellemek → Update
- Ürün silmek → Delete

Bir öğrenci sisteminde:

- Öğrenci eklemek → Create
- Öğrenci bilgilerini görüntülemek → Read
- Öğrenci bilgilerini güncellemek → Update
- Öğrenci kaydını silmek → Delete

CRUD ile HTTP metotları şu şekilde eşleşir:

| CRUD | HTTP Metodu | Örnek Endpoint |
|---|---|---|
| Create | POST | `POST /products` |
| Read | GET | `GET /products` |
| Read | GET | `GET /products/5` |
| Update | PUT | `PUT /products/5` |
| Update | PATCH | `PATCH /products/5` |
| Delete | DELETE | `DELETE /products/5` |

Bu tablo API mantığını kavramak için çok önemlidir.

---

## 14. JSON Nedir?

JSON, API’lerde en yaygın kullanılan veri formatlarından biridir.JSON’un açılımı:

```text
JavaScript Object Notation
```

JSON ilk olarak JavaScript tarafındaki obje yazımına benzese de günümüzde sadece JavaScript’e özel değildir. Neredeyse tüm programlama dilleri JSON formatını destekler.Örneğin:

- JavaScript
- Python
- Java
- C#
- PHP
- Dart
- Go

gibi diller JSON ile çalışabilir.JSON’un amacı verileri düzenli, okunabilir ve taşınabilir bir formatta ifade etmektir.Basit bir JSON örneği:

```json
{
  "name": "Özge",
  "age": 23,
  "isStudent": true
}
```

Bu yapı anahtar-değer ilişkisiyle çalışır.Burada:

```text
"name"      → "Özge"
"age"       → 23
"isStudent" → true
```

şeklinde değerler vardır.API’lerde frontend ve backend arasında veri taşımak için genellikle JSON kullanılır.Örneğin frontend backend’e kullanıcı bilgisi gönderirken JSON kullanabilir:

```json
{
  "email": "ozge@example.com",
  "password": "123456"
}
```

Backend de cevap olarak JSON dönebilir:

```json
{
  "success": true,
  "message": "Login successful",
  "token": "abc123"
}
```

---

## 15. JSON Yapısı

JSON yapısı temel olarak iki ana yapıdan oluşur:

```text
Object
Array
```

---

### 15.1. JSON Object

JSON object, süslü parantez ile yazılır.Örnek:

```json
{
  "id": 1,
  "name": "Laptop",
  "price": 25000
}
```

Burada her alan bir key-value çiftidir.

```text
"id"    → 1
"name"  → "Laptop"
"price" → 25000
```

Object yapısı tek bir varlığı ifade etmek için kullanılır.Örneğin tek bir ürün:

```json
{
  "id": 1,
  "name": "Laptop",
  "price": 25000,
  "stock": 10
}
```

Tek bir kullanıcı:

```json
{
  "id": 7,
  "name": "Ayşe",
  "email": "ayse@example.com"
}
```

---

### 15.2. JSON Array

JSON array, köşeli parantez ile yazılır.Örnek:

```json
[
  "HTML",
  "CSS",
  "JavaScript"
]
```

Array birden fazla veriyi liste halinde tutar.Birden fazla ürün listelemek için array içinde object kullanılabilir:

```json
[
  {
    "id": 1,
    "name": "Laptop",
    "price": 25000
  },
  {
    "id": 2,
    "name": "Mouse",
    "price": 500
  },
  {
    "id": 3,
    "name": "Keyboard",
    "price": 900
  }
]
```

Bu yapı API response’larında çok sık görülür.Örneğin:

```http
GET /products
```

isteğine backend genellikle bir ürün listesi döner. Bu liste de array formatında olur.

---

### 15.3. İç İçe JSON Yapısı

JSON içinde object içinde object veya object içinde array olabilir.Örnek:

```json
{
  "id": 1,
  "name": "Özge",
  "address": {
    "city": "İstanbul",
    "district": "Kadıköy"
  },
  "skills": ["HTML", "CSS", "JavaScript"]
}
```

Burada:

```text
address → Object
skills  → Array
```

şeklindedir.Daha detaylı bir örnek:

```json
{
  "id": 10,
  "customerName": "Özge Keskin",
  "orderDate": "2026-05-20",
  "status": "preparing",
  "items": [
    {
      "productId": 1,
      "productName": "Laptop",
      "quantity": 1,
      "price": 25000
    },
    {
      "productId": 2,
      "productName": "Mouse",
      "quantity": 2,
      "price": 500
    }
  ],
  "shippingAddress": {
    "city": "İstanbul",
    "district": "Üsküdar",
    "postalCode": "34600"
  }
}
```

Bu örnekte bir sipariş bilgisi vardır. Siparişin içinde ürün listesi ve adres bilgisi bulunmaktadır.

---

### 15.4. JSON Veri Tipleri

JSON içinde kullanılan temel veri tipleri şunlardır:

| Veri Tipi | Açıklama | Örnek |
|---|---|---|
| String | Metinsel ifadeler | `"Özge"` |
| Number | Sayısal değerler | `23`, `1500`, `99.5` |
| Boolean | Doğru/yanlış değerleri | `true`, `false` |
| Array | Liste yapısı | `["HTML", "CSS"]` |
| Object | İç içe veri yapısı | `{ "city": "İstanbul" }` |
| Null | Boş değer | `null` |

Örnek:

```json
{
  "name": "Özge",
  "age": 23,
  "isStudent": true,
  "skills": ["HTML", "CSS", "JavaScript"],
  "address": {
    "city": "İstanbul",
    "district": "Kadıköy"
  },
  "profileImage": null
}
```

Bu JSON içinde farklı veri tipleri birlikte kullanılmıştır.

---

### 15.5. JSON Yazım Kuralları

JSON yazarken dikkat edilmesi gereken bazı kurallar vardır. Bu kurallara uyulmazsa JSON geçersiz olur ve API hata verebilir.

#### Key Değerleri Çift Tırnak İçinde Yazılır

Doğru kullanım:

```json
{
  "name": "Özge"
}
```

Yanlış kullanım:

```json
{
  name: "Özge"
}
```

JavaScript objelerinde key değeri bazen tırnaksız yazılabilir. Ancak JSON formatında key mutlaka çift tırnak içinde yazılmalıdır.

#### String Değerler Çift Tırnak İçinde Yazılır

Doğru kullanım:

```json
{
  "city": "İstanbul"
}
```

Yanlış kullanım:

```json
{
  "city": İstanbul
}
```

Metinsel değerler mutlaka çift tırnak içinde olmalıdır.

#### Son Elemandan Sonra Virgül Konmaz

Doğru kullanım:

```json
{
  "name": "Özge",
  "age": 23
}
```

Yanlış kullanım:

```json
{
  "name": "Özge",
  "age": 23,
}
```

Son elemandan sonra virgül koymak JSON’u geçersiz hale getirir.

#### Boolean Değerler Küçük Harfle Yazılır

Doğru kullanım:

```json
{
  "isActive": true
}
```

Yanlış kullanım:

```json
{
  "isActive": True
}
```

JSON’da boolean değerler `true` ve `false` şeklinde küçük harfle yazılır.

#### Null Küçük Harfle Yazılır

Doğru kullanım:

```json
{
  "profileImage": null
}
```

Yanlış kullanım:

```json
{
  "profileImage": Null
}
```

JSON’da boş değer `null` şeklinde yazılır.

---

## 16. Request ve Response Mantığı

API iletişiminin temelinde request ve response vardır.

```text
Request  → İstek
Response → Cevap
```

Client, server’a request gönderir. Server da bu request’i işleyip response döner.

---

### 16.1. Request Nelerden Oluşur?

Bir API request’i genellikle şu parçalardan oluşur:

```text
HTTP Method
URL / Endpoint
Headers
Body
Query Parameters
Path Parameters
```

Örnek request:

```http
POST /products
Content-Type: application/json
Authorization: Bearer token_value
```

Body:

```json
{
  "name": "Keyboard",
  "price": 900,
  "stock": 20
}
```

Bu request şu bilgileri taşır:

```text
POST          → Yeni veri oluşturulacak
/products     → Ürün kaynağına işlem yapılacak
Content-Type  → Gönderilen veri JSON formatında
Authorization → Kullanıcının token bilgisi
Body          → Oluşturulacak ürün bilgileri
```

---

### 16.2. Response Nelerden Oluşur?

Bir API response’u genellikle şu parçalardan oluşur:

```text
Status Code
Headers
Body
```

Örnek response:

```http
201 Created
Content-Type: application/json
```

Body:

```json
{
  "success": true,
  "message": "Product created successfully",
  "data": {
    "id": 3,
    "name": "Keyboard",
    "price": 900,
    "stock": 20
  }
}
```

Burada:

```text
201 Created → Ürün başarıyla oluşturuldu
success     → İşlem başarılı mı?
message     → Açıklama mesajı
data        → Oluşturulan ürün bilgisi
```

---

### 16.3. Header Nedir?

Header, request veya response hakkında ek bilgi taşıyan bölümdür.Header bilgileri kullanıcı tarafından doğrudan görülmez ama API iletişiminde çok önemlidir.Header içinde şu bilgiler yer alabilir:

- Gönderilen verinin formatı
- Kabul edilen response formatı
- Authorization token
- Dil bilgisi
- Cache bilgisi
- Tarayıcı bilgisi

En sık kullanılan headerlardan biri:

```http
Content-Type: application/json
```

Bu header şu anlama gelir:

```text
Gönderdiğim veri JSON formatında.
```

Bir diğer yaygın header:

```http
Authorization: Bearer token_value
```

Bu header kullanıcının kimlik doğrulama bilgisini taşır.Örneğin kullanıcı giriş yaptıktan sonra backend ona bir token verir. Sonraki isteklerde frontend bu token’ı Authorization header içinde gönderir.

```http
GET /profile
Authorization: Bearer abc123token
```

Bu şu anlama gelir:

```text
Ben giriş yapmış kullanıcıyım. İşte token bilgim.
```

Backend bu token’ı kontrol eder. Token geçerliyse işlem yapılır. Geçerli değilse `401 Unauthorized` cevabı dönebilir.

---

### 16.4. HTTP Status Code Mantığı

API response’larında sadece JSON body dönmez. Aynı zamanda HTTP status code da döner.Status code, yapılan isteğin sonucunu anlatır.Status code’lar genellikle şu gruplara ayrılır:

```text
2xx → Başarılı işlemler
3xx → Yönlendirme işlemleri
4xx → Client kaynaklı hatalar
5xx → Server kaynaklı hatalar
```

En sık kullanılan status code’lar şunlardır:

| Status Code | Anlamı | Açıklama |
|---|---|---|
| 200 OK | Başarılı | İstek başarıyla işlendi |
| 201 Created | Oluşturuldu | Yeni kayıt başarıyla oluşturuldu |
| 204 No Content | İçerik yok | İşlem başarılı ama body dönülmedi |
| 400 Bad Request | Hatalı istek | Gönderilen veri hatalı veya eksik |
| 401 Unauthorized | Yetkisiz | Kullanıcı giriş yapmamış veya token geçersiz |
| 403 Forbidden | Yasak | Kullanıcının bu işleme yetkisi yok |
| 404 Not Found | Bulunamadı | İstenen kayıt veya endpoint bulunamadı |
| 500 Internal Server Error | Sunucu hatası | Backend tarafında beklenmeyen hata oluştu |

Örnek:

Yeni ürün başarıyla oluşturulduğunda:

```http
201 Created
```

Ürün bulunamadığında:

```http
404 Not Found
```

Response body:

```json
{
  "success": false,
  "message": "Product not found"
}
```

Kullanıcı giriş yapmadan profile erişmeye çalışırsa:

```http
401 Unauthorized
```

Response body:

```json
{
  "success": false,
  "message": "Authentication required"
}
```

Yetkisi olmayan bir işlem yaparsa:

```http
403 Forbidden
```

Response body:

```json
{
  "success": false,
  "message": "You do not have permission to perform this action"
}
```

---

## 17. Endpoint Nedir?

Endpoint, API üzerinde belirli bir işlem yapmak için kullanılan URL yoludur.Örneğin:

```http
GET /products
```

Bu endpoint ürünleri listelemek için kullanılabilir.Başka örnekler:

```http
GET /products/5
POST /products
PUT /products/5
PATCH /products/5
DELETE /products/5
```

Her endpoint belirli bir amaca hizmet eder.Endpoint kavramını şöyle düşünebiliriz:

```text
API içindeki işlem noktası
```

Bir uygulama API’ye istek atarken aslında belirli bir endpoint’e istek atar.Örneğin:

```text
Ürünleri listelemek için       → GET /products
Tek ürün detayını almak için   → GET /products/5
Yeni ürün eklemek için         → POST /products
Ürün güncellemek için          → PUT /products/5
Ürün kısmi güncellemek için    → PATCH /products/5
Ürün silmek için               → DELETE /products/5
```

---

### 17.1. URL, Endpoint ve Route Farkı

Bu kavramlar bazen birbirine karıştırılır. Aralarında küçük ama önemli farklar vardır.

#### URL Nedir?

URL, bir kaynağın internet üzerindeki tam adresidir.Örnek:

```text
https://api.example.com/products
```

Burada:

```text
https://api.example.com → Domain / Base URL
/products               → Endpoint path
```

#### Endpoint Nedir?

Endpoint, API’nin belirli bir işlem için sunduğu yoldur.Örnek:

```http
GET /products
POST /products
GET /products/5
```

Endpoint, dışarıdan API’ye istek atan kişinin kullandığı işlem noktasıdır.

#### Route Nedir?

Route, backend kodunda bu endpoint’i karşılayan tanımdır.Örneğin Express.js içinde:

```js
app.get("/products", (req, res) => {
  res.send("Products");
});
```

Buradaki:

```js
"/products"
```

bir route’tur.

Kısaca:

```text
Endpoint → Dışarıdan görünen API noktası
Route    → Backend kodunda bu endpoint’i karşılayan yol
URL      → Endpoint’in tam internet adresi
```

Örnek:

```text
Tam URL:
https://api.example.com/products

Endpoint:
GET /products

Backend Route:
app.get("/products", ...)
```

---

### 17.2. Path Parameter ve Query Parameter

API tasarımında iki önemli parametre tipi vardır:

```text
Path Parameter
Query Parameter
```

#### Path Parameter Nedir?

Path parameter, URL yolunun bir parçası olan parametredir.Örnek:

```http
GET /products/5
```

Buradaki `5`, path parameter’dır.Bu genellikle bir kaynağın id değerini belirtmek için kullanılır.Backend tarafında bu yapı genellikle şöyle tanımlanır:

```text
/products/:id
```

Buradaki `:id`, değişken bir alan olduğunu gösterir.Örneğin:

```http
GET /products/5
GET /products/10
GET /products/25
```

Bu isteklerin hepsi aynı route’a gider ama farklı id değerleri taşır.Path parameter genellikle belirli bir kaynağa ulaşmak için kullanılır.Örnekler:

```http
GET /users/3
GET /orders/12
DELETE /comments/8
PUT /products/5
```

#### Query Parameter Nedir?

Query parameter, URL’de soru işaretinden sonra gelen parametrelerdir.Örnek:

```http
GET /products?category=electronics
```

Burada:

```text
category=electronics
```

query parameter’dır.Query parameter genellikle listeleme işlemlerinde filtreleme, arama, sıralama ve sayfalama için kullanılır.Örnekler:

```http
GET /products?search=laptop
GET /products?category=electronics
GET /products?page=1&limit=10
GET /products?sort=price
GET /products?minPrice=1000&maxPrice=5000
```

Birden fazla query parameter kullanmak için `&` işareti kullanılır.Örnek:

```http
GET /products?category=electronics&minPrice=1000&maxPrice=5000
```

Bu istek şu anlama gelir:

```text
Elektronik kategorisindeki, fiyatı 1000 ile 5000 arasında olan ürünleri getir.
```

#### Path Parameter ve Query Parameter Farkı

| Özellik | Path Parameter | Query Parameter |
|---|---|---|
| URL’deki yeri | Yolun parçasıdır | `?` işaretinden sonra gelir |
| Kullanım amacı | Belirli bir kaynağı seçmek | Listeyi filtrelemek/sıralamak |
| Örnek | `/products/5` | `/products?category=phone` |
| Genellikle ne taşır? | id | filtre, arama, sayfa, sıralama |

Kısaca:

```text
Path parameter  → Hangi kayıt?
Query parameter → Nasıl filtreleyeyim?
```

Örnek:

```http
GET /products/5
```

Anlamı:

```text
ID’si 5 olan ürünü getir.
```

Örnek:

```http
GET /products?category=phone
```

Anlamı:

```text
Telefon kategorisindeki ürünleri getir.
```

---

## 18. Basit Bir Endpoint Nasıl Tasarlanır?

Bir endpoint tasarlarken önce hangi kaynak üzerinde işlem yapılacağını belirlemek gerekir.Örneğin bir ürün yönetim sistemi düşünelim.Kaynak:

```text
products
```

Bu kaynak üzerinde yapılacak temel işlemler:

```text
Ürünleri listele
Tek ürün getir
Yeni ürün ekle
Ürün güncelle
Ürün sil
```

REST API tasarımına göre endpointler şöyle olabilir:

| İşlem | HTTP Metodu | Endpoint | Açıklama |
|---|---|---|---|
| Ürünleri listele | GET | `/products` | Tüm ürünleri getirir |
| Tek ürün getir | GET | `/products/:id` | ID’ye göre ürün getirir |
| Ürün ekle | POST | `/products` | Yeni ürün oluşturur |
| Ürün güncelle | PUT | `/products/:id` | ID’ye göre ürünü tamamen günceller |
| Ürün kısmi güncelle | PATCH | `/products/:id` | Belirli alanları günceller |
| Ürün sil | DELETE | `/products/:id` | ID’ye göre ürün siler |

Burada dikkat edilmesi gereken nokta şudur:
Endpoint isimleri genellikle isimdir. İşlem fiili HTTP metodu ile belirtilir.Yani:

```http
GET /products
```

yerine

```http
GET /getProducts
```

yazmaya gerek yoktur.Çünkü `GET` zaten getirme işlemini ifade eder.

---

## 19. Örnek Ürün API Tasarımı

Bu bölümde basit bir ürün API’si için endpointleri detaylı şekilde inceleyelim.

---

### 19.1. Ürünleri Listeleme

Endpoint:

```http
GET /products
```

Amaç:

```text
Sistemde kayıtlı tüm ürünleri listelemek.
```

Örnek response:

```json
{
  "success": true,
  "data": [
    {
      "id": 1,
      "name": "Laptop",
      "price": 25000,
      "stock": 10
    },
    {
      "id": 2,
      "name": "Mouse",
      "price": 500,
      "stock": 50
    }
  ]
}
```

Bu endpoint genellikle ürün listeleme sayfalarında kullanılır.

---

### 19.2. Tek Ürün Getirme

Endpoint:

```http
GET /products/1
```

Amaç:

```text
ID’si 1 olan ürünün detaylarını getirmek.
```

Örnek response:

```json
{
  "success": true,
  "data": {
    "id": 1,
    "name": "Laptop",
    "price": 25000,
    "stock": 10
  }
}
```

Eğer ürün bulunamazsa:

```http
404 Not Found
```

Response:

```json
{
  "success": false,
  "message": "Product not found"
}
```

---

### 19.3. Yeni Ürün Ekleme

Endpoint:

```http
POST /products
```

Amaç:

```text
Yeni bir ürün oluşturmak.
```

Request body:

```json
{
  "name": "Keyboard",
  "price": 900,
  "stock": 20
}
```

Başarılı response:

```http
201 Created
```

Body:

```json
{
  "success": true,
  "message": "Product created successfully",
  "data": {
    "id": 3,
    "name": "Keyboard",
    "price": 900,
    "stock": 20
  }
}
```

Burada `id` backend tarafından oluşturulmuştur.

---

### 19.4. Ürün Güncelleme

Endpoint:

```http
PUT /products/3
```

Amaç:

```text
ID’si 3 olan ürünü tamamen güncellemek.
```

Request body:

```json
{
  "name": "Mechanical Keyboard",
  "price": 1500,
  "stock": 15
}
```

Başarılı response:

```json
{
  "success": true,
  "message": "Product updated successfully",
  "data": {
    "id": 3,
    "name": "Mechanical Keyboard",
    "price": 1500,
    "stock": 15
  }
}
```

---

### 19.5. Ürün Kısmi Güncelleme

Endpoint:

```http
PATCH /products/3
```

Amaç:

```text
ID’si 3 olan ürünün sadece belirli alanlarını güncellemek.
```

Örneğin sadece stok değiştirilecekse:

Request body:

```json
{
  "stock": 35
}
```

Bu request şu anlama gelir:

```text
ID’si 3 olan ürünün sadece stock alanını 35 yap.
```

Başarılı response:

```json
{
  "success": true,
  "message": "Product updated successfully",
  "data": {
    "id": 3,
    "name": "Mechanical Keyboard",
    "price": 1500,
    "stock": 35
  }
}
```

---

### 19.6. Ürün Silme

Endpoint:

```http
DELETE /products/3
```

Amaç:

```text
ID’si 3 olan ürünü silmek.
```

Başarılı response:

```json
{
  "success": true,
  "message": "Product deleted successfully"
}
```

Alternatif olarak sadece şu status code dönebilir:

```http
204 No Content
```

---

## 20. API Testi Nasıl Yapılır?

API’leri test etmek için genellikle şu araçlar kullanılabilir:

- Postman
- Insomnia
- Swagger
- Tarayıcı geliştirici araçları
- Terminal üzerinden curl komutları

---

### 20.1. Postman ile API Testi

Postman, API isteklerini test etmek için kullanılan popüler bir araçtır.Postman ile şunlar yapılabilir:

- GET isteği atılabilir.
- POST isteği atılıp body gönderilebilir.
- Header bilgileri eklenebilir.
- Token ile yetkili istek yapılabilir.
- Response body incelenebilir.
- Status code kontrol edilebilir.
- API hataları analiz edilebilir.

Örneğin yeni ürün eklemek için Postman’de şu ayarlar yapılabilir:

```text
Method: POST
URL: http://localhost:3000/products
Headers:
Content-Type: application/json
```

Body:

```json
{
  "name": "Keyboard",
  "price": 900,
  "stock": 20
}
```

Daha sonra Send butonuna basılır. Backend’den gelen response incelenir.

---

### 20.2. Tarayıcı Üzerinden GET İstekleri

GET istekleri tarayıcı üzerinden de denenebilir.Örneğin:

```text
http://localhost:3000/products
```

adresine gidildiğinde backend JSON response dönebilir.Ancak POST, PUT, PATCH ve DELETE gibi istekler için genellikle Postman, Swagger veya frontend kodu kullanılır.

---

### 20.3. Network Paneli ile API İnceleme

Tarayıcı geliştirici araçlarında Network sekmesi kullanılarak API istekleri incelenebilir.Network panelinde şunlar görülebilir:

- Hangi endpoint’e istek atıldığı
- Hangi HTTP metodunun kullanıldığı
- Request headers
- Request payload/body
- Response
- Status code
- İstek süresi
- Hata mesajları

Özellikle frontend-backend entegrasyonlarında Network paneli çok önemlidir.Bir butona basıldığında gerçekten API isteği gidiyor mu, hangi endpoint’e gidiyor, hangi body gönderiliyor ve backend ne cevap veriyor gibi sorular Network paneliyle anlaşılır.

---

## 21. Kazanım

Bu konunun temel kazanımı backend öğrenmenin ana kapısını açmasıdır.API mantığını anlayan bir kişi şunları daha kolay kavrar:

- Frontend ve backend nasıl haberleşir?
- Bir butona basınca arkada ne olur?
- JSON neden kullanılır?
- GET ve POST farkı nedir?
- PUT ve PATCH farkı nedir?
- DELETE ne zaman kullanılır?
- Endpoint nasıl tasarlanır?
- Request ve response nasıl çalışır?
- Backend neden gereklidir?
- Veritabanı neden doğrudan frontend’e bağlanmaz?
- API testleri nasıl yapılır?
- Network panelinde görülen istekler ne anlama gelir?

API mantığı backend öğrenmenin temel kapısıdır. Çünkü backend geliştirme sürecinde yapılan işlemlerin büyük çoğunluğu API endpointleri oluşturmak, bu endpointlere gelen requestleri işlemek ve doğru response döndürmek üzerine kuruludur.

---

## 22. Genel Özet

API, farklı yazılımların birbirleriyle iletişim kurmasını sağlayan bir yapıdır. Web uygulamalarında genellikle frontend ve backend arasındaki veri alışverişi API üzerinden yapılır.

Frontend kullanıcı arayüzünü oluşturur. Backend verileri işler, veritabanı ile iletişim kurar ve iş kurallarını uygular. API ise bu iki taraf arasında köprü görevi görür.

REST, API tasarlamak için kullanılan yaygın bir mimari yaklaşımdır. REST mantığında sistemdeki veriler kaynak olarak düşünülür. Bu kaynaklara URL’ler üzerinden erişilir ve işlemler HTTP metotlarıyla yapılır.

Temel HTTP metotları şunlardır:

```text
GET    → Veri getirir
POST   → Yeni veri oluşturur
PUT    → Var olan veriyi tamamen günceller
PATCH  → Var olan verinin belirli alanlarını günceller
DELETE → Veri siler
```

JSON, frontend ve backend arasında veri taşımak için yaygın olarak kullanılan formattır. JSON, anahtar-değer mantığıyla çalışır ve object ile array yapıları üzerine kuruludur.

Örnek JSON:

```json
{
  "id": 1,
  "name": "Laptop",
  "price": 25000
}
```

Endpoint, API’de belirli bir işlem yapmak için kullanılan URL yoludur.

Örnek endpointler:

```http
GET /products
GET /products/5
POST /products
PUT /products/5
PATCH /products/5
DELETE /products/5
```

Basit bir REST API tasarımında kaynak isimleri anlaşılır olmalı, HTTP metotları doğru kullanılmalı, response yapısı tutarlı olmalı ve doğru status code dönülmelidir.

Bu konu, backend geliştirme sürecinin temelidir. API mantığını anlamak; web uygulamalarının nasıl çalıştığını, frontend ile backend’in nasıl haberleştiğini ve verilerin sistem içinde nasıl taşındığını anlamak için kritik öneme sahiptir.