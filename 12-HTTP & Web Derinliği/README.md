# 14. Hafta Raporu: HTTP ve Web Derinliği

## İçindekiler

1. [Giriş](#giris)
2. [Web Uygulamalarında İletişimin Genel Yapısı](#web-uygulamalarinda-iletisimin-genel-yapisi)
3. [HTTP Nedir?](#http-nedir)
   - [HTTP'nin Temel Özellikleri](#httpnin-temel-ozellikleri)
   - [İstemci ve Sunucu Kavramları](#istemci-ve-sunucu-kavramlari)
   - [Kaynak ve Temsil Kavramları](#kaynak-ve-temsil-kavramlari)
4. [Bir HTTP İsteğinin Yaşam Döngüsü](#bir-http-isteginin-yasam-dongusu)
5. [URL ve URI Yapısı](#url-ve-uri-yapisi)
   - [URL Bölümleri](#url-bolumleri)
   - [Path Parameter ve Query Parameter](#path-parameter-ve-query-parameter)
6. [HTTP Request Yapısı](#http-request-yapisi)
   - [Request Line](#request-line)
   - [HTTP Metotları](#http-metotlari)
   - [Request Headers](#request-headers)
   - [Boş Satır](#bos-satir)
   - [Request Body](#request-body)
   - [Tam Bir Request Örneği](#tam-bir-request-ornegi)
7. [HTTP Metotları Derinlemesine](#http-metotlari-derinlemesine)
   - [GET](#get)
   - [POST](#post)
   - [PUT](#put)
   - [PATCH](#patch)
   - [DELETE](#delete)
   - [HEAD](#head)
   - [OPTIONS](#options)
   - [TRACE](#trace)
   - [CONNECT](#connect)
   - [QUERY](#query)
   - [Safe ve Idempotent Metotlar](#safe-ve-idempotent-metotlar)
8. [HTTP Response Yapısı](#http-response-yapisi)
   - [Status Line](#status-line)
   - [Response Headers](#response-headers)
   - [Response Body](#response-body)
   - [Tam Bir Response Örneği](#tam-bir-response-ornegi)
9. [HTTP Status Code'ları](#http-status-codelari)
   - [1xx Bilgilendirme Kodları](#1xx-bilgilendirme-kodlari)
   - [2xx Başarı Kodları](#2xx-basari-kodlari)
   - [3xx Yönlendirme Kodları](#3xx-yonlendirme-kodlari)
   - [4xx İstemci Hata Kodları](#4xx-istemci-hata-kodlari)
   - [5xx Sunucu Hata Kodları](#5xx-sunucu-hata-kodlari)
   - [Sık Karıştırılan Status Code'lar](#sik-karistirilan-status-codelar)
10. [HTTP Header'ları Derinlemesine](#http-headerlari-derinlemesine)
    - [Genel Header'lar](#genel-headerlar)
    - [İçerik Header'ları](#icerik-headerlari)
    - [Kimlik Doğrulama Header'ları](#kimlik-dogrulama-headerlari)
    - [Cache Header'ları](#cache-headerlari)
    - [CORS Header'ları](#cors-headerlari)
    - [Güvenlik Header'ları](#guvenlik-headerlari)
11. [HTTP Body ve Veri Formatları](#http-body-ve-veri-formatlari)
    - [JSON](#json)
    - [Form URL Encoded](#form-url-encoded)
    - [Multipart Form Data](#multipart-form-data)
    - [Text, HTML, XML ve Binary İçerikler](#text-html-xml-ve-binary-icerikler)
12. [Content-Type ve Accept Farkı](#content-type-ve-accept-farki)
13. [Stateless Yapı, Cookie ve Session](#stateless-yapi-cookie-ve-session)
    - [Cookie](#cookie)
    - [Session](#session)
    - [Token Tabanlı Kimlik Doğrulama](#token-tabanli-kimlik-dogrulama)
14. [CORS Nedir?](#cors-nedir)
    - [Same-Origin Policy](#same-origin-policy)
    - [Origin Nedir?](#origin-nedir)
    - [Cross-Origin İstek Nedir?](#cross-origin-istek-nedir)
    - [Basit CORS İstekleri](#basit-cors-istekleri)
    - [Preflight İstekleri](#preflight-istekleri)
    - [CORS Response Header'ları](#cors-response-headerlari)
    - [Credentials Kullanımı](#credentials-kullanimi)
    - [CORS Hataları ve Çözümleri](#cors-hatalari-ve-cozumleri)
    - [no-cors Yanılgısı](#no-cors-yanilgisi)
    - [CORS Bir Güvenlik Mekanizması mıdır?](#cors-bir-guvenlik-mekanizmasi-midir)
15. [CORS, CSRF ve Authentication Arasındaki Fark](#cors-csrf-ve-authentication-arasindaki-fark)
16. [HTTPS ve TLS](#https-ve-tls)
17. [HTTP Sürümleri](#http-surumleri)
    - [HTTP/1.0](#http10)
    - [HTTP/1.1](#http11)
    - [HTTP/2](#http2)
    - [HTTP/3](#http3)
18. [HTTP Cache Mekanizması](#http-cache-mekanizmasi)
    - [Freshness ve Validation](#freshness-ve-validation)
    - [Cache-Control Direktifleri](#cache-control-direktifleri)
    - [ETag ve If-None-Match](#etag-ve-if-none-match)
    - [Last-Modified ve If-Modified-Since](#last-modified-ve-if-modified-since)
19. [Content Negotiation ve Compression](#content-negotiation-ve-compression)
20. [Frontend–Backend İletişim Örnekleri](#frontend-backend-iletisim-ornekleri)
    - [GET İsteği](#get-istegi-ornegi)
    - [POST İsteği](#post-istegi-ornegi)
    - [Login Akışı](#login-akisi)
    - [Dosya Yükleme](#dosya-yukleme)
21. [REST API Tasarımında HTTP Kullanımı](#rest-api-tasariminda-http-kullanimi)
22. [Hata Yönetimi ve Standart API Cevabı](#hata-yonetimi-ve-standart-api-cevabi)
23. [Tarayıcı DevTools ile HTTP İnceleme](#tarayici-devtools-ile-http-inceleme)
24. [HTTP Güvenliği Açısından Temel Noktalar](#http-guvenligi-acisindan-temel-noktalar)
25. [Sık Yapılan Hatalar](#sik-yapilan-hatalar)
26. [Mülakat Soruları ve Kısa Cevaplar](#mulakat-sorulari-ve-kisa-cevaplar)
27. [Genel Sonuç](#genel-sonuc)
28. [Kaynakça](#kaynakca)

---

<a id="giris"></a>
## 1. Giriş

Modern web uygulamalarında kullanıcı arayüzü ile sunucu tarafı birbirinden ayrı katmanlar halinde çalışır. Kullanıcı bir butona bastığında, giriş formunu gönderdiğinde, ürün listesini açtığında veya bir dosya yüklediğinde arka planda çoğunlukla bir **HTTP isteği** oluşturulur. Bu istek ağ üzerinden backend sunucusuna gider. Backend isteği işler, veri tabanına erişebilir, çeşitli kontroller yapabilir ve sonucunda bir **HTTP cevabı** döndürür. Bu nedenle HTTP yalnızca tarayıcıya web sayfası getiren basit bir protokol değildir. HTTP;

- frontend ile backend arasındaki temel iletişim dilidir,
- web API'lerinin çalışma temelini oluşturur,
- istemci ile sunucu arasında veri, komut ve hata bilgisinin taşınmasını sağlar,
- kimlik doğrulama, yetkilendirme, önbellekleme, yönlendirme ve içerik anlaşması gibi süreçlerde kullanılır,
- tarayıcı güvenlik mekanizmalarıyla birlikte çalışır,
- mobil uygulamalar, masaüstü uygulamaları, mikroservisler ve IoT sistemlerinde de yaygın olarak kullanılır.

HTTP'yi anlamadan yalnızca `fetch()` veya Axios kullanmayı öğrenmek mümkündür; ancak bu durumda geliştirici çoğu hatayı ezbere çözmeye çalışır. HTTP yapısı kavrandığında ise `400`, `401`, `403`, `404`, `409`, `422`, `500`, CORS, cookie, token, cache ve proxy gibi konular anlamlı bir bütün hâline gelir.

---

<a id="web-uygulamalarinda-iletisimin-genel-yapisi"></a>
## 2. Web Uygulamalarında İletişimin Genel Yapısı

Bir web uygulamasının temel iletişim modeli şu şekilde gösterilebilir:

```text
Kullanıcı
   ↓
Frontend / Tarayıcı
   ↓ HTTP Request
İnternet / Ağ / Proxy / Load Balancer
   ↓
Backend Sunucusu
   ↓
Veri Tabanı veya Başka Servisler
   ↑
Backend Sunucusu
   ↑ HTTP Response
Frontend / Tarayıcı
   ↑
Kullanıcıya Güncellenmiş Arayüz
```

Örneğin bir kullanıcı e-ticaret sitesinde ürünleri görüntülemek istediğinde şu süreç gerçekleşebilir:

1. React uygulaması `GET /api/products` isteği gönderir.
2. Tarayıcı URL, method ve header bilgilerini kullanarak HTTP isteğini oluşturur.
3. İstek DNS çözümleme, TCP veya QUIC bağlantısı ve gerekiyorsa TLS sürecinden geçer.
4. Web sunucusu veya reverse proxy isteği karşılar.
5. Backend ilgili endpoint'i çalıştırır.
6. Backend veri tabanından ürünleri okur.
7. Ürünler JSON formatına dönüştürülür.
8. Sunucu `200 OK` durum koduyla JSON cevabı gönderir.
9. Frontend JSON verisini işler ve ekranda ürün kartlarını oluşturur.

Burada frontend ve backend birbirinin iç yapısını bilmek zorunda değildir. İki tarafın aynı **API sözleşmesine** uyması yeterlidir. Bu sözleşme genellikle aşağıdaki bilgileri belirler:

- Endpoint adresi
- HTTP metodu
- Gönderilecek header'lar
- Request body yapısı
- Başarılı cevap formatı
- Hata cevap formatı
- Kullanılabilecek status code'lar
- Kimlik doğrulama yöntemi

Örneğin:

```text
Endpoint: POST /api/users
Amaç: Yeni kullanıcı oluşturmak
Request Content-Type: application/json
Başarılı cevap: 201 Created
Hatalı veri: 400 Bad Request veya 422 Unprocessable Content
E-posta zaten kayıtlı: 409 Conflict
```

---

<a id="http-nedir"></a>
## 3. HTTP Nedir?

**HTTP**, “Hypertext Transfer Protocol” ifadesinin kısaltmasıdır. Türkçeye “Hiper Metin Aktarım Protokolü” olarak çevrilebilir. HTTP, istemciler ile sunucular arasında kaynakların istenmesi ve cevapların iletilmesi için kullanılan uygulama katmanı protokolüdür. HTTP'nin temel çalışma biçimi **request–response**, yani **istek–cevap** modelidir:

```text
Client  ─── HTTP Request ───>  Server
Client  <── HTTP Response ───  Server
```

İstemci bir kaynağı ister veya bir işlem talep eder. Sunucu bu isteği değerlendirir ve bir cevap üretir.

<a id="httpnin-temel-ozellikleri"></a>
### 3.1. HTTP'nin Temel Özellikleri

#### İstemci–sunucu mimarisine dayanır

İstemci isteği başlatan taraftır. Sunucu ise isteği dinler, işler ve cevaplar.

#### Stateless yapıdadır

HTTP'nin temelinde her istek bağımsızdır. Sunucu, önceki isteği yalnızca HTTP protokolü nedeniyle otomatik olarak hatırlamaz. Kullanıcı oturumu gibi durumlar cookie, session veya token gibi ek mekanizmalarla yönetilir.

#### Genişletilebilir bir protokoldür

HTTP header'ları kullanılarak kimlik doğrulama, cache, içerik türü, sıkıştırma, CORS ve güvenlik gibi birçok davranış belirtilebilir.

#### Kaynak odaklıdır

HTTP ile erişilen her şey bir kaynak olarak düşünülebilir:

- HTML sayfası
- JSON verisi
- Görsel
- Video
- PDF dosyası
- Kullanıcı kaydı
- Ürün kaydı
- Rapor
- API sonucu

#### Metot ve durum kodu semantiğine sahiptir

İstemci ne yapmak istediğini HTTP metodu ile, sunucu ise işlemin sonucunu status code ile ifade eder.

<a id="istemci-ve-sunucu-kavramlari"></a>
### 3.2. İstemci ve Sunucu Kavramları

**İstemci**, HTTP isteğini başlatan yazılımdır. Örnekler:

- Chrome, Firefox, Edge gibi tarayıcılar
- React, Vue veya Angular uygulaması
- Flutter mobil uygulaması
- Postman
- `curl`
- Başka bir backend servisi

**Sunucu**, HTTP isteklerini dinleyen ve cevap üreten taraftır. Örnek teknolojiler:

- Node.js / Express
- ASP.NET Core
- Spring Boot
- Django
- Flask
- Laravel
- Nginx
- Apache HTTP Server

Bir uygulama bazı işlemlerde istemci, bazı işlemlerde sunucu olabilir. Örneğin bir backend, ödeme servisine istek gönderdiğinde ödeme servisine göre istemci konumundadır.

<a id="kaynak-ve-temsil-kavramlari"></a>
### 3.3. Kaynak ve Temsil Kavramları

HTTP'de **resource**, erişilmek istenen mantıksal varlıktır. **Representation** ise bu kaynağın ağ üzerinden gönderilen gösterimidir. Örneğin `/api/users/15` adresi 15 numaralı kullanıcı kaynağını ifade edebilir. Bu kaynağın temsili JSON olabilir:

```json
{
  "id": 15,
  "name": "Özge Keskin",
  "role": "developer"
}
```

Aynı kaynak farklı temsil biçimlerinde gönderilebilir:

- JSON
- XML
- HTML
- PDF
- CSV

İstemci hangi formatı kabul ettiğini `Accept` header'ıyla bildirebilir. Sunucu gönderdiği formatı `Content-Type` header'ıyla açıklar.

---

<a id="bir-http-isteginin-yasam-dongusu"></a>
## 4. Bir HTTP İsteğinin Yaşam Döngüsü

Kullanıcının tarayıcıya bir adres yazmasıyla sunucudan cevap alınması arasında birçok adım gerçekleşir.

### 4.1. URL'nin yorumlanması

Tarayıcı URL içindeki protokolü, domain'i, portu, path'i ve query parametrelerini ayırır.

```text
https://api.example.com:443/products/12?currency=TRY
```

### 4.2. DNS çözümleme

Tarayıcı `api.example.com` domain adının hangi IP adresine karşılık geldiğini DNS sistemi üzerinden öğrenir.

### 4.3. Bağlantı kurulması

- HTTP/1.1 ve HTTP/2 çoğunlukla TCP kullanır.
- HTTPS kullanılıyorsa TCP sonrasında TLS bağlantısı kurulur.
- HTTP/3, TCP yerine QUIC kullanır ve TLS güvenliğini QUIC içine entegre eder.

### 4.4. HTTP isteğinin hazırlanması

Tarayıcı veya uygulama aşağıdaki bilgileri oluşturur:

- HTTP metodu
- Hedef URL
- Header'lar
- Gerekliyse request body

### 4.5. İsteğin ara sistemlerden geçmesi

İstek doğrudan uygulama sunucusuna gitmeyebilir. Şu bileşenlerden geçebilir:

- CDN
- Reverse proxy
- API gateway
- Load balancer
- Web Application Firewall
- Kurumsal proxy

### 4.6. Backend işlemleri

Backend isteği route ile eşleştirir, middleware'leri çalıştırır ve iş mantığını uygular. Örnek süreç:

1. CORS kontrolü
2. Loglama
3. Authentication kontrolü
4. Authorization kontrolü
5. Request doğrulama
6. Controller işlemi
7. Service katmanı
8. Veri tabanı işlemi
9. Response oluşturma

### 4.7. HTTP cevabının gönderilmesi

Sunucu status code, response header'ları ve varsa response body gönderir.

### 4.8. Tarayıcının cevabı işlemesi

Frontend:

- status code'u kontrol eder,
- JSON veya diğer body formatını okur,
- başarılı sonucu ekrana yansıtır,
- hata durumunda kullanıcıya mesaj gösterir,
- gerekiyorsa token veya cookie işlemlerini yapar.

---

<a id="url-ve-uri-yapisi"></a>
## 5. URL ve URI Yapısı

**URI**, bir kaynağı tanımlayan genel ifadedir. **URL** ise kaynağın nerede bulunduğunu ve ona nasıl erişileceğini belirten URI türüdür. Günlük web geliştirmede çoğunlukla URL terimi kullanılır.

<a id="url-bolumleri"></a>
### 5.1. URL Bölümleri

Aşağıdaki URL'yi inceleyelim:

```text
https://user:password@api.example.com:8443/products/42/reviews?sort=desc&page=2#comments
```

| Bölüm | Örnek | Açıklama |
|---|---|---|
| Scheme | `https` | Kullanılan protokol |
| User info | `user:password` | URL içinde kimlik bilgisi; modern uygulamalarda önerilmez |
| Host | `api.example.com` | Sunucunun domain adı |
| Port | `8443` | Sunucunun dinlediği port |
| Path | `/products/42/reviews` | Sunucudaki kaynak yolu |
| Query string | `sort=desc&page=2` | Filtre, sıralama veya sayfalama parametreleri |
| Fragment | `comments` | Genellikle tarayıcı tarafında sayfa içi konumu belirtir; HTTP isteğinde sunucuya gönderilmez |

Varsayılan portlar:

- HTTP: `80`
- HTTPS: `443`

Port varsayılan olduğunda URL içinde yazılması gerekmez.

<a id="path-parameter-ve-query-parameter"></a>
### 5.2. Path Parameter ve Query Parameter

#### Path parameter

Kaynağın kimliğini veya hiyerarşik konumunu belirtir:

```http
GET /api/users/15
```

Burada `15`, kullanıcı kimliğidir.

```http
GET /api/users/15/orders/28
```

Burada 15 numaralı kullanıcının 28 numaralı siparişi hedeflenir.

#### Query parameter

Filtreleme, sıralama, arama, sayfalama veya isteğe bağlı davranışlar için kullanılır:

```http
GET /api/products?category=computer&page=2&pageSize=20&sort=price
```

Query parametreleri URL'de görünür. Bu nedenle parola, access token, kredi kartı bilgisi veya özel veri query string içine konulmamalıdır. URL'ler tarayıcı geçmişinde, sunucu loglarında, proxy kayıtlarında ve analiz sistemlerinde saklanabilir.

#### Encoding

URL içinde boşluk, Türkçe karakter ve özel karakterler uygun biçimde kodlanmalıdır.

```text
Özge Keskin
```

URL encoded hâli yaklaşık olarak şu şekilde görülebilir:

```text
%C3%96zge%20Keskin
```

JavaScript'te:

```javascript
const value = encodeURIComponent("Özge Keskin");
```

---

<a id="http-request-yapisi"></a>
## 6. HTTP Request Yapısı

HTTP request, istemcinin sunucuya gönderdiği mesajdır. HTTP/1.1 açısından bir request genel olarak şu bölümlerden oluşur:

```text
Request Line
Headers
Boş Satır
Opsiyonel Request Body
```

Örnek:

```http
POST /api/users HTTP/1.1
Host: example.com
Content-Type: application/json
Accept: application/json
Authorization: Bearer eyJhbGciOi...
Content-Length: 67

{
  "name": "Özge Keskin",
  "email": "ozge@example.com"
}
```

<a id="request-line"></a>
### 6.1. Request Line

Request line üç temel parçadan oluşur:

```text
METHOD REQUEST-TARGET HTTP-VERSION
```

Örnek:

```http
GET /api/products?page=1 HTTP/1.1
```

- `GET`: HTTP metodu
- `/api/products?page=1`: hedef kaynak
- `HTTP/1.1`: kullanılan HTTP sürümü

HTTP/2 ve HTTP/3 ağ üzerinde farklı binary framing mekanizmaları kullanır. Ancak geliştiricinin gördüğü mantıksal semantik yine method, URL, header ve body kavramlarından oluşur.

<a id="http-metotlari"></a>
### 6.2. HTTP Metotları

HTTP method, istemcinin hedef kaynak üzerinde gerçekleştirmek istediği işlemi açıklar. En sık kullanılan metotlar:

| Method | Temel amaç |
|---|---|
| `GET` | Kaynak okumak |
| `POST` | Yeni işlem veya kaynak oluşturmak |
| `PUT` | Kaynağı tamamen oluşturmak ya da değiştirmek |
| `PATCH` | Kaynağın belirli alanlarını güncellemek |
| `DELETE` | Kaynağı silmek |
| `HEAD` | Body olmadan yalnızca response metadata almak |
| `OPTIONS` | Desteklenen iletişim seçeneklerini öğrenmek |

<a id="request-headers"></a>
### 6.3. Request Headers

Header'lar, istekle ilgili ek bilgileri taşır. Header adı ve değeri iki nokta ile ayrılır:

```http
Header-Name: Header Value
```

Yaygın request header'ları:

#### Host

Hedef sunucuyu belirtir:

```http
Host: api.example.com
```

Aynı IP adresinde birden fazla domain çalışabileceği için önemlidir.

#### Accept

İstemcinin kabul ettiği response formatlarını belirtir:

```http
Accept: application/json
```

#### Content-Type

Request body içeriğinin formatını belirtir:

```http
Content-Type: application/json
```

#### Authorization

Kimlik doğrulama bilgisini taşır:

```http
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
```

#### Cookie

Domain'e ait cookie'leri sunucuya gönderir:

```http
Cookie: sessionId=abc123; theme=dark
```

#### User-Agent

İstemci yazılımı hakkında bilgi verir:

```http
User-Agent: Mozilla/5.0 ...
```

#### Origin

İsteği başlatan origin'i belirtir. CORS kontrollerinde kullanılır:

```http
Origin: https://frontend.example.com
```

#### Referer

İsteğin hangi sayfadan başlatıldığı hakkında bilgi verebilir:

```http
Referer: https://frontend.example.com/products
```

HTTP standardındaki tarihsel yazım nedeniyle header adı `Referer` şeklindedir; doğru İngilizce kelime “referrer” olsa da protokol header'ı bu şekilde kalmıştır.

#### Accept-Encoding

İstemcinin desteklediği sıkıştırma yöntemlerini belirtir:

```http
Accept-Encoding: gzip, br
```

#### If-None-Match

Cache doğrulaması için ETag değerini gönderir:

```http
If-None-Match: "product-list-v18"
```

<a id="bos-satir"></a>
### 6.4. Boş Satır

HTTP/1.1 mesajında header bölümünün bittiğini bir boş satır belirtir. Bu satırdan sonra body başlayabilir.

```http
Content-Type: application/json
Content-Length: 18

{"name":"Özge"}
```

Header ile body arasındaki ayrımın doğru yapılması mesajın doğru parse edilmesi açısından kritiktir.

<a id="request-body"></a>
### 6.5. Request Body

Request body, sunucuya gönderilen asıl veriyi taşır. Her istekte body bulunmak zorunda değildir. Body yaygın olarak şu metotlarla gönderilir:

- POST
- PUT
- PATCH
- QUERY

GET isteklerinde body kullanımı birçok istemci, proxy, cache ve framework tarafından beklenmediği için uygulama API'lerinde genellikle tercih edilmez. JSON request body örneği:

```json
{
  "title": "HTTP Raporu",
  "completed": false
}
```

Dosya yükleme için `multipart/form-data`, klasik HTML formları için `application/x-www-form-urlencoded` kullanılabilir.

<a id="tam-bir-request-ornegi"></a>
### 6.6. Tam Bir Request Örneği

```http
POST /api/auth/login HTTP/1.1
Host: api.example.com
Accept: application/json
Content-Type: application/json
Origin: https://app.example.com
User-Agent: Mozilla/5.0
Content-Length: 62

{
  "email": "ozge@example.com",
  "password": "example-password"
}
```

Bu isteğin anlamı:

- İstemci `/api/auth/login` endpoint'ine istek gönderiyor.
- Method `POST`, çünkü sunucuda bir login işlemi başlatılıyor.
- Body JSON formatında.
- İstemci JSON cevap bekliyor.
- İstek `https://app.example.com` origin'inden başlatılmış.

---

<a id="http-metotlari-derinlemesine"></a>
## 7. HTTP Metotları Derinlemesine

HTTP metotlarını yalnızca CRUD eşleştirmesi olarak ezberlemek yeterli değildir. Her metodun **semantiği**, **güvenli olup olmadığı**, **idempotent olup olmadığı** ve **cache davranışı** önemlidir.

<a id="get"></a>
### 7.1. GET

GET, hedef kaynağın mevcut temsilini almak için kullanılır.

```http
GET /api/products/42 HTTP/1.1
```

Özellikleri:

- Veri okumak için kullanılır.
- Sunucu durumunu değiştirmesi beklenmez.
- Safe metottur.
- Idempotent metottur.
- Uygun cache header'larıyla cache edilebilir.
- Parametreler çoğunlukla path veya query string üzerinden gönderilir.

Doğru kullanım:

```http
GET /api/orders?status=completed&page=1
```

Yanlış tasarım örneği:

```http
GET /api/users/15/delete
```

GET ile silme işlemi yapılmamalıdır. Tarayıcı ön yükleme, crawler, cache veya link önizleme sistemi bu URL'yi istemeden çağırabilir.

<a id="post"></a>
### 7.2. POST

POST, hedef kaynağın istekteki içeriği kendi kurallarına göre işlemesini ister. Genellikle yeni kaynak oluşturmak veya bir işlem başlatmak için kullanılır.

```http
POST /api/users HTTP/1.1
Content-Type: application/json

{
  "name": "Özge"
}
```

Yaygın kullanım alanları:

- Yeni kullanıcı oluşturma
- Sipariş oluşturma
- Login işlemi
- Ödeme başlatma
- Dosya yükleme
- Arama veya raporlama işlemi başlatma
- E-posta gönderme

POST varsayılan olarak idempotent değildir. Aynı istek iki kez gönderildiğinde iki farklı kayıt oluşturulabilir. Örneğin:

```http
POST /api/orders
```

Aynı body iki kez gönderilirse iki sipariş oluşabilir. Ödeme ve sipariş API'lerinde tekrarları önlemek için `Idempotency-Key` gibi uygulama seviyesinde çözümler kullanılabilir. Başarılı kaynak oluşturma cevabı genellikle:

```http
HTTP/1.1 201 Created
Location: /api/users/124
```

<a id="put"></a>
### 7.3. PUT

PUT, hedef kaynağın temsilini request body ile oluşturmak veya tamamen değiştirmek için kullanılır.

```http
PUT /api/users/15 HTTP/1.1
Content-Type: application/json

{
  "name": "Özge Keskin",
  "email": "ozge@example.com",
  "role": "developer"
}
```

PUT idempotent kabul edilir. Aynı PUT isteği birden fazla kez gönderildiğinde ortaya çıkan nihai durum aynı olmalıdır. PUT çoğunlukla kaynağın tamamının temsilini gönderme anlamında kullanılır. Ancak gerçek projelerde framework ve API sözleşmelerine göre davranış değişebilir. API dokümantasyonu açık olmalıdır.

<a id="patch"></a>
### 7.4. PATCH

PATCH, kaynağın belirli bölümlerini güncellemek için kullanılır.

```http
PATCH /api/users/15 HTTP/1.1
Content-Type: application/json

{
  "email": "new-email@example.com"
}
```

Bu istekte yalnızca e-posta alanı değiştirilmektedir. PUT ve PATCH farkı özetle:

| PUT | PATCH |
|---|---|
| Genellikle kaynağın bütün temsilini gönderir | Yalnızca değişecek alanları gönderir |
| Idempotent olacak şekilde tanımlanmıştır | Kullanılan patch formatına ve işleme göre idempotent olabilir veya olmayabilir |
| Eksik alanların silinmesi veya varsayılana dönmesi mümkün olabilir | Gönderilmeyen alanlar genellikle değişmeden kalır |

PATCH body için farklı formatlar kullanılabilir:

- Basit partial JSON
- JSON Merge Patch
- JSON Patch

JSON Patch örneği:

```json
[
  {
    "op": "replace",
    "path": "/email",
    "value": "new-email@example.com"
  }
]
```

<a id="delete"></a>
### 7.5. DELETE

DELETE hedef kaynağın silinmesini ister.

```http
DELETE /api/users/15 HTTP/1.1
```

Başarılı cevap seçenekleri:

```http
204 No Content
```

veya silinen kayıtla ilgili bilgi dönülecekse:

```http
200 OK
Content-Type: application/json

{
  "message": "Kullanıcı silindi."
}
```

DELETE idempotent kabul edilir. İlk istek kaynağı siler. İkinci istek `404 Not Found` dönebilir; ancak sunucunun nihai durumu yine kaynağın bulunmaması olduğu için işlem semantiği idempotenttir. Soft delete kullanan sistemlerde kayıt fiziksel olarak silinmek yerine `isDeleted`, `deletedAt` veya `status` alanı güncellenebilir.

<a id="head"></a>
### 7.6. HEAD

HEAD, GET ile aynı response header'larını istemek için kullanılır; ancak response body gönderilmez.

```http
HEAD /files/report.pdf HTTP/1.1
```

Kullanım alanları:

- Dosyanın var olup olmadığını kontrol etmek
- İçerik boyutunu öğrenmek
- ETag veya Last-Modified bilgisini kontrol etmek
- Kaynağı indirmeden metadata almak

Örnek cevap:

```http
HTTP/1.1 200 OK
Content-Type: application/pdf
Content-Length: 348921
ETag: "report-v4"
```

<a id="options"></a>
### 7.7. OPTIONS

OPTIONS, hedef kaynak veya sunucu için desteklenen iletişim seçeneklerini öğrenmekte kullanılır.

```http
OPTIONS /api/users HTTP/1.1
```

Örnek cevap:

```http
HTTP/1.1 204 No Content
Allow: GET, POST, OPTIONS
```

CORS preflight sürecinde tarayıcı otomatik olarak OPTIONS isteği gönderir.

<a id="trace"></a>
### 7.8. TRACE

TRACE, isteğin ara sistemlerden geçerken nasıl değiştiğini teşhis etmek amacıyla tasarlanmıştır. Güvenlik riskleri nedeniyle çoğu üretim sunucusunda kapatılır. TRACE uygulama API'lerinde günlük geliştirme sırasında neredeyse hiç kullanılmaz.

<a id="connect"></a>
### 7.9. CONNECT

CONNECT, hedef sunucuya bir tünel oluşturmak için kullanılır. Özellikle HTTPS trafiğinin HTTP proxy üzerinden geçirilmesinde kullanılır. Örnek mantık:

```text
Client → Proxy: CONNECT example.com:443
Proxy → Client: Tünel oluşturuldu
Client ↔ Server: Şifreli TLS trafiği
```

<a id="query"></a>
### 7.10. QUERY

`QUERY`, Haziran 2026'da RFC 10008 ile standartlaştırılan bir HTTP metodudur. Request body içinde sorgu verisi taşıyarak hedef kaynağın güvenli ve idempotent bir sorgu işlemi gerçekleştirmesini ifade eder.

```http
QUERY /feed HTTP/1.1
Host: example.org
Content-Type: application/json

{
  "search": "http",
  "limit": 20,
  "sort": "publishedAt:desc"
}
```

QUERY metodunun hedefi, karmaşık sorgularda GET ve POST arasındaki semantik boşluğu azaltmaktır:

- GET güvenli ve idempotenttir; ancak karmaşık sorgular URL'yi büyütebilir.
- POST body taşıyabilir; ancak genel semantiği güvenli ve idempotent değildir.
- QUERY body taşıyabilir ve sorgunun güvenli/idempotent olduğunu açıkça ifade eder.

Yeni bir standart olduğu için framework, proxy, firewall ve API araçlarının desteği zaman içinde yaygınlaşacaktır. Bu nedenle mevcut projelerde kullanılmadan önce altyapı uyumluluğu kontrol edilmelidir.

<a id="safe-ve-idempotent-metotlar"></a>
### 7.11. Safe ve Idempotent Metotlar

#### Safe method

Safe method, istemcinin sunucu durumunu değiştirmeyi talep etmediği metottur. Safe metotlar:

- GET
- HEAD
- OPTIONS
- TRACE
- QUERY

Log kaydı, analiz sayacı veya cache oluşturma gibi yan etkiler gerçekleşebilir. Buradaki güvenlilik, istemcinin kaynak üzerinde değişiklik talep etmemesi anlamına gelir.

#### Idempotent method

Aynı isteğin bir veya birden fazla kez gönderilmesi sonucunda sunucunun hedeflenen nihai durumu aynı kalıyorsa metot idempotenttir.

| Method | Safe | Idempotent | Genel kullanım |
|---|---:|---:|---|
| GET | Evet | Evet | Veri okuma |
| HEAD | Evet | Evet | Metadata okuma |
| OPTIONS | Evet | Evet | Seçenekleri öğrenme |
| TRACE | Evet | Evet | Teşhis |
| QUERY | Evet | Evet | Body içeren güvenli sorgu |
| PUT | Hayır | Evet | Kaynağı tamamen yazma/değiştirme |
| DELETE | Hayır | Evet | Kaynağı silme |
| POST | Hayır | Hayır | Kaynak oluşturma veya işlem başlatma |
| PATCH | Hayır | Garanti değil | Kısmi güncelleme |

Idempotency özellikle ağ hatalarında retry yapılırken önemlidir. İstemci cevabı alamadığında isteğin sunucuya ulaşıp ulaşmadığını bilemeyebilir. Idempotent bir istek güvenli biçimde tekrar gönderilebilir; idempotent olmayan istekte ise çift kayıt veya çift ödeme riski oluşabilir.

---

<a id="http-response-yapisi"></a>
## 8. HTTP Response Yapısı

HTTP response, sunucunun istemciye gönderdiği cevaptır. HTTP/1.1 açısından genel yapı:

```text
Status Line
Headers
Boş Satır
Opsiyonel Response Body
```

<a id="status-line"></a>
### 8.1. Status Line

Status line şu parçalardan oluşur:

```text
HTTP-VERSION STATUS-CODE REASON-PHRASE
```

Örnek:

```http
HTTP/1.1 200 OK
```

- `HTTP/1.1`: protokol sürümü
- `200`: sayısal durum kodu
- `OK`: insan tarafından okunabilir açıklama

Uygulama mantığı sayısal koda dayanmalıdır. Reason phrase protokol sürümüne ve implementasyona göre bulunmayabilir.

<a id="response-headers"></a>
### 8.2. Response Headers

Response header'ları cevap hakkında metadata taşır. Yaygın örnekler:

```http
Content-Type: application/json; charset=utf-8
Content-Length: 125
Cache-Control: no-store
Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=Lax
Access-Control-Allow-Origin: https://app.example.com
ETag: "users-v12"
Location: /api/users/124
```

<a id="response-body"></a>
### 8.3. Response Body

Response body, sunucunun istemciye gönderdiği asıl içeriği taşır. Örnek JSON body:

```json
{
  "id": 124,
  "name": "Özge Keskin",
  "email": "ozge@example.com"
}
```

Her cevapta body olmaz. Örnekler:

- `204 No Content`
- HEAD cevabı
- `304 Not Modified`

<a id="tam-bir-response-ornegi"></a>
### 8.4. Tam Bir Response Örneği

```http
HTTP/1.1 201 Created
Content-Type: application/json; charset=utf-8
Location: /api/users/124
Cache-Control: no-store
Content-Length: 88

{
  "id": 124,
  "name": "Özge Keskin",
  "email": "ozge@example.com"
}
```

Bu cevabın anlamı:

- İşlem başarıyla tamamlandı.
- Yeni bir kaynak oluşturuldu.
- Oluşan kaynağın adresi `/api/users/124`.
- Body JSON formatında.
- Cevabın cache edilmemesi isteniyor.

---

<a id="http-status-codelari"></a>
## 9. HTTP Status Code'ları

HTTP status code, sunucunun isteği nasıl sonuçlandırdığını üç basamaklı bir sayı ile ifade eder. İlk rakam kategoriyi belirtir:

| Aralık | Kategori | Genel anlam |
|---|---|---|
| `1xx` | Informational | İstek alındı, süreç devam ediyor |
| `2xx` | Success | İstek başarıyla işlendi |
| `3xx` | Redirection | İşlemi tamamlamak için başka adım gerekiyor |
| `4xx` | Client Error | İstemci isteğinde veya erişiminde problem var |
| `5xx` | Server Error | Sunucu geçerli görünen isteği işlerken hata yaşadı |

Frontend yalnızca `200` ile `500` kodlarını bilmemelidir. Doğru status code, istemcinin doğru davranışı göstermesini sağlar.

<a id="1xx-bilgilendirme-kodlari"></a>
### 9.1. 1xx Bilgilendirme Kodları

#### 100 Continue

İstemci büyük bir body göndermeden önce header'ları yollayıp sunucunun devam etmesini onaylamasını bekleyebilir.

```http
Expect: 100-continue
```

Sunucu:

```http
HTTP/1.1 100 Continue
```

#### 101 Switching Protocols

Sunucunun protokol değişikliğini kabul ettiğini belirtir. WebSocket yükseltme sürecinde görülebilir.

#### 102 Processing

Sunucunun isteği işlediğini fakat henüz final cevap üretmediğini belirten WebDAV durum kodudur.

#### 103 Early Hints

Sunucu final cevaptan önce bazı kaynakların önceden yüklenebilmesi için `Link` header'ları gönderebilir.

```http
HTTP/1.1 103 Early Hints
Link: </styles.css>; rel=preload; as=style
```

<a id="2xx-basari-kodlari"></a>
### 9.2. 2xx Başarı Kodları

#### 200 OK

İstek başarıyla tamamlanmıştır. En genel başarı kodudur. GET örneği:

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 15,
  "name": "Özge"
}
```

POST, PUT, PATCH veya DELETE işlemlerinde de body dönülecekse kullanılabilir.

#### 201 Created

Yeni bir kaynak başarıyla oluşturulmuştur. Çoğunlukla POST sonrasında kullanılır.

```http
HTTP/1.1 201 Created
Location: /api/products/87
```

`Location` header'ı yeni kaynağın adresini gösterebilir.

#### 202 Accepted

İstek işleme alınmıştır fakat henüz tamamlanmamıştır. Kullanım örnekleri:

- Arka planda rapor oluşturma
- Video dönüştürme
- Toplu e-posta gönderimi
- Queue'ya iş ekleme

```json
{
  "jobId": "job-7821",
  "status": "queued"
}
```

202, işlemin kesin olarak başarıyla tamamlanacağı anlamına gelmez. Sadece kabul edildiğini belirtir.

#### 203 Non-Authoritative Information

Dönen metadata'nın origin sunucudan birebir gelmediğini, bir ara sistem tarafından değiştirilmiş olabileceğini belirtir.

#### 204 No Content

İşlem başarılıdır fakat response body yoktur.

```http
HTTP/1.1 204 No Content
```

Kullanım alanları:

- Başarılı DELETE
- Body gerektirmeyen PUT/PATCH
- Form işlemi sonrası yalnızca başarı bildirme

Frontend, 204 cevabında `response.json()` çağırmamalıdır; çünkü parse edilecek body yoktur.

#### 205 Reset Content

İstemcinin veri giriş görünümünü sıfırlamasını önerir.

#### 206 Partial Content

Range request sonucunda kaynağın bir kısmı gönderilir. Video streaming, büyük dosya indirme ve devam ettirilebilir indirmelerde önemlidir.

```http
Range: bytes=0-999
```

Cevap:

```http
HTTP/1.1 206 Partial Content
Content-Range: bytes 0-999/5000
```

#### 207 Multi-Status

Birden fazla alt işlemin farklı sonuçlarını tek cevapta ifade etmek için WebDAV tarafından tanımlanmıştır.

<a id="3xx-yonlendirme-kodlari"></a>
### 9.3. 3xx Yönlendirme Kodları

#### 300 Multiple Choices

Kaynak için birden fazla olası temsil veya hedef bulunduğunu belirtir.

#### 301 Moved Permanently

Kaynak kalıcı olarak başka adrese taşınmıştır. Tarayıcılar ve arama motorları yeni adresi kalıcı olarak kullanabilir.

```http
HTTP/1.1 301 Moved Permanently
Location: https://example.com/new-page
```

#### 302 Found

Kaynak geçici olarak farklı bir adreste bulunuyor olabilir. Tarihsel istemci davranışları nedeniyle POST yönlendirmelerinde method değişimi görülebilir.

#### 303 See Other

İşlem sonucunun başka bir URI üzerinden GET ile alınmasını söyler. POST sonrası formun tekrar gönderilmesini önlemek için kullanılan Post/Redirect/Get deseninde yararlıdır.

```text
POST /orders
→ 303 See Other
→ Location: /orders/124
→ GET /orders/124
```

#### 304 Not Modified

İstemcideki cache kopyası hâlâ geçerlidir. Response body gönderilmez.

```http
GET /app.js
If-None-Match: "app-v9"
```

```http
HTTP/1.1 304 Not Modified
ETag: "app-v9"
```

#### 307 Temporary Redirect

Geçici yönlendirmedir. İstemci orijinal HTTP metodunu ve body'yi korur. POST isteği 307 ile yönlendirilirse yeni adrese yine POST olarak gönderilir.

#### 308 Permanent Redirect

Kalıcı yönlendirmedir ve orijinal HTTP metodunu/body'yi korur.

#### 301/302 ile 307/308 farkı

| Kod | Kalıcılık | Method korunması |
|---|---|---|
| 301 | Kalıcı | Tarihsel istemci davranışları nedeniyle garanti edilmeyebilir |
| 302 | Geçici | Tarihsel istemci davranışları nedeniyle garanti edilmeyebilir |
| 307 | Geçici | Evet |
| 308 | Kalıcı | Evet |

<a id="4xx-istemci-hata-kodlari"></a>
### 9.4. 4xx İstemci Hata Kodları

4xx kodları, isteğin mevcut hâliyle istemci tarafında düzeltme gerektirdiğini belirtir. Ancak hata yalnızca frontend kodundan kaynaklanmak zorunda değildir; URL, authentication, authorization veya gönderilen veri sorunu olabilir.

#### 400 Bad Request

Sunucu isteği hatalı sözdizimi, eksik veri veya geçersiz request yapısı nedeniyle işleyememiştir. Örnekler:

- Bozuk JSON
- Zorunlu alan eksik
- Parametre formatı hatalı
- Geçersiz tarih
- Beklenmeyen request yapısı

```json
{
  "error": "BAD_REQUEST",
  "message": "Doğum tarihi geçerli bir tarih olmalıdır."
}
```

#### 401 Unauthorized

İsmi “Unauthorized” olsa da pratikte anlamı **kimlik doğrulama gerekli veya başarısız** şeklindedir. Örnekler:

- Access token yok
- Token geçersiz
- Token süresi dolmuş
- Kullanıcı giriş yapmamış

```http
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer
```

Frontend davranışı:

- Refresh token akışını deneyebilir.
- Kullanıcıyı login sayfasına yönlendirebilir.
- Oturum süresi doldu mesajı gösterebilir.

#### 403 Forbidden

Sunucu kullanıcının kimliğini biliyor olabilir; ancak kullanıcının bu işlemi yapma yetkisi yoktur. Örnek:

- Normal kullanıcı admin paneline erişmeye çalışıyor.
- Kullanıcı başka kişinin özel kaydını silmeye çalışıyor.

Temel ayrım:

```text
401 → Sen kimsin veya geçerli şekilde giriş yaptın mı?
403 → Kim olduğunu biliyorum ama bu işlem için yetkin yok.
```

#### 404 Not Found

İstenen kaynak bulunamamıştır.

```http
GET /api/users/999999
```

Kaynak gerçekten yok olabilir veya güvenlik amacıyla varlığı gizlenebilir.

#### 405 Method Not Allowed

Endpoint vardır fakat kullanılan HTTP metodu desteklenmiyordur.

```http
DELETE /api/reports
```

Sunucu yalnızca GET destekliyorsa:

```http
HTTP/1.1 405 Method Not Allowed
Allow: GET, HEAD
```

#### 406 Not Acceptable

Sunucu, istemcinin `Accept` header'ında belirttiği formatta cevap üretemiyordur.

```http
Accept: application/xml
```

API yalnızca JSON üretiyorsa 406 dönebilir.

#### 407 Proxy Authentication Required

İstemcinin aradaki proxy sunucusunda kimlik doğrulaması yapması gerekir.

#### 408 Request Timeout

Sunucu istemciden tam isteği beklerken zaman aşımı oluşmuştur.

#### 409 Conflict

İstek, kaynağın mevcut durumuyla çelişmektedir. Örnekler:

- Aynı e-posta ile kullanıcı zaten var.
- Aynı kullanıcı adına sahip kayıt var.
- Versiyon çakışması oluştu.
- Silinmek istenen kayıt başka kayıtlar tarafından kullanılıyor.

```json
{
  "error": "EMAIL_ALREADY_EXISTS",
  "message": "Bu e-posta adresi zaten kayıtlı."
}
```

#### 410 Gone

Kaynak daha önce vardı ancak kalıcı olarak kaldırıldı. 404 kaynağın geçmişte var olup olmadığı konusunda bilgi vermez; 410 kalıcı kaldırılmayı açıkça belirtir.

#### 411 Length Required

Sunucu `Content-Length` olmadan isteği kabul etmiyordur.

#### 412 Precondition Failed

`If-Match`, `If-Unmodified-Since` gibi koşullu request header'ları karşılanmamıştır.

Optimistic concurrency kontrolünde kullanılabilir.

#### 413 Content Too Large

Request body sunucunun kabul ettiği sınırdan büyüktür. Örnek:

- 10 MB sınırı olan endpoint'e 40 MB dosya yüklemek

#### 414 URI Too Long

URL sunucunun kabul edebileceğinden uzundur. Çok büyük filtre veya veriyi query string'e koymak bu hataya yol açabilir.

#### 415 Unsupported Media Type

Sunucu request body formatını desteklemiyordur. Örnek:

```http
Content-Type: text/plain
```

Endpoint yalnızca `application/json` kabul ediyorsa 415 dönebilir.

#### 416 Range Not Satisfiable

İstenen byte aralığı kaynağın boyutunun dışındadır.

#### 418

RFC 9110 içinde kullanılmayan kod olarak tutulur. “I'm a teapot” şakasıyla tanınsa da gerçek API tasarımında iş semantiği için kullanılmamalıdır.

#### 421 Misdirected Request

İstek, bu origin için cevap üretmeye uygun olmayan bir sunucu bağlantısına yönelmiştir. HTTP/2 bağlantı paylaşımı gibi senaryolarda görülebilir.

#### 422 Unprocessable Content

Request'in sözdizimi doğrudur; ancak içerik semantik veya doğrulama kuralları nedeniyle işlenemiyordur. Örnekler:

- E-posta formatı yanlış
- Şifre minimum uzunluğu sağlamıyor
- Başlangıç tarihi bitiş tarihinden sonra
- Miktar negatif

```json
{
  "error": "VALIDATION_ERROR",
  "fieldErrors": {
    "email": "Geçerli bir e-posta adresi girilmelidir.",
    "password": "Şifre en az 8 karakter olmalıdır."
  }
}
```

400 ve 422 kullanımı API tasarım kararına bağlıdır. Önemli olan davranışın dokümante edilmesi ve tutarlı olmasıdır.

#### 423 Locked

Kaynak kilitlidir.

#### 424 Failed Dependency

İşlemin bağlı olduğu başka bir işlem başarısız olmuştur.

#### 425 Too Early

İstemcinin isteği çok erken tekrar gönderme riski bulunduğunu belirtir; TLS 0-RTT replay riskleriyle ilişkilidir.

#### 426 Upgrade Required

İstemcinin farklı bir protokole veya protokol sürümüne geçmesi gerekir.

#### 428 Precondition Required

Sunucu isteğin koşullu olmasını ister. Kayıp güncelleme problemini azaltmak için `If-Match` zorunlu tutulabilir.

#### 429 Too Many Requests

İstemci rate limit sınırını aşmıştır.

```http
HTTP/1.1 429 Too Many Requests
Retry-After: 60
```

Frontend 60 saniye sonra tekrar deneyebilir. Otomatik retry yapılırken exponential backoff uygulanması faydalıdır.

#### 431 Request Header Fields Too Large

Request header'ları çok büyüktür. Çok büyük cookie'ler veya aşırı sayıda header bu hataya neden olabilir.

#### 451 Unavailable For Legal Reasons

Kaynak hukuki nedenlerle sunulamıyordur.

<a id="5xx-sunucu-hata-kodlari"></a>
### 9.5. 5xx Sunucu Hata Kodları

5xx kodları, sunucunun geçerli görünen isteği işlerken başarısız olduğunu belirtir.

#### 500 Internal Server Error

Beklenmeyen genel sunucu hatasıdır. Örnek nedenler:

- Yakalanmamış exception
- Null reference
- Kod hatası
- Beklenmeyen veri tabanı hatası
- Hatalı yapılandırma

Kullanıcıya stack trace, SQL sorgusu veya gizli sistem bilgisi gönderilmemelidir. Doğru örnek:

```json
{
  "error": "INTERNAL_SERVER_ERROR",
  "message": "İşlem sırasında beklenmeyen bir hata oluştu.",
  "traceId": "5f47d6f2d1d84d6f"
}
```

Detaylı hata sunucu loglarında `traceId` ile bulunabilir.

#### 501 Not Implemented

Sunucu istenen method veya işlevi desteklemiyordur. 405 ile fark:

- 405: Bu kaynak için method desteklenmiyor.
- 501: Sunucu method veya işlevi genel olarak tanımıyor/uygulamıyor.

#### 502 Bad Gateway

Gateway veya proxy, upstream sunucudan geçerli cevap alamamıştır.

```text
Client → Nginx → Backend
                 ✕ Backend bozuk cevap verdi
Client ← 502 Bad Gateway
```

#### 503 Service Unavailable

Servis geçici olarak kullanılamıyordur. Nedenler:

- Bakım
- Aşırı yük
- Servis başlatılıyor
- Bağımlı servis devre dışı

```http
HTTP/1.1 503 Service Unavailable
Retry-After: 120
```

#### 504 Gateway Timeout

Gateway veya proxy, upstream sunucudan zamanında cevap alamamıştır. 502 ve 504 farkı:

```text
502 → Upstream'den geçerli cevap alınamadı.
504 → Upstream beklenen sürede cevap vermedi.
```

#### 505 HTTP Version Not Supported

Sunucu istekte kullanılan HTTP sürümünü desteklemiyordur.

#### 507 Insufficient Storage

Sunucu işlemi tamamlamak için yeterli depolama alanına sahip değildir.

#### 508 Loop Detected

Sunucu işlemi gerçekleştirirken sonsuz döngü niteliğinde bir yönlendirme veya bağ çözümleme döngüsü tespit etmiştir.

#### 511 Network Authentication Required

Ağa erişmek için kimlik doğrulaması gerektiğini belirtir. Otel veya havaalanı Wi-Fi captive portal sistemlerinde görülebilir.

<a id="sik-karistirilan-status-codelar"></a>
### 9.6. Sık Karıştırılan Status Code'lar

#### 200 ve 201

- `200 OK`: İşlem başarılı.
- `201 Created`: Yeni kaynak oluşturuldu.

#### 200 ve 204

- `200 OK`: Body gönderilebilir.
- `204 No Content`: Body gönderilmez.

#### 400 ve 422

- `400 Bad Request`: İstek yapısı, sözdizimi veya genel doğrulama sorunu.
- `422 Unprocessable Content`: Yapı anlaşılır fakat iş kurallarına göre içerik işlenemiyor.

#### 401 ve 403

- `401 Unauthorized`: Geçerli authentication yok.
- `403 Forbidden`: Authentication olabilir; yetki yok.

#### 404 ve 410

- `404 Not Found`: Kaynak bulunamıyor.
- `410 Gone`: Kaynak bilerek ve kalıcı biçimde kaldırılmış.

#### 409 ve 422

- `409 Conflict`: Kaynağın mevcut durumu ile çelişki.
- `422 Unprocessable Content`: Gönderilen alanların semantik doğrulaması başarısız.

#### 500, 502, 503 ve 504

- `500`: Uygulama içinde beklenmeyen hata.
- `502`: Proxy upstream'den geçerli cevap alamadı.
- `503`: Servis geçici olarak kullanılamıyor.
- `504`: Proxy upstream'i beklerken zaman aşımına uğradı.

---

<a id="http-headerlari-derinlemesine"></a>
## 10. HTTP Header'ları Derinlemesine

HTTP header'ları request veya response hakkında kontrol bilgisi ve metadata taşır. Header adları teknik olarak case-insensitive'dir; yani `Content-Type` ve `content-type` aynı alanı ifade eder. Buna rağmen okunabilirlik için standart yazım biçimleri kullanılır.

<a id="genel-headerlar"></a>
### 10.1. Genel Header'lar

#### Date

Cevabın oluşturulduğu zamanı belirtir.

```http
Date: Sat, 01 Aug 2026 10:30:00 GMT
```

#### Connection

HTTP/1.1 bağlantı davranışını etkileyebilir.

```http
Connection: keep-alive
```

Hop-by-hop header'lar proxy sınırlarını geçmemelidir. HTTP/2 ve HTTP/3 bağlantı yönetimi farklı olduğu için `Connection` header'ı kullanılmaz.

#### Via

Mesajın geçtiği proxy veya gateway bilgilerini gösterebilir.

```http
Via: 1.1 proxy.example.com
```

#### Forwarded ve X-Forwarded-*

Reverse proxy arkasındaki asıl istemci ve protokol bilgisini taşıyabilir.

```http
Forwarded: for=203.0.113.15;proto=https;host=example.com
X-Forwarded-For: 203.0.113.15
X-Forwarded-Proto: https
X-Forwarded-Host: example.com
```

Bu header'lara yalnızca güvenilir proxy tarafından ayarlanıyorsa güvenilmelidir. İstemci kendisi sahte değer gönderebilir.

<a id="icerik-headerlari"></a>
### 10.2. İçerik Header'ları

#### Content-Type

Body'nin media type'ını belirtir.

```http
Content-Type: application/json; charset=utf-8
```

#### Content-Length

Body'nin byte cinsinden uzunluğunu belirtir.

```http
Content-Length: 348
```

#### Content-Encoding

Body'nin hangi sıkıştırma veya kodlama ile gönderildiğini belirtir.

```http
Content-Encoding: br
```

#### Content-Language

İçeriğin doğal dilini belirtir.

```http
Content-Language: tr
```

#### Content-Disposition

İçeriğin tarayıcıda görüntülenmesi veya dosya olarak indirilmesi için bilgi sağlar.

```http
Content-Disposition: attachment; filename="rapor.pdf"
```

#### Content-Range

Partial content cevabında gönderilen byte aralığını belirtir.

```http
Content-Range: bytes 1000-1999/5000
```

<a id="kimlik-dogrulama-headerlari"></a>
### 10.3. Kimlik Doğrulama Header'ları

#### Authorization

İstemci kimlik doğrulama bilgisini gönderir.Bearer token:

```http
Authorization: Bearer eyJhbGciOi...
```

Basic authentication:

```http
Authorization: Basic dXNlcjpwYXNzd29yZA==
```

Basic authentication şifreleme değildir; yalnızca Base64 kodlamadır. Mutlaka HTTPS üzerinden kullanılmalıdır.

#### WWW-Authenticate

Sunucu 401 cevabında kullanılacak authentication şemasını belirtebilir.

```http
WWW-Authenticate: Bearer realm="api"
```

#### Proxy-Authorization

Proxy kimlik doğrulaması için kullanılır.

<a id="cache-headerlari"></a>
### 10.4. Cache Header'ları

- `Cache-Control`
- `ETag`
- `If-None-Match`
- `Last-Modified`
- `If-Modified-Since`
- `Expires`
- `Age`
- `Vary`

Bu header'lar gereksiz veri transferini azaltır ve uygulama performansını artırır.

<a id="cors-headerlari"></a>
### 10.5. CORS Header'ları

Request tarafında:

- `Origin`
- `Access-Control-Request-Method`
- `Access-Control-Request-Headers`

Response tarafında:

- `Access-Control-Allow-Origin`
- `Access-Control-Allow-Methods`
- `Access-Control-Allow-Headers`
- `Access-Control-Allow-Credentials`
- `Access-Control-Expose-Headers`
- `Access-Control-Max-Age`

<a id="guvenlik-headerlari"></a>
### 10.6. Güvenlik Header'ları

#### Strict-Transport-Security

Tarayıcıya ilgili domain için yalnızca HTTPS kullanmasını söyler.

```http
Strict-Transport-Security: max-age=31536000; includeSubDomains
```

#### Content-Security-Policy

Hangi kaynaklardan script, style, image ve diğer içeriklerin yüklenebileceğini sınırlar. XSS riskini azaltmada güçlü bir katmandır.

```http
Content-Security-Policy: default-src 'self'; script-src 'self'
```

#### X-Content-Type-Options

Tarayıcının MIME type tahmini yapmasını engeller.

```http
X-Content-Type-Options: nosniff
```

#### X-Frame-Options

Sayfanın iframe içinde gösterilmesini sınırlar.

```http
X-Frame-Options: DENY
```

Modern projelerde daha esnek kontrol için CSP `frame-ancestors` direktifi tercih edilebilir.

#### Referrer-Policy

Referer bilgisinin ne kadarının gönderileceğini belirler.

```http
Referrer-Policy: strict-origin-when-cross-origin
```

#### Permissions-Policy

Kamera, mikrofon ve konum gibi tarayıcı özelliklerinin kullanımını sınırlar.

```http
Permissions-Policy: camera=(), microphone=(), geolocation=(self)
```

---

<a id="http-body-ve-veri-formatlari"></a>
## 11. HTTP Body ve Veri Formatları

HTTP body farklı veri formatları taşıyabilir. Body'nin nasıl yorumlanacağını `Content-Type` belirler.

<a id="json"></a>
### 11.1. JSON

Modern web API'lerinde en yaygın formattır.

```http
Content-Type: application/json
```

```json
{
  "name": "Özge Keskin",
  "skills": ["JavaScript", "React", "Python"],
  "active": true
}
```

Avantajları:

- İnsan tarafından okunabilir
- JavaScript ile doğal uyumlu
- Çoğu programlama dilinde kolayca parse edilir
- Nesne, dizi, sayı, boolean ve null değerlerini destekler

Dikkat edilmesi gerekenler:

- JSON'da yorum satırı yoktur.
- Property adları çift tırnak içinde olmalıdır.
- Son elemandan sonra trailing comma olmamalıdır.
- Tarih için yerleşik veri tipi yoktur; çoğunlukla ISO 8601 string kullanılır.

```json
{
  "createdAt": "2026-08-01T10:30:00Z"
}
```

<a id="form-url-encoded"></a>
### 11.2. Form URL Encoded

Klasik HTML form gönderimlerinde kullanılır.

```http
Content-Type: application/x-www-form-urlencoded
```

Body:

```text
name=%C3%96zge+Keskin&email=ozge%40example.com
```

Alanlar `&`, anahtar ve değer `=` ile ayrılır.

<a id="multipart-form-data"></a>
### 11.3. Multipart Form Data

Dosya ve form alanlarını aynı request içinde göndermek için kullanılır.

```http
Content-Type: multipart/form-data; boundary=----ExampleBoundary
```

```text
------ExampleBoundary
Content-Disposition: form-data; name="title"

Profil Fotoğrafı
------ExampleBoundary
Content-Disposition: form-data; name="file"; filename="photo.jpg"
Content-Type: image/jpeg

...binary data...
------ExampleBoundary--
```

Frontend'de `FormData` kullanıldığında `Content-Type` header'ını elle yazmak çoğunlukla hatadır. Tarayıcı boundary değerini otomatik oluşturmalıdır.

```javascript
const formData = new FormData();
formData.append("title", "Profil Fotoğrafı");
formData.append("file", fileInput.files[0]);

await fetch("/api/files", {
  method: "POST",
  body: formData,
});
```

<a id="text-html-xml-ve-binary-icerikler"></a>
### 11.4. Text, HTML, XML ve Binary İçerikler

Yaygın media type örnekleri:

| İçerik | Content-Type |
|---|---|
| Düz metin | `text/plain` |
| HTML | `text/html` |
| CSS | `text/css` |
| JavaScript | `text/javascript` |
| JSON | `application/json` |
| XML | `application/xml` |
| PDF | `application/pdf` |
| ZIP | `application/zip` |
| JPEG | `image/jpeg` |
| PNG | `image/png` |
| SVG | `image/svg+xml` |
| MP4 | `video/mp4` |
| Genel binary | `application/octet-stream` |

---

<a id="content-type-ve-accept-farki"></a>
## 12. Content-Type ve Accept Farkı

Bu iki header sık karıştırılır.

### Content-Type

Gönderilen body'nin formatını açıklar. Request:

```http
Content-Type: application/json
```

“Sunucuya gönderdiğim request body JSON formatındadır.”

Response:

```http
Content-Type: application/json
```

“İstemciye gönderdiğim response body JSON formatındadır.”

### Accept

İstemcinin hangi response formatlarını kabul ettiğini belirtir.

```http
Accept: application/json
```

“Bana JSON formatında cevap gönder.”

Bir request içinde ikisi aynı anda bulunabilir:

```http
POST /api/reports HTTP/1.1
Content-Type: application/json
Accept: application/pdf

{
  "month": 7,
  "year": 2026
}
```

Bu isteğin anlamı:

- Request body JSON.
- İstemci cevap olarak PDF istiyor.

---

<a id="stateless-yapi-cookie-ve-session"></a>
## 13. Stateless Yapı, Cookie ve Session

HTTP stateless olduğu için sunucu, iki isteğin aynı kullanıcıdan geldiğini kendiliğinden bilemez.

```text
1. istek: GET /products
2. istek: POST /orders
```

Bu iki isteği aynı kullanıcıyla ilişkilendirmek için ek mekanizmalar gerekir.

<a id="cookie"></a>
### 13.1. Cookie

Cookie, tarayıcının bir domain için sakladığı küçük veri parçalarıdır. Sunucu response içinde `Set-Cookie` gönderir:

```http
Set-Cookie: sessionId=abc123; Path=/; HttpOnly; Secure; SameSite=Lax
```

Tarayıcı sonraki uygun isteklerde cookie'yi otomatik gönderir:

```http
Cookie: sessionId=abc123
```

Önemli cookie attribute'ları:

#### HttpOnly

JavaScript'in cookie'ye `document.cookie` ile erişmesini engeller. XSS sonucu session cookie çalınması riskini azaltır.

#### Secure

Cookie'nin yalnızca HTTPS bağlantılarında gönderilmesini sağlar.

#### SameSite

Cookie'nin cross-site isteklerde gönderilme davranışını belirler.

- `Strict`: En katı davranış
- `Lax`: Birçok normal gezinme senaryosuna izin verir
- `None`: Cross-site gönderime izin verir; `Secure` zorunludur

#### Path

Cookie'nin hangi path'lerde gönderileceğini belirler.

#### Domain

Cookie'nin hangi domain veya alt domainlerde geçerli olacağını belirler.

#### Max-Age ve Expires

Cookie'nin yaşam süresini belirler.

<a id="session"></a>
### 13.2. Session

Session tabanlı authentication süreci:

1. Kullanıcı login isteği gönderir.
2. Sunucu kimlik bilgilerini doğrular.
3. Sunucu session kaydı oluşturur.
4. Session ID cookie içinde istemciye gönderilir.
5. Tarayıcı sonraki isteklerde session cookie'sini gönderir.
6. Sunucu session ID üzerinden kullanıcıyı bulur.

```text
Browser Cookie: sessionId=abc123
Server Session Store:
abc123 → userId: 15, role: admin
```

Session verisi sunucu belleğinde, veri tabanında veya Redis gibi bir sistemde tutulabilir.

<a id="token-tabanli-kimlik-dogrulama"></a>
### 13.3. Token Tabanlı Kimlik Doğrulama

Token tabanlı sistemlerde istemci access token alır ve isteklerde gönderir:

```http
Authorization: Bearer access-token-value
```

Yaygın kavramlar:

- Access token
- Refresh token
- JWT
- Token expiration
- Token revocation

Token'ın nerede saklanacağı güvenlik kararıdır. LocalStorage erişilebilirliği XSS açısından risk taşır. HttpOnly cookie JavaScript erişimini engeller; ancak cookie tabanlı isteklerde CSRF önlemleri değerlendirilmelidir. Authentication yöntemi ne olursa olsun HTTPS kullanılmalıdır.

---

<a id="cors-nedir"></a>
## 14. CORS Nedir?

**CORS**, “Cross-Origin Resource Sharing” ifadesinin kısaltmasıdır. Türkçesi “Kaynaklar Arası Kaynak Paylaşımı” olarak ifade edilebilir. CORS, bir web sayfasının kendi origin'inden farklı bir origin'deki kaynağa JavaScript aracılığıyla erişip erişemeyeceğini kontrol eden HTTP tabanlı tarayıcı mekanizmasıdır. Örnek:

```text
Frontend: http://localhost:5173
Backend:  http://localhost:3000
```

Portlar farklı olduğu için bu iki adres farklı origin'dir. React uygulaması backend'e `fetch()` isteği gönderdiğinde tarayıcı CORS kurallarını uygular.

<a id="same-origin-policy"></a>
### 14.1. Same-Origin Policy

**Same-Origin Policy**, tarayıcıların uyguladığı temel güvenlik politikasıdır. Bir origin'den çalışan script'in başka bir origin'deki hassas verilere sınırsız erişmesini engeller. Bu politika olmasaydı şu saldırı mümkün olurdu:

1. Kullanıcı bankanın sitesinde oturum açar.
2. Aynı tarayıcıda kötü amaçlı siteyi açar.
3. Kötü amaçlı sitenin JavaScript'i bankanın endpoint'lerine istek gönderir.
4. Banka cevaplarını okuyarak kullanıcının özel verilerini çalabilir.

Same-Origin Policy, origin'ler arası JavaScript erişimini varsayılan olarak sınırlar. CORS ise sunucunun belirli origin'lere kontrollü biçimde izin vermesini sağlar.

<a id="origin-nedir"></a>
### 14.2. Origin Nedir?

Origin üç parçadan oluşur:

```text
scheme + host + port
```

Örnek origin:

```text
https://example.com:443
```

Aşağıdaki karşılaştırmalar önemlidir:

| Adres 1 | Adres 2 | Aynı origin mi? | Neden? |
|---|---|---:|---|
| `https://example.com/a` | `https://example.com/b` | Evet | Scheme, host ve port aynı |
| `http://example.com` | `https://example.com` | Hayır | Scheme farklı |
| `https://example.com` | `https://api.example.com` | Hayır | Host farklı |
| `http://localhost:3000` | `http://localhost:5173` | Hayır | Port farklı |
| `https://example.com:443` | `https://example.com` | Evet | HTTPS varsayılan portu 443 |

Path origin hesabına dahil değildir.

<a id="cross-origin-istek-nedir"></a>
### 14.3. Cross-Origin İstek Nedir?

Bir sayfa kendi origin'inden farklı scheme, host veya porttaki kaynağa istek gönderiyorsa bu cross-origin istektir.

```javascript
// Sayfa http://localhost:5173 üzerinde çalışıyor.
fetch("http://localhost:3000/api/products");
```

Tarayıcı request'e şu header'ı ekleyebilir:

```http
Origin: http://localhost:5173
```

Backend izin veriyorsa response içinde şunu gönderir:

```http
Access-Control-Allow-Origin: http://localhost:5173
```

Tarayıcı bu header'ı kontrol eder. Uygun değilse cevap ağ seviyesinde gelmiş olsa bile JavaScript'in response'u okumasını engeller. 

CORS kontrolünü sunucudan çok **tarayıcı uygular**. Postman veya backend-to-backend isteklerde tarayıcı Same-Origin Policy olmadığı için aynı CORS davranışı görülmeyebilir.

<a id="basit-cors-istekleri"></a>
### 14.4. Basit CORS İstekleri

Bazı cross-origin istekler doğrudan gönderilir. Bunlara günlük anlatımda “simple request” denir. Genel olarak basit istek olabilmesi için:

- Method `GET`, `HEAD` veya `POST` olmalıdır.
- Yalnızca CORS safelisted request header'ları kullanılmalıdır.
- `Content-Type` kullanılıyorsa değerlerden biri olmalıdır:
  - `application/x-www-form-urlencoded`
  - `multipart/form-data`
  - `text/plain`

Örnek:

```javascript
fetch("https://api.example.com/public-news");
```

Tarayıcı isteği doğrudan gönderir. Sunucu response içinde uygun `Access-Control-Allow-Origin` header'ını döndürmezse frontend response'a erişemez. Basit olması isteğin güvenli veya authentication gerektirmeyen bir işlem olduğu anlamına gelmez. “Simple request” yalnızca CORS protokolündeki teknik sınıflandırmadır.

<a id="preflight-istekleri"></a>
### 14.5. Preflight İstekleri

Bazı cross-origin isteklerden önce tarayıcı gerçek isteği göndermeden sunucuya otomatik `OPTIONS` isteği yollar. Buna **preflight request** denir. Preflight'ın amacı:

> “Bu origin'den, şu method ve header'larla gerçek isteği göndermeme izin veriyor musun?”

Preflight gerektirebilecek durumlar:

- `PUT`, `PATCH`, `DELETE` gibi metotlar
- `Content-Type: application/json`
- `Authorization` gibi safelist dışı header'lar
- Özel header'lar

Örnek gerçek istek:

```javascript
fetch("https://api.example.com/users/15", {
  method: "PATCH",
  headers: {
    "Content-Type": "application/json",
    Authorization: "Bearer token-value",
  },
  body: JSON.stringify({ name: "Özge" }),
});
```

Tarayıcı önce şuna benzer bir istek gönderebilir:

```http
OPTIONS /users/15 HTTP/1.1
Host: api.example.com
Origin: https://app.example.com
Access-Control-Request-Method: PATCH
Access-Control-Request-Headers: authorization, content-type
```

Sunucu izin veriyorsa:

```http
HTTP/1.1 204 No Content
Access-Control-Allow-Origin: https://app.example.com
Access-Control-Allow-Methods: GET, POST, PATCH, DELETE, OPTIONS
Access-Control-Allow-Headers: Authorization, Content-Type
Access-Control-Max-Age: 600
```

Bunun ardından tarayıcı gerçek PATCH isteğini gönderir. Preflight başarısız olursa gerçek istek gönderilmez.

<a id="cors-response-headerlari"></a>
### 14.6. CORS Response Header'ları

#### Access-Control-Allow-Origin

Hangi origin'in response'u okuyabileceğini belirtir. Tek origin:

```http
Access-Control-Allow-Origin: https://app.example.com
```

Herkese açık kaynak:

```http
Access-Control-Allow-Origin: *
```

`*`, credentials kullanılan isteklerle birlikte kullanılamaz. Birden fazla origin'e izin verilecekse header'a virgülle liste yazmak standart çözüm değildir. Sunucu request'teki `Origin` değerini allowlist ile karşılaştırıp uygun olan tek origin'i response'a yansıtmalıdır.

```text
Allowed origins:
- https://app.example.com
- https://admin.example.com
```

Request:

```http
Origin: https://admin.example.com
```

Response:

```http
Access-Control-Allow-Origin: https://admin.example.com
Vary: Origin
```

Dinamik origin cevabında `Vary: Origin`, cache'in farklı origin cevaplarını birbirine karıştırmasını engeller.

#### Access-Control-Allow-Methods

Preflight cevabında izin verilen metotları belirtir.

```http
Access-Control-Allow-Methods: GET, POST, PUT, PATCH, DELETE, OPTIONS
```

#### Access-Control-Allow-Headers

Gerçek istekte kullanılmasına izin verilen request header'larını belirtir.

```http
Access-Control-Allow-Headers: Authorization, Content-Type, X-Request-Id
```

#### Access-Control-Allow-Credentials

Cookie veya HTTP authentication gibi credentials içeren cross-origin isteklere izin verildiğini belirtir.

```http
Access-Control-Allow-Credentials: true
```

Bu header'ın tek geçerli izin değeri `true` şeklindedir.

#### Access-Control-Expose-Headers

Tarayıcı JavaScript'inin okuyabileceği ek response header'larını belirtir.

```http
Access-Control-Expose-Headers: X-Total-Count, Content-Disposition
```

Örneğin sayfalama için `X-Total-Count` header'ını frontend'in okuması gerekiyorsa expose edilmelidir.

#### Access-Control-Max-Age

Preflight sonucunun kaç saniye cache edilebileceğini belirtir.

```http
Access-Control-Max-Age: 600
```

Bu sayede her gerçek istekten önce tekrar OPTIONS gönderilmesi azaltılabilir. Tarayıcıların uyguladığı üst sınırlar değişebilir.

<a id="credentials-kullanimi"></a>
### 14.7. Credentials Kullanımı

Cookie tabanlı cross-origin isteklerde frontend açıkça credentials göndermelidir. Fetch:

```javascript
fetch("https://api.example.com/profile", {
  credentials: "include",
});
```

Axios:

```javascript
axios.get("https://api.example.com/profile", {
  withCredentials: true,
});
```

Backend cevabı:

```http
Access-Control-Allow-Origin: https://app.example.com
Access-Control-Allow-Credentials: true
```

Şu kombinasyon geçersizdir:

```http
Access-Control-Allow-Origin: *
Access-Control-Allow-Credentials: true
```

Credentials kullanıldığında spesifik origin gönderilmelidir. Cookie'nin cross-site gönderilebilmesi için cookie ayarları da uygun olmalıdır:

```http
Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=None
```

CORS doğru olsa bile `SameSite`, `Secure`, domain veya third-party cookie politikaları nedeniyle cookie gönderilmeyebilir.

<a id="cors-hatalari-ve-cozumleri"></a>
### 14.8. CORS Hataları ve Çözümleri

Yaygın tarayıcı hatası:

```text
Access to fetch at 'http://localhost:3000/api/products'
from origin 'http://localhost:5173' has been blocked by CORS policy:
No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

#### Olası neden 1: Backend CORS header'ı göndermiyor

Çözüm: Backend'de izin verilen frontend origin'i tanımlanmalıdır.

#### Olası neden 2: Yanlış origin tanımlanmış

```text
İzin verilen: http://localhost:3000
Gerçek frontend: http://localhost:5173
```

Origin tam olarak scheme, host ve port ile eşleşmelidir.

#### Olası neden 3: Preflight OPTIONS işlenmiyor

Sunucu OPTIONS isteğine 404, 401 veya 500 döndürüyor olabilir. CORS middleware'i authentication kontrolünden önce çalışacak şekilde konumlandırılmalıdır.

#### Olası neden 4: Method izinli değil

Frontend PATCH gönderiyor fakat backend:

```http
Access-Control-Allow-Methods: GET, POST
```

#### Olası neden 5: Header izinli değil

Frontend `Authorization` gönderiyor fakat backend:

```http
Access-Control-Allow-Headers: Content-Type
```

#### Olası neden 6: Credentials ayarları uyumsuz

- Frontend `credentials: "include"` kullanmamış olabilir.
- Backend `Access-Control-Allow-Credentials: true` göndermiyor olabilir.
- Backend wildcard origin kullanıyor olabilir.
- Cookie `SameSite` veya `Secure` ayarı uyumsuz olabilir.

#### Olası neden 7: Asıl hata CORS gibi görünüyor

Backend 500 hata cevabında CORS header'larını eklemezse tarayıcı yalnızca CORS hatası gösterebilir. Gerçek hata sunucu loglarında olabilir.

#### Olası neden 8: Redirect sırasında CORS sorunu

İstek başka bir origin'e yönleniyor ve yeni hedef gerekli CORS header'larını göndermiyor olabilir.

#### Olası neden 9: Proxy CORS header'larını siliyor veya değiştiriyor

Nginx, CDN veya API gateway yapılandırması kontrol edilmelidir.

#### Geliştirme ortamında proxy çözümü

Vite örneği:

```javascript
// vite.config.js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

export default defineConfig({
  plugins: [react()],
  server: {
    proxy: {
      "/api": {
        target: "http://localhost:3000",
        changeOrigin: true,
      },
    },
  },
});
```

Frontend:

```javascript
fetch("/api/products");
```

Tarayıcı isteği frontend development server'a yapar; Vite proxy isteği backend'e aktarır. Bu geliştirme kolaylığıdır. Üretimde doğru reverse proxy ve CORS tasarımı yine yapılmalıdır.

<a id="no-cors-yanilgisi"></a>
### 14.9. no-cors Yanılgısı

Bazı geliştiriciler CORS hatasını çözmek için şunu ekler:

```javascript
fetch("https://api.example.com/data", {
  mode: "no-cors",
});
```

Bu genellikle çözüm değildir. `no-cors` modunda:

- Kullanılabilecek method ve header'lar ciddi şekilde kısıtlanır.
- Response çoğunlukla `opaque` olur.
- JavaScript status code'u, header'ları ve body'yi okuyamaz.

```javascript
const response = await fetch(url, { mode: "no-cors" });
console.log(response.type); // "opaque"
```

CORS problemi frontend'den “kapatılmaz”. İzin, isteğin ulaştığı sunucu tarafından doğru response header'larıyla verilmelidir.

<a id="cors-bir-guvenlik-mekanizmasi-midir"></a>
### 14.10. CORS Bir Güvenlik Mekanizması mıdır?

CORS bir **erişim yetkilendirme sistemi** değildir. CORS, tarayıcının cross-origin response'u JavaScript'e açıp açmayacağını kontrol eder. CORS şunların yerine geçmez:

- Authentication
- Authorization
- API key kontrolü
- Rate limiting
- Input validation
- CSRF koruması
- Veri şifreleme

Bir API'ye `Access-Control-Allow-Origin: *` eklemek API'yi internete açan tek şey değildir. API zaten ağ üzerinden erişilebiliyorsa Postman, curl veya başka bir sunucu tarafından çağrılabilir. CORS yalnızca tarayıcı JavaScript bağlamındaki erişimi kontrol eder. Bu nedenle hassas endpoint'ler her zaman sunucu tarafında authentication ve authorization uygulamalıdır.

---

<a id="cors-csrf-ve-authentication-arasindaki-fark"></a>
## 15. CORS, CSRF ve Authentication Arasındaki Fark

Bu üç kavram birbirinden farklıdır.

### CORS

Bir origin'deki tarayıcı JavaScript'inin başka origin'deki response'u okuyup okuyamayacağını belirler.

### Authentication

Kullanıcının kim olduğunu doğrular.

```text
Kullanıcı giriş yaptı mı?
Token geçerli mi?
Session geçerli mi?
```

### Authorization

Kimliği bilinen kullanıcının belirli işlemi yapma yetkisini kontrol eder.

```text
Bu kullanıcı admin panelini görebilir mi?
Bu siparişi silebilir mi?
```

### CSRF

Cross-Site Request Forgery, kullanıcının tarayıcısındaki otomatik cookie davranışını kötüye kullanarak kullanıcının haberi olmadan başka sitede işlem yaptırma saldırısıdır. Örnek:

1. Kullanıcı bankada giriş yapmıştır.
2. Banka session cookie kullanmaktadır.
3. Kullanıcı kötü amaçlı siteye girer.
4. Kötü site bankanın para transfer endpoint'ine form gönderir.
5. Tarayıcı banka cookie'sini otomatik ekleyebilir.

CORS response'un okunmasını engelleyebilir; ancak bazı cross-origin isteklerin gönderilmesini tamamen engellemez. Bu nedenle CORS tek başına CSRF koruması değildir. CSRF önlemleri:

- SameSite cookie
- CSRF token
- Origin/Referer doğrulaması
- Hassas işlemlerde yeniden doğrulama
- Custom header ve doğru CORS politikası
- GET ile durum değiştirmeme

Özet tablo:

| Kavram | Temel soru |
|---|---|
| Authentication | Kullanıcı kim? |
| Authorization | Bu kullanıcı ne yapabilir? |
| CORS | Tarayıcıdaki başka origin bu response'u okuyabilir mi? |
| CSRF koruması | Başka site kullanıcı adına istek yaptırtabilir mi? |

---

<a id="https-ve-tls"></a>
## 16. HTTPS ve TLS

**HTTPS**, HTTP iletişiminin TLS üzerinden güvenli biçimde yapılmasıdır.

```text
HTTP + TLS = HTTPS
```

HTTPS üç ana güvenlik özelliği sağlar:

### Gizlilik

İstemci ile sunucu arasındaki trafik şifrelenir. Ağdaki üçüncü kişiler içeriği kolayca okuyamaz.

### Bütünlük

Verinin iletim sırasında değiştirilip değiştirilmediği kontrol edilir.

### Sunucu kimliğinin doğrulanması

TLS sertifikası sayesinde istemci doğru sunucuyla iletişim kurduğunu doğrulamaya çalışır. HTTPS olmadan şu bilgiler ağ üzerinde açığa çıkabilir:

- Şifreler
- Token'lar
- Cookie'ler
- Kişisel veriler
- API request ve response body'leri

TLS genel olarak şu süreci içerir:

1. İstemci sunucuyla bağlantı başlatır.
2. Desteklenen TLS sürümleri ve şifreleme seçenekleri paylaşılır.
3. Sunucu sertifikasını gönderir.
4. İstemci sertifikayı doğrular.
5. Oturum anahtarları oluşturulur.
6. HTTP mesajları şifreli kanal üzerinden taşınır.

HTTPS kullanmak uygulamanın kendi başına güvenli olduğu anlamına gelmez. HTTPS taşıma katmanını korur; SQL Injection, XSS, yetki hatası veya zayıf parola gibi uygulama açıklarını çözmez. Mixed content hatası, HTTPS sayfanın HTTP kaynak çağırması durumunda oluşabilir:

```text
Frontend: https://app.example.com
API:      http://api.example.com
```

Tarayıcı güvenlik nedeniyle bu isteği engelleyebilir. Üretimde tüm kaynakların HTTPS kullanması gerekir.

---

<a id="http-surumleri"></a>
## 17. HTTP Sürümleri

HTTP sürümleri temel semantiği korurken taşıma ve performans mekanizmalarını geliştirir. GET, POST, status code ve header kavramları sürümler arasında büyük ölçüde aynı kalır.

<a id="http10"></a>
### 17.1. HTTP/1.0

HTTP/1.0 döneminde her istek için ayrı TCP bağlantısı açılması yaygındı:

```text
TCP bağlantısı → Request 1 → Response 1 → Bağlantı kapanır
TCP bağlantısı → Request 2 → Response 2 → Bağlantı kapanır
```

Bu durum çok sayıda kaynağı olan web sayfalarında bağlantı kurma maliyetini artırır.

<a id="http11"></a>
### 17.2. HTTP/1.1

HTTP/1.1 kalıcı bağlantıları yaygınlaştırdı.

```text
Tek TCP bağlantısı
├── Request 1 / Response 1
├── Request 2 / Response 2
└── Request 3 / Response 3
```

Önemli özellikler:

- Persistent connections
- `Host` header'ı
- Chunked transfer encoding
- Cache mekanizmaları
- Range requests
- Gelişmiş method ve status code semantiği

HTTP/1.1 mesajları start line, header satırları, boş satır ve opsiyonel body şeklinde metinsel yapıya sahiptir. HTTP/1.1 pipelining teorik olarak birden fazla isteği beklemeden gönderebilir; ancak cevap sırası ve head-of-line blocking sorunları nedeniyle yaygın kullanılmamıştır. Tarayıcılar paralellik için genellikle birden fazla TCP bağlantısı açmıştır.

<a id="http2"></a>
### 17.3. HTTP/2

HTTP/2, HTTP semantiğini değiştirmek yerine ağ üzerindeki ifade biçimini optimize eder. Önemli özellikler:

#### Binary framing

Mesajlar metinsel satırlar yerine binary frame'lere ayrılır.

#### Multiplexing

Tek TCP bağlantısı üzerinde birden fazla request/response stream'i eş zamanlı ilerleyebilir.

```text
Tek TCP bağlantısı
├── Stream 1: HTML
├── Stream 3: CSS
├── Stream 5: JS
└── Stream 7: Image
```

#### Header compression

Tekrarlayan header'lar HPACK ile sıkıştırılır.

#### Akış kontrolü

Connection ve stream seviyesinde veri akışı kontrol edilir. HTTP/2 uygulama seviyesindeki head-of-line blocking sorununu azaltır; ancak tüm stream'ler aynı TCP bağlantısını kullandığı için TCP paket kaybı bağlantıdaki diğer stream'leri de geçici olarak etkileyebilir.

<a id="http3"></a>
### 17.4. HTTP/3

HTTP/3, HTTP semantiğini QUIC taşıma protokolü üzerinde çalıştırır. Temel özellikler:

- TCP yerine UDP üzerinde çalışan QUIC
- TLS 1.3 entegrasyonu
- Stream seviyesinde bağımsız teslim
- Daha hızlı bağlantı kurulumu potansiyeli
- Ağ değişimlerinde connection migration desteği
- Header compression için QPACK

HTTP/3'te bir stream'deki paket kaybı diğer bağımsız stream'leri TCP'deki kadar bloke etmez. Karşılaştırma:

| Özellik | HTTP/1.1 | HTTP/2 | HTTP/3 |
|---|---|---|---|
| Taşıma | TCP | TCP | QUIC/UDP |
| Mesaj biçimi | Metinsel | Binary framing | Binary framing |
| Multiplexing | Sınırlı | Evet | Evet |
| Header compression | Yok | HPACK | QPACK |
| TLS | Opsiyonel, HTTPS ile | Pratikte çoğunlukla TLS | QUIC içinde TLS 1.3 |
| Paket kaybı etkisi | Bağlantıyı etkiler | TCP nedeniyle stream'leri etkileyebilir | Büyük ölçüde ilgili stream ile sınırlanabilir |

Geliştirici çoğunlukla `fetch()` kodunu HTTP sürümüne göre değiştirmez. Tarayıcı ve sunucu desteklenen sürümü bağlantı kurulurken seçer.

---

<a id="http-cache-mekanizmasi"></a>
## 18. HTTP Cache Mekanizması

HTTP cache, aynı kaynağın gereksiz yere tekrar indirilmesini azaltır. Cache türleri:

- Browser cache
- Shared proxy cache
- CDN cache
- Reverse proxy cache
- Service worker cache

Cache faydaları:

- Daha hızlı sayfa açılışı
- Daha az bandwidth kullanımı
- Backend yükünün azalması
- Kullanıcı deneyiminin iyileşmesi

<a id="freshness-ve-validation"></a>
### 18.1. Freshness ve Validation

#### Fresh response

Cache'deki cevap belirlenen süre içinde hâlâ güncel kabul edilir. Sunucuya istek göndermeden kullanılabilir.

#### Stale response

Cevabın tazelik süresi dolmuştur. Tekrar kullanılmadan önce doğrulama gerekebilir.

#### Validation

İstemci sunucuya cache'deki kopyanın hâlâ geçerli olup olmadığını sorar.

<a id="cache-control-direktifleri"></a>
### 18.2. Cache-Control Direktifleri

#### max-age

Cevabın saniye cinsinden ne kadar süre fresh olduğunu belirtir.

```http
Cache-Control: public, max-age=3600
```

#### public

Shared cache'lerin de cevabı saklayabilmesine izin verir.

#### private

Cevabın yalnızca kullanıcıya özel cache'de saklanmasını belirtir.

```http
Cache-Control: private, max-age=300
```

#### no-cache

Cevabın saklanabileceğini; ancak tekrar kullanılmadan önce sunucuyla doğrulanması gerektiğini belirtir. `no-cache`, “hiç saklama” anlamına gelmez.

#### no-store

Cevabın hiçbir cache'de saklanmamasını ister.

```http
Cache-Control: no-store
```

Hassas verilerde kullanılabilir.

#### must-revalidate

Cevap stale olduğunda sunucuyla doğrulama yapılmadan kullanılmamasını ister.

#### immutable

Kaynağın cache ömrü boyunca değişmeyeceğini belirtir. Hash'li statik dosyalarda yararlıdır.

```http
Cache-Control: public, max-age=31536000, immutable
```

```text
app.a83f1c.js
```

Dosya değiştiğinde adı/hash'i değişeceği için uzun süre cache edilebilir.

<a id="etag-ve-if-none-match"></a>
### 18.3. ETag ve If-None-Match

Sunucu kaynağın sürümünü temsil eden ETag döndürür:

```http
ETag: "product-15-v7"
```

Sonraki istek:

```http
If-None-Match: "product-15-v7"
```

Kaynak değişmediyse:

```http
HTTP/1.1 304 Not Modified
ETag: "product-15-v7"
```

Body gönderilmediği için trafik azalır. ETag concurrency kontrolünde de kullanılabilir:

```http
If-Match: "product-15-v7"
```

Başka biri kaynağı değiştirmişse ETag artık eşleşmez ve sunucu `412 Precondition Failed` dönebilir.

<a id="last-modified-ve-if-modified-since"></a>
### 18.4. Last-Modified ve If-Modified-Since

Sunucu:

```http
Last-Modified: Fri, 31 Jul 2026 10:00:00 GMT
```

İstemci:

```http
If-Modified-Since: Fri, 31 Jul 2026 10:00:00 GMT
```

Değişiklik yoksa `304 Not Modified` döner. ETag genellikle daha hassas doğrulama sağlar; Last-Modified zaman çözünürlüğü ve saat davranışlarına bağlıdır.

#### Vary header'ı

Cevabın hangi request header'larına göre farklılaşabileceğini cache'e bildirir.

```http
Vary: Accept-Encoding, Origin
```

Örneğin gzip ve Brotli cevapları veya farklı origin'lere göre CORS cevapları ayrı cache entry olarak tutulmalıdır.

---

<a id="content-negotiation-ve-compression"></a>
## 19. Content Negotiation ve Compression

Content negotiation, istemci ve sunucunun uygun temsil üzerinde anlaşmasıdır.

### Media type negotiation

İstemci:

```http
Accept: application/json
```

Sunucu:

```http
Content-Type: application/json
```

### Dil anlaşması

İstemci:

```http
Accept-Language: tr-TR,tr;q=0.9,en;q=0.8
```

Sunucu Türkçe içerik dönebilir:

```http
Content-Language: tr
```

`q` değeri tercih önceliğini belirtir.

### Sıkıştırma anlaşması

İstemci:

```http
Accept-Encoding: br, gzip
```

Sunucu:

```http
Content-Encoding: br
Vary: Accept-Encoding
```

Yaygın yöntemler:

- gzip
- Brotli (`br`)
- zstd

Sıkıştırma metin tabanlı dosyalarda ciddi kazanç sağlar:

- HTML
- CSS
- JavaScript
- JSON
- SVG

JPEG, PNG, MP4 veya ZIP gibi zaten sıkıştırılmış içeriklerde ek kazanç sınırlı olabilir.

---

<a id="frontend-backend-iletisim-ornekleri"></a>
## 20. Frontend–Backend İletişim Örnekleri

<a id="get-istegi-ornegi"></a>
### 20.1. GET İsteği

Frontend:

```javascript
async function getProducts() {
  const response = await fetch("https://api.example.com/products");

  if (!response.ok) {
    throw new Error(`Ürünler alınamadı: ${response.status}`);
  }

  return response.json();
}
```

`response.ok`, status code `200–299` aralığındaysa `true` olur. Backend response:

```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "id": 1,
    "name": "Laptop",
    "price": 35000
  },
  {
    "id": 2,
    "name": "Monitor",
    "price": 8000
  }
]
```

Önemli nokta: `fetch()` 404 veya 500 cevabında otomatik olarak promise rejection oluşturmaz. Ağ hatası dışında response gelir ve status code ayrıca kontrol edilmelidir.

<a id="post-istegi-ornegi"></a>
### 20.2. POST İsteği

Frontend:

```javascript
async function createProduct(product) {
  const response = await fetch("https://api.example.com/products", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Accept: "application/json",
    },
    body: JSON.stringify(product),
  });

  const data = await response.json();

  if (!response.ok) {
    throw new Error(data.message ?? "Ürün oluşturulamadı.");
  }

  return data;
}
```

Gönderilen veri:

```json
{
  "name": "Keyboard",
  "price": 2500
}
```

Backend başarılı cevap:

```http
HTTP/1.1 201 Created
Content-Type: application/json
Location: /products/73

{
  "id": 73,
  "name": "Keyboard",
  "price": 2500
}
```

<a id="login-akisi"></a>
### 20.3. Login Akışı

#### Adım 1: Login request

```http
POST /api/auth/login HTTP/1.1
Content-Type: application/json

{
  "email": "ozge@example.com",
  "password": "example-password"
}
```

#### Adım 2: Backend doğrulama

Backend:

- kullanıcıyı bulur,
- password hash kontrolü yapar,
- kullanıcı aktif mi kontrol eder,
- session veya token üretir.

#### Seçenek A: HttpOnly cookie

```http
HTTP/1.1 200 OK
Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=Lax; Path=/
Content-Type: application/json

{
  "user": {
    "id": 15,
    "name": "Özge"
  }
}
```

Sonraki istek:

```javascript
fetch("https://api.example.com/profile", {
  credentials: "include",
});
```

#### Seçenek B: Bearer token

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "accessToken": "eyJhbGciOi...",
  "expiresIn": 900
}
```

Sonraki istek:

```javascript
fetch("https://api.example.com/profile", {
  headers: {
    Authorization: `Bearer ${accessToken}`,
  },
});
```

#### Hata cevapları

Yanlış şifre:

```http
401 Unauthorized
```

Hesap kapalıysa tasarıma göre:

```http
403 Forbidden
```

Doğrulama problemi:

```http
400 Bad Request
```

Güvenlik için login cevabında “Bu e-posta sistemde yok” ve “Şifre yanlış” şeklinde aşırı ayrıntılı ayrım yapmak kullanıcı enumerasyonu riskini artırabilir. Genel mesaj tercih edilebilir:

```json
{
  "message": "E-posta veya şifre hatalı."
}
```

<a id="dosya-yukleme"></a>
### 20.4. Dosya Yükleme

Frontend:

```javascript
async function uploadFile(file) {
  const formData = new FormData();
  formData.append("file", file);

  const response = await fetch("https://api.example.com/files", {
    method: "POST",
    body: formData,
  });

  if (response.status === 413) {
    throw new Error("Dosya boyutu izin verilen sınırı aşıyor.");
  }

  if (!response.ok) {
    throw new Error("Dosya yüklenemedi.");
  }

  return response.json();
}
```

Backend'in kontrol etmesi gerekenler:

- Dosya boyutu
- MIME type
- Gerçek dosya içeriği/signature
- Dosya adı güvenliği
- Zararlı içerik taraması
- Depolama kotası
- Kullanıcı yetkisi

Yalnızca frontend dosya uzantısı kontrolüne güvenilmemelidir.

---

<a id="rest-api-tasariminda-http-kullanimi"></a>
## 21. REST API Tasarımında HTTP Kullanımı

REST, HTTP ile aynı şey değildir; ancak HTTP'nin kaynak, method, status code, header ve cache özelliklerinden yararlanan bir mimari yaklaşımdır.

### Kaynak isimleri isim olmalıdır

Tercih edilen:

```http
GET /api/users
GET /api/users/15
POST /api/users
DELETE /api/users/15
```

Daha zayıf tasarım:

```http
GET /api/getUsers
POST /api/createUser
POST /api/deleteUser
```

HTTP metodu zaten eylemi ifade eder. URL kaynağı temsil etmelidir.

### Tutarlı çoğul isimlendirme

```text
/users
/products
/orders
```

Tekil veya çoğul seçilebilir; önemli olan tutarlılıktır.

### Nested resource kullanımı

```http
GET /api/users/15/orders
GET /api/orders/28/items
```

Aşırı derin URL'lerden kaçınılmalıdır:

```text
/users/15/orders/28/items/4/comments/9/replies
```

### Filtreleme ve sayfalama

```http
GET /api/products?category=computer&minPrice=10000&page=2&pageSize=20
```

### Doğru status code

```text
GET başarılı              → 200
POST ile kaynak oluştu     → 201
DELETE başarılı, body yok  → 204
Geçersiz veri              → 400 veya 422
Authentication yok         → 401
Yetki yok                  → 403
Kaynak yok                 → 404
Çakışma                    → 409
Rate limit                 → 429
Sunucu hatası              → 500
```

### Location header kullanımı

```http
HTTP/1.1 201 Created
Location: /api/orders/125
```

### API versioning

URL üzerinden:

```http
GET /api/v1/users
```

Header üzerinden:

```http
Accept: application/vnd.example.v2+json
```

Versioning stratejisi, geriye uyumluluk ve bakım maliyeti dikkate alınarak seçilmelidir.

### Pagination metadata

Response body içinde:

```json
{
  "items": [],
  "page": 2,
  "pageSize": 20,
  "totalItems": 184,
  "totalPages": 10
}
```

veya header:

```http
X-Total-Count: 184
```

Cross-origin frontend bu özel header'ı okuyacaksa:

```http
Access-Control-Expose-Headers: X-Total-Count
```

---

<a id="hata-yonetimi-ve-standart-api-cevabi"></a>
## 22. Hata Yönetimi ve Standart API Cevabı

Frontend'in hataları kolay işleyebilmesi için backend tutarlı bir hata formatı döndürmelidir. Örnek standart hata cevabı:

```json
{
  "type": "https://example.com/problems/validation-error",
  "title": "Validation Error",
  "status": 422,
  "detail": "Gönderilen alanlardan bazıları geçersiz.",
  "instance": "/api/users",
  "traceId": "00-4bf92f3577b34da6-00f067aa0ba902b7-01",
  "errors": {
    "email": [
      "Geçerli bir e-posta adresi girilmelidir."
    ],
    "password": [
      "Şifre en az 8 karakter olmalıdır."
    ]
  }
}
```

Bu yapı RFC 9457 Problem Details yaklaşımına benzer bir hata modeli sağlar. Frontend hata yönetimi örneği:

```javascript
async function request(url, options) {
  const response = await fetch(url, options);

  if (response.status === 204) {
    return null;
  }

  const contentType = response.headers.get("content-type") ?? "";
  const isJson = contentType.includes("application/json");
  const data = isJson ? await response.json() : await response.text();

  if (!response.ok) {
    const error = new Error(
      typeof data === "object" && data?.detail
        ? data.detail
        : "İstek başarısız oldu."
    );

    error.status = response.status;
    error.data = data;
    throw error;
  }

  return data;
}
```

Status code'a göre olası frontend davranışları:

| Status | Frontend davranışı |
|---|---|
| 400/422 | Form alanı hatalarını göster |
| 401 | Oturumu yenile veya login'e yönlendir |
| 403 | Yetkiniz yok mesajı göster |
| 404 | Kayıt bulunamadı ekranı göster |
| 409 | Çakışma mesajını açıkla |
| 429 | Retry-After'a göre bekle |
| 500 | Genel hata mesajı ve trace ID göster |
| 502/503/504 | Geçici servis problemi; kontrollü retry düşünülebilir |

### Her hatada otomatik retry yapılmamalıdır

- 400 için retry anlamsızdır; veri düzeltilmelidir.
- 401 için token yenileme denenebilir.
- 429 için `Retry-After` dikkate alınmalıdır.
- 503 veya 504 için sınırlı retry yapılabilir.
- POST gibi idempotent olmayan işlemler körlemesine tekrar edilmemelidir.

### Exponential backoff

Retry aralıkları giderek artırılır:

```text
1. deneme sonrası 1 saniye
2. deneme sonrası 2 saniye
3. deneme sonrası 4 saniye
4. deneme sonrası 8 saniye
```

Sistemde aynı anda çok sayıda istemcinin tekrar denemesini önlemek için jitter eklenebilir.

---

<a id="tarayici-devtools-ile-http-inceleme"></a>
## 23. Tarayıcı DevTools ile HTTP İnceleme

Chrome/Edge DevTools içindeki **Network** sekmesi HTTP sorunlarını anlamanın en önemli araçlarından biridir.

### İncelenecek alanlar

#### Name

İsteğin hedef kaynağı.

#### Status

HTTP status code.

#### Type

Fetch, xhr, document, stylesheet, script, image gibi kaynak türü.

#### Initiator

İsteği hangi kod veya kaynak başlatmış.

#### Size

Transfer edilen veri boyutu ve cache bilgisi.

#### Time / Waterfall

DNS, bağlantı, TLS, request gönderme, sunucu bekleme ve download süreleri.

### Headers sekmesi

Aşağıdaki bilgiler görülür:

- Request URL
- Request Method
- Status Code
- Remote Address
- Referrer Policy
- Request Headers
- Response Headers
- Query String Parameters

### Payload sekmesi

- Request JSON
- Form data
- Query parametreleri
- Multipart alanları

### Preview ve Response sekmesi

Sunucudan dönen body incelenir.

### Timing sekmesi

Yaklaşık aşamalar:

- Queueing
- Stalled
- DNS Lookup
- Initial Connection
- SSL
- Request Sent
- Waiting for Server Response / TTFB
- Content Download

TTFB yüksekse backend, veri tabanı, ağ veya upstream servis yavaş olabilir. Content Download yüksekse response boyutu veya ağ hızı incelenmelidir.

### Preserve log

Sayfa yönlendirmesi veya yenileme olduğunda isteklerin kaybolmaması için kullanılabilir.

### Disable cache

DevTools açıkken cache etkisini kaldırarak test yapmayı sağlar.

### Copy as cURL

Network isteğine sağ tıklayıp “Copy as cURL” ile istek terminalde tekrar üretilebilir. Frontend kaynaklı mı backend kaynaklı mı anlamak için oldukça yararlıdır.

Örnek:

```bash
curl 'https://api.example.com/products/15' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer token-value'
```

### CORS hatası incelerken kontrol listesi

1. OPTIONS isteği var mı?
2. OPTIONS status code nedir?
3. `Origin` doğru mu?
4. `Access-Control-Allow-Origin` geliyor mu?
5. Method allow list içinde mi?
6. Authorization ve Content-Type izinli mi?
7. Credentials ayarları eşleşiyor mu?
8. Asıl request gönderilmiş mi?
9. Response redirect olmuş mu?
10. Backend loglarında gerçek hata var mı?

---

<a id="http-guvenligi-acisindan-temel-noktalar"></a>
## 24. HTTP Güvenliği Açısından Temel Noktalar

### Her zaman HTTPS kullan

Token, cookie ve kullanıcı verileri HTTP üzerinden gönderilmemelidir.

### Hassas verileri URL'ye koyma

Yanlış:

```text
GET /reset-password?token=secret-token&newPassword=123456
```

URL loglanabilir ve geçmişte saklanabilir.

### Authentication ve authorization'ı backend'de uygula

Frontend'de butonu gizlemek güvenlik değildir. Kullanıcı doğrudan endpoint'e istek gönderebilir.

### Input validation yap

Frontend validation kullanıcı deneyimi içindir. Güvenlik açısından backend her girdiyi tekrar doğrulamalıdır.

### Hata cevaplarında gizli bilgi sızdırma

Gönderilmemesi gerekenler:

- Stack trace
- SQL sorguları
- Veri tabanı bağlantı bilgileri
- Dosya yolları
- Secret key
- Token
- Sistem iç mimarisi

### CORS allowlist kullan

Hassas credentialed API'lerde yalnızca gerekli origin'lere izin verilmelidir.

### Origin yansıtmayı doğrulamadan yapma

Tehlikeli örnek:

```text
Access-Control-Allow-Origin: request.headers.origin
```

Her origin'i kontrolsüz kabul etmek allowlist'i anlamsızlaştırır.

### Cookie güvenlik attribute'larını ayarla

```http
Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=Lax
```

### Rate limiting uygula

Özellikle:

- Login
- Password reset
- OTP
- Public API
- Arama
- Dosya yükleme

### Request boyutu sınırla

Çok büyük body ve dosyalar kaynak tüketimine neden olabilir.

### Güvenlik header'larını kullan

- HSTS
- CSP
- X-Content-Type-Options
- Referrer-Policy
- Permissions-Policy

### GET ile veri değiştirme

GET endpoint'leri safe semantiğe uymalıdır. Linke tıklama, prefetch veya crawler kritik işlem başlatmamalıdır.

### Loglarda hassas veriyi maskele

Loglanmaması veya maskelenmesi gerekenler:

- Authorization header
- Cookie
- Password
- Refresh token
- Kredi kartı verisi
- Kimlik numarası

### Request smuggling ve header parsing

Proxy ve backend HTTP mesaj sınırlarını farklı yorumlarsa request smuggling riski doğabilir. Güncel, standart uyumlu proxy ve sunucu kullanmak; çelişkili `Content-Length`/`Transfer-Encoding` mesajlarını reddetmek önemlidir.

---

<a id="sik-yapilan-hatalar"></a>
## 25. Sık Yapılan Hatalar

### 1. Her başarılı işlemde 200 dönmek

Yeni kaynak için 201, body olmayan cevap için 204 daha açıklayıcı olabilir.

### 2. Her hatada 500 dönmek

Kullanıcı geçersiz alan gönderdiğinde 500 değil 400 veya 422 dönülmelidir. 500 sunucu hatasını ifade eder.

### 3. 401 ve 403'ü karıştırmak

- 401: authentication yok veya geçersiz.
- 403: kullanıcı biliniyor fakat yetkisi yok.

### 4. 404 cevabında HTML dönmek

Frontend JSON beklerken backend framework'ün varsayılan HTML hata sayfasını döndürürse `response.json()` parse hatası oluşur. API hata formatı tutarlı olmalıdır.

### 5. 204 cevabını JSON parse etmeye çalışmak

```javascript
const data = await response.json();
```

204'te body olmadığı için hata oluşabilir.

### 6. Fetch'in 404/500'de reject olacağını sanmak

Fetch yalnızca ağ seviyesinde başarısızlıkta reject olabilir. HTTP hata kodları için `response.ok` kontrolü yapılmalıdır.

### 7. CORS'u frontend'de çözmeye çalışmak

CORS izinleri backend veya reverse proxy tarafından doğru response header'larıyla verilmelidir.

### 8. no-cors kullanınca problemi çözdüğünü sanmak

Opaque response nedeniyle body ve status okunamaz.

### 9. Postman çalışıyor, tarayıcı çalışmıyor diye backend sağlam sanmak

Postman tarayıcı Same-Origin Policy uygulamaz. CORS problemi yalnızca tarayıcıda görülebilir.

### 10. `Access-Control-Allow-Origin: *` değerini her yerde kullanmak

Public ve credentials gerektirmeyen kaynaklarda uygun olabilir. Hassas veya cookie kullanan sistemlerde kontrollü allowlist gerekir.

### 11. FormData ile Content-Type'ı elle belirlemek

Boundary eksik kalabilir. Tarayıcının otomatik belirlemesine izin verilmelidir.

### 12. Token'ı query string'e koymak

Token URL loglarına sızabilir. Authorization header veya güvenli cookie tercih edilmelidir.

### 13. İdempotent olmayan POST'u kontrolsüz retry etmek

Çift ödeme, çift sipariş veya çift kayıt oluşabilir.

### 14. Cache'i tamamen görmezden gelmek

Eski veri, beklenmeyen 304 davranışı veya güncellenmeyen frontend dosyaları ortaya çıkabilir.

### 15. Yalnızca frontend validation'a güvenmek

İstemci kontrolü atlanabilir. Backend validation zorunludur.

### 16. CORS ile CSRF'yi aynı şey sanmak

CORS response okuma politikasını, CSRF ise kullanıcı adına istek yaptırma saldırısını ilgilendirir.

### 17. Header isimlerini ve body formatını dokümante etmemek

Frontend ve backend arasında entegrasyon hataları artar.

### 18. Hata cevabında yalnızca mesaj dönmek

Makine tarafından işlenebilir `code`, `status`, `fieldErrors` ve `traceId` alanları hata yönetimini kolaylaştırır.

### 19. Proxy arkasında gerçek protokolü yanlış anlamak

Backend bağlantıyı HTTP görebilir; fakat kullanıcı dışarıdan HTTPS ile bağlanmıştır. Güvenilir proxy ve forwarded header yapılandırması doğru yapılmalıdır.

### 20. Çok büyük response dönmek

Sayfalama, filtreleme, alan seçimi, sıkıştırma ve streaming düşünülmelidir.

---

<a id="mulakat-sorulari-ve-kisa-cevaplar"></a>
## 26. Mülakat Soruları ve Kısa Cevaplar

### 1. HTTP nedir?

HTTP, istemci ile sunucu arasında request–response modeliyle kaynak ve işlem bilgisi taşıyan uygulama katmanı protokolüdür.

### 2. HTTP request hangi bölümlerden oluşur?

Method ve hedefi içeren request line, request header'ları, boş satır ve opsiyonel request body'den oluşur.

### 3. HTTP response hangi bölümlerden oluşur?

Status line, response header'ları, boş satır ve opsiyonel response body'den oluşur.

### 4. GET ve POST arasındaki temel fark nedir?

GET kaynak okumak için safe ve idempotent bir metottur. POST ise genellikle kaynak oluşturmak veya işlem başlatmak için kullanılır ve varsayılan olarak idempotent değildir.

### 5. PUT ve PATCH farkı nedir?

PUT genellikle kaynağın bütün temsilini değiştirmek için; PATCH ise belirli alanlarını kısmi olarak güncellemek için kullanılır.

### 6. Safe HTTP method nedir?

İstemcinin sunucu durumunu değiştirmeyi talep etmediği metottur. GET, HEAD, OPTIONS ve QUERY örnektir.

### 7. Idempotent ne demektir?

Aynı isteğin birden fazla uygulanmasının hedeflenen nihai sunucu durumunu ilk uygulamaya göre değiştirmemesidir.

### 8. 200 ve 201 farkı nedir?

200 genel başarıyı, 201 yeni bir kaynak oluşturulduğunu ifade eder.

### 9. 204 ne zaman kullanılır?

İşlem başarılı olduğunda ancak response body gönderilmeyeceğinde kullanılır.

### 10. 400 ve 422 farkı nedir?

400 genel request biçimi veya doğrulama hatası için; 422 request yapısı anlaşılır olduğu hâlde içeriğin semantik kurallara uymaması için kullanılabilir.

### 11. 401 ve 403 farkı nedir?

401 geçerli kimlik doğrulama olmadığını, 403 kimlik bilinse bile işlem için yetki bulunmadığını ifade eder.

### 12. 404 ve 410 farkı nedir?

404 kaynağın bulunamadığını; 410 kaynağın daha önce var olup kalıcı olarak kaldırıldığını belirtir.

### 13. 502 ve 504 farkı nedir?

502 gateway'in upstream'den geçerli cevap alamadığını, 504 ise upstream'i beklerken zaman aşımına uğradığını belirtir.

### 14. CORS nedir?

Tarayıcının bir origin'deki JavaScript'in başka origin'deki response'a erişimini sunucunun HTTP header'larıyla kontrollü biçimde açmasını sağlayan mekanizmadır.

### 15. Origin hangi parçalardan oluşur?

Scheme, host ve port.

### 16. Same-Origin Policy nedir?

Tarayıcının farklı origin'ler arasında JavaScript erişimini varsayılan olarak sınırlandıran güvenlik politikasıdır.

### 17. Preflight request nedir?

Tarayıcının gerçek cross-origin isteğinden önce OPTIONS methoduyla sunucudan method ve header izni istediği kontroldür.

### 18. Hangi durumlarda preflight oluşabilir?

PUT/PATCH/DELETE kullanıldığında, application/json body gönderildiğinde, Authorization veya özel header kullanıldığında oluşabilir.

### 19. CORS hatası neden Postman'de görülmeyebilir?

Çünkü CORS'u tarayıcı Same-Origin Policy kapsamında uygular. Postman tarayıcı değildir.

### 20. `Access-Control-Allow-Origin: *` ile credentials kullanılabilir mi?

Hayır. Credentials için spesifik origin ve `Access-Control-Allow-Credentials: true` gerekir.

### 21. `mode: "no-cors"` CORS sorununu çözer mi?

Genellikle hayır. Response opaque olur ve JavaScript body, header ve status bilgisine erişemez.

### 22. Content-Type ve Accept farkı nedir?

Content-Type gönderilen body'nin formatını, Accept ise istemcinin kabul ettiği response formatını belirtir.

### 23. Cookie ile session arasındaki ilişki nedir?

Session verisi sunucuda tutulabilir; tarayıcı çoğunlukla session ID'yi cookie içinde taşır.

### 24. HttpOnly ne işe yarar?

JavaScript'in cookie'yi okumasını engelleyerek XSS sonucu cookie çalınması riskini azaltır.

### 25. Secure cookie ne işe yarar?

Cookie'nin yalnızca HTTPS üzerinden gönderilmesini sağlar.

### 26. SameSite ne işe yarar?

Cookie'nin cross-site isteklerde ne zaman gönderileceğini kontrol eder ve CSRF riskini azaltmaya yardımcı olur.

### 27. ETag ne işe yarar?

Kaynağın belirli sürümünü tanımlar; cache validation ve optimistic concurrency için kullanılabilir.

### 28. 304 ne anlama gelir?

Cache'deki temsil değişmemiştir; istemci mevcut kopyayı kullanabilir ve response body gönderilmez.

### 29. HTTP/2'nin temel avantajı nedir?

Tek TCP bağlantısında multiplexing, binary framing ve header compression ile daha verimli iletişim sağlar.

### 30. HTTP/3'ün HTTP/2'den temel farkı nedir?

HTTP/3 TCP yerine QUIC kullanır ve stream seviyesinde paket kaybı etkisini azaltmayı hedefler.

### 31. HTTPS ne sağlar?

Trafiğin gizliliğini, bütünlüğünü ve sunucu kimliğinin sertifika ile doğrulanmasını sağlar.

### 32. Fetch neden 404'te catch'e düşmeyebilir?

Çünkü 404 geçerli bir HTTP response'dur. Fetch promise'i ağ hatası olmadıkça resolve olabilir; `response.ok` kontrol edilmelidir.

### 33. 429 durumunda ne yapılmalıdır?

`Retry-After` header'ı dikkate alınmalı, kontrollü retry ve exponential backoff kullanılmalıdır.

### 34. API'de hata response'u nasıl olmalıdır?

Tutarlı status code, makine tarafından okunabilir hata kodu, kullanıcı mesajı, alan bazlı validation hataları ve trace ID içermelidir.

### 35. CORS authentication yerine geçer mi?

Hayır. CORS tarayıcı response erişimini kontrol eder. Endpoint her durumda backend tarafında authentication ve authorization uygulamalıdır.

---

<a id="genel-sonuc"></a>
## 27. Genel Sonuç

HTTP, frontend ile backend arasındaki iletişimin temel dilidir. Bir frontend geliştiricisinin yalnızca API adresini çağırmayı değil, gönderilen isteğin ve alınan cevabın bütün parçalarını anlaması gerekir. Bu raporda ele alınan temel noktalar şunlardır:

- HTTP istemci–sunucu ve request–response modeline dayanır.
- Request; method, hedef, header ve opsiyonel body taşır.
- Response; status code, header ve opsiyonel body taşır.
- GET, POST, PUT, PATCH ve DELETE yalnızca CRUD karşılıkları değil, farklı semantik özelliklere sahip metotlardır.
- Safe ve idempotent kavramları retry, cache ve güvenli API tasarımı açısından önemlidir.
- Status code'lar frontend'e işlemin nasıl sonuçlandığını standart biçimde bildirir.
- 401 authentication, 403 authorization, 409 durum çakışması, 422 semantik validation ve 500 sunucu hatası gibi ayrımlar doğru yapılmalıdır.
- Header'lar içerik formatı, authentication, cache, CORS ve güvenlik bilgilerini taşır.
- HTTP stateless olduğu için session, cookie veya token gibi oturum mekanizmaları gerekir.
- CORS, Same-Origin Policy üzerine kuruludur ve sunucunun belirli origin'lere tarayıcı erişimi vermesini sağlar.
- Preflight, tarayıcının gerçek istekten önce OPTIONS ile izin kontrolü yapmasıdır.
- CORS, authentication veya authorization yerine geçmez ve tek başına CSRF koruması değildir.
- HTTPS, HTTP trafiğine gizlilik, bütünlük ve sunucu doğrulaması ekler.
- HTTP/2 ve HTTP/3, temel HTTP semantiğini korurken performans ve bağlantı kullanımını geliştirir.
- Cache, ETag, 304, compression ve content negotiation web performansının önemli parçalarıdır.
- DevTools Network paneli, frontend–backend iletişim sorunlarını teşhis etmek için temel araçtır.

Bu bilgiler kavrandığında geliştirici yalnızca “istek çalıştı mı?” sorusuna değil, aşağıdaki sorulara da cevap verebilir:

- İstek gerçekten hangi URL ve method ile gönderildi?
- Hangi header'lar taşındı?
- Body doğru formatta mıydı?
- Backend neden 400, 401, 403 veya 422 döndürdü?
- CORS hatası preflight aşamasında mı oluştu?
- Cookie neden gönderilmedi?
- Response neden cache'den geldi?
- 304 neden body içermiyor?
- 502 ile 504 arasındaki fark ne?
- İstek neden yavaş?
- Hata frontend, backend, proxy, ağ veya tarayıcı politikasının hangi katmanında?

Dolayısıyla HTTP bilgisi, frontend ve backend'in birbirinden kopuk iki alan olmadığını; aynı iletişim sözleşmesinin iki tarafı olduğunu anlamayı sağlar.