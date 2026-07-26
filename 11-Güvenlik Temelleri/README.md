# 11. Hafta Raporu: Güvenlik Temelleri — Security Basics

## İçindekiler

- [1. Giriş](#1-giriş)
- [2. Yazılım Güvenliğinin Temel Amacı](#2-yazılım-güvenliğinin-temel-amacı)
  - [2.1. Confidentiality — Gizlilik](#21-confidentiality--gizlilik)
  - [2.2. Integrity — Bütünlük](#22-integrity--bütünlük)
  - [2.3. Availability — Erişilebilirlik](#23-availability--erişilebilirlik)

- [3. Authentication — Kimlik Doğrulama](#3-authentication--kimlik-doğrulama)
  - [3.1. Authentication Nedir?](#31-authentication-nedir)
  - [3.2. Authentication Faktörleri](#32-authentication-faktörleri)
    - [Bilinen bir şey](#bilinen-bir-şey)
    - [Sahip olunan bir şey](#sahip-olunan-bir-şey)
    - [Kullanıcıya ait bir özellik](#kullanıcıya-ait-bir-özellik)
  - [3.3. MFA — Multi-Factor Authentication](#33-mfa--multi-factor-authentication)
  - [3.4. Güvenli Authentication Akışı](#34-güvenli-authentication-akışı)
  - [3.5. Parolalar Nasıl Saklanmalıdır?](#35-parolalar-nasıl-saklanmalıdır)
    - [Hashing](#hashing)
    - [Salt](#salt)
    - [Pepper](#pepper)
  - [3.6. Authentication Sistemlerine Yönelik Saldırılar](#36-authentication-sistemlerine-yönelik-saldırılar)
    - [Brute Force](#brute-force)
    - [Credential Stuffing](#credential-stuffing)
    - [Password Spraying](#password-spraying)
    - [User Enumeration](#user-enumeration)
    - [Session Hijacking](#session-hijacking)
    - [Session Fixation](#session-fixation)

- [4. Authorization — Yetkilendirme](#4-authorization--yetkilendirme)
  - [4.1. Authorization Nedir?](#41-authorization-nedir)
  - [4.2. Yetkilendirme Nerede Yapılmalıdır?](#42-yetkilendirme-nerede-yapılmalıdır)
  - [4.3. Yetkilendirme Modelleri](#43-yetkilendirme-modelleri)
    - [RBAC — Role-Based Access Control](#rbac--role-based-access-control)
    - [ABAC — Attribute-Based Access Control](#abac--attribute-based-access-control)
    - [ACL — Access Control List](#acl--access-control-list)
    - [ReBAC — Relationship-Based Access Control](#rebac--relationship-based-access-control)
  - [4.4. Least Privilege — En Az Yetki İlkesi](#44-least-privilege--en-az-yetki-i̇lkesi)
  - [4.5. Deny by Default](#45-deny-by-default)
  - [4.6. IDOR — Insecure Direct Object Reference](#46-idor--insecure-direct-object-reference)

- [5. Authentication ve Authorization Arasındaki Fark](#5-authentication-ve-authorization-arasındaki-fark)
  - [401 ve 403 Farkı](#401-ve-403-farkı)
    - [401 Unauthorized](#401-unauthorized)
    - [403 Forbidden](#403-forbidden)

- [6. Oturum ve Session Yönetimi](#6-oturum-ve-session-yönetimi)
  - [6.1. Server-Side Session](#61-server-side-session)
    - [Avantajları](#avantajları)
    - [Dezavantajları](#dezavantajları)
  - [6.2. Güvenli Cookie Ayarları](#62-güvenli-cookie-ayarları)
    - [HttpOnly](#httponly)
    - [Secure](#secure)
    - [SameSite](#samesite)
    - [Path ve Domain](#path-ve-domain)
  - [6.3. Session Güvenliği İçin Kurallar](#63-session-güvenliği-i̇çin-kurallar)

- [7. JWT — JSON Web Token](#7-jwt--json-web-token)
  - [7.1. JWT Nedir?](#71-jwt-nedir)
  - [7.2. JWT Yapısı](#72-jwt-yapısı)
    - [Header](#header)
    - [Payload](#payload)
    - [Signature](#signature)
  - [7.3. JWT Claim Türleri](#73-jwt-claim-türleri)
    - [Registered Claims](#registered-claims)
    - [Public Claims](#public-claims)
    - [Private Claims](#private-claims)
  - [7.4. JWT Nasıl Çalışır?](#74-jwt-nasıl-çalışır)
  - [7.5. JWT İmzalama Algoritmaları](#75-jwt-i̇mzalama-algoritmaları)
    - [Simetrik Algoritmalar](#simetrik-algoritmalar)
    - [Asimetrik Algoritmalar](#asimetrik-algoritmalar)
  - [7.6. JWT Doğrulamasında Kontrol Edilmesi Gerekenler](#76-jwt-doğrulamasında-kontrol-edilmesi-gerekenler)
  - [7.7. Access Token ve Refresh Token](#77-access-token-ve-refresh-token)
    - [Access Token](#access-token)
    - [Refresh Token](#refresh-token)
    - [Refresh Token Rotation](#refresh-token-rotation)
  - [7.8. JWT Nerede Saklanmalıdır?](#78-jwt-nerede-saklanmalıdır)
    - [LocalStorage](#localstorage)
    - [HttpOnly Cookie](#httponly-cookie)
    - [Memory](#memory)
  - [7.9. JWT Kullanmanın Avantajları](#79-jwt-kullanmanın-avantajları)
  - [7.10. JWT Kullanmanın Dezavantajları](#710-jwt-kullanmanın-dezavantajları)

- [8. OAuth 2.0 Mantığı](#8-oauth-20-mantığı)
  - [8.1. OAuth Nedir?](#81-oauth-nedir)
  - [8.2. OAuth Neden Gereklidir?](#82-oauth-neden-gereklidir)
  - [8.3. OAuth Rolleri](#83-oauth-rolleri)
    - [Resource Owner](#resource-owner)
    - [Client](#client)
    - [Authorization Server](#authorization-server)
    - [Resource Server](#resource-server)
  - [8.4. Authorization Code Flow](#84-authorization-code-flow)
    - [Akış](#akış)
  - [8.5. PKCE Nedir?](#85-pkce-nedir)
  - [8.6. Scope Nedir?](#86-scope-nedir)
  - [8.7. Consent Nedir?](#87-consent-nedir)
  - [8.8. State Parametresi](#88-state-parametresi)
  - [8.9. Redirect URI Güvenliği](#89-redirect-uri-güvenliği)
  - [8.10. Eski ve Riskli OAuth Akışları](#810-eski-ve-riskli-oauth-akışları)
    - [Implicit Grant](#implicit-grant)
    - [Resource Owner Password Credentials Grant](#resource-owner-password-credentials-grant)

- [9. OpenID Connect ve OAuth Farkı](#9-openid-connect-ve-oauth-farkı)
  - [Kritik Hata](#kritik-hata)

- [10. SQL Injection](#10-sql-injection)
  - [10.1. SQL Injection Nedir?](#101-sql-injection-nedir)
  - [10.2. Güvensiz SQL Sorgusu](#102-güvensiz-sql-sorgusu)
  - [10.3. SQL Injection Sonuçları](#103-sql-injection-sonuçları)
  - [10.4. SQL Injection Türleri](#104-sql-injection-türleri)
    - [In-Band SQL Injection](#in-band-sql-injection)
    - [Error-Based SQL Injection](#error-based-sql-injection)
    - [Union-Based SQL Injection](#union-based-sql-injection)
    - [Blind SQL Injection](#blind-sql-injection)
      - [Boolean-Based Blind](#boolean-based-blind)
      - [Time-Based Blind](#time-based-blind)
    - [Out-of-Band SQL Injection](#out-of-band-sql-injection)
  - [10.5. SQL Injection Nasıl Önlenir?](#105-sql-injection-nasıl-önlenir)
    - [Parametreli Sorgular](#parametreli-sorgular)
    - [Prepared Statements](#prepared-statements)
    - [ORM Kullanımı](#orm-kullanımı)
    - [Allow-List Validation](#allow-list-validation)
    - [En Az Yetkili Veri Tabanı Kullanıcısı](#en-az-yetkili-veri-tabanı-kullanıcısı)
    - [Hata Mesajlarını Gizleme](#hata-mesajlarını-gizleme)
    - [Input Validation](#input-validation)
    - [WAF](#waf)
  - [10.6. Parolayı SQL Sorgusunda Aramamak](#106-parolayı-sql-sorgusunda-aramamak)

- [11. Cross-Site Scripting — XSS](#11-cross-site-scripting--xss)
  - [11.1. XSS Nedir?](#111-xss-nedir)
  - [11.2. Güvensiz Örnek](#112-güvensiz-örnek)
  - [11.3. Reflected XSS](#113-reflected-xss)
  - [11.4. Stored XSS](#114-stored-xss)
  - [11.5. DOM-Based XSS](#115-dom - [11.4. Stored XSS](#114-stored-xss-based-xss)
  - [11.6. XSS Sonuçları](#116-xss-sonuçları)
  - [11.7. XSS Nasıl Önlenir?](#117-xss-nasıl-önlenir)
    - [Output Encoding](#output-encoding)
    - [Güvenli DOM API’leri](#güvenli-dom-apileri)
    - [HTML Sanitization](#html-sanitization)
    - [Framework Korumasını Devre Dışı Bırakmamak](#framework-korumasını-devre-dışı-bırakmamak)
    - [Content Security Policy — CSP](#content-security-policy--csp)
    - [HttpOnly Cookie](#httponly-cookie-1)
    - [Tehlikeli JavaScript Fonksiyonlarından Kaçınmak](#tehlikeli-javascript-fonksiyonlarından-kaçınmak)
    - [URL Doğrulama](#url-doğrulama)

- [12. SQL Injection ve XSS Karşılaştırması](#12-sql-injection-ve-xss-karşılaştırması)

- [13. Güvenli Bir Giriş Sisteminin Genel Akışı](#13-güvenli-bir-giriş-sisteminin-genel-akışı)
  - [13.1. Kayıt İşlemi](#131-kayıt-i̇şlemi)
  - [13.2. Giriş İşlemi](#132-giriş-i̇şlemi)
  - [13.3. Yetkili API İsteği](#133-yetkili-api-i̇steği)

- [14. Yaygın Güvenlik Hataları](#14-yaygın-güvenlik-hataları)
  - [14.1. Yalnızca Frontend’de Yetki Kontrolü Yapmak](#141-yalnızca-frontendde-yetki-kontrolü-yapmak)
  - [14.2. JWT’yi Yalnızca Decode Etmek](#142-jwtyi-yalnızca-decode-etmek)
  - [14.3. JWT İçerisine Parola Koymak](#143-jwt-i̇çerisine-parola-koymak)
  - [14.4. Çok Uzun Ömürlü Access Token Kullanmak](#144-çok-uzun-ömürlü-access-token-kullanmak)
  - [14.5. OAuth’u Authentication Sanmak](#145-oauthu-authentication-sanmak)
  - [14.6. Kullanıcı Rolünü İstemciden Kabul Etmek](#146-kullanıcı-rolünü-i̇stemciden-kabul-etmek)
  - [14.7. Input Validation’ı Tek Savunma Sanmak](#147-input-validationı-tek-savunma-sanmak)
  - [14.8. Hataları Kullanıcıya Ayrıntılı Göstermek](#148-hataları-kullanıcıya-ayrıntılı-göstermek)
  - [14.9. Gizli Bilgileri Kaynak Koda Yazmak](#149-gizli-bilgileri-kaynak-koda-yazmak)
  - [14.10. Her Kullanıcıya Fazla Yetki Vermek](#1410-her-kullanıcıya-fazla-yetki-vermek)
  - [14.11. Logout İşleminde Yalnızca Arayüzü Değiştirmek](#1411-logout-i̇şleminde-yalnızca-arayüzü-değiştirmek)

- [15. Güvenli Yazılım Geliştirme Kontrol Listesi](#15-güvenli-yazılım-geliştirme-kontrol-listesi)
  - [Authentication](#authentication)
  - [Authorization](#authorization)
  - [Session ve Token](#session-ve-token)
  - [SQL Injection](#sql-injection)
  - [XSS](#xss)

- [16. Mülakat Soruları ve Kısa Cevaplar](#16-mülakat-soruları-ve-kısa-cevaplar)
  - [Authentication ve authorization arasındaki fark nedir?](#authentication-ve-authorization-arasındaki-fark-nedir)
  - [Kullanıcı giriş yaptıysa neden yeniden authorization kontrolü gerekir?](#kullanıcı-giriş-yaptıysa-neden-yeniden-authorization-kontrolü-gerekir)
  - [JWT şifrelenmiş midir?](#jwt-şifrelenmiş-midir)
  - [JWT’nin üç bölümü nedir?](#jwtnin-üç-bölümü-nedir)
  - [JWT payload’ına parola koyulur mu?](#jwt-payloadına-parola-koyulur-mu)
  - [Access token ile refresh token arasındaki fark nedir?](#access-token-ile-refresh-token-arasındaki-fark-nedir)
  - [JWT neden kolayca iptal edilemez?](#jwt-neden-kolayca-iptal-edilemez)
  - [OAuth nedir?](#oauth-nedir)
  - [OAuth authentication sağlar mı?](#oauth-authentication-sağlar-mı)
  - [Access token ve ID token arasındaki fark nedir?](#access-token-ve-id-token-arasındaki-fark-nedir)
  - [PKCE neden kullanılır?](#pkce-neden-kullanılır)
  - [SQL Injection nedir?](#sql-injection-nedir)
  - [SQL Injection’a karşı en etkili temel savunma nedir?](#sql-injectiona-karşı-en-etkili-temel-savunma-nedir)
  - [Input validation SQL Injection’ı tamamen önler mi?](#input-validation-sql-injectionı-tamamen-önler-mi)
  - [ORM kullanmak SQL Injection’ı tamamen önler mi?](#orm-kullanmak-sql-injectionı-tamamen-önler-mi)
  - [XSS nedir?](#xss-nedir)
  - [XSS türleri nelerdir?](#xss-türleri-nelerdir)
  - [XSS’e karşı temel savunma nedir?](#xsse-karşı-temel-savunma-nedir)
  - [`innerHTML` neden risklidir?](#innerhtml-neden-risklidir)
  - [CSP tek başına XSS’i önler mi?](#csp-tek-başına-xssi-önler-mi)
  - [401 ve 403 arasındaki fark nedir?](#401-ve-403-arasındaki-fark-nedir)
  - [Frontend’de butonu gizlemek authorization sağlar mı?](#frontendde-butonu-gizlemek-authorization-sağlar-mı)
  - [IDOR nedir?](#idor-nedir)

- [17. Genel Sonuç](#17-genel-sonuç)

---

# 1. Giriş

Bir yazılımın yalnızca çalışması yeterli değildir. Yazılımın aynı zamanda kullanıcı bilgilerini, uygulama verilerini ve sistem kaynaklarını yetkisiz erişimlere karşı koruması gerekir.

Bir uygulama teknik olarak beklenen işlevleri yerine getiriyor olabilir. Ancak kullanıcı parolalarını açık biçimde saklıyor, giriş yapan her kullanıcının yönetici işlemlerine erişmesine izin veriyor veya kullanıcıdan alınan verileri doğrudan SQL sorgularına ekliyorsa bu uygulama çalışmasına rağmen güvenli değildir.

Güvenli yazılım geliştirme sürecinde temel olarak şu sorular sorulur:

* Sisteme erişmeye çalışan kişi gerçekten iddia ettiği kişi mi?
* Bu kullanıcının yapmak istediği işlem için yetkisi var mı?
* Kullanıcıdan gelen veriler güvenli biçimde işleniyor mu?
* Kullanıcı oturumu ele geçirilebilir mi?
* Veriler aktarılırken veya saklanırken korunuyor mu?
* Hatalı ya da kötü niyetli istekler sistemin davranışını değiştirebilir mi?
* Kullanıcının tarayıcısında saldırgan tarafından gönderilen kod çalıştırılabilir mi?

Bu sorular sırasıyla authentication, authorization, session yönetimi, token güvenliği, SQL Injection ve XSS gibi güvenlik konularıyla ilgilidir.

---

# 2. Yazılım Güvenliğinin Temel Amacı

Bilgi güvenliği çoğunlukla üç temel hedef üzerinden değerlendirilir:

## 2.1. Confidentiality — Gizlilik

Bilgilere yalnızca yetkili kişilerin erişebilmesidir.

Örneğin:

* Bir kullanıcının özel mesajlarını başka kullanıcıların görememesi
* Müşteri bilgilerinin yetkisiz çalışanlara gösterilmemesi
* Parolaların veri tabanında açık biçimde tutulmaması
* Access token ve API anahtarlarının korunması

Gizlilik ihlali gerçekleştiğinde hassas bilgiler yetkisiz kişiler tarafından görüntülenebilir.

---

## 2.2. Integrity — Bütünlük

Verilerin yetkisiz kişiler tarafından değiştirilememesidir.

Örneğin:

* Bir kullanıcının banka hesabındaki bakiyeyi değiştirememesi
* Sipariş tutarının tarayıcı üzerinden manipüle edilememesi
* Bir token içerisindeki kullanıcı rolünün sonradan değiştirilememesi
* Veri tabanındaki kayıtların izinsiz biçimde güncellenememesi

JWT imzası gibi mekanizmalar, verinin değiştirildiğinin tespit edilmesine yardımcı olur. Ancak imza, token içerisindeki verileri gizlemez.

---

## 2.3. Availability — Erişilebilirlik

Sistemin ihtiyaç duyulduğu zaman kullanılabilir olmasıdır.

Örneğin:

* Sunucunun aşırı istekler nedeniyle hizmet veremez hâle gelmemesi
* Veri tabanı bağlantılarının kontrolsüz tüketilmemesi
* Kritik servislerin düzenli olarak yedeklenmesi
* Sistem arızalarında hizmetin tamamen kesilmemesi

Güvenlik yalnızca veri çalınmasını önlemek değildir. Sistemin kullanılabilir durumda kalması da güvenliğin bir parçasıdır.

---

# 3. Authentication — Kimlik Doğrulama

## 3.1. Authentication Nedir?

Authentication, bir kullanıcının veya sistemin iddia ettiği kimliğe gerçekten sahip olup olmadığının doğrulanmasıdır.

Türkçede genellikle **kimlik doğrulama** olarak ifade edilir.

Authentication şu soruya cevap verir:

> “Sen kimsin ve gerçekten söylediğin kişi misin?”

Örneğin bir kullanıcı sisteme e-posta adresi ve parola ile giriş yaptığında uygulama, verilen bilgileri kontrol ederek kullanıcının kimliğini doğrulamaya çalışır.

OWASP, authentication kavramını bir bireyin, sistemin veya varlığın iddia ettiği kimliğe sahip olduğunun bir ya da daha fazla doğrulayıcı aracılığıyla kontrol edilmesi olarak tanımlar.

---

## 3.2. Authentication Faktörleri

Kimlik doğrulama yöntemleri genellikle üç temel faktör altında değerlendirilir.

### Bilinen bir şey

Kullanıcının bildiği bilgidir.

Örnekler:

* Parola
* PIN kodu
* Güvenlik cevabı

### Sahip olunan bir şey

Kullanıcının fiziksel veya dijital olarak sahip olduğu araçtır.

Örnekler:

* Cep telefonu
* Güvenlik anahtarı
* Akıllı kart
* Tek kullanımlık kod üreten cihaz

### Kullanıcıya ait bir özellik

Kullanıcının biyometrik özelliğidir.

Örnekler:

* Parmak izi
* Yüz tanıma
* İris taraması
* Ses tanıma

Bir sistem yalnızca parola kullanıyorsa tek faktörlü kimlik doğrulama yapmaktadır. Parolaya ek olarak telefon kodu veya güvenlik anahtarı kullanılıyorsa çok faktörlü kimlik doğrulama uygulanmış olur.

---

## 3.3. MFA — Multi-Factor Authentication

MFA, kullanıcının kimliğini en az iki farklı faktörle doğrulayan güvenlik yöntemidir.

Örneğin:

1. Kullanıcı parolasını girer.
2. Telefonuna gelen tek kullanımlık kodu girer.
3. İki kontrol de başarılı olursa giriş yapılır.

Burada parola “bilinen bir şey”, telefon ise “sahip olunan bir şey” faktörüdür.

İki farklı parola istemek MFA değildir. Çünkü iki bilgi de aynı kategoriye, yani “bilinen bir şey” kategorisine girer.

MFA özellikle şu saldırıların etkisini azaltabilir:

* Çalınmış parola kullanımı
* Credential stuffing
* Phishing sonrası parola ele geçirilmesi
* Zayıf veya tahmin edilebilir parola kullanımı

Ancak MFA tek başına tüm saldırıları durdurmaz. Örneğin saldırgan aktif bir kullanıcı oturumunu veya session token’ını ele geçirirse bazı MFA kontrollerini aşabilir.

---

## 3.4. Güvenli Authentication Akışı

Temel bir kullanıcı giriş işlemi şu adımlardan oluşur:

1. Kullanıcı e-posta adresini ve parolasını gönderir.
2. Sunucu kullanıcının veri tabanında bulunup bulunmadığını kontrol eder.
3. Veri tabanında saklanan parola özeti alınır.
4. Kullanıcının gönderdiği parola güvenli parola doğrulama fonksiyonuyla karşılaştırılır.
5. Bilgiler doğruysa kullanıcı doğrulanır.
6. Sunucu güvenli bir session oluşturur veya token üretir.
7. Kullanıcının sonraki isteklerinde bu session veya token kontrol edilir.

Parola doğrulama işlemi istemci tarafında değil, güvenilir sunucu tarafında yapılmalıdır.

Frontend tarafından gönderilen `isAdmin`, `role` veya `authenticated` gibi değerlere güvenilmemelidir. Kullanıcı tarayıcıdaki JavaScript kodlarını ve gönderilen istekleri değiştirebilir.

---

## 3.5. Parolalar Nasıl Saklanmalıdır?

Parolalar veri tabanında kesinlikle açık metin biçiminde saklanmamalıdır.

Yanlış örnek:

```text
email: ozge@example.com
password: 123456
```

Veri tabanı ele geçirilirse saldırgan bütün kullanıcı parolalarını doğrudan görebilir.

Parolalar ayrıca geri çözülebilir bir şifreleme yöntemiyle saklanmamalıdır. Parolaların genellikle tekrar elde edilmesine ihtiyaç yoktur. Sistem yalnızca kullanıcının gönderdiği parolanın doğru olup olmadığını kontrol etmelidir.

Bu nedenle parola saklama işleminde **hashing** kullanılır.

OWASP; Argon2id, scrypt, bcrypt veya uygun yapılandırılmış PBKDF2 gibi parola saklamak için tasarlanmış yavaş algoritmaların kullanılmasını, hızlı SHA-256 gibi genel amaçlı özet algoritmalarının tek başına parola saklamak için tercih edilmemesini önerir.

### Hashing

Hash fonksiyonu girdiyi sabit uzunlukta bir çıktıya dönüştürür.

```text
Parola → Hash fonksiyonu → Parola özeti
```

Hashing işlemi tek yönlüdür. Hash değerinden orijinal parolanın doğrudan elde edilmesi amaçlanmaz.

### Salt

Salt, her parola için üretilen rastgele veridir.

Parola hash’lenmeden önce salt ile birlikte işlenir:

```text
Hash(parola + salt)
```

Salt sayesinde aynı parolaya sahip iki kullanıcının veri tabanındaki parola özetleri farklı olur.

Salt ayrıca önceden hazırlanmış rainbow table saldırılarının etkinliğini azaltır.

### Pepper

Pepper, parola hash işlemine eklenen ve veri tabanından ayrı tutulan gizli bir değerdir.

Salt genellikle parola özetiyle birlikte veri tabanında tutulabilirken pepper gizli yapılandırma veya secret management sisteminde saklanmalıdır.

---

## 3.6. Authentication Sistemlerine Yönelik Saldırılar

### Brute Force

Saldırgan çok sayıda parola deneyerek doğru parolayı bulmaya çalışır.

Korunma yöntemleri:

* Rate limiting
* Geçici hesap kilitleme
* Artan bekleme süresi
* MFA
* Güçlü parola politikaları
* Şüpheli giriş tespiti

### Credential Stuffing

Başka sistemlerden sızdırılmış kullanıcı adı ve parolaların farklı uygulamalarda denenmesidir.

Kullanıcılar aynı parolayı birden fazla sistemde kullanıyorsa saldırı başarılı olabilir.

### Password Spraying

Saldırgan tek bir hesap üzerinde çok fazla parola denemek yerine çok sayıda kullanıcı hesabında birkaç yaygın parola dener.

Örneğin yüzlerce hesap üzerinde `Password123` parolası denenebilir.

### User Enumeration

Uygulamanın hata mesajları, belirli bir kullanıcının sistemde kayıtlı olup olmadığını ortaya çıkarabilir.

Riskli mesaj:

```text
Bu e-posta sistemde kayıtlı değildir.
```

Daha güvenli mesaj:

```text
E-posta veya parola hatalıdır.
```

Ancak parola sıfırlama sistemlerinde kullanıcı deneyimi ve güvenlik dengesi ayrıca değerlendirilmelidir.

### Session Hijacking

Saldırgan kullanıcının session kimliğini veya token’ını ele geçirerek kullanıcı gibi davranır.

### Session Fixation

Saldırgan önceden bildiği bir session kimliğinin mağdur tarafından kullanılmasını sağlamaya çalışır. Kullanıcı giriş yaptıktan sonra session kimliği değiştirilmezse saldırgan aynı session üzerinden hesaba erişebilir.

Bunun önlenmesi için başarılı girişten sonra session kimliği yenilenmelidir.

---

# 4. Authorization — Yetkilendirme

## 4.1. Authorization Nedir?

Authorization, kimliği belirlenmiş bir kullanıcının belirli bir kaynağa erişme veya belirli bir işlemi gerçekleştirme iznine sahip olup olmadığının kontrol edilmesidir.

Türkçede **yetkilendirme** olarak ifade edilir.

Authorization şu soruya cevap verir:

> “Bu işlemi yapmaya yetkin var mı?”

Bir kullanıcının giriş yapmış olması, sistemdeki bütün işlemleri yapabileceği anlamına gelmez.

Örneğin:

* Normal kullanıcı kendi profilini görüntüleyebilir.
* Yönetici bütün kullanıcıları görüntüleyebilir.
* Editör içerik oluşturabilir.
* Müşteri sipariş verebilir.
* Muhasebe çalışanı faturaları görüntüleyebilir.
* Normal kullanıcı başka bir kullanıcının siparişini görüntüleyemez.

OWASP, authentication ile kimliğin doğrulandığını; authorization ile doğrulanmış veya belirli bir bağlamdaki varlığın istenen işlem için izne sahip olup olmadığının belirlendiğini belirtir.

---

## 4.2. Yetkilendirme Nerede Yapılmalıdır?

Yetkilendirme kontrolleri mutlaka sunucu tarafında yapılmalıdır.

Yalnızca frontend’de bir butonu gizlemek güvenlik sağlamaz.

Örneğin normal kullanıcı için “Kullanıcıyı Sil” butonu gizlenmiş olabilir. Ancak kullanıcı tarayıcının geliştirici araçlarını veya Postman gibi bir aracı kullanarak doğrudan silme API’sine istek gönderebilir.

Frontend kontrolü:

```javascript
if (user.role === "admin") {
  showDeleteButton();
}
```

Bu kontrol yalnızca arayüz davranışını düzenler.

Gerçek güvenlik kontrolü backend tarafında yapılmalıdır:

```javascript
if (currentUser.role !== "admin") {
  return response.status(403).json({
    message: "Bu işlem için yetkiniz bulunmamaktadır."
  });
}
```

En güvenli yaklaşım, hem arayüzde uygun seçenekleri göstermek hem de her kritik API isteğinde sunucu tarafında yetki kontrolü yapmaktır.

---

## 4.3. Yetkilendirme Modelleri

### RBAC — Role-Based Access Control

Yetkilerin rollere göre belirlenmesidir.

Örnek roller:

* Admin
* Editor
* User
* Manager
* Accountant

Örnek:

```text
Admin   → Kullanıcı ekleme, silme, güncelleme
Editor  → İçerik ekleme ve güncelleme
User    → İçerik görüntüleme
```

RBAC anlaşılır ve yaygın bir modeldir. Ancak çok karmaşık iş kurallarında yalnızca roller yetersiz kalabilir.

### ABAC — Attribute-Based Access Control

Yetkilendirme kararı kullanıcı, kaynak, işlem ve ortam özelliklerine göre verilir.

Örneğin:

* Kullanıcının departmanı
* Belgenin gizlilik seviyesi
* İşlemin yapıldığı saat
* Kullanıcının ülkesi
* Kaydın sahibi
* Erişim yapılan cihaz

Örnek kural:

```text
Kullanıcı İnsan Kaynakları departmanındaysa
ve belge kendi şubesine aitse
ve işlem şirket ağı içerisinden yapılıyorsa
belgeyi görüntüleyebilir.
```

### ACL — Access Control List

Her kaynak için hangi kullanıcı veya grupların hangi izinlere sahip olduğunun tutulmasıdır.

Örnek:

```text
rapor.pdf:
- Özge: görüntüleme
- Ahmet: görüntüleme ve düzenleme
- Stajyerler: erişim yok
```

### ReBAC — Relationship-Based Access Control

Yetkilendirme kararının kullanıcılar veya varlıklar arasındaki ilişkilere göre verilmesidir.

Örneğin:

* Kullanıcı belgenin sahibiyse düzenleyebilir.
* Kullanıcı proje ekibindeyse projeyi görüntüleyebilir.
* Kullanıcı yöneticinin altında çalışıyorsa belirli raporlara erişebilir.

---

## 4.4. Least Privilege — En Az Yetki İlkesi

Bir kullanıcıya, servise veya uygulamaya yalnızca görevini yerine getirebilmesi için gerekli minimum yetkiler verilmelidir.

Örneğin yalnızca kayıt okuyan bir uygulamanın veri tabanı kullanıcısına `DELETE`, `DROP` veya yönetici yetkisi verilmemelidir.

En az yetki ilkesi, bir hesap ele geçirildiğinde oluşabilecek zararı sınırlar.

---

## 4.5. Deny by Default

Varsayılan davranış erişime izin vermek değil, erişimi reddetmek olmalıdır.

Yanlış yaklaşım:

```text
Özel olarak yasaklanmadıysa izin ver.
```

Daha güvenli yaklaşım:

```text
Açıkça izin verilmediyse reddet.
```

Yeni bir endpoint eklendiğinde gerekli yetkilendirme kuralı tanımlanmadıysa endpoint varsayılan olarak kapalı kalmalıdır.

---

## 4.6. IDOR — Insecure Direct Object Reference

IDOR, nesne seviyesindeki yetkilendirme kontrolünün eksik olması nedeniyle kullanıcının başka kullanıcılara ait kaynaklara erişebilmesidir.

Örnek istek:

```http
GET /api/orders/1001
```

Kullanıcı adres çubuğundaki değeri değiştirir:

```http
GET /api/orders/1002
```

Sunucu yalnızca kullanıcının giriş yapıp yapmadığını kontrol ediyor fakat `1002` numaralı siparişin bu kullanıcıya ait olup olmadığını kontrol etmiyorsa yetkilendirme açığı oluşur.

Güvenli kontrol:

```javascript
const order = await findOrderById(orderId);

if (!order) {
  return response.status(404).send();
}

if (order.userId !== currentUser.id && currentUser.role !== "admin") {
  return response.status(403).send();
}
```

Tahmin edilmesi zor UUID kullanmak yardımcı olabilir ancak yetkilendirme kontrolünün yerini tutmaz. Her kaynak erişiminde kullanıcının o kaynağa erişim izni kontrol edilmelidir. OWASP da IDOR’un temel nedenini eksik nesne seviyesi authorization kontrolü olarak açıklar.

---

# 5. Authentication ve Authorization Arasındaki Fark

| Özellik               | Authentication                    | Authorization                                  |
| --------------------- | --------------------------------- | ---------------------------------------------- |
| Türkçesi              | Kimlik doğrulama                  | Yetkilendirme                                  |
| Temel soru            | Sen kimsin?                       | Ne yapabilirsin?                               |
| Amaç                  | Kullanıcının kimliğini doğrulamak | Kullanıcının izinlerini kontrol etmek          |
| Örnek                 | E-posta ve parola ile giriş       | Yalnızca admin kullanıcının kayıt silebilmesi  |
| Sıralama              | Genellikle önce yapılır           | Genellikle kimlik doğrulamadan sonra yapılır   |
| Kullanılan veriler    | Parola, MFA, biyometri, token     | Rol, izin, sahiplik, politika, kaynak ilişkisi |
| Başarısız HTTP sonucu | Genellikle 401                    | Genellikle 403                                 |

## 401 ve 403 Farkı

### 401 Unauthorized

Adında “Unauthorized” geçmesine rağmen çoğunlukla kullanıcının kimliğinin doğrulanamadığını ifade eder.

Örnekler:

* Token bulunmuyor.
* Token geçersiz.
* Token süresi dolmuş.
* Kullanıcı giriş yapmamış.

### 403 Forbidden

Kullanıcının kimliği bilinmektedir fakat istenen işlem için yetkisi yoktur.

Örnek:

* Normal kullanıcının yönetici paneline erişmeye çalışması
* Kullanıcının başka bir kullanıcıya ait kaydı silmeye çalışması

---

# 6. Oturum ve Session Yönetimi

HTTP temelde durumsuz bir protokoldür. Her istek bağımsızdır. Sunucunun, bir isteği gönderen kullanıcının daha önce giriş yapıp yapmadığını anlayabilmesi için bir oturum mekanizmasına ihtiyaç vardır.

OWASP, web session’ını aynı kullanıcıyla ilişkilendirilen HTTP istek ve cevaplarının oluşturduğu bir süreç olarak tanımlar. Session mekanizması, sonraki isteklerde kullanıcıyı tanımayı ve erişim kontrolleri uygulamayı sağlar.

---

## 6.1. Server-Side Session

Kullanıcı giriş yaptığında sunucu rastgele bir session kimliği üretir.

```text
sessionId = a8f7c2...
```

Sunucu session bilgilerini kendi tarafında saklar:

```text
a8f7c2... → userId: 42, role: admin
```

Tarayıcıya yalnızca session kimliği gönderilir.

Sonraki isteklerde tarayıcı cookie aracılığıyla session kimliğini gönderir ve sunucu kullanıcıyı session deposundan bulur.

### Avantajları

* Session kolayca iptal edilebilir.
* Kullanıcı bilgileri istemciye gönderilmez.
* Yetki değişiklikleri daha hızlı uygulanabilir.

### Dezavantajları

* Sunucunun session durumunu saklaması gerekir.
* Dağıtık sistemlerde ortak session deposu gerekebilir.
* Çok sayıda kullanıcıda ek depolama ihtiyacı doğabilir.

---

## 6.2. Güvenli Cookie Ayarları

Session kimliği cookie içinde tutuluyorsa şu özellikler önemlidir:

### HttpOnly

JavaScript’in cookie değerini okumasını engeller.

Bu ayar, XSS sonucunda token veya session kimliğinin JavaScript ile okunması riskini azaltır. Ancak XSS açığını tamamen çözmez; saldırgan kurbanın tarayıcısından istek göndermeye devam edebilir.

### Secure

Cookie’nin yalnızca HTTPS bağlantıları üzerinden gönderilmesini sağlar.

### SameSite

Cookie’nin farklı sitelerden başlatılan isteklerde gönderilme davranışını kontrol eder.

Yaygın değerler:

* `Strict`
* `Lax`
* `None`

`SameSite=None` kullanılıyorsa cookie’nin genellikle `Secure` olarak işaretlenmesi gerekir.

### Path ve Domain

Cookie’nin hangi adreslere gönderileceğini sınırlar.

Cookie mümkün olduğunca dar kapsamlı tanımlanmalıdır.

---

## 6.3. Session Güvenliği İçin Kurallar

* Giriş yapıldıktan sonra session kimliği yenilenmelidir.
* Logout işleminde session sunucu tarafında geçersiz hâle getirilmelidir.
* Uzun süre kullanılmayan session’lar zaman aşımına uğramalıdır.
* Kritik işlemler öncesinde yeniden kimlik doğrulama istenebilir.
* Session kimliği URL parametresinde taşınmamalıdır.
* Session değerleri loglara yazılmamalıdır.
* Session kimlikleri tahmin edilemez ve yeterince rastgele olmalıdır.
* Bütün iletişim HTTPS üzerinden gerçekleştirilmelidir.

---

# 7. JWT — JSON Web Token

## 7.1. JWT Nedir?

JWT, iki taraf arasında claim adı verilen bilgilerin kompakt ve URL uyumlu bir biçimde taşınmasını sağlayan token formatıdır.

JWT genellikle şu amaçlarla kullanılır:

* API kimlik doğrulaması
* Yetki bilgilerinin taşınması
* OAuth access token’ları
* OpenID Connect ID token’ları
* Dağıtık servisler arasında kimlik bilgilerinin aktarılması

RFC 7519’a göre JWT, taraflar arasında claim’leri taşımak için kullanılan kompakt ve URL güvenli bir formattır. JWT; imzalanmış bir JWS veya şifrelenmiş bir JWE biçiminde olabilir.

Önemli nokta şudur:

> Her JWT şifrelenmiş değildir.

Yaygın olarak kullanılan imzalı JWT’lerin içeriği Base64URL ile kodlanır. Kodlama, şifreleme değildir. Token’ı elde eden kişi header ve payload bölümünü okuyabilir.

---

## 7.2. JWT Yapısı

Yaygın bir imzalı JWT üç bölümden oluşur:

```text
HEADER.PAYLOAD.SIGNATURE
```

Örnek görünüm:

```text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
.
eyJzdWIiOiI0MiIsInJvbGUiOiJhZG1pbiJ9
.
imza-degeri
```

### Header

Token türünü ve kullanılan imza algoritmasını belirtir.

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### Payload

Claim adı verilen bilgileri içerir.

```json
{
  "sub": "42",
  "role": "admin",
  "exp": 1785067200
}
```

### Signature

Header ve payload’ın gizli anahtar veya özel anahtar kullanılarak imzalanmasıyla oluşturulur.

İmzanın amacı:

* Token’ın değiştirilip değiştirilmediğini kontrol etmek
* Token’ın güvenilen bir üretici tarafından oluşturulduğunu doğrulamak

İmza payload içeriğini gizlemez.

---

## 7.3. JWT Claim Türleri

Claim, token içerisinde taşınan bilgi alanıdır.

### Registered Claims

JWT standardında tanımlanmış yaygın alanlardır.

| Claim | Açıklama                                     |
| ----- | -------------------------------------------- |
| `iss` | Token’ı üreten taraf                         |
| `sub` | Token’ın temsil ettiği kullanıcı veya varlık |
| `aud` | Token’ın kullanılacağı hedef servis          |
| `exp` | Token’ın sona erme zamanı                    |
| `nbf` | Token’ın kullanılmaya başlanabileceği zaman  |
| `iat` | Token’ın oluşturulma zamanı                  |
| `jti` | Token’a ait benzersiz kimlik                 |

### Public Claims

Uygulamalar arasında ortak kullanılabilen, çakışmayacak şekilde tanımlanmış claim’lerdir.

### Private Claims

Uygulamaya özel alanlardır.

Örnek:

```json
{
  "userId": 42,
  "department": "IT",
  "permissions": ["report.read", "report.create"]
}
```

Token içerisine hassas bilgiler konulmamalıdır.

Şu bilgiler imzalı fakat şifrelenmemiş JWT payload’ında tutulmamalıdır:

* Parola
* Kredi kartı bilgisi
* Gizli anahtar
* Kimlik belgesi bilgileri
* Gereksiz kişisel veriler

---

## 7.4. JWT Nasıl Çalışır?

1. Kullanıcı e-posta ve parola ile giriş yapar.
2. Sunucu bilgileri doğrular.
3. Sunucu kullanıcı için access token oluşturur.
4. Token istemciye gönderilir.
5. İstemci sonraki API isteklerinde token’ı gönderir.
6. API token imzasını ve claim’lerini doğrular.
7. Token geçerliyse istek işlenir.
8. Token süresi dolmuşsa kullanıcıdan yeni token veya tekrar giriş istenir.

Yaygın kullanım:

```http
Authorization: Bearer ACCESS_TOKEN
```

`Bearer` token, token’a sahip olan tarafın token’ın sağladığı yetkileri kullanabilmesi anlamına gelir. Bu nedenle token’ın ele geçirilmesi ciddi bir güvenlik riskidir.

---

## 7.5. JWT İmzalama Algoritmaları

### Simetrik Algoritmalar

Örnek:

```text
HS256
```

Token’ı imzalayan ve doğrulayan taraf aynı gizli anahtarı kullanır.

Avantajı basit ve hızlı olmasıdır.

Dezavantajı ise token doğrulayan bütün servislerin gizli anahtarı bilmesi gerekebilmesidir. Bu servislerden biri ele geçirilirse saldırgan yeni token üretebilir.

### Asimetrik Algoritmalar

Örnekler:

```text
RS256
ES256
```

Token özel anahtarla imzalanır ve açık anahtarla doğrulanır.

Özel anahtar yalnızca token üreten serviste bulunur. Diğer servisler açık anahtarla doğrulama yapabilir.

Dağıtık sistemlerde bu yaklaşım anahtar paylaşımı açısından avantaj sağlayabilir.

---

## 7.6. JWT Doğrulamasında Kontrol Edilmesi Gerekenler

Bir JWT yalnızca decode edilmemelidir. Kriptografik olarak doğrulanmalıdır.

Kontrol edilmesi gereken başlıca alanlar:

* İmza geçerli mi?
* Beklenen algoritma mı kullanılmış?
* `alg: none` reddediliyor mu?
* Token’ın süresi dolmuş mu?
* `nbf` zamanı uygun mu?
* `iss` beklenen token üreticisi mi?
* `aud` bu API’yi gösteriyor mu?
* Token doğru amaç için mi üretilmiş?
* Kullanıcı hâlâ aktif mi?
* Kullanıcının yetkileri değişmiş mi?
* Token iptal edilmiş mi?
* Gerekliyse `jti` daha önce kullanılmış mı?

RFC 8725, uygulamaların izin verilen algoritmaları açık biçimde belirlemesini, token’ın kendi header alanından gelen algoritma seçimine körü körüne güvenmemesini ve issuer, audience gibi claim’leri doğrulamasını önerir.

---

## 7.7. Access Token ve Refresh Token

### Access Token

API’ye erişmek için kullanılan, genellikle kısa ömürlü token’dır.

Örneğin:

```text
Geçerlilik süresi: 10 dakika
```

Access token ele geçirilirse saldırgan token süresi boyunca API’ye erişebilir. Bu nedenle kısa ömürlü tutulması riski sınırlar.

### Refresh Token

Yeni access token almak için kullanılır.

Genellikle access token’dan daha uzun ömürlüdür ve daha hassastır.

Refresh token:

* API işlemlerinde doğrudan kullanılmamalıdır.
* Güvenli biçimde saklanmalıdır.
* Kullanıldığında rotation uygulanabilir.
* Logout veya şüpheli aktivite durumunda iptal edilebilmelidir.
* Ele geçirildiği tespit edilirse token ailesi geçersiz hâle getirilebilir.

### Refresh Token Rotation

Her refresh işlemi sırasında:

1. Eski refresh token alınır.
2. Eski token geçersiz hâle getirilir.
3. Yeni access token oluşturulur.
4. Yeni refresh token oluşturulur.

Eski refresh token tekrar kullanılırsa token’ın çalınmış olma ihtimali değerlendirilir.

---

## 7.8. JWT Nerede Saklanmalıdır?

JWT saklama konusunda tek bir çözüm her uygulama için doğru değildir. Uygulamanın mimarisi, XSS ve CSRF tehditleri birlikte değerlendirilmelidir.

### LocalStorage

Avantajı JavaScript tarafından kolayca kullanılabilmesidir.

Ancak sayfada XSS açığı varsa saldırgan JavaScript ile localStorage içerisindeki token’ı okuyabilir.

Bu nedenle hassas session token’larını localStorage’da tutmak ciddi risk oluşturabilir. OWASP, tarayıcı tarafındaki depolamanın gizlilik sağladığının varsayılmaması gerektiğini ve hassas kimlik doğrulama verilerinin istemci depolarında tutulmasının dikkatle değerlendirilmesini belirtir.

### HttpOnly Cookie

JavaScript cookie değerini doğrudan okuyamaz.

Bu durum token hırsızlığı riskini azaltabilir. Ancak cookie isteklerle otomatik gönderildiği için CSRF riski değerlendirilmelidir.

Koruma yöntemleri:

* `SameSite`
* CSRF token
* Origin veya Referer kontrolü
* Kritik işlemlerde yeniden authentication

### Memory

Access token yalnızca uygulama belleğinde tutulabilir.

Sayfa yenilendiğinde token kaybolur. Kullanıcı deneyimi için HttpOnly cookie içerisinde refresh token gibi ek bir mekanizma kullanılabilir.

---

## 7.9. JWT Kullanmanın Avantajları

* Kompakt bir veri yapısına sahiptir.
* HTTP header içinde kolayca taşınabilir.
* Birden fazla servis tarafından doğrulanabilir.
* Asimetrik imza ile doğrulama servislerine özel anahtar verilmesi gerekmez.
* Claim’ler sayesinde kimlik ve yetki bilgileri taşınabilir.
* Dağıtık sistemlerde merkezi session sorgularını azaltabilir.

---

## 7.10. JWT Kullanmanın Dezavantajları

* Token üretildikten sonra anında iptal edilmesi klasik session’a göre daha zordur.
* Payload genellikle okunabilir durumdadır.
* Token içerisine eski yetkiler yazılmış olabilir.
* Büyük token’lar her istekte ağ üzerinden taşınır.
* Yanlış algoritma ve anahtar yönetimi ciddi açıklara yol açabilir.
* Uzun ömürlü token ele geçirilirse risk uzun süre devam eder.
* Logout işlemi yalnızca istemciden token silmekle sınırlı kalırsa sunucu tarafında token hâlâ geçerli olabilir.

JWT her projede session yerine kullanılması gereken otomatik bir çözüm değildir. Basit web uygulamalarında güvenli server-side session daha kolay yönetilebilir.

---

# 8. OAuth 2.0 Mantığı

## 8.1. OAuth Nedir?

OAuth 2.0, bir uygulamanın kullanıcının parolasını almadan başka bir servisteki belirli kaynaklara sınırlı erişim elde etmesini sağlayan yetkilendirme çerçevesidir.

OAuth’un temel amacı authentication değil, **delegated authorization**, yani devredilmiş yetkilendirmedir.

RFC 6749, OAuth 2.0’ın üçüncü taraf uygulamalara kullanıcı adına veya kendi adına HTTP servislerine sınırlı erişim verilmesini sağladığını belirtir. Kullanıcı parolasını üçüncü taraf uygulamaya vermek yerine uygulamaya belirli kapsam ve süreye sahip access token verilir.

---

## 8.2. OAuth Neden Gereklidir?

Bir fotoğraf düzenleme uygulamasının Google Drive içerisindeki belirli fotoğraflara erişmek istediğini düşünelim.

Güvensiz yöntem:

```text
Google kullanıcı adını ve parolanı uygulamaya ver.
```

Bu durumda üçüncü taraf uygulama kullanıcının bütün hesabına erişebilir ve parolayı saklayabilir.

OAuth yaklaşımında:

1. Uygulama kullanıcıyı Google’ın yetkilendirme ekranına yönlendirir.
2. Kullanıcı doğrudan Google üzerinde giriş yapar.
3. Google uygulamanın istediği izinleri gösterir.
4. Kullanıcı izin verirse uygulamaya sınırlı token gönderilir.
5. Uygulama yalnızca verilen kapsamda işlem yapabilir.
6. Kullanıcı daha sonra uygulamanın erişimini kaldırabilir.

Üçüncü taraf uygulama kullanıcının Google parolasını öğrenmez.

---

## 8.3. OAuth Rolleri

OAuth 2.0 dört temel rol tanımlar.

### Resource Owner

Korunan kaynağın sahibi veya erişim izni verebilen taraftır.

Çoğunlukla son kullanıcıdır.

### Client

Korumalı kaynağa erişmek isteyen uygulamadır.

Örnek:

* Mobil uygulama
* Web uygulaması
* Masaüstü uygulaması
* Backend servisi

### Authorization Server

Kullanıcının kimliğini doğrular, izin ekranını gösterir ve token üretir.

### Resource Server

Korunan API veya verileri barındıran sunucudur.

Access token’ı kontrol ederek istenen kaynağa erişim verir.

---

## 8.4. Authorization Code Flow

Modern web ve mobil uygulamalarda en yaygın akışlardan biridir.

### Akış

1. Kullanıcı client uygulamada “Google ile devam et” butonuna basar.
2. Client, kullanıcıyı authorization server’a yönlendirir.
3. Kullanıcı authorization server üzerinde giriş yapar.
4. Kullanıcı istenen izinleri onaylar.
5. Authorization server kullanıcıyı client’ın kayıtlı callback adresine yönlendirir.
6. Callback isteğinde kısa ömürlü authorization code bulunur.
7. Client bu code’u authorization server’ın token endpoint’ine gönderir.
8. Authorization server code’u doğrular.
9. Client’a access token ve gerekirse refresh token verilir.
10. Client access token ile resource server’a istek gönderir.

Access token’ın tarayıcı yönlendirmesi üzerinden doğrudan taşınması yerine kısa ömürlü authorization code kullanılır.

---

## 8.5. PKCE Nedir?

PKCE, Authorization Code Flow’un özellikle public client’larda güvenliğini artırmak için kullanılır.

Public client’lar şunları içerebilir:

* Mobil uygulamalar
* Tek sayfa web uygulamaları
* Masaüstü uygulamalar

Bu uygulamalarda kalıcı bir client secret güvenli biçimde saklanamaz.

PKCE akışında client:

1. Rastgele bir `code_verifier` üretir.
2. Bundan bir `code_challenge` oluşturur.
3. Authorization isteğinde `code_challenge` gönderir.
4. Token isteğinde orijinal `code_verifier` gönderir.
5. Authorization server ikisinin eşleştiğini doğrular.

Saldırgan authorization code’u ele geçirse bile `code_verifier` değerine sahip olmadığı için token alamaz.

Güncel OAuth güvenlik önerileri Authorization Code Flow’un PKCE ile korunmasını, redirect URI değerlerinin kesin biçimde doğrulanmasını ve eski, daha riskli akışların kullanılmamasını önerir.

---

## 8.6. Scope Nedir?

Scope, access token’ın hangi işlemleri yapabileceğini belirtir.

Örnek scope’lar:

```text
profile.read
email.read
calendar.read
calendar.write
orders.read
orders.create
```

Uygulama yalnızca ihtiyaç duyduğu izinleri istemelidir.

Örneğin yalnızca takvim etkinliklerini görüntüleyen bir uygulamanın silme veya e-posta gönderme izni istemesi en az yetki ilkesine aykırıdır.

---

## 8.7. Consent Nedir?

Consent, kullanıcının client uygulamaya hangi yetkileri verdiğini onayladığı süreçtir.

İzin ekranı kullanıcıya açık biçimde şunları göstermelidir:

* Hangi uygulama erişim istiyor?
* Hangi verilere erişilecek?
* Hangi işlemler yapılabilecek?
* İzin ne kadar süre geçerli olacak?
* Erişim daha sonra kaldırılabilecek mi?

---

## 8.8. State Parametresi

`state`, OAuth yönlendirme sürecinde isteğin client tarafından başlatıldığını doğrulamaya ve CSRF benzeri saldırıları önlemeye yardımcı olur.

Client authorization isteğinden önce tahmin edilemez bir `state` üretir.

Authorization server callback yaptığında aynı değer geri gelir. Client dönen değeri daha önce oluşturduğu değerle karşılaştırır.

Eşleşmiyorsa işlem reddedilir.

---

## 8.9. Redirect URI Güvenliği

Authorization server, yönlendirme adresini önceden kayıtlı adresle kesin biçimde karşılaştırmalıdır.

Riskli davranış:

```text
https://example.com/callback ile başlayan her adrese izin ver.
```

Bu yaklaşım saldırganın benzer veya kötü niyetli adresler kullanmasına yol açabilir.

RFC 9700, kayıtlı redirect URI değerlerinin genel olarak kesin string eşleşmesiyle doğrulanmasını ve açık yönlendiricilerden kaçınılmasını güncel güvenlik uygulamaları arasında belirtir.

---

## 8.10. Eski ve Riskli OAuth Akışları

### Implicit Grant

Token’ın tarayıcı yönlendirmesinde doğrudan döndürülmesine dayanır.

Modern uygulamalarda Authorization Code Flow ve PKCE tercih edilir.

### Resource Owner Password Credentials Grant

Kullanıcı, parolasını doğrudan client uygulamaya verir.

Bu yaklaşım OAuth’un temel avantajlarından biri olan “parolayı üçüncü tarafla paylaşmama” ilkesini zayıflatır.

RFC 9700 güncel güvenlik uygulamalarında implicit grant kullanımından kaçınılmasını ve Resource Owner Password Credentials grant’in kullanılmamasını belirtir.

---

# 9. OpenID Connect ve OAuth Farkı

OAuth 2.0 esas olarak authorization içindir.

OAuth tek başına standart bir kullanıcı kimliği doğrulama protokolü değildir.

OpenID Connect, OAuth 2.0 üzerine bir kimlik katmanı ekler ve authentication amacıyla kullanılmasını sağlar.

OpenID Connect, client’ın kullanıcının kimliğini doğrulamasına yardımcı olan bir **ID Token** tanımlar. OpenID Connect Core standardı, OIDC’yi OAuth 2.0 üzerinde çalışan bir kimlik katmanı olarak tanımlar.

| Kavram         | Temel amacı                                |
| -------------- | ------------------------------------------ |
| OAuth 2.0      | Yetkilendirme ve API erişimi               |
| OpenID Connect | Kimlik doğrulama                           |
| Access Token   | API’ye erişmek                             |
| ID Token       | Kullanıcının kimliği hakkında bilgi vermek |
| Refresh Token  | Yeni access token almak                    |

## Kritik Hata

ID token, API’ye erişmek için access token yerine kullanılmamalıdır.

Access token resource server için üretilir.

ID token ise client uygulamanın kullanıcı kimliğini doğrulaması için üretilir.

---

# 10. SQL Injection

## 10.1. SQL Injection Nedir?

SQL Injection, kullanıcıdan gelen verilerin güvenli biçimde ayrıştırılmadan SQL sorgusuna eklenmesi sonucunda saldırganın sorgunun yapısını değiştirebilmesidir.

OWASP’a göre SQL Injection çoğunlukla kullanıcı girdilerinin string birleştirme yoluyla dinamik SQL sorgularına eklenmesi sonucunda oluşur. Temel savunma, kullanıcı verisini SQL kodundan ayıran parametreli sorgular kullanmaktır.

---

## 10.2. Güvensiz SQL Sorgusu

```javascript
const query =
  "SELECT * FROM users WHERE email = '" +
  email +
  "' AND password = '" +
  password +
  "'";
```

Burada kullanıcı girdisi doğrudan SQL sorgusuna eklenmektedir.

Saldırgan, girdi alanına SQL sözdizimini değiştiren özel karakterler gönderirse sorgunun mantığını değiştirebilir.

Sorun, saldırganın belirli bir karakter kullanması değildir. Asıl sorun, uygulamanın **veri ile SQL komutunu birbirinden ayırmamasıdır**.

---

## 10.3. SQL Injection Sonuçları

Başarılı bir SQL Injection saldırısı sonucunda saldırgan:

* Authentication kontrolünü aşabilir.
* Hassas verileri okuyabilir.
* Kayıtları değiştirebilir.
* Kayıtları silebilir.
* Yeni yönetici hesabı oluşturabilir.
* Veri tabanı yapısını öğrenebilir.
* Uygulamanın kullandığı veri tabanı hesabının yetkilerine bağlı olarak daha ileri işlemler gerçekleştirebilir.

OWASP, başarılı SQL Injection saldırılarının veri okuma, ekleme, güncelleme ve silme işlemlerine; bazı durumlarda veri tabanı yönetim işlemlerine kadar ilerleyebileceğini belirtir.

---

## 10.4. SQL Injection Türleri

### In-Band SQL Injection

Saldırının gönderildiği kanal ile sonuçların alındığı kanal aynıdır.

Örneğin sonuçlar doğrudan web sayfasında gösterilir.

### Error-Based SQL Injection

Saldırgan veri tabanının hata mesajlarından bilgi toplamaya çalışır.

Ayrıntılı hata mesajları tablo adlarını, sütunları veya veri tabanı türünü ortaya çıkarabilir.

### Union-Based SQL Injection

Saldırgan mevcut sorgunun sonucuna başka bir sorgunun sonucunu eklemeye çalışır.

### Blind SQL Injection

Uygulama sorgu sonucunu doğrudan göstermez. Saldırgan uygulamanın davranışını gözlemleyerek bilgi çıkarmaya çalışır.

#### Boolean-Based Blind

Uygulamanın doğru ve yanlış koşullarda farklı davranması gözlemlenir.

#### Time-Based Blind

Belirli koşullarda veri tabanının gecikmeli cevap vermesi sağlanarak bilgi çıkarılmaya çalışılır.

### Out-of-Band SQL Injection

Veri, saldırının gönderildiği kanal dışında başka bir iletişim kanalı üzerinden alınır.

OWASP SQL Injection saldırılarını in-band, inferential veya blind ve out-of-band gibi sınıflar altında değerlendirir.

---

## 10.5. SQL Injection Nasıl Önlenir?

### Parametreli Sorgular

En önemli savunma yöntemidir.

Güvenli örnek:

```javascript
const query =
  "SELECT * FROM users WHERE email = ? AND status = ?";

const result = await database.execute(query, [
  email,
  "active"
]);
```

Burada SQL komutu ile kullanıcı verisi ayrı gönderilir.

Veri tabanı `email` değerini SQL kodu olarak değil veri olarak işler.

### Prepared Statements

Sorgu yapısı önceden hazırlanır ve kullanıcı değerleri parametre olarak bağlanır.

### ORM Kullanımı

ORM araçları parametreli sorguların kullanımını kolaylaştırabilir.

Ancak ORM kullanmak otomatik olarak bütün SQL Injection risklerini ortadan kaldırmaz.

Şu durumlarda risk yeniden ortaya çıkabilir:

* Raw SQL kullanılması
* String birleştirme yapılması
* Dinamik sıralama alanlarının kontrol edilmemesi
* Kullanıcı girdisiyle sorgu yapısının oluşturulması

### Allow-List Validation

Özellikle tablo adı, sütun adı veya sıralama yönü gibi parametrelenmesi zor alanlarda yalnızca önceden izin verilen değerler kabul edilmelidir.

```javascript
const allowedSortFields = [
  "name",
  "created_at",
  "price"
];

if (!allowedSortFields.includes(sortField)) {
  throw new Error("Geçersiz sıralama alanı.");
}
```

### En Az Yetkili Veri Tabanı Kullanıcısı

Uygulamanın veri tabanı hesabına yalnızca ihtiyaç duyduğu yetkiler verilmelidir.

Örneğin yalnızca okuma yapan rapor servisine:

```text
SELECT
```

yetkisi verilebilir.

Aşağıdaki yetkilerin verilmesi gereksiz olabilir:

```text
DROP
ALTER
CREATE USER
GRANT
```

### Hata Mesajlarını Gizleme

Kullanıcıya ham veri tabanı hatası gösterilmemelidir.

Riskli:

```text
SQL syntax error near users.password at line 1
```

Daha güvenli:

```text
İşlem sırasında bir hata oluştu.
```

Ayrıntılı hata güvenli sunucu loglarında tutulabilir.

### Input Validation

Girdinin beklenen biçimde olup olmadığı kontrol edilmelidir.

Ancak input validation tek başına SQL Injection savunması değildir. OWASP da input validation’ın yardımcı bir katman olduğunu, asıl savunmanın güvenli ve parametreli API kullanımı olduğunu vurgular.

### WAF

Web Application Firewall bazı şüpheli istekleri engelleyebilir.

Ancak WAF temel açığı düzeltmez ve tek savunma olarak kullanılmamalıdır. Güvenli kodlama yapılmadan yalnızca WAF’a güvenmek yeterli değildir.

---

## 10.6. Parolayı SQL Sorgusunda Aramamak

Şu yaklaşım önerilmez:

```sql
SELECT *
FROM users
WHERE email = ?
AND password = ?;
```

Parola hash’lenmiş olsa bile daha doğru akış şöyledir:

1. E-posta ile kullanıcı kaydı bulunur.
2. Kullanıcının saklanan parola hash’i alınır.
3. Parola, güvenli parola doğrulama fonksiyonuyla karşılaştırılır.
4. Sonuç doğruysa authentication başarılı olur.

---

# 11. Cross-Site Scripting — XSS

## 11.1. XSS Nedir?

XSS, saldırganın kontrol ettiği içeriğin başka kullanıcıların tarayıcısında çalıştırılabilir HTML veya JavaScript olarak yorumlanmasıdır.

XSS’in hedefi veri tabanı değil, çoğunlukla kullanıcının tarayıcısıdır.

OWASP, XSS’in güvenilmeyen verinin dinamik web içeriğine güvenli biçimde dönüştürülmeden eklenmesi sonucunda oluştuğunu belirtir. Saldırı; hesap taklidi, session bilgisi hırsızlığı, hassas verilerin okunması veya sayfa içeriğinin değiştirilmesi gibi sonuçlara neden olabilir.

---

## 11.2. Güvensiz Örnek

```javascript
resultElement.innerHTML =
  "Arama sonucu: " + userInput;
```

Kullanıcı girdisi doğrudan `innerHTML` içerisine yerleştirilmektedir.

Tarayıcı bu girdiyi yalnızca metin olarak değil HTML olarak yorumlayabilir. Girdi içerisinde çalıştırılabilir bir yapı bulunuyorsa saldırgan kodu sayfada çalışabilir.

Güvenli yaklaşım:

```javascript
resultElement.textContent =
  "Arama sonucu: " + userInput;
```

`textContent`, girdiyi HTML olarak yorumlamak yerine metin olarak ekler.

---

## 11.3. Reflected XSS

Zararlı girdi istekte gönderilir ve sunucunun cevabında hemen geri yansıtılır.

Örneğin arama parametresi sayfada güvenli biçimde encode edilmeden gösterilebilir.

```text
/search?q=kullanıcı-girdisi
```

Saldırgan özel hazırlanmış bağlantıyı mağdura gönderir. Mağdur bağlantıyı açtığında zararlı içerik mağdurun tarayıcısında çalışabilir.

---

## 11.4. Stored XSS

Zararlı içerik veri tabanına veya kalıcı bir depoya kaydedilir.

Örnek alanlar:

* Yorum
* Profil açıklaması
* Ürün yorumu
* Forum mesajı
* Destek talebi
* Kullanıcı adı
* Dosya adı

Başka kullanıcılar bu içeriği görüntülediğinde zararlı kod çalışabilir.

Stored XSS, tek bir girdinin çok sayıda kullanıcıyı etkileyebilmesi nedeniyle oldukça tehlikelidir.

---

## 11.5. DOM-Based XSS

Güvenlik açığı tamamen tarayıcı tarafındaki JavaScript kodunda oluşur.

Örneğin:

```javascript
page.innerHTML = window.location.hash;
```

URL fragment değeri güvenli biçimde işlenmeden DOM’a yazıldığı için saldırgan tarayıcı tarafındaki kod akışını kullanabilir.

OWASP, reflected, stored ve DOM tabanlı olmak üzere genel olarak üç XSS biçimini ele alır.

---

## 11.6. XSS Sonuçları

XSS sonucunda saldırgan:

* Kullanıcı adına işlem yapabilir.
* Sayfa içeriğini değiştirebilir.
* Sahte giriş formu gösterebilir.
* Kullanıcı girdilerini okuyabilir.
* Hassas verileri dışarı gönderebilir.
* Kullanıcıyı başka bir siteye yönlendirebilir.
* API isteklerini kullanıcı oturumu üzerinden çalıştırabilir.
* HttpOnly olmayan cookie ve token’ları okuyabilir.
* Yönetici hesabını hedefleyerek daha büyük zarar oluşturabilir.

---

## 11.7. XSS Nasıl Önlenir?

### Output Encoding

Veri, yerleştirileceği bağlama uygun biçimde encode edilmelidir.

Bağlamlar birbirinden farklıdır:

* HTML gövdesi
* HTML attribute
* URL
* JavaScript
* CSS

HTML için güvenli olan encoding yöntemi JavaScript bağlamında yeterli olmayabilir.

Bu nedenle yalnızca genel bir “özel karakterleri değiştir” fonksiyonu bütün XSS türlerini engelleyemez.

### Güvenli DOM API’leri

Riskli:

```javascript
element.innerHTML = userInput;
```

Daha güvenli:

```javascript
element.textContent = userInput;
```

Riskli:

```javascript
document.write(userInput);
```

Daha güvenli:

```javascript
document.createTextNode(userInput);
```

### HTML Sanitization

Uygulamanın kullanıcıdan gerçekten HTML kabul etmesi gerekiyorsa içerik güvenilir ve güncel bir sanitizer kütüphanesiyle temizlenmelidir.

Örneğin zengin metin editörlerinde şu etiketlere izin verilebilir:

```html
<p>
<strong>
<em>
<ul>
<li>
```

Ancak script, event handler ve tehlikeli URL şemaları kaldırılmalıdır.

Sanitization ile encoding aynı şey değildir:

* Encoding, HTML’in metin olarak gösterilmesini sağlar.
* Sanitization, izin verilen HTML yapısını korurken tehlikeli kısımları kaldırır.

### Framework Korumasını Devre Dışı Bırakmamak

React gibi modern framework’ler değerleri JSX içerisinde varsayılan olarak escape eder.

Genellikle güvenli:

```jsx
<p>{userComment}</p>
```

Riskli:

```jsx
<div
  dangerouslySetInnerHTML={{
    __html: userComment
  }}
/>
```

OWASP, React’in `dangerouslySetInnerHTML`, Angular’ın güvenlik kontrollerini atlayan fonksiyonları ve benzeri “escape hatch” kullanım biçimlerinin XSS riski oluşturabileceğini belirtir.

### Content Security Policy — CSP

CSP, tarayıcının hangi kaynaklardan script, stil, görsel veya başka içerik yükleyebileceğini sınırlar.

Örnek politika:

```http
Content-Security-Policy:
default-src 'self';
script-src 'self';
object-src 'none';
```

CSP, XSS’e karşı ek savunma katmanıdır.

Ancak güvenli output encoding ve sanitization yerine geçmez. OWASP da CSP’nin temel güvenli geliştirme uygulamalarının üzerine eklenen bir savunma katmanı olması gerektiğini belirtir.

### HttpOnly Cookie

Session cookie’sine `HttpOnly` eklenmesi JavaScript ile cookie değerinin okunmasını engeller.

Ancak XSS açığını ortadan kaldırmaz. Saldırgan kullanıcının tarayıcısı üzerinden yetkili istekler gönderebilir.

### Tehlikeli JavaScript Fonksiyonlarından Kaçınmak

Dikkat edilmesi gereken bazı yapılar:

```javascript
eval()
document.write()
innerHTML
outerHTML
new Function()
setTimeout(string)
setInterval(string)
```

Bu fonksiyonların tamamı her durumda güvensiz değildir. Ancak kullanıcı kontrollü veriler bu yapılara gönderildiğinde ciddi risk oluşur.

### URL Doğrulama

Kullanıcı girdisi `href` veya `src` gibi alanlarda kullanılıyorsa izin verilen protokoller kontrol edilmelidir.

Örneğin yalnızca şunlara izin verilebilir:

```text
https:
http:
```

`javascript:` gibi çalıştırılabilir URL şemaları reddedilmelidir.

---

# 12. SQL Injection ve XSS Karşılaştırması

| Özellik                      | SQL Injection                                        | XSS                                                                 |
| ---------------------------- | ---------------------------------------------------- | ------------------------------------------------------------------- |
| Hedef                        | Veri tabanı ve backend sorguları                     | Kullanıcının tarayıcısı                                             |
| Temel neden                  | Kullanıcı girdisinin SQL koduyla birleştirilmesi     | Güvenilmeyen içeriğin çalıştırılabilir web içeriğine dönüştürülmesi |
| Çalıştığı yer                | Genellikle sunucu tarafı                             | Genellikle istemci tarafı                                           |
| Olası sonuç                  | Veri okuma, değiştirme, silme, authentication bypass | Kullanıcı oturumunu kötüye kullanma, sayfa değiştirme, veri çalma   |
| Temel savunma                | Parametreli sorgular                                 | Bağlama uygun output encoding                                       |
| Ek savunma                   | Allow-list, least privilege, güvenli ORM kullanımı   | Sanitization, CSP, güvenli DOM API’leri                             |
| Input validation yeterli mi? | Hayır                                                | Hayır                                                               |
| WAF tek başına yeterli mi?   | Hayır                                                | Hayır                                                               |

---

# 13. Güvenli Bir Giriş Sisteminin Genel Akışı

Aşağıdaki yapı temel bir güvenli authentication ve authorization akışını göstermektedir.

## 13.1. Kayıt İşlemi

1. Kullanıcı e-posta ve parola gönderir.
2. Backend alanları doğrular.
3. Parola politikası kontrol edilir.
4. E-posta normalize edilir.
5. Parola Argon2id veya uygun parola hashing algoritmasıyla hash’lenir.
6. Her parola için benzersiz salt kullanılır.
7. Yalnızca parola hash’i veri tabanına kaydedilir.
8. E-posta doğrulama token’ı oluşturulur.
9. Token sınırlı süreyle geçerli olur.
10. Kullanıcı e-posta adresini doğrular.

---

## 13.2. Giriş İşlemi

1. Kullanıcı e-posta ve parola gönderir.
2. Rate limiting kontrol edilir.
3. Kullanıcı kaydı bulunur.
4. Parola güvenli doğrulama fonksiyonuyla karşılaştırılır.
5. Hesap durumu kontrol edilir.
6. Gerekiyorsa MFA tamamlanır.
7. Başarılı giriş loglanır.
8. Session kimliği yenilenir veya token oluşturulur.
9. Kullanıcıya yalnızca ihtiyaç duyulan bilgiler gönderilir.

---

## 13.3. Yetkili API İsteği

1. Kullanıcı API isteği gönderir.
2. Session veya token alınır.
3. Token imzası doğrulanır.
4. Token süresi kontrol edilir.
5. Issuer ve audience kontrol edilir.
6. Kullanıcının aktif olup olmadığı kontrol edilir.
7. Endpoint için gerekli izin belirlenir.
8. Kullanıcının bu izne sahip olup olmadığı kontrol edilir.
9. Kaynak sahipliği kontrol edilir.
10. Yalnızca izin verilen işlem gerçekleştirilir.

Örneğin:

```text
Authentication:
Kullanıcı giriş yapmış mı?

Endpoint authorization:
Kullanıcının order.read izni var mı?

Object authorization:
Bu sipariş gerçekten bu kullanıcıya mı ait?
```

Üç kontrol birbirinden farklıdır ve her biri gerekebilir.

---

# 14. Yaygın Güvenlik Hataları

## 14.1. Yalnızca Frontend’de Yetki Kontrolü Yapmak

Buton gizlemek API’yi korumaz.

Yetkilendirme backend tarafında uygulanmalıdır.

---

## 14.2. JWT’yi Yalnızca Decode Etmek

Decode işlemi payload’ı okumaktır.

Doğrulama değildir.

İmza ve claim kontrolleri yapılmadan token’a güvenilmemelidir.

---

## 14.3. JWT İçerisine Parola Koymak

JWT payload’ı çoğunlukla okunabilir durumdadır.

Token içerisine sır veya gereksiz kişisel bilgi konulmamalıdır.

---

## 14.4. Çok Uzun Ömürlü Access Token Kullanmak

Token çalınırsa uzun süre kullanılabilir.

Kısa ömürlü access token ve kontrollü refresh token yaklaşımı tercih edilmelidir.

---

## 14.5. OAuth’u Authentication Sanmak

OAuth, temel olarak authorization içindir.

Kullanıcı girişi için OpenID Connect kullanılmalıdır.

---

## 14.6. Kullanıcı Rolünü İstemciden Kabul Etmek

Riskli istek:

```json
{
  "email": "user@example.com",
  "role": "admin"
}
```

Kayıt sırasında rol istemcinin gönderdiği değerden alınmamalıdır.

Varsayılan rol sunucu tarafından belirlenmelidir:

```javascript
const role = "user";
```

---

## 14.7. Input Validation’ı Tek Savunma Sanmak

Input validation önemlidir ancak:

* SQL Injection için parametreli sorgunun,
* XSS için output encoding veya sanitization’ın,
* Authorization için sunucu tarafı erişim kontrolünün

yerine geçmez.

---

## 14.8. Hataları Kullanıcıya Ayrıntılı Göstermek

Stack trace, SQL hatası, dosya yolu veya kullanılan framework sürümü saldırgana bilgi verebilir.

Kullanıcıya genel hata gösterilmeli, ayrıntılar güvenli loglarda tutulmalıdır.

---

## 14.9. Gizli Bilgileri Kaynak Koda Yazmak

Riskli:

```javascript
const JWT_SECRET = "my-secret-key";
```

Gizli bilgiler:

* Environment variable
* Secret manager
* Güvenli deployment yapılandırması

üzerinden yönetilmelidir.

Ancak environment variable kullanmak tek başına yeterli değildir. Production ortamında erişimler ve loglar da korunmalıdır.

---

## 14.10. Her Kullanıcıya Fazla Yetki Vermek

Bütün kullanıcıların admin olması geliştirme sürecini kolaylaştırabilir fakat ciddi güvenlik riski oluşturur.

Least privilege ilkesi uygulanmalıdır.

---

## 14.11. Logout İşleminde Yalnızca Arayüzü Değiştirmek

Kullanıcıyı login sayfasına yönlendirmek gerçek logout değildir.

Gerekli durumda:

* Session sunucuda silinmeli,
* Cookie temizlenmeli,
* Refresh token iptal edilmeli,
* Token rotation kayıtları güncellenmelidir.

---

# 15. Güvenli Yazılım Geliştirme Kontrol Listesi

## Authentication

* Parolalar açık metin olarak saklanmıyor.
* Parolalar güçlü parola hashing algoritmasıyla saklanıyor.
* Her parola için benzersiz salt kullanılıyor.
* Login endpoint’inde rate limiting bulunuyor.
* MFA desteği değerlendiriliyor.
* Hata mesajları kullanıcı varlığını gereksiz biçimde açıklamıyor.
* Başarılı girişten sonra session kimliği yenileniyor.
* Kritik işlemlerde yeniden authentication uygulanıyor.

## Authorization

* Her kritik endpoint sunucu tarafında korunuyor.
* Varsayılan erişim politikası reddetme üzerine kurulu.
* Kullanıcı rolleri ve izinleri açık biçimde tanımlı.
* Nesne sahipliği kontrol ediliyor.
* Kullanıcı yalnızca kendi verilerine erişebiliyor.
* Yönetici işlemleri ayrı izinlerle korunuyor.
* Yetkilendirme testleri yazılıyor.
* Frontend’den gelen rol ve kullanıcı kimliği değerlerine güvenilmiyor.

## Session ve Token

* HTTPS zorunlu.
* Cookie’lerde `HttpOnly`, `Secure` ve uygun `SameSite` ayarları bulunuyor.
* Access token kısa ömürlü.
* Refresh token güvenli saklanıyor.
* Refresh token rotation uygulanıyor.
* JWT imzası doğrulanıyor.
* `exp`, `iss`, `aud` ve gerekliyse `nbf` kontrol ediliyor.
* İzin verilen JWT algoritmaları sunucu tarafından belirleniyor.
* Token ve session değerleri loglanmıyor.
* Logout gerçek token veya session iptali gerçekleştiriyor.

## SQL Injection

* String birleştirmeyle SQL sorgusu oluşturulmuyor.
* Parametreli sorgular kullanılıyor.
* Raw SQL kullanımı kod incelemesinden geçiriliyor.
* Dinamik tablo ve sütun adları allow-list ile kontrol ediliyor.
* Veri tabanı kullanıcısı en az yetkiye sahip.
* Ham veri tabanı hataları kullanıcıya gösterilmiyor.
* ORM kullanılması otomatik güvenlik garantisi sayılmıyor.

## XSS

* Kullanıcı girdileri uygun bağlamda encode ediliyor.
* Gereksiz `innerHTML` kullanılmıyor.
* React içerisinde `dangerouslySetInnerHTML` kullanımından kaçınılıyor.
* HTML gerektiğinde güvenilir sanitizer kullanılıyor.
* Tehlikeli URL şemaları doğrulanıyor.
* CSP ek güvenlik katmanı olarak uygulanıyor.
* Cookie’ler mümkün olduğunda `HttpOnly` olarak işaretleniyor.
* Kullanıcı girdileri script, style veya event handler bağlamına doğrudan yerleştirilmiyor.

---

# 16. Mülakat Soruları ve Kısa Cevaplar

## Authentication ve authorization arasındaki fark nedir?

Authentication kullanıcının kim olduğunu doğrular. Authorization ise doğrulanan kullanıcının hangi işlemleri yapabileceğini belirler.

---

## Kullanıcı giriş yaptıysa neden yeniden authorization kontrolü gerekir?

Giriş yapmak yalnızca kullanıcının kimliğini doğrular. Her kullanıcı aynı kaynaklara ve işlemlere erişemez. Bu nedenle her kritik işlemde rol, izin ve kaynak sahipliği kontrol edilmelidir.

---

## JWT şifrelenmiş midir?

Her zaman değildir. Yaygın JWT’ler imzalanmıştır fakat payload Base64URL ile kodlandığı için okunabilir. İmza bütünlüğü sağlar; gizlilik sağlamaz. Şifreleme gerekiyorsa JWE gibi uygun mekanizmalar kullanılmalıdır.

---

## JWT’nin üç bölümü nedir?

Header, payload ve signature.

---

## JWT payload’ına parola koyulur mu?

Hayır. Payload çoğunlukla okunabilir. Parola, gizli anahtar ve hassas kişisel bilgiler token içinde tutulmamalıdır.

---

## Access token ile refresh token arasındaki fark nedir?

Access token API’ye erişmek için kullanılır ve genellikle kısa ömürlüdür. Refresh token yeni access token almak için kullanılır, daha uzun ömürlü ve daha hassastır.

---

## JWT neden kolayca iptal edilemez?

JWT genellikle kendi içerisinde geçerlilik bilgisi taşıyan stateless bir token’dır. Sunucu yalnızca imzayı ve süreyi kontrol ediyorsa token süresi dolana kadar geçerli kalır. İptal için deny-list, token version, kısa access token ömrü veya stateful kontrol mekanizması gerekebilir.

---

## OAuth nedir?

OAuth, kullanıcının parolasını üçüncü taraf uygulamayla paylaşmadan belirli kaynaklara sınırlı erişim verilmesini sağlayan authorization framework’üdür.

---

## OAuth authentication sağlar mı?

OAuth’un temel amacı authorization’dır. Authentication için OAuth üzerinde çalışan OpenID Connect kullanılabilir.

---

## Access token ve ID token arasındaki fark nedir?

Access token API’ye erişmek için kullanılır. ID token, client uygulamaya kullanıcının kimliği hakkında doğrulanabilir bilgi sağlamak için kullanılır.

---

## PKCE neden kullanılır?

Authorization code’un ele geçirilmesi durumunda saldırganın code’u token’a çevirmesini zorlaştırır. Client’ın oluşturduğu `code_verifier` ile authorization isteğindeki `code_challenge` eşleştirilir.

---

## SQL Injection nedir?

Kullanıcı girdisinin SQL sorgusuna güvenli biçimde ayrıştırılmadan eklenmesi sonucunda saldırganın sorgunun yapısını değiştirebilmesidir.

---

## SQL Injection’a karşı en etkili temel savunma nedir?

Prepared statement ve parametreli sorgu kullanmaktır.

---

## Input validation SQL Injection’ı tamamen önler mi?

Hayır. Yardımcı bir güvenlik katmanıdır. Asıl savunma kullanıcı verisini SQL kodundan ayıran parametreli sorgulardır.

---

## ORM kullanmak SQL Injection’ı tamamen önler mi?

Hayır. ORM güvenli sorgu oluşturmayı kolaylaştırabilir fakat raw query, string birleştirme ve hatalı dinamik sorgu kullanımı tekrar açık oluşturabilir.

---

## XSS nedir?

Güvenilmeyen içeriğin başka kullanıcıların tarayıcısında çalıştırılabilir HTML veya JavaScript olarak yorumlanmasıdır.

---

## XSS türleri nelerdir?

Reflected XSS, stored XSS ve DOM-based XSS.

---

## XSS’e karşı temel savunma nedir?

Veriyi kullanılacağı bağlama uygun şekilde encode etmek, HTML gerekiyorsa güvenilir sanitization kullanmak ve güvenli DOM API’lerini tercih etmektir.

---

## `innerHTML` neden risklidir?

Atanan değeri yalnızca metin olarak değil HTML olarak yorumlar. Kullanıcı kontrollü içerik eklenirse çalıştırılabilir kod oluşabilir.

---

## CSP tek başına XSS’i önler mi?

Hayır. CSP ek bir savunma katmanıdır. Output encoding, sanitization ve güvenli kodlamanın yerine geçmez.

---

## 401 ve 403 arasındaki fark nedir?

401 genellikle kullanıcının kimliğinin doğrulanamadığını veya geçerli kimlik bilgisinin bulunmadığını ifade eder. 403 ise kullanıcı doğrulanmış olsa bile istenen işlem için yetkisinin olmadığını belirtir.

---

## Frontend’de butonu gizlemek authorization sağlar mı?

Hayır. Kullanıcı API isteğini doğrudan gönderebilir. Gerçek authorization kontrolü backend tarafında yapılmalıdır.

---

## IDOR nedir?

Kullanıcının URL veya istek içerisindeki nesne kimliğini değiştirerek başka kullanıcılara ait verilere erişebilmesidir. Temel neden eksik nesne seviyesi authorization kontrolüdür.

---

# 17. Genel Sonuç

Güvenli yazılım geliştirmek, geliştirme tamamlandıktan sonra sisteme eklenecek ayrı bir özellik değildir. Güvenlik; kullanıcı kayıt işleminden API tasarımına, veri tabanı sorgularından frontend’de içerik göstermeye kadar bütün geliştirme sürecinin parçasıdır.

Authentication ve authorization birbirine bağlı fakat farklı kavramlardır. Authentication kullanıcının kim olduğunu doğrularken authorization kullanıcının hangi işlemleri gerçekleştirebileceğini belirler. Bir kullanıcının sisteme giriş yapmış olması, sistemdeki bütün kaynaklara erişebileceği anlamına gelmez.

JWT, kullanıcı veya yetki bilgilerini servisler arasında taşımak için kullanılabilen güçlü bir token formatıdır. Ancak JWT şifreleme ile karıştırılmamalı, payload içerisine hassas bilgi konulmamalı, imza ve bütün claim’ler doğrulanmalıdır. Access token’lar kısa ömürlü tutulmalı, refresh token’lar daha sıkı korunmalı ve token yaşam döngüsü dikkatle yönetilmelidir.

OAuth 2.0, kullanıcı parolalarının üçüncü taraf uygulamalarla paylaşılmadan sınırlı erişim verilmesini sağlar. Ancak OAuth doğrudan authentication protokolü değildir. Kullanıcı kimliğinin doğrulanması gerektiğinde OpenID Connect kullanılmalıdır. Modern OAuth uygulamalarında Authorization Code Flow, PKCE, kesin redirect URI kontrolü ve en az yetkili scope kullanımı önemlidir.

SQL Injection, kullanıcı verisinin SQL komutuyla birleştirilmesi sonucunda oluşur. Temel savunma parametreli sorgulardır. Input validation, ORM, WAF ve veri tabanı yetkileri ek koruma sağlayabilir ancak parametreli sorgunun yerini tutmaz.

XSS ise güvenilmeyen içeriğin kullanıcının tarayıcısında kod olarak çalıştırılmasıdır. XSS’e karşı bağlama uygun output encoding, gerektiğinde sanitization, güvenli DOM API’leri ve ek katman olarak Content Security Policy kullanılmalıdır.

Sonuç olarak güvenli bir yazılım:

* Kullanıcı kimliğini güvenli şekilde doğrular.
* Her işlemde gerekli yetkiyi kontrol eder.
* Parolaları geri döndürülemeyecek şekilde saklar.
* Session ve token yaşam döngüsünü yönetir.
* Kullanıcı girdilerini hiçbir zaman güvenilir kabul etmez.
* SQL kodu ile kullanıcı verisini birbirinden ayırır.
* Tarayıcıya gönderilen veriyi uygun bağlamda güvenli hâle getirir.
* Hataları, logları ve gizli bilgileri kontrollü biçimde yönetir.
* Bütün güvenlik kontrollerini yalnızca frontend’de değil, güvenilir backend tarafında uygular.

Bu prensipler uygulandığında yalnızca “çalışan” değil, aynı zamanda saldırılara karşı daha dayanıklı, sürdürülebilir ve güvenilir yazılımlar geliştirilebilir.