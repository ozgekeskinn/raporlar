# 14. Testing Mantığı

## İçindekiler

1. [Testing Nedir?](#1-testing-nedir)
2. [Neden Test Yazarız?](#2-neden-test-yazarız)
3. [Manuel Test ve Otomatik Test](#3-manuel-test-ve-otomatik-test)
4. [Test Seviyelerine Genel Bakış](#4-test-seviyelerine-genel-bakış)
5. [Unit Test Nedir?](#5-unit-test-nedir)
   - [5.1 Unit Testin Temel Özellikleri](#51-unit-testin-temel-özellikleri)
   - [5.2 Unit Testte Ne Test Edilir?](#52-unit-testte-ne-test-edilir)
   - [5.3 Unit Test Örneği](#53-unit-test-örneği)
   - [5.4 İyi Bir Unit Test Nasıl Olmalıdır?](#54-iyi-bir-unit-test-nasıl-olmalıdır)
   - [5.5 Unit Testin Avantajları](#55-unit-testin-avantajları)
   - [5.6 Unit Testin Sınırları](#56-unit-testin-sınırları)
6. [Integration Test Nedir?](#6-integration-test-nedir)
   - [6.1 Integration Testte Ne Test Edilir?](#61-integration-testte-ne-test-edilir)
   - [6.2 Integration Test Örneği](#62-integration-test-örneği)
   - [6.3 Integration Testin Avantajları](#63-integration-testin-avantajları)
   - [6.4 Integration Testin Dezavantajları](#64-integration-testin-dezavantajları)
7. [E2E Test Nedir?](#7-e2e-test-nedir)
   - [7.1 E2E Testte Ne Test Edilir?](#71-e2e-testte-ne-test-edilir)
   - [7.2 E2E Test Örneği](#72-e2e-test-örneği)
   - [7.3 E2E Testin Avantajları](#73-e2e-testin-avantajları)
   - [7.4 E2E Testin Dezavantajları](#74-e2e-testin-dezavantajları)
8. [Unit vs Integration vs E2E](#8-unit-vs-integration-vs-e2e)
9. [Test Piramidi](#9-test-piramidi)
10. [Mocking Nedir?](#10-mocking-nedir)
    - [10.1 Mocking Neden Kullanılır?](#101-mocking-neden-kullanılır)
    - [10.2 Mock Neleri Taklit Edebilir?](#102-mock-neleri-taklit-edebilir)
    - [10.3 Mock Örneği](#103-mock-örneği)
    - [10.4 Mock Kullanmanın Avantajları](#104-mock-kullanmanın-avantajları)
    - [10.5 Mock Kullanırken Dikkat Edilmesi Gerekenler](#105-mock-kullanırken-dikkat-edilmesi-gerekenler)
11. [Test Doubles: Dummy, Stub, Fake, Spy ve Mock](#11-test-doubles-dummy-stub-fake-spy-ve-mock)
12. [Arrange - Act - Assert Yapısı](#12-arrange---act---assert-yapısı)
13. [Given - When - Then Yaklaşımı](#13-given---when---then-yaklaşımı)
14. [Test Case Nedir?](#14-test-case-nedir)
15. [Positive, Negative ve Edge Case Testleri](#15-positive-negative-ve-edge-case-testleri)
16. [Regression Testing Nedir?](#16-regression-testing-nedir)
17. [Smoke Test ve Sanity Test](#17-smoke-test-ve-sanity-test)
18. [Test Coverage Nedir?](#18-test-coverage-nedir)
19. [Test Isolation Nedir?](#19-test-isolation-nedir)
20. [Deterministic Test Nedir?](#20-deterministic-test-nedir)
21. [Flaky Test Nedir?](#21-flaky-test-nedir)
22. [Test Edilebilir Kod Nasıl Yazılır?](#22-test-edilebilir-kod-nasıl-yazılır)
23. [Dependency Injection ve Testing İlişkisi](#23-dependency-injection-ve-testing-ilişkisi)
24. [Frontend Testing Mantığı](#24-frontend-testing-mantığı)
25. [Backend Testing Mantığı](#25-backend-testing-mantığı)
26. [API Testing](#26-api-testing)
27. [Database Testing](#27-database-testing)
28. [CI/CD Süreçlerinde Testlerin Rolü](#28-cicd-süreçlerinde-testlerin-rolü)
29. [TDD - Test Driven Development](#29-tdd---test-driven-development)
30. [BDD - Behavior Driven Development](#30-bdd---behavior-driven-development)
31. [İyi Test Yazma Prensipleri](#31-iyi-test-yazma-prensipleri)
32. [Sık Yapılan Testing Hataları](#32-sık-yapılan-testing-hataları)
33. [Gerçek Bir Uygulamada Test Stratejisi](#33-gerçek-bir-uygulamada-test-stratejisi)
34. [Testing Araçları](#34-testing-araçları)
35. [Mülakatlarda Bilinmesi Gereken Temel Noktalar](#35-mülakatlarda-bilinmesi-gereken-temel-noktalar)
36. [Özet Tablo](#36-özet-tablo)
37. [Genel Sonuç](#37-genel-sonuç)

---

# 1. Testing Nedir?

**Software Testing**, geliştirilen bir yazılımın beklenen şekilde çalışıp çalışmadığını kontrol etme sürecidir. Testing yalnızca "uygulama çalışıyor mu?" sorusuna cevap vermez. Aynı zamanda şu sorulara da cevap arar:

- Girilen doğru veride doğru sonuç üretiliyor mu?
- Hatalı veri geldiğinde sistem kontrollü davranıyor mu?
- Yeni eklenen özellik eski özellikleri bozuyor mu?
- Backend ile frontend doğru haberleşiyor mu?
- Veritabanına doğru veri yazılıyor mu?
- API doğru HTTP status code'u döndürüyor mu?
- Kullanıcı uygulamadaki temel işlemleri baştan sona tamamlayabiliyor mu?
- Sistem beklenmeyen durumlarda güvenli şekilde hata verebiliyor mu?

Testing'in temel amacı, yazılım hatalarını mümkün olduğunca **erken**, **tekrar üretilebilir** ve **otomatik** şekilde yakalamaktır. Bir yazılım projesi büyüdükçe yalnızca manuel kontrol yapmak sürdürülebilir olmaktan çıkar. Çünkü bir değişiklik, uygulamanın başka bir bölümünü fark edilmeden bozabilir. Bu nedenle profesyonel yazılım projelerinde testler, kodun yanında yaşayan ikinci bir güvenlik katmanı olarak düşünülebilir.

---

# 2. Neden Test Yazarız?

Test yazmanın temel amacı yalnızca bug bulmak değildir. Testler aynı zamanda yazılım geliştirme sürecinin güvenilirliğini artırır.

## Testlerin sağladığı başlıca faydalar

### Hataları erken yakalar

Bir hata production ortamına çıktıktan sonra düzeltilmesi çok daha maliyetlidir. Unit test sırasında bulunan bir hata ise çoğu zaman birkaç dakika içinde düzeltilebilir.

---

### Refactoring yapmayı kolaylaştırır

**Refactoring**, kodun dış davranışını değiştirmeden iç yapısını iyileştirmektir. Örneğin:

```text
Eski kod çalışıyor
        ↓
Kod temizleniyor / yeniden düzenleniyor
        ↓
Testler çalıştırılıyor
        ↓
Tüm testler geçiyorsa davranış korunmuş demektir
```

Testler olmadan refactoring yapmak daha risklidir.

---

### Regression hatalarını önler

Yeni bir özellik eklediğimizde daha önce çalışan bir özellik bozulabilir. Bu duruma **regression** denir. Örneğin:

```text
Sepete ürün ekleme çalışıyor.
Yeni indirim sistemi geliştiriliyor.
Ancak yeni kod nedeniyle sepette toplam fiyat yanlış hesaplanmaya başlıyor.
```

Daha önce yazılmış testler bu problemi otomatik olarak yakalayabilir.

---

### Kodun davranışını belgeler

İyi yazılmış testler, bir fonksiyonun nasıl çalışması gerektiğini açıkça gösterir. Örneğin:

```javascript
expect(calculateDiscount(1000, 10)).toBe(900);
```

Bu test aynı zamanda fonksiyonun beklenen davranışını anlatmaktadır.

---

### Kod kalitesini artırır

Test yazması zor olan kod çoğu zaman:

- çok fazla sorumluluk taşır,
- bağımlılıkları fazladır,
- tightly coupled yapıdadır,
- global state kullanıyordur,
- birden fazla işi aynı fonksiyonda yapıyordur.

Bu nedenle test yazmak, geliştiriciyi daha modüler kod yazmaya teşvik eder.

---

### Takım çalışmasını güvenli hale getirir

Büyük projelerde aynı kod tabanı üzerinde birçok developer çalışır. Testler sayesinde bir developer'ın yaptığı değişikliğin diğer modülleri bozup bozmadığı otomatik olarak kontrol edilebilir.

---

# 3. Manuel Test ve Otomatik Test

Testing iki temel şekilde yapılabilir.

## Manuel Test

Bir kişinin uygulamayı doğrudan kullanarak kontrol etmesidir. Örneğin:

1. Login ekranını açmak
2. Kullanıcı adı ve şifre girmek
3. Login butonuna basmak
4. Dashboard açılıyor mu kontrol etmek

Avantajı:

- Kullanıcı deneyimi problemlerini fark etmek kolaydır.
- Exploratory testing için faydalıdır.

Dezavantajı:

- Tekrarlanması zaman alır.
- İnsan hatasına açıktır.
- Her kod değişikliğinde tüm sistemi manuel kontrol etmek mümkün değildir.

---

## Otomatik Test

Test senaryolarının kod ile yazılması ve otomatik çalıştırılmasıdır. Örneğin:

```javascript
test("iki sayıyı toplar", () => {
    expect(sum(2, 3)).toBe(5);
});
```

CI/CD pipeline içerisinde yüzlerce veya binlerce test otomatik olarak çalıştırılabilir.

---

# 4. Test Seviyelerine Genel Bakış

Yazılım testleri farklı seviyelerde yapılabilir. En yaygın üç test seviyesi:

```text
Unit Test
   ↓
Integration Test
   ↓
E2E Test
```

Her test seviyesi farklı bir problemi kontrol eder.

| Test Türü | Ne Test Edilir? |
|---|---|
| Unit Test | Tek fonksiyon, class veya component |
| Integration Test | Birden fazla modülün birlikte çalışması |
| E2E Test | Kullanıcı akışının baştan sona çalışması |

---

# 5. Unit Test Nedir?

**Unit Test**, uygulamanın en küçük bağımsız parçasını test eden test türüdür. Bu küçük parça genellikle:

- fonksiyon,
- method,
- class,
- component,
- service fonksiyonu

olabilir. Unit testin amacı, ilgili parçanın diğer sistemlerden mümkün olduğunca bağımsız şekilde doğru çalışıp çalışmadığını kontrol etmektir.

---

## 5.1 Unit Testin Temel Özellikleri

İyi bir unit test genellikle:

- hızlıdır,
- küçük bir kod parçasını test eder,
- dış sistemlere bağımlı değildir,
- veritabanına bağlanmaz,
- gerçek API çağrısı yapmaz,
- kolay tekrar çalıştırılır,
- aynı girdide aynı sonucu üretir.

Örneğin:

```javascript
function multiply(a, b) {
    return a * b;
}
```

Test:

```javascript
test("3 ile 4 çarpıldığında 12 döner", () => {
    expect(multiply(3, 4)).toBe(12);
});
```

Burada yalnızca `multiply` fonksiyonu test edilir.

---

## 5.2 Unit Testte Ne Test Edilir?

Unit test ile aşağıdaki yapılar test edilebilir:

### Hesaplama fonksiyonları

```javascript
calculatePrice()
calculateDiscount()
calculateTax()
```

### Validation fonksiyonları

```javascript
isValidEmail()
validatePassword()
validatePhoneNumber()
```

### Business logic

```javascript
canUserPurchase()
calculateShippingCost()
isEligibleForDiscount()
```

### Utility fonksiyonları

```javascript
formatDate()
capitalizeText()
convertCurrency()
```

### Frontend component davranışları

Örneğin:

```text
Button disabled mı?
Hata mesajı gösteriliyor mu?
Component doğru veriyi render ediyor mu?
```

---

## 5.3 Unit Test Örneği

Bir indirim fonksiyonumuz olsun:

```javascript
function calculateDiscount(price, discountRate) {
    return price - price * discountRate / 100;
}
```

Testler:

```javascript
describe("calculateDiscount", () => {

    test("%10 indirim uygular", () => {
        expect(calculateDiscount(1000, 10)).toBe(900);
    });

    test("%0 indirim fiyatı değiştirmez", () => {
        expect(calculateDiscount(1000, 0)).toBe(1000);
    });

    test("%100 indirim sonucu sıfır yapar", () => {
        expect(calculateDiscount(1000, 100)).toBe(0);
    });

});
```

Burada yalnızca "happy path" değil, sınır durumları da test edilmiştir.

---

## 5.4 İyi Bir Unit Test Nasıl Olmalıdır?

Unit testler mümkün olduğunca:

### Küçük

Bir test çok fazla davranışı aynı anda kontrol etmemelidir.

### Bağımsız

Bir test diğer testin sonucuna bağlı olmamalıdır. Yanlış:

```text
Test 2 çalışabilmek için önce Test 1'in çalışması gerekiyor.
```

Doğru:

```text
Her test kendi verisini oluşturur.
Her test bağımsız çalışır.
```

### Hızlı

Unit testlerde gerçek:

- database,
- network,
- filesystem,
- external API

kullanmak genellikle tercih edilmez.

### Anlaşılır

Test ismi beklenen davranışı açıklamalıdır. Kötü:

```javascript
test("test1", () => {})
```

Daha iyi:

```javascript
test("geçersiz email girildiğinde false döndürür", () => {})
```

---

## 5.5 Unit Testin Avantajları

- Çok hızlı çalışır.
- Hatanın hangi fonksiyonda olduğunu bulmayı kolaylaştırır.
- Refactoring güvenliği sağlar.
- Business logic hatalarını erkenden yakalar.
- Kod kalitesini artırır.
- CI/CD için oldukça uygundur.
- Developer feedback süresini kısaltır.

---

## 5.6 Unit Testin Sınırları

Unit testler tek başına yeterli değildir. Örneğin:

```text
UserService doğru çalışıyor.
DatabaseService doğru çalışıyor.
```

Ancak:

```text
UserService → DatabaseService
```

bağlantısı yanlış kurulmuş olabilir. Yani parçalar ayrı ayrı doğru çalışırken birlikte çalışmayabilir. Bu nedenle **integration test** gereklidir.

---

# 6. Integration Test Nedir?

**Integration Test**, birden fazla modülün veya sistem bileşeninin birlikte doğru çalışıp çalışmadığını kontrol eder. Unit test:

```text
A modülü doğru mu?
```

Integration test:

```text
A modülü B modülü ile doğru iletişim kuruyor mu?
```

Örneğin:

```text
Controller
   ↓
Service
   ↓
Repository
   ↓
Database
```

Bu zincirin birkaç veya tüm parçası birlikte test edilebilir.

---

## 6.1 Integration Testte Ne Test Edilir?

Örnek integration senaryoları:

```text
API → Database
```

```text
Controller → Service
```

```text
Service → Repository
```

```text
Frontend → Backend API
```

```text
Authentication Service → User Repository
```

```text
Order Service → Payment Service
```

---

## 6.2 Integration Test Örneği

Örneğin:

```http
POST /users
```

endpoint'i yeni kullanıcı oluşturuyor. Integration test şu akışı kontrol edebilir:

```text
HTTP Request
      ↓
Controller
      ↓
User Service
      ↓
Repository
      ↓
Test Database
```

Örnek:

```javascript
test("POST /users yeni kullanıcı oluşturur", async () => {

    const response = await request(app)
        .post("/users")
        .send({
            name: "Ayşe",
            email: "ayse@example.com"
        });

    expect(response.status).toBe(201);
    expect(response.body.name).toBe("Ayşe");

});
```

Burada yalnızca bir fonksiyon değil, birden fazla katman birlikte test edilmektedir.

---

## 6.3 Integration Testin Avantajları

- Modüller arasındaki bağlantı hatalarını yakalar.
- API ve database ilişkisini test edebilir.
- Gerçek sisteme unit testten daha yakındır.
- Configuration hatalarını ortaya çıkarabilir.
- Serialization / deserialization sorunlarını yakalayabilir.
- Authentication ve authorization akışlarını test etmek için uygundur.

---

## 6.4 Integration Testin Dezavantajları

Integration testler unit testlere göre:

- daha yavaştır,
- kurulumu daha karmaşıktır,
- database setup gerektirebilir,
- test verisinin temizlenmesini gerektirebilir,
- dış bağımlılıkların yönetilmesi daha zordur.

---

# 7. E2E Test Nedir?

**E2E (End-to-End) Test**, uygulamanın gerçek kullanıcı davranışına benzer şekilde baştan sona test edilmesidir. E2E test şu soruya cevap verir:

> "Gerçek bir kullanıcı bu işlemi uygulamada gerçekten tamamlayabiliyor mu?"

Örneğin bir e-commerce uygulamasında:

```text
Siteyi aç
   ↓
Login ol
   ↓
Ürün ara
   ↓
Ürün detayına git
   ↓
Sepete ekle
   ↓
Checkout yap
   ↓
Sipariş oluştur
```

Bu akışın tamamının otomatik test edilmesi E2E testtir.

---

## 7.1 E2E Testte Ne Test Edilir?

E2E testlerde genellikle kritik kullanıcı akışları test edilir. Örnekler:

### Login

```text
Login sayfası açılır
Email girilir
Şifre girilir
Login butonuna basılır
Dashboard görüntülenir
```

### E-commerce checkout

```text
Ürün seç
Sepete ekle
Adres gir
Ödeme yap
Sipariş oluştur
```

### İş başvuru sistemi

```text
Login
İlan aç
Başvur butonuna bas
Form doldur
Başvuru gönder
Başvurular ekranında kayıt görünür
```

---

## 7.2 E2E Test Örneği

Cypress benzeri bir örnek:

```javascript
describe("Login Flow", () => {
    it("kullanıcı başarılı şekilde giriş yapabilir", () => {
        cy.visit("/login");
        cy.get("#email")
            .type("user@example.com");
        cy.get("#password")
            .type("123456");
        cy.get("#login-button")
            .click();
        cy.url()
            .should("include", "/dashboard");
    });
});
```

Burada gerçek kullanıcı davranışı simüle edilmektedir.

---

## 7.3 E2E Testin Avantajları

- Gerçek kullanıcı deneyimine en yakın testtir.
- Frontend + backend + database zincirini birlikte test eder.
- Kritik user flow'ları doğrular.
- Sistem seviyesindeki problemlerin bulunmasını sağlar.
- Release öncesi yüksek güven verir.

---

## 7.4 E2E Testin Dezavantajları

E2E testler:

- unit testlere göre çok daha yavaştır,
- bakımı daha zordur,
- test ortamına bağımlıdır,
- UI değişikliklerinden kolay etkilenebilir,
- flaky olma ihtimali daha yüksektir.

Bu nedenle tüm sistemi yalnızca E2E testlerle test etmek doğru bir strateji değildir.

---

# 8. Unit vs Integration vs E2E

| Özellik | Unit Test | Integration Test | E2E Test |
|---|---|---|---|
| Test kapsamı | Küçük | Orta | Büyük |
| Hız | Çok hızlı | Orta | Yavaş |
| Test edilen alan | Fonksiyon / class | Modüller arası iletişim | Tüm sistem |
| Database | Genellikle yok | Olabilir | Genellikle vardır |
| Network | Mock olabilir | Olabilir | Gerçek akışa yakın |
| Hata bulma kolaylığı | Çok yüksek | Orta | Daha zor |
| Gerçek sisteme yakınlık | Düşük | Orta | Çok yüksek |
| Bakım maliyeti | Düşük | Orta | Yüksek |
| Test sayısı | Çok | Orta | Az |

---

# 9. Test Piramidi

Testing stratejisinde sık kullanılan kavramlardan biri **Test Pyramid** yaklaşımıdır.

```text       
               / \
              /   \
             /     \
            /  E2E  \
           /---------\
          /Integration\
         /-------------\
        /   Unit Tests  \
       /_________________\
```

Temel fikir:

```text
Çok sayıda Unit Test
        ↓
Daha az Integration Test
        ↓
Az sayıda kritik E2E Test
```

## Neden?

Çünkü unit testler:

- hızlı,
- ucuz,
- kararlı,
- kolay debug edilebilir.

E2E testler ise:

- daha yavaş,
- daha pahalı,
- daha kırılgan,
- hatanın kaynağını bulması daha zor.

Bu nedenle test stratejisinde denge kurulmalıdır.

---

# 10. Mocking Nedir?

**Mocking**, gerçek bir bağımlılık yerine onun davranışını taklit eden sahte bir nesne veya fonksiyon kullanmaktır. Örneğin bir fonksiyon dış API çağrısı yapıyor olsun:

```text
getWeather()
     ↓
Weather API
```

Unit test sırasında gerçek API'ye istek atmak istemeyebiliriz. Bunun yerine:

```text
getWeather()
     ↓
Mock Weather API
```

kullanabiliriz.

---

## 10.1 Mocking Neden Kullanılır?

Mocking'in temel amaçları şunlardır:

### Testi bağımsız hale getirmek

Unit test yalnızca test edilen kodu kontrol etmelidir. Gerçek API başarısız olursa testimizin de başarısız olması istenmez.

---

### Testi hızlandırmak

Gerçek network çağrıları milisaniyeler veya saniyeler sürebilir. Mock çağrıları ise çok hızlıdır.

---

### Dış sistem bağımlılığını kaldırmak

Örneğin:

- Payment API
- Email Service
- SMS Service
- Google Maps API
- Weather API
- Database
- File system

unit test sırasında gerçek sistemlerle haberleşmek zorunda değildir.

---

### Kontrol edilebilir senaryolar üretmek

Gerçek API'den belirli bir hata almak zor olabilir. Mock ile kolayca oluşturabiliriz:

```text
200 OK
404 Not Found
500 Internal Server Error
Timeout
Network Error
```

---

### Para maliyetini önlemek

Bazı API'ler çağrı başına ücretlendirme yapabilir. Test sırasında gerçek API kullanmak gereksiz maliyet oluşturabilir.

---

## 10.2 Mock Neleri Taklit Edebilir?

Mock aşağıdaki bağımlılıkların yerine kullanılabilir:

- API
- database
- repository
- service
- email sender
- payment gateway
- filesystem
- clock/time
- random generator
- authentication service

---

## 10.3 Mock Örneği

Fonksiyon:

```javascript
async function getUserName(userService, id) {
    const user = await userService.getUser(id);
    return user.name;
}
```

Gerçek `userService` yerine mock kullanabiliriz:

```javascript
test("kullanıcı adını döndürür", async () => {

    const mockUserService = {
        getUser: jest.fn().mockResolvedValue({
            id: 1,
            name: "Özge"
        })
    };

    const result = await getUserName(
        mockUserService,
        1
    );

    expect(result).toBe("Özge");

});
```

Burada gerçek backend veya database çağrısı yapılmaz.

---

## 10.4 Mock Kullanmanın Avantajları

- Testleri hızlandırır.
- Test izolasyonu sağlar.
- Network bağımlılığını kaldırır.
- Hata senaryolarını kolay test etmeyi sağlar.
- Üçüncü taraf servislerin testleri bozmasını engeller.
- Karmaşık sistemleri küçük parçalara ayırarak test etmeyi kolaylaştırır.

---

## 10.5 Mock Kullanırken Dikkat Edilmesi Gerekenler

Aşırı mocking tehlikeli olabilir. Örneğin:

```text
Controller mock
Service mock
Repository mock
Database mock
API mock
```

Her şey mocklanırsa test yalnızca oluşturduğumuz sahte dünyayı test eder. Gerçek sistemde:

```text
Service → Repository
```

entegrasyonu bozuk olabilir. Ancak her ikisi de mocklandığı için test geçebilir. Bu nedenle:

> Unit testlerde mock kullanılır, ancak integration testlerle gerçek bağlantılar da doğrulanmalıdır.

---

# 11. Test Doubles: Dummy, Stub, Fake, Spy ve Mock

Testing dünyasında gerçek bağımlılıkların yerine kullanılan yapılara genel olarak **Test Double** denir.

## Dummy

Test sırasında sadece parametre doldurmak için kullanılan, davranışı önemli olmayan nesnedir.

```text
Fonksiyon parametre istiyor
ama test açısından bu parametrenin davranışı önemli değil.
```

---

## Stub

Belirli bir durumda önceden hazırlanmış cevap döndürür. Örnek:

```javascript
const userService = {
    getUser: () => ({
        id: 1,
        name: "Özge"
    })
};
```

---

## Fake

Gerçek sistemin daha basit çalışan versiyonudur. Örneğin gerçek database yerine:

```text
In-memory database
```

kullanılabilir.

---

## Spy

Bir fonksiyonun çağrılıp çağrılmadığını veya nasıl çağrıldığını kontrol eder. Örneğin:

```javascript
expect(sendEmail).toHaveBeenCalled();
```

veya:

```javascript
expect(sendEmail)
    .toHaveBeenCalledWith("user@example.com");
```

---

## Mock

Belirli davranışları simüle eder ve aynı zamanda interaction doğrulaması yapılmasına izin verebilir. Örneğin:

```text
sendEmail() çağrıldı mı?
kaç kere çağrıldı?
hangi parametrelerle çağrıldı?
```

kontrol edilebilir.

---

# 12. Arrange - Act - Assert Yapısı

Test yazarken en yaygın yapılardan biri **AAA Pattern**'dır.

```text
Arrange
Act
Assert
```

## Arrange

Test için gerekli veriler hazırlanır.

```javascript
const price = 1000;
const discount = 10;
```

## Act

Test edilen fonksiyon çalıştırılır.

```javascript
const result = calculateDiscount(
    price,
    discount
);
```

## Assert

Beklenen sonuç kontrol edilir.

```javascript
expect(result).toBe(900);
```

Tam örnek:

```javascript
test("indirim hesaplanır", () => {

    // Arrange
    const price = 1000;
    const discount = 10;

    // Act
    const result = calculateDiscount(
        price,
        discount
    );

    // Assert
    expect(result).toBe(900);

});
```

---

# 13. Given - When - Then Yaklaşımı

BDD yaklaşımında sık kullanılan yapı:

```text
Given
When
Then
```

Örneğin:

```text
Given: Kullanıcının sepetinde 1000 TL ürün var.
When: %10 indirim uygulanıyor.
Then: Toplam fiyat 900 TL olmalıdır.
```

Bu yapı test senaryolarını business diliyle anlatmayı kolaylaştırır.

---

# 14. Test Case Nedir?

**Test Case**, belirli bir davranışı kontrol etmek için tanımlanan test senaryosudur. Bir test case genellikle şu bölümlerden oluşur:

```text
Test ID
Test adı
Ön koşullar
Input
Adımlar
Beklenen sonuç
Gerçek sonuç
Durum
```

Örnek:

```text
Test: Başarılı Login

Input:
email = user@example.com
password = 123456

Expected:
Dashboard açılmalı.
```

---

# 15. Positive, Negative ve Edge Case Testleri

İyi testler yalnızca doğru girdileri kontrol etmez.

## Positive Test

Normal kullanım senaryosu.

```text
Doğru email + doğru password
→ Login başarılı
```

---

## Negative Test

Hatalı giriş senaryosu.

```text
Doğru email + yanlış password
→ Login başarısız
```

---

## Edge Case

Sınır değerler test edilir. Örneğin yaş sınırı 18 ise:

```text
17
18
19
```

değerleri test edilmelidir. Password minimum 8 karakter ise:

```text
7 karakter
8 karakter
9 karakter
```

test edilmelidir.

---

# 16. Regression Testing Nedir?

**Regression Testing**, yeni yapılan değişikliklerin daha önce çalışan özellikleri bozup bozmadığını kontrol etmektir. Örneğin:

```text
Login sistemi çalışıyor.
        ↓
Yeni "Remember Me" özelliği ekleniyor.
        ↓
Eski login testleri tekrar çalıştırılıyor.
```

Eğer eski testlerden biri başarısız olursa regression problemi oluşmuş olabilir. Otomatik testlerin en büyük faydalarından biri regression kontrolüdür.

---

# 17. Smoke Test ve Sanity Test

## Smoke Test

Sistemin en temel fonksiyonlarının çalışıp çalışmadığını hızlı şekilde kontrol eder. Örneğin:

```text
Uygulama açılıyor mu?
Login çalışıyor mu?
Dashboard açılıyor mu?
Ana API cevap veriyor mu?
```

Amaç:

> "Build test edilmeye değer durumda mı?"

---

## Sanity Test

Belirli bir değişiklik veya bug fix sonrasında ilgili özelliğin temel olarak çalıştığını kontrol eder. Örneğin:

```text
Sepete ürün ekleme hatası düzeltildi.

Sanity test:
Sepete ürün eklenebiliyor mu?
```

---

# 18. Test Coverage Nedir?

**Test Coverage**, kodun ne kadarının testler tarafından çalıştırıldığını ölçen metriktir. Örneğin:

```text
1000 satır kod
800 satır test sırasında çalıştırılıyor
```

yaklaşık:

```text
%80 coverage
```

elde edilebilir. Coverage türleri:

- Line Coverage
- Function Coverage
- Branch Coverage
- Statement Coverage

---

## Line Coverage

Kaç kod satırının test sırasında çalıştığını ölçer.

---

## Function Coverage

Kaç fonksiyonun test edildiğini ölçer.

---

## Branch Coverage

`if / else` gibi farklı kontrol akışlarının test edilip edilmediğini ölçer. Örneğin:

```javascript
if (age >= 18) {
    return "adult";
} else {
    return "minor";
}
```

İyi coverage için hem:

```text
age >= 18
```

hem de:

```text
age < 18
```

senaryoları test edilmelidir.

---

## Yüksek Coverage Her Zaman İyi Test Demek Değildir

Önemli bir nokta:

```text
%100 coverage ≠ %100 doğru yazılım
```

Kötü assertion'lar ile yüksek coverage elde edilebilir. Önemli olan sadece kodu çalıştırmak değil, doğru davranışı kontrol etmektir.

---

# 19. Test Isolation Nedir?

Her test mümkün olduğunca bağımsız olmalıdır. Bir testin sonucu başka testin sonucuna bağlı olmamalıdır. Yanlış:

```text
Test 1 kullanıcı oluşturuyor.
Test 2 Test 1'in oluşturduğu kullanıcıyı kullanıyor.
```

Test 1 başarısız olursa Test 2 de başarısız olur. Daha iyi yaklaşım:

```text
Her test kendi test datasını oluşturur.
Test sonunda temizler.
```

---

# 20. Deterministic Test Nedir?

**Deterministic test**, aynı koşullarda her çalıştırıldığında aynı sonucu veren testtir. Örneğin:

```text
Input: 2 + 2
Expected: 4
```

Her zaman geçmelidir. Testin sonucu:

- internet hızına,
- saate,
- rastgele sayıya,
- başka teste,
- dış API'ye

bağlı olmamalıdır.

---

# 21. Flaky Test Nedir?

**Flaky Test**, kod değişmemesine rağmen bazen geçen bazen başarısız olan testtir. Örneğin:

```text
Run 1 → PASS
Run 2 → PASS
Run 3 → FAIL
Run 4 → PASS
```

Flaky testlerin yaygın nedenleri:

- network bağımlılığı,
- yanlış async yönetimi,
- race condition,
- zamanlama problemleri,
- random değerler,
- shared database state,
- UI elementlerinin geç yüklenmesi,
- testlerin birbirine bağımlı olması.

Flaky testler CI/CD sistemlerinde güven kaybına neden olur.

---

# 22. Test Edilebilir Kod Nasıl Yazılır?

Testing yalnızca test dosyası yazmak değildir. Kodun da test edilebilir tasarlanması gerekir. Test edilebilir kod genellikle:

- küçük fonksiyonlardan oluşur,
- tek sorumluluk taşır,
- bağımlılıkları dışarıdan alır,
- global state'e az bağımlıdır,
- side effectleri kontrollüdür,
- interface veya abstraction kullanır.

---

## Test edilmesi zor kod

```javascript
function createOrder(order) {
    const db = new Database();
    const payment = new StripePayment();
    const email = new EmailService();

    db.save(order);
    payment.pay(order.total);
    email.send(order.userEmail);
}
```

Fonksiyon:

- database oluşturuyor,
- payment çağırıyor,
- email gönderiyor.

Unit test yazmak zorlaşır.

---

## Daha test edilebilir yapı

```javascript
function createOrder(
    order,
    db,
    paymentService,
    emailService
) {
    db.save(order);
    paymentService.pay(order.total);
    emailService.send(order.userEmail);
}
```

Bağımlılıklar dışarıdan verildiği için mock kullanılabilir.

---

# 23. Dependency Injection ve Testing İlişkisi

**Dependency Injection**, bir class veya fonksiyonun ihtiyaç duyduğu bağımlılıkların içeride oluşturulmak yerine dışarıdan verilmesidir. Örneğin:

```javascript
class OrderService {
    constructor(paymentService) {
        this.paymentService = paymentService;
    }
}
```

Production:

```javascript
new OrderService(
    new StripePaymentService()
);
```

Test:

```javascript
new OrderService(
    mockPaymentService
);
```

Bu yaklaşım test yazmayı ciddi şekilde kolaylaştırır.

---

# 24. Frontend Testing Mantığı

Frontend testleri birkaç seviyede yapılabilir.

## Component Unit Test

Bir React component'in render davranışı test edilir. Örneğin:

```text
Button görünüyor mu?
Loading mesajı doğru mu?
Error mesajı gösteriliyor mu?
```

---

## Component Interaction Test

Kullanıcı etkileşimi test edilir. Örneğin:

```text
Button tıklanınca modal açılıyor mu?
Form submit edilince callback çalışıyor mu?
```

---

## Integration Test

Birden fazla component birlikte test edilir. Örneğin:

```text
SearchInput
    ↓
ProductList
    ↓
Filtered Products
```

---

## E2E Test

Browser üzerinde gerçek kullanıcı akışı test edilir. Örneğin:

```text
Login
→ ürün ara
→ ürün aç
→ sepete ekle
```

---

## Frontend testinde neyi test etmeliyiz?

Kullanıcının görebildiği davranışları test etmek genellikle daha değerlidir. Örneğin kötü yaklaşım:

```text
component state şu değere geldi mi?
```

Daha iyi yaklaşım:

```text
kullanıcı ekranda beklenen sonucu görüyor mu?
```

---

# 25. Backend Testing Mantığı

Backend tarafında testler genellikle şu katmanlarda yapılır:

```text
Controller
Service
Repository
Database
External API
```

## Service Unit Test

Business logic test edilir. Örneğin:

```text
kullanıcı yeterli bakiyeye sahip mi?
indirim uygulanmalı mı?
sipariş oluşturulabilir mi?
```

---

## Controller Test

Request ve response davranışı test edilir. Örneğin:

```text
POST /users
→ 201 Created
```

Hatalı input:

```text
POST /users
→ 400 Bad Request
```

---

## Repository Test

Database işlemleri test edilir. Örneğin:

```text
save()
findById()
delete()
update()
```

---

# 26. API Testing

API testlerinde aşağıdaki noktalar kontrol edilir:

## HTTP Status Code

Örneğin:

```text
200 OK
201 Created
400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
500 Internal Server Error
```

---

## Response Body

Örneğin:

```json
{
  "id": 15,
  "name": "Laptop"
}
```

---

## Validation

Hatalı veri gönderildiğinde:

```text
400 Bad Request
```

dönmeli.

---

## Authentication

Token olmadan:

```text
401 Unauthorized
```

dönmeli.

---

## Authorization

Yetkisiz kullanıcı:

```text
403 Forbidden
```

almalı.

---

# 27. Database Testing

Database içeren integration testlerde dikkat edilmesi gereken konular vardır.

## Test database kullanılmalıdır

Production database kesinlikle kullanılmamalıdır. Örneğin:

```text
app_database
app_test_database
```

---

## Test verisi kontrollü olmalıdır

Her test kendi datasını oluşturmalıdır.

---

## Cleanup yapılmalıdır

Test sonrasında oluşturulan kayıtlar silinmelidir. Örneğin:

```text
beforeEach
afterEach
```

hookları kullanılabilir.

---

## Transaction rollback

Bazı sistemlerde test sonunda transaction rollback yapılarak database eski haline getirilebilir.

---

# 28. CI/CD Süreçlerinde Testlerin Rolü

Modern yazılım geliştirmede testler genellikle CI/CD pipeline içerisinde otomatik çalıştırılır. Örnek akış:

```text
Developer kod yazar
        ↓
     Git push
        ↓
    CI Pipeline
        ↓
       Lint
        ↓
    Unit Tests
        ↓
 Integration Tests
        ↓
      Build
        ↓
    E2E Tests
        ↓
     Deploy
```

Eğer testlerden biri başarısız olursa deployment durdurulabilir. Bu sayede bozuk kodun production ortamına çıkması engellenir.

---

# 29. TDD - Test Driven Development

**TDD (Test Driven Development)**, önce testin yazıldığı geliştirme yaklaşımıdır. TDD döngüsü:

```text
   RED
    ↓
  GREEN
    ↓
 REFACTOR
```

## Red

Önce başarısız test yazılır.

```javascript
expect(sum(2, 3)).toBe(5);
```

Fonksiyon henüz olmadığı için test başarısızdır.

---

## Green

Testi geçirecek minimum kod yazılır.

```javascript
function sum(a, b) {
    return a + b;
}
```

---

## Refactor

Kod temizlenir ve iyileştirilir. Testler tekrar çalıştırılır.

---

# 30. BDD - Behavior Driven Development

**BDD (Behavior Driven Development)**, sistemi teknik implementasyondan çok davranış üzerinden tanımlar. Örnek:

```text
Given kullanıcı login ekranında
When doğru email ve password girer
Then dashboard görüntülenmelidir
```

BDD teknik ekip ile business ekibi arasında ortak dil oluşturmayı amaçlar.

---

# 31. İyi Test Yazma Prensipleri

İyi testler için bazı temel prensipler vardır.

## 1. Bir test tek davranışı test etsin

Bir test içerisinde onlarca farklı özellik kontrol edilmemelidir.

---

## 2. Test adı açıklayıcı olsun

Kötü:

```text
test1
userTest
works
```

İyi:

```text
geçersiz şifre girildiğinde login başarısız olmalıdır
```

---

## 3. Implementation değil behavior test edin

Test:

```text
Kod bunu nasıl yaptı?
```

yerine:

```text
Kod doğru sonucu üretti mi?
```

sorusuna odaklanmalıdır.

---

## 4. Testler bağımsız olmalı

Bir test diğerine bağlı olmamalıdır.

---

## 5. Test verisi anlaşılır olmalı

Magic number kullanımından kaçınılmalıdır.

---

## 6. Gereksiz mock kullanmayın

Sadece izolasyon gerektiğinde mock kullanılmalıdır.

---

## 7. Edge case'leri unutmayın

Özellikle:

```text
null
undefined
empty string
0
negative values
maximum values
minimum values
```

gibi durumlar önemlidir.

---

## 8. Testler hızlı olmalı

Özellikle unit testler birkaç saniye içinde yüzlerce çalışabilmelidir.

---

## 9. Testler tekrar üretilebilir olmalı

Her makinede aynı sonucu vermelidir.

---

## 10. Kritik business logic mutlaka test edilmeli

Özellikle:

- ödeme,
- fiyat,
- indirim,
- yetkilendirme,
- sipariş,
- finansal hesaplama,
- validation

gibi alanlar yüksek önceliklidir.

---

# 32. Sık Yapılan Testing Hataları

## Sadece Happy Path Test Etmek

Örneğin yalnızca:

```text
doğru email
doğru password
```

test edilirse hata senaryoları kaçırılır.

---

## Çok Fazla E2E Test Yazmak

Her şeyi E2E ile test etmek:

- test süresini artırır,
- bakımı zorlaştırır,
- flaky test sayısını artırabilir.

---

## Aşırı Mock Kullanmak

Her bağımlılığı mocklamak gerçek entegrasyon problemlerini gizleyebilir.

---

## Private Implementation Detaylarını Test Etmek

Kod refactor edildiğinde davranış aynı kalmasına rağmen testler bozulabilir.

---

## Testleri Birbirine Bağımlı Yazmak

Test sırası değiştiğinde testler başarısız olabilir.

---

## Gerçek Production API Kullanmak

Test ortamı dış servise bağımlı hale gelir.

---

## Rastgele Veriyi Kontrolsüz Kullanmak

Her çalıştırmada farklı sonuç oluşabilir.

---

## Testleri Yazıp CI'da Çalıştırmamak

Testlerin asıl gücü otomatik çalıştırıldığında ortaya çıkar.

---

# 33. Gerçek Bir Uygulamada Test Stratejisi

Örnek bir e-commerce sistemi düşünelim. Sistemde:

```text
Product
Cart
Order
Payment
User
Authentication
```

modülleri bulunuyor.

## Unit Test

```text
calculateTotal()
calculateDiscount()
validateEmail()
validatePassword()
canUserCheckout()
```

---

## Integration Test

```text
OrderService → OrderRepository
UserController → UserService
POST /orders → Database
```

---

## E2E Test

```text
    Login
      ↓
  Ürün seç
      ↓
 Sepete ekle
      ↓
   Checkout
      ↓
    Ödeme
      ↓
Sipariş oluştur
```

Bu yaklaşım test piramidine uygundur.

---

# 34. Testing Araçları

Kullanılan teknolojiye göre testing araçları değişebilir.

## JavaScript / TypeScript

### Jest

Genellikle unit testing için kullanılır.

### Vitest

Özellikle Vite projelerinde yaygındır.

### React Testing Library

React componentlerini kullanıcı davranışına yakın şekilde test etmek için kullanılır.

### Cypress

Frontend ve E2E testing için kullanılır.

### Playwright

Modern browser automation ve E2E testing için kullanılır.

### Supertest

Node.js API endpoint testlerinde kullanılabilir.

---

## Python

### pytest

En yaygın Python testing frameworklerinden biridir.

### unittest

Python standard library içerisinde bulunur.

---

## Java

### JUnit

Java için en yaygın unit testing frameworklerinden biridir.

### Mockito

Mocking için kullanılır.

---

## .NET

### xUnit

Unit testing frameworküdür.

### NUnit

Yaygın .NET testing frameworklerinden biridir.

### Moq

Mock oluşturmak için kullanılabilir.

---

## API Testing

### Postman

Manuel ve otomatik API testleri yapılabilir.

### Newman

Postman collection'larını terminal veya CI/CD üzerinde çalıştırmayı sağlar.

---

# 35. Mülakatlarda Bilinmesi Gereken Temel Noktalar

## Unit test nedir?

Bir fonksiyon, class veya component gibi küçük ve izole bir kod biriminin davranışını test eden test türüdür.

---

## Integration test nedir?

Birden fazla modülün veya sistem bileşeninin birlikte doğru çalışıp çalışmadığını test eder.

---

## E2E test nedir?

Gerçek bir kullanıcı akışını frontend'den backend ve database'e kadar baştan sona test eder.

---

## Mock nedir?

Gerçek bir bağımlılığın yerine kullanılan ve onun davranışını taklit eden test nesnesidir.

---

## Mock neden kullanılır?

- dış bağımlılıkları izole etmek,
- testleri hızlandırmak,
- network veya database bağımlılığını azaltmak,
- hata senaryolarını kolay simüle etmek.

---

## Unit test ile integration test arasındaki fark nedir?

Unit test tek bir parçayı izole test eder.
Integration test birden fazla parçanın birlikte çalışmasını test eder.

---

## E2E test neden az yazılır?

Çünkü:
- yavaştır,
- bakımı daha maliyetlidir,
- UI değişikliklerinden etkilenebilir,
- flaky olma ihtimali daha yüksektir.

---

## Test Pyramid nedir?

Testlerin çoğunun unit test, daha azının integration test ve en azının E2E test olması gerektiğini anlatan testing yaklaşımıdır.

---

## Test coverage nedir?

Kodun ne kadarının testler tarafından çalıştırıldığını gösteren metriktir. Ancak yüksek coverage tek başına yüksek test kalitesi anlamına gelmez.

---

## Regression test nedir?

Yeni yapılan değişikliklerin eski çalışan özellikleri bozup bozmadığını kontrol eden testtir.

---

## Flaky test nedir?

Aynı kodda bazı çalıştırmalarda geçen bazı çalıştırmalarda başarısız olan kararsız testtir.

---

## Mock ile Stub farkı nedir?

Basitleştirilmiş şekilde:

```text
Stub: Belirli input için hazırlanmış cevap döndürür.
Mock: Davranışı taklit eder ve çoğu zaman çağrıların nasıl yapıldığını da doğrular.
```

---

# 36. Özet Tablo

| Kavram | Açıklama |
|---|---|
| Testing | Yazılımın beklenen davranışı gösterip göstermediğini kontrol etme süreci |
| Unit Test | Küçük ve izole kod parçalarını test eder |
| Integration Test | Birden fazla modülün birlikte çalışmasını test eder |
| E2E Test | Kullanıcı akışını baştan sona test eder |
| Mocking | Gerçek bağımlılığın davranışını taklit eder |
| Stub | Önceden belirlenmiş cevap döndüren test double |
| Fake | Gerçek sistemin basitleştirilmiş çalışan versiyonu |
| Spy | Fonksiyon çağrılarını gözlemlemek için kullanılır |
| Regression Test | Yeni değişikliklerin eski özellikleri bozup bozmadığını kontrol eder |
| Smoke Test | Sistemin temel özelliklerinin çalıştığını hızlıca kontrol eder |
| Sanity Test | Belirli değişiklik sonrası ilgili alanın çalışmasını kontrol eder |
| Test Coverage | Kodun ne kadarının test sırasında çalıştırıldığını gösterir |
| Flaky Test | Bazen geçen bazen başarısız olan kararsız test |
| Test Isolation | Testlerin birbirinden bağımsız olması |
| TDD | Önce test, sonra kod yazma yaklaşımı |
| BDD | Sistemi davranışlar üzerinden tanımlayan yaklaşım |
| AAA | Arrange, Act, Assert test yapısı |
| Test Pyramid | Çok unit, daha az integration, az E2E yaklaşımı |
| CI/CD Testing | Testlerin otomatik pipeline içerisinde çalıştırılması |

---

# 37. Genel Sonuç

Testing, profesyonel yazılım geliştirmenin temel parçalarından biridir. Bir proje küçükken bütün sistemi manuel olarak kontrol etmek mümkün görünebilir. Ancak uygulama büyüdükçe yeni özelliklerin mevcut kodu bozma ihtimali artar. Bu nedenle otomatik testler, yazılımın güvenli şekilde büyümesini sağlar. Temel testing stratejisi şu şekilde düşünülebilir:

```text
 Business Logic
      ↓
  Unit Tests

Modüller Arası İletişim
      ↓
Integration Tests

Kritik Kullanıcı Akışları
          ↓
      E2E Tests
```

Mocking ise özellikle unit testlerde dış bağımlılıkları izole ederek testlerin hızlı ve güvenilir çalışmasını sağlar. Sağlıklı bir projede amaç yalnızca "çok test yazmak" değildir. Amaç:

```text
Doğru seviyede
doğru davranışı
doğru test türüyle
kontrol etmektir.
```

İyi bir test sistemi sayesinde developer:

- yeni özellik eklerken daha güvenli hareket eder,
- refactoring yapmaktan korkmaz,
- regression hatalarını daha erken yakalar,
- production buglarını azaltır,
- kod kalitesini yükseltir,
- takım içinde daha sürdürülebilir bir kod tabanı oluşturur.

Kısacası:

> **Testler kodun büyümesini yavaşlatmaz; doğru yazıldığında kodun güvenli ve kontrollü şekilde büyümesini sağlar.**