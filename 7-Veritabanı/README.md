# Veritabanı Mantığı ve SQL Temelleri

## İçindekiler

## İçindekiler

1. [Veritabanı Nedir?](#1-veritabanı-nedir)
2. [Relational Database (İlişkisel Veritabanı) Nedir?](#2-relational-database-ilişkisel-veritabanı-nedir)
3. [Tablo, Satır ve Sütun Mantığı](#3-tablo-satır-ve-sütun-mantığı)
4. [SQL (Structured Query Language) Nedir?](#4-sql-structured-query-language-nedir)
5. [SQL Komut Türleri](#5-sql-komut-türleri)
   - [5.1. DQL - Data Query Language](#51-dql---data-query-language)
   - [5.2. DML - Data Manipulation Language](#52-dml---data-manipulation-language)
   - [5.3. DDL - Data Definition Language](#53-ddl---data-definition-language)
6. [Primary Key Nedir?](#6-primary-key-nedir)
7. [Foreign Key Nedir?](#7-foreign-key-nedir)
8. [Primary Key ve Foreign Key Farkı](#8-primary-key-ve-foreign-key-farkı)
9. [SELECT Nedir?](#9-select-nedir)
10. [WHERE, ORDER BY ve LIMIT Kullanımı](#10-where-order-by-ve-limit-kullanımı)
11. [JOIN Nedir?](#11-join-nedir)
12. [JOIN Türleri](#12-join-türleri)
    - [12.1. INNER JOIN](#121-inner-join)
    - [12.2. LEFT JOIN](#122-left-join)
    - [12.3. RIGHT JOIN](#123-right-join)
    - [12.4. FULL JOIN](#124-full-join)
13. [GROUP BY Nedir?](#13-group-by-nedir)
14. [Aggregate Fonksiyonlar](#14-aggregate-fonksiyonlar)
15. [GROUP BY ve JOIN Birlikte Kullanımı](#15-group-by-ve-join-birlikte-kullanımı)
16. [HAVING Nedir?](#16-having-nedir)
17. [WHERE ve HAVING Farkı](#17-where-ve-having-farkı)
18. [SQL Sorgularında Mantıksal Çalışma Sırası](#18-sql-sorgularında-mantıksal-çalışma-sırası)
19. [Index Nedir?](#19-index-nedir)
20. [Index Ne İşe Yarar?](#20-index-ne-işe-yarar)
21. [Index Her Zaman İyi midir?](#21-index-her-zaman-iyi-midir)
22. [Unique Index Nedir?](#22-unique-index-nedir)
23. [Veritabanı İlişki Türleri](#23-veritabanı-ilişki-türleri)
    - [23.1. One-to-One İlişki](#231-one-to-one-ilişki)
    - [23.2. One-to-Many İlişki](#232-one-to-many-ilişki)
    - [23.3. Many-to-Many İlişki](#233-many-to-many-ilişki)
24. [Normalizasyon Nedir?](#24-normalizasyon-nedir)
25. [CRUD Mantığı](#25-crud-mantığı)
26. [SQL ve Backend İlişkisi](#26-sql-ve-backend-ilişkisi)
27. [Örnek E-Ticaret Veritabanı Tasarımı](#27-örnek-e-ticaret-veritabanı-tasarımı)
28. [SELECT, JOIN ve GROUP BY Birlikte Örnek](#28-select-join-ve-group-by-birlikte-örnek)
29. [SQL Veri Tipleri](#29-sql-veri-tipleri)
30. [NULL Nedir?](#30-null-nedir)
31. [En Çok Kullanılan SQL Kalıpları](#31-en-çok-kullanılan-sql-kalıpları)
32. [İş Hayatında SQL Kullanımı](#32-iş-hayatında-sql-kullanımı)
33. [Mini Pratik Örnekler](#33-mini-pratik-örnekler)
34. [Genel Özet](#34-genel-özet)

---

# 1. Veritabanı Nedir?

Veritabanı, verilerin düzenli, güvenli ve yönetilebilir şekilde saklandığı sistemdir.

Bir yazılım uygulamasında kullanılan veriler genellikle geçici değildir. Kullanıcı sisteme kayıt olduğunda, ürün sepete eklendiğinde, sipariş oluşturulduğunda, ödeme yapıldığında veya bir rapor alındığında bu bilgilerin kalıcı olarak saklanması gerekir.

Bu verilerin rastgele dosyalarda tutulması büyük projelerde ciddi sorunlara neden olur. Çünkü veri miktarı arttıkça arama yapmak, veri güncellemek, veri silmek, rapor almak ve veriler arasında ilişki kurmak zorlaşır.

Bu yüzden veriler belirli bir sistem içinde saklanır. Bu sisteme veritabanı denir. Örneğin bir e-ticaret sitesinde şu veriler bulunabilir:

- Kullanıcı bilgileri
- Ürün bilgileri
- Sipariş bilgileri
- Sepet bilgileri
- Ödeme bilgileri
- Kargo adresleri
- Ürün yorumları
- Stok bilgileri
- Kategori bilgileri

Bu veriler veritabanında düzenli tablolar halinde tutulur. Örneğin kullanıcı bilgileri için bir tablo oluşturulabilir:

| id | ad | email | telefon |
|---|---|---|---|
| 1 | Ayşe | ayse@gmail.com | 5551112233 |
| 2 | Mehmet | mehmet@gmail.com | 5554445566 |

Ürün bilgileri için ayrı bir tablo oluşturulabilir:

| id | urun_adi | fiyat | stok |
|---|---|---|---|
| 1 | Laptop | 25000 | 12 |
| 2 | Mouse | 500 | 40 |

Sipariş bilgileri için de ayrı bir tablo oluşturulabilir:

| id | kullanici_id | toplam_tutar | tarih |
|---|---|---|---|
| 1 | 2 | 25500 | 2026-05-30 |
| 2 | 1 | 500 | 2026-05-31 |

Bu yapı sayesinde her veri kendi alanına uygun şekilde saklanır. Kısaca veritabanı, yazılım sistemlerinde verilerin düzenli şekilde saklandığı, yönetildiği ve sorgulandığı yapıdır.

---

# 2. Relational Database (İlişkisel Veritabanı) Nedir?

İlişkisel veritabanı, verileri tablolar halinde saklayan ve bu tablolar arasında ilişki kurulmasını sağlayan veritabanı türüdür. İlişkisel veritabanlarında temel mantık şudur:

> Her bilgi doğru tabloda tutulur ve tablolar birbirine anahtar alanlar üzerinden bağlanır.

Örneğin bir sipariş sisteminde kullanıcı bilgileri, ürün bilgileri ve sipariş bilgileri aynı tabloda tutulmaz. Her biri ayrı tabloda tutulur. Kötü bir tablo tasarımı şu şekilde olabilir:

| siparis_id | kullanici_adi | kullanici_email | urun_adi | fiyat |
|---|---|---|---|---|
| 1 | Ayşe | ayse@gmail.com | Mouse | 500 |
| 2 | Ayşe | ayse@gmail.com | Klavye | 1200 |
| 3 | Ayşe | ayse@gmail.com | Kulaklık | 900 |

Bu yapıda Ayşe’nin adı ve e-posta adresi tekrar tekrar yazılmıştır. Bu durum iyi bir veritabanı tasarımı değildir. Çünkü:

- Gereksiz veri tekrarı oluşur.
- Kullanıcının e-posta adresi değişirse birden fazla satır güncellenmek zorunda kalır.
- Güncelleme sırasında bazı satırlar unutulabilir.
- Veri tutarsızlığı oluşabilir.
- Tablo büyüdükçe bakım zorlaşır.
- Raporlama işlemleri karmaşıklaşır.

Daha doğru tasarımda kullanıcı bilgileri ayrı tabloda, sipariş bilgileri ayrı tabloda tutulur.

## users tablosu

| id | ad | email |
|---|---|---|
| 1 | Ayşe | ayse@gmail.com |

## orders tablosu

| id | user_id | tarih |
|---|---|---|
| 1 | 1 | 2026-05-30 |
| 2 | 1 | 2026-05-31 |

Burada `orders` tablosundaki `user_id`, `users` tablosundaki `id` alanına bağlanır. Yani sistem şu mantıkla çalışır:

> orders tablosundaki user_id değeri 1 ise, bu sipariş users tablosunda id değeri 1 olan kullanıcıya aittir.

Bu yapı ilişkisel veritabanı mantığının temelidir.

---

# 3. Tablo, Satır ve Sütun Mantığı

İlişkisel veritabanlarında veriler tablo yapısı içinde tutulur. Bir tablo, belirli bir veri grubunu saklamak için kullanılır. Örneğin:

- `users` tablosu kullanıcıları tutar.
- `products` tablosu ürünleri tutar.
- `orders` tablosu siparişleri tutar.
- `categories` tablosu kategorileri tutar.
- `payments` tablosu ödeme bilgilerini tutar.

## Sütun Nedir?

Sütun, tablodaki her kayıt için tutulacak bilgi türünü ifade eder. Örneğin `users` tablosunda şu sütunlar olabilir:

| id | name | email | password |
|---|---|---|---|

Burada:

- `id` kullanıcı kimliğini tutar.
- `name` kullanıcı adını tutar.
- `email` kullanıcının e-posta adresini tutar.
- `password` kullanıcının şifresini tutar.

## Satır Nedir?

Satır, tablodaki gerçek bir kaydı temsil eder. Örneğin:

| id | name | email |
|---|---|---|
| 1 | Özge | ozge@gmail.com |

Bu satır bir kullanıcı kaydıdır.

# 4. SQL (Structured Query Language) Nedir?

SQL, veritabanlarıyla iletişim kurmak için kullanılan sorgu dilidir. SQL sayesinde veritabanına komutlar verebiliriz.Örneğin:

- Tüm kullanıcıları getir.
- Yeni ürün ekle.
- Bir kullanıcının e-posta adresini güncelle.
- Stok miktarı sıfır olan ürünleri sil.
- En çok sipariş veren müşterileri listele.
- Kullanıcı ve sipariş tablolarını birleştir.
- Verileri gruplandır.
- Toplam satış miktarını hesapla.
- En pahalı ürünü bul.

Basit bir SQL sorgusu şu şekildedir:

    SELECT * FROM users;

Bu sorgunun anlamı:

> users tablosundaki tüm kayıtları getir.

SQL, özellikle ilişkisel veritabanlarında kullanılır. MySQL, PostgreSQL, Microsoft SQL Server, Oracle ve SQLite gibi veritabanı sistemlerinde SQL kullanılır.

---

# 5. SQL Komut Türleri

SQL komutları kullanım amacına göre farklı kategorilere ayrılır. En temel SQL komut türleri şunlardır:

- DQL
- DML
- DDL
- DCL
- TCL

Başlangıç seviyesinde en çok DQL, DML ve DDL kullanılır.

---

## 5.1. DQL - Data Query Language

DQL, veri sorgulamak için kullanılır. En temel komut:

    SELECT

Örnek:

    SELECT name, email
    FROM users;

Bu sorgu `users` tablosundan sadece `name` ve `email` sütunlarını getirir.

---

## 5.2. DML - Data Manipulation Language

DML, veri ekleme, veri güncelleme ve veri silme işlemlerinde kullanılır. Başlıca komutlar:

    INSERT
    UPDATE
    DELETE

Yeni kullanıcı ekleme örneği:

    INSERT INTO users (name, email)
    VALUES ('Özge', 'ozge@gmail.com');

Kullanıcı e-posta adresi güncelleme örneği:

    UPDATE users
    SET email = 'yeni@mail.com'
    WHERE id = 1;

Kullanıcı silme örneği:

    DELETE FROM users
    WHERE id = 1;

Burada `WHERE` kullanımı çok önemlidir. Çünkü `WHERE` kullanılmazsa tüm tablo etkilenebilir.Tehlikeli kullanım:

    DELETE FROM users;

Bu sorgu, `users` tablosundaki tüm kullanıcıları silebilir.

---

## 5.3. DDL - Data Definition Language

DDL, veritabanı yapısını oluşturmak veya değiştirmek için kullanılır. Başlıca komutlar:

    CREATE
    ALTER
    DROP

Tablo oluşturma örneği:

    CREATE TABLE users (
        id INT PRIMARY KEY,
        name VARCHAR(100),
        email VARCHAR(150)
    );

Tabloya yeni sütun ekleme örneği:

    ALTER TABLE users
    ADD phone VARCHAR(20);

Tablo silme örneği:

    DROP TABLE users;

DDL komutları doğrudan veritabanı yapısını etkilediği için dikkatli kullanılmalıdır.

---

# 6. Primary Key Nedir?

Primary key, bir tablodaki her satırı benzersiz şekilde tanımlayan alandır. Genellikle `id` alanı primary key olarak kullanılır.

Örnek:

| id | name | email |
|---|---|---|
| 1 | Ayşe | ayse@gmail.com |
| 2 | Mehmet | mehmet@gmail.com |
| 3 | Zeynep | zeynep@gmail.com |

Burada `id` alanı primary key’dir. Çünkü:

- Her kullanıcıyı benzersiz şekilde tanımlar.
- Aynı `id` iki farklı kullanıcıda olamaz.
- Boş bırakılamaz.
- Diğer tablolar bu kullanıcıya `id` üzerinden bağlanabilir.

SQL ile primary key tanımlama örneği:

    CREATE TABLE users (
        id INT PRIMARY KEY,
        name VARCHAR(100),
        email VARCHAR(150)
    );

Primary key için iki temel kural vardır:

1. Tekrarlanamaz.
2. Boş olamaz.

Yanlış bir kullanım:

| id | name |
|---|---|
| 1 | Ayşe |
| 1 | Mehmet |

Bu doğru değildir. Çünkü iki farklı kullanıcının aynı primary key değerine sahip olması veri bütünlüğünü bozar.

---

# 7. Foreign Key Nedir?

Foreign key, bir tablodaki alanın başka bir tablodaki primary key alanına bağlanmasıdır. Foreign key, tablolar arasında ilişki kurmak için kullanılır. Örneğin kullanıcılar ve siparişler arasında ilişki olduğunu düşünelim.

## users tablosu

| id | name |
|---|---|
| 1 | Ayşe |
| 2 | Mehmet |

## orders tablosu

| id | user_id | total |
|---|---|---|
| 1 | 1 | 500 |
| 2 | 2 | 1200 |
| 3 | 1 | 300 |

Burada `orders` tablosundaki `user_id`, `users` tablosundaki `id` alanına bağlanır. Yani:

- `orders.user_id = 1` ise sipariş Ayşe’ye aittir.
- `orders.user_id = 2` ise sipariş Mehmet’e aittir.

SQL ile foreign key tanımlama örneği:

    CREATE TABLE orders (
        id INT PRIMARY KEY,
        user_id INT,
        total DECIMAL(10,2),
        FOREIGN KEY (user_id) REFERENCES users(id)
    );

Bu yapı sayesinde veritabanı şunu kontrol eder:

> orders tablosuna eklenen user_id değeri gerçekten users tablosunda var mı?

Örneğin `users` tablosunda id değeri 99 olan bir kullanıcı yoksa şu kayıt mantıksal olarak hatalıdır:

| id | user_id | total |
|---|---|---|
| 4 | 99 | 800 |

Çünkü 99 numaralı kullanıcı sistemde yoktur. Foreign key sayesinde bu tür hataların önüne geçilir ve veri bütünlüğü korunur.

---

# 8. Primary Key ve Foreign Key Farkı

Primary key ve foreign key veritabanı ilişkilerinin temelini oluşturur.

| Kavram | Görevi | Nerede Bulunur? |
|---|---|---|
| Primary Key | Kendi tablosundaki kaydı benzersiz tanımlar | Ana tabloda |
| Foreign Key | Başka bir tablodaki primary key’e bağlanır | İlişkili tabloda |

Örnek:

## users tablosu

| id | name |
|---|---|
| 1 | Ayşe |

Burada `id`, primary key’dir.

## orders tablosu

| id | user_id |
|---|---|
| 10 | 1 |

Burada:

- `orders.id` kendi tablosunun primary key alanıdır.
- `orders.user_id`, `users.id` alanına bağlanan foreign key alanıdır.

---

# 9. SELECT Nedir?

SELECT, veritabanından veri çekmek için kullanılan SQL komutudur. En temel kullanım:

    SELECT * FROM users;

Buradaki `*` işareti, tüm sütunları getir anlamına gelir. Bu sorgu şu anlama gelir:

> users tablosundaki tüm sütunları ve tüm kayıtları getir.

Daha kontrollü kullanım:

    SELECT name, email
    FROM users;

Bu sorgu sadece `name` ve `email` sütunlarını getirir. Gerçek projelerde genellikle tüm sütunları getirmek yerine ihtiyaç duyulan sütunları seçmek daha doğru bir yaklaşımdır. Çünkü gereksiz veri çekmek performansı olumsuz etkileyebilir.

---

# 10. WHERE, ORDER BY ve LIMIT Kullanımı

## WHERE

WHERE, verileri belirli bir şarta göre filtrelemek için kullanılır. Örnek:

    SELECT *
    FROM products
    WHERE price > 1000;

Bu sorgunun anlamı:

> Fiyatı 1000’den büyük olan ürünleri getir.

Başka bir örnek:

    SELECT *
    FROM users
    WHERE name = 'Ayşe';

Bu sorgu adı Ayşe olan kullanıcıları getirir.

---

## ORDER BY

ORDER BY, sorgu sonucunu belirli bir sütuna göre sıralamak için kullanılır. Küçükten büyüğe sıralama:

    SELECT *
    FROM products
    ORDER BY price ASC;

Büyükten küçüğe sıralama:

    SELECT *
    FROM products
    ORDER BY price DESC;

Burada:

- `ASC` ascending anlamına gelir. Küçükten büyüğe sıralar.
- `DESC` descending anlamına gelir. Büyükten küçüğe sıralar.

---

## LIMIT

LIMIT, getirilecek kayıt sayısını sınırlandırmak için kullanılır. Örnek:

    SELECT *
    FROM products
    LIMIT 5;

Bu sorgu sadece ilk 5 ürünü getirir. SQL Server tarafında benzer işlem için genellikle `TOP` kullanılır:

    SELECT TOP 5 *
    FROM products;

---

# 11. JOIN Nedir?

JOIN, iki veya daha fazla tabloyu ilişkili alanlar üzerinden birleştirmek için kullanılır. İlişkisel veritabanlarının en önemli konularından biridir. Örneğin elimizde iki tablo olsun.

## users tablosu

| id | name |
|---|---|
| 1 | Ayşe |
| 2 | Mehmet |
| 3 | Zeynep |

## orders tablosu

| id | user_id | total |
|---|---|---|
| 1 | 1 | 500 |
| 2 | 2 | 1200 |
| 3 | 1 | 300 |

`orders` tablosunda siparişin hangi kullanıcıya ait olduğu `user_id` ile tutulur. Ancak kullanıcı adı bu tabloda yoktur. Eğer siparişleri kullanıcı adıyla birlikte görmek istersek JOIN kullanırız.

    SELECT orders.id, users.name, orders.total
    FROM orders
    JOIN users ON orders.user_id = users.id;

Bu sorgunun anlamı:

> orders tablosunu users tablosu ile birleştir. orders tablosundaki user_id ile users tablosundaki id eşleşsin. Sonuçta sipariş id, kullanıcı adı ve toplam tutar bilgilerini getir.

Sonuç şu şekilde olabilir:

| id | name | total |
|---|---|---|
| 1 | Ayşe | 500 |
| 2 | Mehmet | 1200 |
| 3 | Ayşe | 300 |

JOIN sayesinde ilişkili tablolardaki veriler birlikte görüntülenebilir.

---

# 12. JOIN Türleri

SQL’de farklı JOIN türleri vardır. En çok kullanılan JOIN türleri şunlardır:

- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- FULL JOIN

---

## 12.1. INNER JOIN

INNER JOIN, sadece iki tabloda da eşleşen kayıtları getirir. Örnek:

    SELECT users.name, orders.total
    FROM users
    INNER JOIN orders ON users.id = orders.user_id;

Bu sorgu sadece siparişi olan kullanıcıları getirir. Eğer bir kullanıcının hiç siparişi yoksa sonuçta görünmez.

---

## 12.2. LEFT JOIN

LEFT JOIN, sol tablodaki tüm kayıtları getirir. Sağ tabloda eşleşme varsa eşleşen verileri getirir, eşleşme yoksa NULL döndürür. Örnek:

    SELECT users.name, orders.total
    FROM users
    LEFT JOIN orders ON users.id = orders.user_id;

Bu sorgu tüm kullanıcıları getirir. Kullanıcının siparişi varsa sipariş bilgisi de gelir. Siparişi yoksa sipariş alanı NULL olur. Örnek sonuç:

| name | total |
|---|---|
| Ayşe | 500 |
| Ayşe | 300 |
| Mehmet | 1200 |
| Zeynep | NULL |

Burada Zeynep’in siparişi yoktur ama LEFT JOIN kullanıldığı için sonuçta görünür.

---

## 12.3. RIGHT JOIN

RIGHT JOIN, sağ tablodaki tüm kayıtları getirir. Sol tabloda eşleşme varsa eşleşen verileri getirir, eşleşme yoksa NULL döndürür. Örnek:

    SELECT users.name, orders.total
    FROM users
    RIGHT JOIN orders ON users.id = orders.user_id;

RIGHT JOIN çok sık kullanılmaz. Genellikle tablo sırası değiştirilerek LEFT JOIN tercih edilir.

---

## 12.4. FULL JOIN

FULL JOIN, iki tablodaki tüm kayıtları getirir. Eşleşen kayıtlar birlikte gösterilir, eşleşmeyen taraflar NULL olarak gelir. Örnek:

    SELECT users.name, orders.total
    FROM users
    FULL JOIN orders ON users.id = orders.user_id;

Her veritabanı sistemi FULL JOIN desteklemeyebilir.

---

## JOIN Türleri Kısa Özet

| JOIN Türü | Açıklama |
|---|---|
| INNER JOIN | Sadece eşleşen kayıtları getirir |
| LEFT JOIN | Sol tablodaki tüm kayıtları getirir |
| RIGHT JOIN | Sağ tablodaki tüm kayıtları getirir |
| FULL JOIN | İki tablodaki tüm kayıtları getirir |

En sık kullanılan JOIN türleri:

- INNER JOIN
- LEFT JOIN

---

# 13. GROUP BY Nedir?

GROUP BY, verileri belirli bir sütuna göre gruplamak için kullanılır. Genellikle raporlama işlemlerinde kullanılır. Örneğin:

- Her kullanıcının toplam sipariş tutarı
- Her kategoride kaç ürün olduğu
- Her şehirde kaç müşteri olduğu
- Her ay kaç satış yapıldığı
- Her departmanda kaç çalışan olduğu

gibi sorular GROUP BY ile cevaplanabilir. Örnek orders tablosu:

| id | user_id | total |
|---|---|---|
| 1 | 1 | 500 |
| 2 | 2 | 1200 |
| 3 | 1 | 300 |
| 4 | 2 | 800 |
| 5 | 1 | 700 |

Her kullanıcının toplam sipariş tutarını bulmak için:

    SELECT user_id, SUM(total)
    FROM orders
    GROUP BY user_id;

Sonuç:

| user_id | SUM(total) |
|---|---|
| 1 | 1500 |
| 2 | 2000 |

Burada SQL şu işlemi yapar:

1. Aynı user_id değerine sahip kayıtları gruplar.
2. Her grup için total değerlerini toplar.
3. Sonuç olarak her kullanıcı için toplam sipariş tutarını verir.

---

# 14. Aggregate Fonksiyonlar

GROUP BY genellikle aggregate fonksiyonlarla birlikte kullanılır. Aggregate fonksiyonlar birden fazla satır üzerinde hesaplama yapar. En çok kullanılan aggregate fonksiyonlar:

| Fonksiyon | Açıklama |
|---|---|
| COUNT() | Kayıt sayısını hesaplar |
| SUM() | Toplam değer hesaplar |
| AVG() | Ortalama hesaplar |
| MIN() | En küçük değeri bulur |
| MAX() | En büyük değeri bulur |

---

## COUNT Kullanımı

Her kullanıcının kaç sipariş verdiğini bulmak için:

    SELECT user_id, COUNT(*) AS order_count
    FROM orders
    GROUP BY user_id;

Sonuç:

| user_id | order_count |
|---|---|
| 1 | 3 |
| 2 | 2 |

Buradaki `AS order_count`, sonuç sütununa takma ad vermek için kullanılır.

---

## SUM Kullanımı

Her kullanıcının toplam harcamasını bulmak için:

    SELECT user_id, SUM(total) AS total_spent
    FROM orders
    GROUP BY user_id;

---

## AVG Kullanımı

Ürünlerin ortalama fiyatını bulmak için:

    SELECT AVG(price) AS average_price
    FROM products;

---

## MIN Kullanımı

En ucuz ürünü bulmak için:

    SELECT MIN(price) AS min_price
    FROM products;

---

## MAX Kullanımı

En pahalı ürünü bulmak için:

    SELECT MAX(price) AS max_price
    FROM products;

---

# 15. GROUP BY ve JOIN Birlikte Kullanımı

GROUP BY ve JOIN gerçek projelerde sık sık birlikte kullanılır. Örneğin kullanıcı adlarıyla birlikte toplam sipariş tutarlarını görmek isteyelim.

## users tablosu

| id | name |
|---|---|
| 1 | Ayşe |
| 2 | Mehmet |

## orders tablosu

| id | user_id | total |
|---|---|---|
| 1 | 1 | 500 |
| 2 | 1 | 300 |
| 3 | 2 | 1200 |

Sorgu:

    SELECT users.name, SUM(orders.total) AS total_spent
    FROM users
    JOIN orders ON users.id = orders.user_id
    GROUP BY users.name;

Sonuç:

| name | total_spent |
|---|---|
| Ayşe | 800 |
| Mehmet | 1200 |

Bu sorguda:

1. users ve orders tabloları eşleştirilir.
2. Kullanıcı adına göre gruplama yapılır.
3. Her kullanıcının sipariş toplamı hesaplanır.

---

# 16. HAVING Nedir?

HAVING, gruplanmış veriler üzerinde filtreleme yapmak için kullanılır. WHERE satırları filtrelerken, HAVING grupları filtreler. Örneğin toplam sipariş tutarı 1000 TL’den fazla olan kullanıcıları bulmak için:

    SELECT user_id, SUM(total) AS total_spent
    FROM orders
    GROUP BY user_id
    HAVING SUM(total) > 1000;

Bu sorgunun anlamı:

1. Siparişleri user_id değerine göre grupla.
2. Her kullanıcının toplam sipariş tutarını hesapla.
3. Toplam tutarı 1000’den büyük olan grupları getir.

Burada `WHERE SUM(total) > 1000` yazılamaz. Çünkü WHERE gruplama yapılmadan önce çalışır. SUM sonucu ise gruplama işleminden sonra ortaya çıkar.

---

# 17. WHERE ve HAVING Farkı

WHERE ve HAVING sık karıştırılan iki kavramdır.

| Kavram | Ne Zaman Çalışır? | Ne İçin Kullanılır? |
|---|---|---|
| WHERE | Gruplamadan önce | Satırları filtrelemek için |
| HAVING | Gruplamadan sonra | Grupları filtrelemek için |

Örnek:

    SELECT user_id, SUM(total) AS total_spent
    FROM orders
    WHERE total > 100
    GROUP BY user_id
    HAVING SUM(total) > 1000;

Bu sorgunun çalışma mantığı:

1. Önce `total > 100` olan satırlar seçilir.
2. Sonra bu satırlar user_id değerine göre gruplandırılır.
3. Sonra toplamı 1000’den büyük olan gruplar getirilir.

---

# 18. SQL Sorgularında Mantıksal Çalışma Sırası

SQL sorguları yazılırken genelde şu sırayla yazılır:

    SELECT
    FROM
    JOIN
    WHERE
    GROUP BY
    HAVING
    ORDER BY
    LIMIT

Fakat SQL’in mantıksal çalışma sırası farklıdır:

1. FROM
2. JOIN
3. WHERE
4. GROUP BY
5. HAVING
6. SELECT
7. ORDER BY
8. LIMIT

Bu bilgi SQL hatalarını anlamak açısından önemlidir. Örneğin SELECT içinde oluşturulan bir alias, WHERE içinde her zaman doğrudan kullanılamayabilir. Çünkü WHERE, SELECT aşamasından önce çalışır.

---

# 19. Index Nedir?

Index, veritabanında arama işlemlerini hızlandırmak için kullanılan özel bir yapıdır. Index mantığını kitap örneğiyle anlayabiliriz. Bir kitabın sonunda indeks bölümü olduğunu düşünelim. Bir kelimeyi aramak istediğinde kitabı baştan sona okumak yerine indeks bölümünden ilgili kelimenin hangi sayfalarda geçtiğine bakarsın.

Örneğin:

    JOIN -> 120, 135, 160

Bu sayede aradığın bilgiye çok daha hızlı ulaşırsın. Veritabanındaki index de benzer şekilde çalışır. Örneğin `users` tablosunda milyonlarca kayıt olduğunu düşünelim.

    SELECT *
    FROM users
    WHERE email = 'ozge@gmail.com';

Eğer `email` alanında index yoksa veritabanı tüm tabloyu baştan sona tarayabilir. Bu işleme full table scan denir. Yani sistem her satıra tek tek bakar ve aranan e-posta adresini bulmaya çalışır. Eğer `email` alanında index varsa veritabanı ilgili kayda çok daha hızlı ulaşabilir. Index oluşturma örneği:

    CREATE INDEX idx_users_email
    ON users(email);

Bu sorgu, users tablosundaki email alanı için index oluşturur.

---

# 20. Index Ne İşe Yarar?

Index’in temel amacı sorgu performansını artırmaktır. Özellikle şu durumlarda kullanışlıdır:

- Büyük tablolarda arama yaparken
- WHERE ile filtreleme yaparken
- JOIN işlemlerinde
- ORDER BY ile sıralama yaparken
- Sık kullanılan sorgularda
- Foreign key alanlarında
- Unique olması gereken alanlarda

Örnek:

    SELECT *
    FROM customers
    WHERE phone = '5551234567';

Eğer customers tablosunda milyonlarca kayıt varsa ve phone alanında index yoksa sorgu yavaş çalışabilir. Phone alanına index eklemek için:

    CREATE INDEX idx_customers_phone
    ON customers(phone);

Bu işlemden sonra telefon numarasına göre yapılan aramalar daha hızlı olabilir.

---

# 21. Index Her Zaman İyi midir?

Index faydalıdır ancak her alana index eklemek doğru değildir. Çünkü index kullanmanın maliyeti vardır.

## Index Avantajları

- SELECT sorgularını hızlandırabilir.
- Arama işlemlerini hızlandırabilir.
- JOIN işlemlerini daha verimli hale getirebilir.
- ORDER BY ve filtreleme işlemlerinde performans sağlayabilir.

## Index Dezavantajları

- Ekstra disk alanı kullanır.
- INSERT işlemlerini yavaşlatabilir.
- UPDATE işlemlerini yavaşlatabilir.
- DELETE işlemlerini yavaşlatabilir.
- Çok fazla index bakım maliyetini artırır.

Çünkü tabloya yeni bir kayıt eklendiğinde sadece tablo değil, index yapısı da güncellenir. Bu yüzden index özellikle sık arama yapılan ve çok kullanılan sütunlara eklenmelidir. Örneğin email, telefon, kullanıcı adı, foreign key alanları veya sık filtrelenen tarih alanları index için uygun olabilir. Ancak çok az farklı değer içeren alanlarda index her zaman çok faydalı olmayabilir. Örneğin sadece iki farklı değer alan bir sütun düşünelim:

| gender |
|---|
| Female |
| Male |
| Female |
| Male |

Bu tarz düşük çeşitliliğe sahip alanlarda index performans kazancı sağlamayabilir.

---

# 22. Unique Index Nedir?

Unique index, bir sütundaki değerlerin tekrar etmesini engeller. Örneğin kullanıcıların e-posta adresleri benzersiz olmalıdır. 

    CREATE UNIQUE INDEX idx_users_email
    ON users(email);

Bu durumda iki kullanıcı aynı e-posta adresiyle kaydedilemez. Hatalı örnek:

| id | email |
|---|---|
| 1 | test@gmail.com |
| 2 | test@gmail.com |

Bu yapı doğru değildir. Çünkü aynı e-posta adresi iki farklı kullanıcıya ait olmamalıdır.

---

# 23. Veritabanı İlişki Türleri

İlişkisel veritabanlarında tablolar arasında farklı ilişki türleri vardır. Temel ilişki türleri:

- One-to-One
- One-to-Many
- Many-to-Many

---

## 23.1. One-to-One İlişki

Bir kayıt sadece bir kayıtla ilişkilidir. Örnek:

- Bir kullanıcının bir profil detayı olabilir.
- Bir kişinin bir kimlik bilgisi olabilir.

## users tablosu

| id | name |
|---|---|
| 1 | Ayşe |

## user_profiles tablosu

| id | user_id | address |
|---|---|---|
| 1 | 1 | İstanbul |

Burada bir kullanıcıya bir profil kaydı bağlıdır.

---

## 23.2. One-to-Many İlişki

Bir kayıt, başka bir tabloda birden fazla kayıtla ilişkili olabilir. En yaygın ilişki türüdür.

Örnek:

- Bir kullanıcı birden fazla sipariş verebilir.
- Bir kategoriye birden fazla ürün bağlı olabilir.
- Bir müşteri birden fazla destek talebi oluşturabilir.
- Bir departmanda birden fazla çalışan olabilir.

## users tablosu

| id | name |
|---|---|
| 1 | Ayşe |

## orders tablosu

| id | user_id | total |
|---|---|---|
| 1 | 1 | 500 |
| 2 | 1 | 300 |
| 3 | 1 | 700 |

Burada Ayşe’nin birden fazla siparişi vardır. Bu ilişki şu şekilde ifade edilir:

    users 1 -> orders many

Yani bir kullanıcıya karşılık birden fazla sipariş olabilir.

---

## 23.3. Many-to-Many İlişki

Birden fazla kayıt, başka bir tabloda birden fazla kayıtla ilişkili olabilir. Örnek:

- Bir öğrenci birden fazla ders alabilir.
- Bir dersin birden fazla öğrencisi olabilir.
- Bir ürün birden fazla etikete sahip olabilir.
- Bir etiket birden fazla üründe kullanılabilir.

Bu tür ilişkilerde araya bağlantı tablosu konur.

## students tablosu

| id | name |
|---|---|
| 1 | Ali |
| 2 | Elif |

## courses tablosu

| id | course_name |
|---|---|
| 1 | Matematik |
| 2 | Fizik |

## student_courses tablosu

| student_id | course_id |
|---|---|
| 1 | 1 |
| 1 | 2 |
| 2 | 1 |

Bu yapıda:

- Ali Matematik ve Fizik derslerini alır.
- Elif Matematik dersini alır.
- Matematik dersinde hem Ali hem Elif vardır.

Many-to-many ilişkiler doğrudan iki tablo arasında değil, ara tablo yardımıyla kurulur.

---

# 24. Normalizasyon Nedir?

Normalizasyon, veritabanında veri tekrarını azaltmak ve veriyi daha düzenli hale getirmek için yapılan tasarım sürecidir. Amaç:

- Veri tekrarını azaltmak
- Veri tutarlılığını artırmak
- Güncelleme hatalarını önlemek
- Tabloları daha mantıklı parçalara ayırmak
- Bakımı kolaylaştırmak
- Veri bütünlüğünü korumak

Kötü tasarım örneği:

| order_id | customer_name | customer_email | product_name | category_name |
|---|---|---|---|---|
| 1 | Ayşe | ayse@gmail.com | Laptop | Elektronik |
| 2 | Ayşe | ayse@gmail.com | Mouse | Elektronik |

Burada müşteri ve kategori bilgileri tekrar etmektedir. Daha doğru tasarımda tablolar ayrılır:

- customers tablosu
- products tablosu
- categories tablosu
- orders tablosu
- order_items tablosu

Böylece her bilgi kendi tablosunda tutulur. Örneğin müşteri e-posta adresi değişirse sadece customers tablosundaki tek kayıt güncellenir. Bu da veri tutarlılığını artırır.

---

# 25. CRUD Mantığı

CRUD, yazılım sistemlerinde temel veri işlemlerini ifade eder. CRUD açılımı:

| Harf | Açılım | SQL Karşılığı |
|---|---|---|
| C | Create | INSERT |
| R | Read | SELECT |
| U | Update | UPDATE |
| D | Delete | DELETE |

## Create

Yeni veri ekleme işlemidir.

    INSERT INTO products (name, price, stock)
    VALUES ('Mouse', 500, 20);

## Read

Veri okuma işlemidir.

    SELECT *
    FROM products;

## Update

Mevcut veriyi güncelleme işlemidir.

    UPDATE products
    SET price = 600
    WHERE id = 1;

## Delete

Veri silme işlemidir.

    DELETE FROM products
    WHERE id = 1;

Backend tarafında API geliştirirken de çoğu işlem CRUD mantığına dayanır.

| API İşlemi | SQL Karşılığı |
|---|---|
| GET /products | SELECT |
| POST /products | INSERT |
| PUT /products/1 | UPDATE |
| PATCH /products/1 | UPDATE |
| DELETE /products/1 | DELETE |

---

# 26. SQL ve Backend İlişkisi

Bir web uygulamasında kullanıcı ekranda işlem yaptığında, arka planda genellikle veritabanı işlemi gerçekleşir. Örneğin kullanıcı bir ürün ekleme formu doldursun:

| Alan | Değer |
|---|---|
| Ürün adı | Mouse |
| Fiyat | 500 |
| Stok | 20 |

Kullanıcı kaydet butonuna bastığında frontend bu bilgileri backend’e gönderir. Backend ise bu veriyi veritabanına kaydeder:

    INSERT INTO products (name, price, stock)
    VALUES ('Mouse', 500, 20);

Kullanıcı ürün listesini açtığında backend şu sorguyu çalıştırabilir:

    SELECT *
    FROM products;

Yani frontend kullanıcının gördüğü arayüzdür. Backend iş kurallarının çalıştığı yerdir. Veritabanı ise verilerin kalıcı olarak saklandığı yerdir. Bu üç yapı genellikle birlikte çalışır:

    Frontend -> Backend -> Database

Örnek akış:

1. Kullanıcı ürün ekleme formunu doldurur.
2. Frontend bu bilgileri backend’e gönderir.
3. Backend veriyi kontrol eder.
4. Backend SQL sorgusu ile veriyi veritabanına kaydeder.
5. Veritabanı kayıt işlemini tamamlar.
6. Backend frontend’e başarılı cevabı döner.
7. Kullanıcı ekranda yeni ürünü görür.

---

# 27. Örnek E-Ticaret Veritabanı Tasarımı

Bir e-ticaret uygulaması için temel tablolar şu şekilde olabilir:

- users
- products
- categories
- orders
- order_items
- payments

---

## users tablosu

Kullanıcı bilgilerini tutar.

    CREATE TABLE users (
        id INT PRIMARY KEY,
        name VARCHAR(100),
        email VARCHAR(150)
    );

---

## categories tablosu

Ürün kategorilerini tutar.

    CREATE TABLE categories (
        id INT PRIMARY KEY,
        name VARCHAR(100)
    );

---

## products tablosu

Ürün bilgilerini tutar.

    CREATE TABLE products (
        id INT PRIMARY KEY,
        category_id INT,
        name VARCHAR(100),
        price DECIMAL(10,2),
        stock INT,
        FOREIGN KEY (category_id) REFERENCES categories(id)
    );

Burada `category_id`, products tablosunu categories tablosuna bağlar.

---

## orders tablosu

Siparişin ana bilgisini tutar.

    CREATE TABLE orders (
        id INT PRIMARY KEY,
        user_id INT,
        order_date DATE,
        FOREIGN KEY (user_id) REFERENCES users(id)
    );

Burada `user_id`, siparişin hangi kullanıcıya ait olduğunu gösterir.

---

## order_items tablosu

Siparişin içindeki ürünleri tutar.

    CREATE TABLE order_items (
        id INT PRIMARY KEY,
        order_id INT,
        product_id INT,
        quantity INT,
        price DECIMAL(10,2),
        FOREIGN KEY (order_id) REFERENCES orders(id),
        FOREIGN KEY (product_id) REFERENCES products(id)
    );

`orders` ve `order_items` tablolarının ayrı olmasının sebebi şudur:

Bir siparişin içinde birden fazla ürün olabilir. Örneğin Ayşe tek bir siparişte şunları alabilir:

- Mouse
- Klavye
- Kulaklık

Bu yüzden:

- `orders` tablosu siparişin genel bilgisini tutar.
- `order_items` tablosu siparişin içindeki ürünleri tutar.

Bu tasarım ilişkisel veritabanı mantığına uygundur.

---

# 28. SELECT, JOIN ve GROUP BY Birlikte Örnek

Elimizde şu tablolar olsun:

## customers tablosu

| id | name |
|---|---|
| 1 | Ayşe |
| 2 | Mehmet |
| 3 | Zeynep |

## orders tablosu

| id | customer_id | order_date |
|---|---|---|
| 1 | 1 | 2026-05-01 |
| 2 | 1 | 2026-05-02 |
| 3 | 2 | 2026-05-05 |

## order_items tablosu

| id | order_id | product_name | price |
|---|---|---|---|
| 1 | 1 | Mouse | 500 |
| 2 | 1 | Klavye | 1000 |
| 3 | 2 | Kulaklık | 800 |
| 4 | 3 | Laptop | 25000 |

Soru:

> Her müşterinin toplam harcamasını bul.

Sorgu:

    SELECT 
        customers.name,
        SUM(order_items.price) AS total_spent
    FROM customers
    JOIN orders ON customers.id = orders.customer_id
    JOIN order_items ON orders.id = order_items.order_id
    GROUP BY customers.name;

Bu sorgunun adım adım açıklaması:

1. customers tablosundan başlanır.
2. orders tablosu customer_id üzerinden bağlanır.
3. order_items tablosu order_id üzerinden bağlanır.
4. Müşteri adına göre gruplama yapılır.
5. Her müşterinin ürün fiyatları toplanır.

Sonuç:

| name | total_spent |
|---|---|
| Ayşe | 2300 |
| Mehmet | 25000 |

Zeynep sonuçta görünmez çünkü hiç siparişi yoktur. Eğer siparişi olmayan müşteriler de görünsün istenirse LEFT JOIN kullanılabilir:

    SELECT 
        customers.name,
        SUM(order_items.price) AS total_spent
    FROM customers
    LEFT JOIN orders ON customers.id = orders.customer_id
    LEFT JOIN order_items ON orders.id = order_items.order_id
    GROUP BY customers.name;

Bu sorguda Zeynep de gelir ancak toplam tutarı NULL olabilir. NULL yerine 0 göstermek için COALESCE kullanılabilir:

    SELECT 
        customers.name,
        COALESCE(SUM(order_items.price), 0) AS total_spent
    FROM customers
    LEFT JOIN orders ON customers.id = orders.customer_id
    LEFT JOIN order_items ON orders.id = order_items.order_id
    GROUP BY customers.name;

COALESCE şu anlama gelir:

> Eğer değer NULL ise onun yerine belirtilen değeri kullan.

Burada:

    COALESCE(SUM(order_items.price), 0)

ifadesi şu anlama gelir:

> Eğer toplam değer NULL ise 0 göster.

---

# 29. SQL Veri Tipleri

Tablo oluştururken her sütunun veri tipi belirlenir. Örnek tablo:

    CREATE TABLE products (
        id INT PRIMARY KEY,
        name VARCHAR(100),
        price DECIMAL(10,2),
        stock INT,
        created_at DATE
    );

Temel veri tipleri:

| Veri Tipi | Açıklama |
|---|---|
| INT | Tam sayı |
| VARCHAR | Kısa metin |
| TEXT | Uzun metin |
| DECIMAL | Ondalıklı sayı |
| DATE | Tarih |
| DATETIME | Tarih ve saat |
| TIMESTAMP | Zaman bilgisi |
| BOOLEAN | True / False değeri |

Örneğin:

    price DECIMAL(10,2)

Bu ifade, toplam 10 basamaklı ve virgülden sonra 2 basamaklı bir sayı tutulabileceğini gösterir.

---

# 30. NULL Nedir?

NULL, boş veya bilinmeyen değer anlamına gelir. NULL şu değerlerle karıştırılmamalıdır:

    NULL = 0 değildir.
    NULL = boş string değildir.
    NULL = false değildir.

NULL, değer yok anlamına gelir. Örnek:

| id | name | phone |
|---|---|---|
| 1 | Ayşe | NULL |

Bu kayıt, Ayşe’nin telefon bilgisinin sistemde olmadığını ifade eder. NULL kontrolü şu şekilde yapılır:

    SELECT *
    FROM users
    WHERE phone IS NULL;

NULL olmayan kayıtları getirmek için:

    SELECT *
    FROM users
    WHERE phone IS NOT NULL;

Yanlış kullanım:

    WHERE phone = NULL

Doğru kullanım:

    WHERE phone IS NULL

---

# 31. En Çok Kullanılan SQL Kalıpları

## Tüm kayıtları getirme

    SELECT *
    FROM users;

## Belirli sütunları getirme

    SELECT name, email
    FROM users;

## Şarta göre veri getirme

    SELECT *
    FROM products
    WHERE price > 1000;

## Sıralama yapma

    SELECT *
    FROM products
    ORDER BY price DESC;

## Kayıt sayısını bulma

    SELECT COUNT(*)
    FROM users;

## Toplam hesaplama

    SELECT SUM(total)
    FROM orders;

## Ortalama hesaplama

    SELECT AVG(price)
    FROM products;

## En yüksek değeri bulma

    SELECT MAX(price)
    FROM products;

## En düşük değeri bulma

    SELECT MIN(price)
    FROM products;

## Gruplama yapma

    SELECT category_id, COUNT(*)
    FROM products
    GROUP BY category_id;

## Tablo birleştirme

    SELECT users.name, orders.total
    FROM users
    JOIN orders ON users.id = orders.user_id;

---

# 32. İş Hayatında SQL Kullanımı

SQL yalnızca backend geliştiricilerin kullandığı bir teknoloji değildir. Yazılım sektöründe birçok rolde SQL bilgisi önemlidir.

---

## Backend Developer İçin SQL

Backend geliştiriciler, uygulamanın veritabanı ile iletişim kurmasını sağlar. Örnek işlemler:

- Kullanıcı kaydı oluşturma
- Login işlemi
- Ürün listeleme
- Sipariş oluşturma
- Fatura kaydetme
- Kullanıcı bilgisi güncelleme

---

## Data Analyst ve Data Scientist İçin SQL

Veri analistleri ve veri bilimciler, veriyi analiz etmek için SQL kullanır. Örnek işlemler:

- En çok satış yapılan ürünleri bulma
- Aylık gelir hesaplama
- Kullanıcı davranışlarını analiz etme
- Fraud işlemleri inceleme
- Trafik verilerini analiz etme
- Rapor ve dashboard için veri hazırlama

---

## Software Tester / QA İçin SQL

Test mühendisleri SQL’i test verilerini kontrol etmek için kullanabilir. Örnek işlemler:

- API kayıt oluşturdu mu?
- Silinen kayıt gerçekten silindi mi?
- Güncellenen veri veritabanına yansıdı mı?
- Test senaryosu için veri eklemek gerekiyor mu?
- Hatalı kayıtlar sistemde oluşuyor mu?

---

## Business Analyst İçin SQL

İş analistleri sistemin veri yapısını anlamak için SQL mantığına ihtiyaç duyar. Örnek sorular:

- Müşteri hangi tabloda tutuluyor?
- Sipariş sürecinde hangi kayıtlar oluşuyor?
- Rapor hangi alanlardan besleniyor?
- Bir modülde hangi veri ilişkileri var?
- Formdaki alanlar veritabanında hangi sütunlara karşılık geliyor?

---

# 33. Mini Pratik Örnekler

## Stokta azalan ürünleri getirme

    SELECT *
    FROM products
    WHERE stock < 10;

Bu sorgu stok miktarı 10’dan az olan ürünleri getirir.

---

## En pahalı ürünleri sıralama

    SELECT *
    FROM products
    ORDER BY price DESC;

Bu sorgu ürünleri fiyatı en yüksekten en düşüğe doğru sıralar.

---

## Her kategoride kaç ürün olduğunu bulma

    SELECT category_id, COUNT(*) AS product_count
    FROM products
    GROUP BY category_id;

Bu sorgu ürünleri kategoriye göre gruplar ve her kategoride kaç ürün olduğunu hesaplar.

---

## Kullanıcıların siparişlerini getirme

    SELECT users.name, orders.id, orders.total
    FROM users
    JOIN orders ON users.id = orders.user_id;

Bu sorgu kullanıcı adıyla birlikte sipariş bilgilerini getirir.

---

## Hiç siparişi olmayan kullanıcıları bulma

    SELECT users.name
    FROM users
    LEFT JOIN orders ON users.id = orders.user_id
    WHERE orders.id IS NULL;

Bu sorgunun mantığı:

1. Tüm kullanıcılar alınır.
2. Siparişleri varsa orders tablosu ile eşleştirilir.
3. Sipariş id değeri NULL olanlar seçilir.
4. Böylece hiç siparişi olmayan kullanıcılar bulunur.

---


# 34. Genel Özet

- Veritabanı, verilerin düzenli şekilde saklandığı ve yönetildiği sistemdir.
- İlişkisel veritabanı, verileri tablolar halinde tutar ve tablolar arasında ilişki kurulmasını sağlar.
- Tablo, belirli bir veri grubunu saklar.
- Satır, tablodaki gerçek bir kaydı temsil eder.
- Sütun, kaydın hangi özelliklerden oluşacağını belirtir.
- SQL, veritabanıyla iletişim kurmak için kullanılan sorgu dilidir.
- Primary key, bir tablodaki her kaydı benzersiz şekilde tanımlar.
- Foreign key, bir tablodaki alanı başka bir tablodaki primary key alanına bağlar.
- SELECT, veritabanından veri çekmek için kullanılır.
- JOIN, birden fazla tabloyu ilişkili alanlar üzerinden birleştirir.
- GROUP BY, verileri belirli bir alana göre gruplar.
- HAVING, gruplanmış veriler üzerinde filtreleme yapar.
- Index, sorguların daha hızlı çalışmasını sağlayan özel bir veritabanı yapısıdır.
- CRUD, temel veri işlemlerini ifade eder:
    - Create
    - Read
    - Update
    - Delete
- SQL’in yazılım geliştirme sürecindeki önemi çok büyüktür. Çünkü yazılım sistemlerinin büyük bölümü veriler etrafında çalışır.
- Bir kullanıcı sisteme kayıt olduğunda veri oluşur.
- Bir ürün sepete eklendiğinde veri oluşur.
- Bir sipariş verildiğinde veri oluşur.
- Bir ödeme yapıldığında veri oluşur.
- Bir rapor alındığında veri sorgulanır.
- Bir hata test edildiğinde veri kontrol edilir.
- Bir dashboard hazırlandığında veri gruplanır.
- Bu yüzden veritabanı mantığını öğrenmek, yalnızca SQL yazmayı değil, bir yazılım sisteminin arka planda nasıl çalıştığını anlamayı da sağlar.