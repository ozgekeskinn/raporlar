# 17 CI/CD Mantığı

> **Kazanım:** Kod değişiklikleri otomatik olarak derlenir, test edilir, paketlenir ve güvenli biçimde yayınlanır.

## İçindekiler

1. [CI/CD nedir?](#1-cicd-nedir)
2. [CI, Continuous Delivery ve Continuous Deployment](#2-ci-continuous-delivery-ve-continuous-deployment)
3. [Build – Test – Deploy pipeline](#3-build--test--deploy-pipeline)
4. [Temel CI/CD kavramları](#4-temel-cicd-kavramları)
5. [Bir değişikliğin üretime yolculuğu](#5-bir-değişikliğin-üretime-yolculuğu)
6. [Continuous Integration ayrıntıları](#6-continuous-integration-ayrıntıları)
7. [Test stratejisi ve quality gate](#7-test-stratejisi-ve-quality-gate)
8. [Build, paketleme ve artifact yönetimi](#8-build-paketleme-ve-artifact-yönetimi)
9. [Ortamlar ve yapılandırma](#9-ortamlar-ve-yapılandırma)
10. [Deployment stratejileri](#10-deployment-stratejileri)
11. [Veritabanı değişiklikleri](#11-veritabanı-değişiklikleri)
12. [Güvenlik ve DevSecOps](#12-güvenlik-ve-devsecops)
13. [Rollback ve hata yönetimi](#13-rollback-ve-hata-yönetimi)
14. [Monitoring ve pipeline metrikleri](#14-monitoring-ve-pipeline-metrikleri)
15. [GitHub Actions ile .NET örneği](#15-github-actions-ile-net-örneği)
16. [Docker tabanlı pipeline örneği](#16-docker-tabanlı-pipeline-örneği)
17. [Yaygın hatalar ve iyi uygulamalar](#17-yaygın-hatalar-ve-iyi-uygulamalar)
18. [Araçlar, kavram özeti ve çalışma soruları](#18-araçlar-kavram-özeti-ve-çalışma-soruları)

---

## 1. CI/CD nedir?

**CI/CD**, yazılım değişikliklerinin kaynak kod deposundan kullanıcıya ulaşmasına kadar geçen süreci otomatikleştiren yöntemler ve araçlar bütünüdür.

- **CI – Continuous Integration (Sürekli Entegrasyon):** Geliştiricilerin değişikliklerini sık sık ortak dala birleştirmesi; her değişiklikte derleme, test ve kalite kontrollerinin otomatik çalışmasıdır.
- **CD – Continuous Delivery (Sürekli Teslimat):** Testlerden geçen yazılımın üretime alınabilecek durumda otomatik olarak hazırlanmasıdır. Üretime geçiş için insan onayı bulunabilir.
- **CD – Continuous Deployment (Sürekli Dağıtım):** Tüm kontrolleri geçen değişikliğin ayrıca insan onayı beklemeden üretime otomatik yayınlanmasıdır.

CI/CD yalnızca bir YAML dosyası veya bir araç değildir. Küçük ve sık değişiklik, otomatik test, hızlı geri bildirim, tekrarlanabilir süreç, gözlemlenebilirlik ve ekip disiplini üzerine kurulu bir geliştirme kültürüdür.

### Neden gereklidir?

Manuel yayın sürecinde komutlar unutulabilir, yanlış dosya kopyalanabilir, farklı bilgisayarlarda farklı sonuçlar alınabilir ve hata geç fark edilebilir. CI/CD aynı adımları her seferinde aynı sırada çalıştırır.

Başlıca faydaları:

- Hataları geliştirme sürecinin başında yakalar.
- Entegrasyon problemlerini küçültür.
- Yayın süresini ve insan hatasını azaltır.
- Sık, küçük ve daha düşük riskli sürümler çıkarılmasını sağlar.
- Hangi kodun, kim tarafından, ne zaman ve nasıl yayınlandığını izlenebilir hâle getirir.
- Test, güvenlik ve kod kalitesi kurallarını standartlaştırır.
- Gerektiğinde önceki sürüme dönüşü kolaylaştırır.

> **Temel fikir:** CI/CD kötü kodu iyi kılmaz; iyi tanımlanmış kontrolleri hızlı, tutarlı ve tekrarlanabilir hâle getirir.

---

## 2. CI, Continuous Delivery ve Continuous Deployment

| Kavram | Otomatik işlemler | Üretime geçiş | Temel amaç |
|---|---|---|---|
| Continuous Integration | Build, test, analiz | Kapsam dışı olabilir | Değişiklikleri güvenle birleştirmek |
| Continuous Delivery | Build, test, paketleme, test ortamına dağıtım | Genellikle manuel onay | Her an yayınlanabilir sürüm üretmek |
| Continuous Deployment | Tüm doğrulamalar ve production deploy | Otomatik | Başarılı her değişikliği kullanıcıya ulaştırmak |

### Continuous Delivery ile Continuous Deployment farkı

İkisi aynı şey değildir. Delivery modelinde sistem üretime hazır paketi oluşturur fakat son yayın kararı bir kişi veya kurul tarafından verilebilir. Deployment modelinde kalite kapılarını geçen değişiklik doğrudan üretime gider.

Her ekip Continuous Deployment kullanmak zorunda değildir. Bankacılık, sağlık ve kamu gibi düzenlemeye tabi alanlarda onay adımı gerekli olabilir. Burada amaç “her şeyi otomatik yayınlamak” değil, manuel karar dışındaki tüm teknik adımları güvenilir biçimde otomatikleştirmektir.

---

## 3. Build – Test – Deploy pipeline

Bir **pipeline**, kodun belirli aşamalardan sırayla veya paralel biçimde geçtiği otomatik iş akışıdır.

```text
Kod Değişikliği
      ↓
Kaynak Kodu Alma
      ↓
Bağımlılıkları Yükleme
      ↓
Build → Statik Analiz → Test
      ↓
Paket / Artifact Oluşturma
      ↓
Test veya Staging Ortamına Deploy
      ↓
Smoke / Entegrasyon Testleri
      ↓
Onay veya Otomatik Quality Gate
      ↓
Production Deploy
      ↓
Sağlık Kontrolü + Monitoring
```

### 3.1 Build

Build aşaması kaynak kodu çalıştırılabilir veya dağıtılabilir çıktıya dönüştürür.

Örnek işlemler:

- NuGet, npm veya Maven bağımlılıklarını geri yükleme
- C# kodunu derleme
- TypeScript kodunu JavaScript'e dönüştürme
- Frontend dosyalarını küçültme ve paketleme
- Docker image oluşturma
- Derleme uyarılarını kontrol etme

Build başarısızsa sonraki aşamalara geçilmemelidir. Çünkü derlenemeyen kod test veya deploy edilemez.

### 3.2 Test

Test aşaması değişikliğin beklenen davranışı koruyup korumadığını doğrular. Sadece unit test çalıştırmak yeterli değildir; projenin riskine göre farklı kontroller gerekir.

- Kod biçimi ve lint kontrolü
- Statik kod analizi
- Unit test
- Integration test
- API testleri
- UI/E2E testleri
- Güvenlik ve bağımlılık taraması
- Performans testleri
- Test coverage ölçümü

Bir test başarısızsa pipeline durmalı ve hatalı sürüm dağıtılmamalıdır. Buna **fail fast** yaklaşımı denir.

### 3.3 Deploy

Deploy, doğrulanmış paketin hedef ortama kurulması ve çalıştırılmasıdır. Sunucuya dosya kopyalamaktan daha geniş bir süreçtir:

- Uygulama paketini veya container image'ını hedefe aktarma
- Ortam değişkenlerini bağlama
- Veritabanı migration'larını kontrollü çalıştırma
- Servisi başlatma
- Health check yapma
- Trafiği yeni sürüme yönlendirme
- Sorunda rollback uygulama

### Job, step ve stage ilişkisi

- **Step:** Tek komut veya tek action; örneğin `dotnet test`.
- **Job:** Aynı runner üzerinde çalışan step grubu; örneğin `build-and-test`.
- **Stage:** Mantıksal büyük aşama; örneğin build, staging deploy veya production deploy.
- **Workflow/Pipeline:** Tüm sürecin tanımı.

Bağımsız işler paralel çalıştırılabilir. Örneğin unit test ile güvenlik taraması eş zamanlı yürüyebilir. Deploy ise başarılı build ve test işlerine bağımlı olmalıdır.

---

## 4. Temel CI/CD kavramları

### Repository ve trigger

Pipeline tanımı genellikle kodla aynı Git deposunda tutulur. Pipeline'ı başlatan olaya **trigger** denir.

Yaygın trigger'lar:

- Bir dala `push`
- Pull request açılması veya güncellenmesi
- Tag oluşturulması
- Zamanlanmış çalışma
- Manuel başlatma
- Başka bir workflow'un tamamlanması
- Harici webhook veya API çağrısı

### Runner / Agent

Pipeline komutlarını çalıştıran makinedir. Sağlayıcı tarafından barındırılan geçici runner veya kurumun yönettiği self-hosted runner kullanılabilir.

Self-hosted runner daha fazla kontrol sağlar; ancak güncelleme, izolasyon, sır yönetimi ve zararlı kod riskleri ekibin sorumluluğundadır. Özellikle güvenilmeyen pull request kodları kalıcı ve hassas ağa erişebilen runner'larda çalıştırılmamalıdır.

### Artifact

Build sonucunda üretilen ve sonraki aşamalarda kullanılan sürümlenmiş çıktıdır.

Örnekler:

- `.dll`, `.jar`, `.zip` veya frontend `dist/` paketi
- Docker/OCI image
- Test sonucu ve coverage raporu
- SBOM dosyası

İdeal yaklaşım **bir kez build et, aynı artifact'ı her ortama dağıt** ilkesidir. Staging ve production için ayrı ayrı build almak, test edilen çıktı ile yayınlanan çıktının farklılaşmasına neden olabilir.

### Cache ile artifact farkı

| Özellik | Cache | Artifact |
|---|---|---|
| Amaç | Pipeline'ı hızlandırmak | Çıktıyı saklamak ve aşamalar arasında taşımak |
| Örnek | NuGet/npm bağımlılıkları | Derlenmiş uygulama paketi |
| Güvenilirlik | Olmasa da pipeline çalışmalıdır | Deploy için gerekli olabilir |
| Yaşam süresi | Anahtar ve politikaya bağlı | Saklama politikasına bağlı |

### Pipeline as Code

Pipeline'ın YAML veya benzeri bir dosyayla kaynak kontrolünde tutulmasıdır. Böylece değişiklikler review edilir, geçmiş izlenir ve pipeline sürümlenir.

### Idempotency

Aynı deploy işlemi tekrarlandığında sistemin bozulmaması ve mümkün olduğunca aynı sonuca ulaşmasıdır. Ağ kesintisi sonrası bir job yeniden çalıştırıldığında duplicate kayıt veya tutarsız altyapı üretmemesi önemlidir.

---

## 5. Bir değişikliğin üretime yolculuğu

Örnek akış:

1. Geliştirici kısa ömürlü bir feature branch açar.
2. Küçük commit'ler yapar ve uzak depoya gönderir.
3. Pull request açılınca CI tetiklenir.
4. Restore, build, lint, test ve güvenlik taramaları çalışır.
5. Sonuçlar pull request üzerinde görünür.
6. Zorunlu kontroller başarılı ve review tamamlanmışsa kod ana dala birleştirilir.
7. Ana dal pipeline'ı sürümlenmiş artifact veya container image üretir.
8. Aynı çıktı staging ortamına dağıtılır.
9. Smoke ve integration testleri çalışır.
10. Politika gerektiriyorsa production onayı alınır.
11. Artifact production'a dağıtılır.
12. Health check, log, metric ve alarm sonuçları takip edilir.
13. Hata oranı yükselirse otomatik veya manuel rollback yapılır.

Kısa ömürlü branch'ler entegrasyon gecikmesini azaltır. Haftalarca ayrı kalan büyük branch'ler merge conflict ve “integration hell” riskini artırır.

---

## 6. Continuous Integration ayrıntıları

Başarılı CI için üç temel alışkanlık vardır:

1. **Sık entegrasyon:** Kod küçük parçalar hâlinde sık sık ana akışla birleştirilir.
2. **Otomatik doğrulama:** Her değişiklik build ve testlerden geçer.
3. **Hızlı düzeltme:** Kırık ana dal öncelikli problem kabul edilir.

### Branch protection

Ana dal doğrudan yazmaya kapatılabilir. Birleştirme için şunlar zorunlu tutulabilir:

- Pull request review
- Başarılı status check'ler
- Güncel branch
- İmzalı commit
- Belirli kişilerin onayı
- Code owner onayı
- Çözülmemiş konuşma bulunmaması

### Trunk-based development ve Git Flow

**Trunk-based development**, geliştiricilerin küçük değişiklikleri sık biçimde ana dala yakın tutmasıdır. Hızlı CI/CD ile iyi uyumludur. Tamamlanmamış özellikler feature flag ile gizlenebilir.

**Git Flow**, `develop`, release ve hotfix gibi daha fazla uzun ömürlü dal kullanır. Sürüm bazlı ürünlerde işe yarayabilir ancak entegrasyon ve süreç maliyetini artırabilir.

Seçim; ekip büyüklüğü, yayın sıklığı, düzenlemeler ve ürün yapısına göre yapılmalıdır.

### Merge sonrası kırılma neden olabilir?

İki pull request ayrı ayrı başarılıyken birbirleriyle uyumsuz olabilir. Çözümler:

- Merge queue kullanmak
- PR'ı ana dalın güncel hâliyle yeniden test etmek
- Küçük PR'lar oluşturmak
- Deterministik test ortamları kullanmak

---

## 7. Test stratejisi ve quality gate

### Test piramidi

| Test türü | Sayı | Hız | Amaç |
|---|---:|---:|---|
| Unit test | Çok | Çok hızlı | Küçük iş mantığı parçaları |
| Integration test | Orta | Orta | Veritabanı, API ve servis etkileşimi |
| E2E/UI test | Az | Yavaş | Kritik kullanıcı senaryoları |

E2E testleri değerlidir fakat yavaş ve kırılgan olabilir. Her davranışı E2E ile test etmek yerine çoğu kural unit ve integration seviyesinde doğrulanmalıdır.

### Quality gate nedir?

Pipeline'ın devam etmesi için sağlanması gereken ölçülebilir koşuldur. Örnekler:

- Build hatası yok
- Tüm kritik testler başarılı
- Yeni kodda belirlenen coverage eşiği sağlanmış
- Kritik/yüksek güvenlik açığı yok
- Lint veya statik analiz hatası yok
- Gerekli review tamamlanmış

Coverage tek başına kalite ölçüsü değildir. Yüzde 100 coverage, doğru assertion veya doğru senaryo anlamına gelmez. Eşik, düşünmeyi teşvik eden bir güvenlik ağı olmalıdır.

### Flaky test

Kod değişmediği hâlde bazen geçen bazen kalan testtir. Genellikle zaman bağımlılığı, ortak durum, ağ, yarış koşulu veya yanlış izolasyondan kaynaklanır.

Flaky testleri sürekli yeniden çalıştırıp görmezden gelmek güveni azaltır. Test karantinaya alınmalı, nedeni bulunmalı ve düzeltilmelidir. Rastgele retry asıl çözüm değildir.

---

## 8. Build, paketleme ve artifact yönetimi

### Reproducible build

Aynı kaynak kod ve bağımlılıklarla aynı çıktının üretilebilmesidir. Bunun için:

- Lock dosyaları repoya eklenir.
- SDK ve temel image sürümleri sabitlenir.
- Build sırasında ortamdan gizli bağımlılıklar kaldırılır.
- Üretilen artifact commit SHA ve sürümle etiketlenir.

### Sürümleme

Yaygın yaklaşım **Semantic Versioning** biçimidir:

```text
MAJOR.MINOR.PATCH
2.4.1
```

- **MAJOR:** Geriye uyumsuz değişiklik
- **MINOR:** Geriye uyumlu yeni özellik
- **PATCH:** Geriye uyumlu hata düzeltmesi

Container image için yalnızca `latest` etiketi kullanılmamalıdır. `1.4.2`, Git tag'i veya değişmez commit SHA etiketi hangi sürümün çalıştığını kesinleştirir.

### Artifact güvenilirliği

- Artifact repository/registry içinde saklanmalıdır.
- Retention politikası tanımlanmalıdır.
- Bütünlük için checksum veya imza kullanılabilir.
- Production'a giden çıktı yeniden build edilmemelidir.
- Kaynak commit ile artifact arasında izlenebilir bağ kurulmalıdır.

---

## 9. Ortamlar ve yapılandırma

Yaygın ortamlar:

- **Development:** Geliştiricinin hızlı deneme ortamı
- **Test/QA:** Fonksiyonel testlerin yürütüldüğü ortam
- **Staging/Pre-production:** Production'a olabildiğince benzeyen son doğrulama ortamı
- **Production:** Gerçek kullanıcıların kullandığı ortam

### Ortam eşitliği

Staging ile production arasında işletim sistemi, runtime, container, ağ ve bağımlılık açısından büyük farklar varsa staging başarısı production başarısını garanti etmez. Infrastructure as Code ve container kullanımı farkı azaltır.

### Configuration ile secret ayrımı

- **Configuration:** Log seviyesi, feature flag, servis adresi gibi gizli olmayan ortam ayarıdır.
- **Secret:** Şifre, API anahtarı, connection string'in hassas bölümü, sertifika veya token'dır.

Secret'lar:

- Kaynak koda ve YAML içine açık metin yazılmamalı
- Log'a basılmamalı
- Secret manager veya platformun şifreli secret alanında tutulmalı
- En az yetkiyle sınırlandırılmalı
- Düzenli döndürülmeli
- Mümkünse uzun ömürlü anahtar yerine OIDC ile kısa ömürlü kimlik bilgisi kullanılmalı

> `.gitignore`, daha önce commit edilmiş bir sırrı Git geçmişinden silmez. Böyle bir durumda sır derhâl iptal edilmeli ve geçmiş ayrıca temizlenmelidir.

---

## 10. Deployment stratejileri

### Recreate / Big Bang

Eski sürüm durdurulur, yeni sürüm başlatılır. Basittir fakat kısa kesinti oluşturabilir ve geri dönüşü daha risklidir.

### Rolling deployment

Instance'lar gruplar hâlinde yeni sürüme geçirilir. Hizmet devam eder ancak bir süre iki sürüm birlikte çalışır. Sürümler arası uyumluluk gerekir.

### Blue-Green deployment

İki eş ortam vardır:

- Blue: Mevcut production
- Green: Yeni sürüm

Yeni sürüm boş ortamda hazırlanıp test edilir, ardından trafik Green'e geçirilir. Geri dönüş hızlıdır; fakat iki ortam kaynak maliyeti oluşturur.

### Canary deployment

Yeni sürüm önce kullanıcıların küçük bir yüzdesine açılır. Hata oranı ve gecikme sağlıklıysa trafik kademeli artırılır. Risk sınırlanır, fakat trafik yönlendirme ve ölçüm altyapısı gerekir.

### Feature flag

Kod production'a dağıtılmış olsa da özellik yapılandırma ile açılıp kapatılır. **Deploy** ile **release** birbirinden ayrılır. Feature flag avantajları:

- Özelliği küçük kullanıcı grubunda deneme
- Sorunda deploy yapmadan kapatma
- Tamamlanmamış kodu ana dalda tutabilme

Eski flag'ler teknik borç oluşturur; sahibi ve kaldırılma tarihi tanımlanmalıdır.

### Strateji seçimi

| Strateji | Kesinti | Geri dönüş | Maliyet | Uygun durum |
|---|---|---|---|---|
| Recreate | Olabilir | Orta | Düşük | Küçük/iç sistem |
| Rolling | Genellikle yok | Orta | Orta | Çok instance'lı servis |
| Blue-Green | Yok denecek kadar az | Hızlı | Yüksek | Kritik uygulama |
| Canary | Yok | Hızlı ve kontrollü | Yüksek karmaşıklık | Büyük kullanıcı trafiği |

---

## 11. Veritabanı değişiklikleri

Uygulama rollback'i kolay olsa da veri değişikliği her zaman geri alınamaz. Bu nedenle migration ayrı dikkat ister.

### Güvenli migration ilkeleri

- Migration dosyaları sürüm kontrolünde tutulur.
- Production yedeği ve geri dönüş planı bulunur.
- Büyük tabloları kilitleyebilecek işlemler önceden test edilir.
- Migration tekrar çalıştırmaya karşı güvenli tasarlanır.
- Uygulama ve şema değişiklikleri geriye uyumlu yapılır.
- Silme işlemleri mümkünse sonraki bir sürüme bırakılır.

### Expand–Migrate–Contract örneği

Bir kolon adını doğrudan değiştirmek yerine:

1. **Expand:** Yeni kolon eklenir; uygulama eski ve yeni şemayla uyumlu tutulur.
2. **Migrate:** Veriler yeni kolona taşınır; yazma/okuma yeni yapıya geçirilir.
3. **Contract:** Artık kullanılmayan eski kolon daha sonraki sürümde silinir.

Bu yöntem rolling veya blue-green sırasında eski ve yeni uygulama sürümlerinin birlikte çalışmasını kolaylaştırır.

---

## 12. Güvenlik ve DevSecOps

Güvenlik yalnızca son aşamada yapılan tarama değildir. Kontrollerin geliştirme sürecine erken eklenmesine **shift left** denir.

### Pipeline'da güvenlik kontrolleri

- **SAST:** Kaynak kodu çalıştırmadan güvenlik açığı arar.
- **SCA:** Açık kaynak bağımlılıklarını ve bilinen açıkları inceler.
- **Secret scanning:** Yanlışlıkla commit edilmiş sırları arar.
- **Container scanning:** Image paketlerindeki açıkları tarar.
- **IaC scanning:** Terraform/Kubernetes gibi altyapı tanımlarındaki riskleri inceler.
- **DAST:** Çalışan uygulamaya dışarıdan güvenlik testleri uygular.
- **SBOM:** Yazılım bileşenlerinin envanterini oluşturur.

### Least privilege

Workflow token'ına yalnızca ihtiyaç duyduğu izinler verilmelidir. Test job'ının production deploy yetkisine ihtiyacı yoktur. Production secret'ları sadece korumalı production environment job'ına açılmalıdır.

### Supply-chain güvenliği

- Üçüncü taraf action ve bağımlılıklar güvenilir kaynaktan seçilir.
- Action sürümleri mümkünse değişmez commit SHA ile sabitlenir.
- Artifact imzalama ve doğrulama uygulanabilir.
- Build provenance kaydı üretilebilir.
- Pull request'lerden gelen güvenilmeyen kodun secret erişimi engellenir.

### OIDC neden önemlidir?

CI platformu, bulut sağlayıcısından kısa ömürlü erişim belirteci alabilir. Böylece depoda uzun ömürlü cloud access key saklama ihtiyacı azalır. Yetki; repository, branch, environment ve workflow koşullarıyla sınırlandırılabilir.

---

## 13. Rollback ve hata yönetimi

Pipeline başarılı olmak zorunda değildir; güvenli biçimde başarısız olabilmelidir.

### Hata durumunda sorulacaklar

- Hangi step ve hangi commit başarısız oldu?
- Hata build sırasında mı deploy sonrasında mı oluştu?
- Kullanıcı etkisi var mı?
- Otomatik retry güvenli mi?
- Rollback mi, roll-forward mı daha güvenli?
- Veritabanı değişikliği geri alınabilir mi?

### Rollback

Önceki çalışan artifact'ın yeniden dağıtılması veya trafiğin önceki ortama çevrilmesidir. Bunun için eski artifact'lar saklanmalı ve sürüm bilgisi açık olmalıdır.

### Roll-forward

Hatayı düzelten yeni bir sürüm yayınlamaktır. Geriye döndürülemeyen veri dönüşümlerinde veya küçük düzeltmelerde daha uygun olabilir.

### Health check türleri

- **Liveness:** Uygulama çalışıyor mu?
- **Readiness:** Trafik almaya hazır mı?
- **Startup:** Başlangıç tamamlandı mı?
- **Smoke test:** Kritik birkaç uçtan uca davranış çalışıyor mu?

Deploy komutunun başarılı dönmesi, yayının gerçekten sağlıklı olduğu anlamına gelmez. Deploy sonrası doğrulama zorunludur.

---

## 14. Monitoring ve pipeline metrikleri

### Uygulama gözlemlenebilirliği

Üretim dağıtımından sonra şu sinyaller izlenir:

- Log'lar
- Metrikler
- Dağıtık trace'ler
- Error rate
- Response time / latency
- Trafik
- CPU, bellek ve disk
- İş metriği: sipariş başarısı, ödeme reddi gibi

### DORA metrikleri

- **Deployment Frequency:** Ne sıklıkla production'a çıkılıyor?
- **Lead Time for Changes:** Commit'in production'a ulaşması ne kadar sürüyor?
- **Change Failure Rate:** Yayınların ne kadarı hata veya müdahale doğuruyor?
- **Failed Deployment Recovery Time:** Hatalı yayından sonra hizmet ne kadar sürede toparlanıyor?

Bu metrikler kişileri değerlendirmek için değil, teslimat sistemindeki darboğazları görmek için kullanılmalıdır.

### Diğer yararlı pipeline metrikleri

- Pipeline başarı oranı
- Ortalama build süresi
- Queue bekleme süresi
- Flaky test oranı
- Cache hit oranı
- Aşama bazında hata dağılımı

---

## 15. GitHub Actions ile .NET örneği

Workflow dosyaları `.github/workflows/` altında tutulur. Aşağıdaki örnek pull request'lerde ve `main` dalına push edildiğinde projeyi restore eder, Release modunda derler, test eder ve `main` için artifact üretir.

> Proje/solution yollarını kendi klasör yapına göre değiştirmelisin.

```yaml
name: .NET CI

on:
  pull_request:
    branches: [main]
  push:
    branches: [main]

permissions:
  contents: read

concurrency:
  group: ci-${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    timeout-minutes: 15

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup .NET
        uses: actions/setup-dotnet@v4
        with:
          dotnet-version: '8.0.x'
          cache: true
          cache-dependency-path: '**/packages.lock.json'

      - name: Restore dependencies
        run: dotnet restore --locked-mode

      - name: Build
        run: dotnet build --configuration Release --no-restore

      - name: Test
        run: >-
          dotnet test
          --configuration Release
          --no-build
          --logger "trx;LogFileName=test-results.trx"
          --collect "XPlat Code Coverage"

      - name: Upload test results
        if: always()
        uses: actions/upload-artifact@v4
        with:
          name: test-results
          path: '**/TestResults/**'
          if-no-files-found: warn

      - name: Publish application
        if: github.event_name == 'push'
        run: dotnet publish --configuration Release --no-build --output ./publish

      - name: Upload application artifact
        if: github.event_name == 'push'
        uses: actions/upload-artifact@v4
        with:
          name: application-${{ github.sha }}
          path: ./publish
          retention-days: 14
```

### Örneğin açıklaması

- `on`: Workflow'un hangi olaylarda çalışacağını belirler.
- `permissions`: Varsayılan token yetkisini salt okumayla sınırlar.
- `concurrency`: Aynı branch için eski gereksiz çalışmayı iptal eder.
- `runs-on`: Job'ın çalışacağı runner türüdür.
- `timeout-minutes`: Takılan işin sonsuza kadar kaynak tüketmesini önler.
- `--locked-mode`: Bağımlılık kilit dosyasına aykırı restore'u engeller.
- `--no-restore` / `--no-build`: Aynı işin gereksiz tekrarını azaltır.
- `if: always()`: Test kalsa bile sonuçların inceleme için yüklenmesini sağlar.
- `${{ github.sha }}`: Artifact'ı tam commit ile ilişkilendirir.

### Ayrı deploy job'ı örneği

Aşağıdaki iskelet gerçek hosting komutunu temsilî bırakır. Production ortamında approval ve secret kuralları GitHub environment üzerinden tanımlanabilir.

```yaml
  deploy-production:
    if: github.ref == 'refs/heads/main' && github.event_name == 'push'
    needs: build-and-test
    runs-on: ubuntu-latest
    environment: production
    permissions:
      contents: read
      id-token: write

    steps:
      - name: Download application artifact
        uses: actions/download-artifact@v4
        with:
          name: application-${{ github.sha }}
          path: ./publish

      - name: Authenticate with cloud by OIDC
        run: echo "Bulut sağlayıcısına özel OIDC adımı burada çalışır."

      - name: Deploy
        run: echo "Uygulamaya ve sağlayıcıya özel deploy komutu burada çalışır."

      - name: Smoke test
        run: curl --fail --retry 5 --retry-delay 5 https://example.com/health
```

Buradaki önemli tasarım: deploy job'ı yeniden build almaz; test edilen artifact'ı indirir. `needs` nedeniyle build/test başarısızsa deploy başlamaz.

---

## 16. Docker tabanlı pipeline örneği

Container yaklaşımında artifact çoğu zaman bir image'dır.

```yaml
name: Container CI

on:
  push:
    branches: [main]

permissions:
  contents: read
  packages: write

jobs:
  build-image:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Log in to registry
        uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - name: Set up Buildx
        uses: docker/setup-buildx-action@v3

      - name: Build and push immutable image
        uses: docker/build-push-action@v6
        with:
          context: .
          push: true
          tags: ghcr.io/${{ github.repository }}:${{ github.sha }}
          cache-from: type=gha
          cache-to: type=gha,mode=max
```

Üretime dağıtımda `${{ github.sha }}` ile etiketlenen aynı image kullanılmalıdır. Kullanılan üçüncü taraf action'ların major tag yerine denetlenmiş commit SHA ile sabitlenmesi supply-chain güvenliğini daha da artırır.

---

## 17. Yaygın hatalar ve iyi uygulamalar

### Yaygın hatalar

1. **Sadece build almak:** Test ve kalite kapısı olmadan derlenmesi, kodun doğru olduğu anlamına gelmez.
2. **Production'da yeniden build:** Test edilen artifact ile yayınlanan artifact farklılaşabilir.
3. **Secret'ı YAML'a yazmak:** Kaynak geçmişinde kalıcı güvenlik açığı oluşturur.
4. **Her şeyi tek dev job'a koymak:** Hatanın yerini bulmayı ve paralelliği zorlaştırır.
5. **Yalnızca `latest` etiketi:** Çalışan sürümün izini ve rollback'i zorlaştırır.
6. **Deploy sonrası kontrol yapmamak:** Teknik olarak tamamlanan deploy işlevsel olarak bozuk olabilir.
7. **Flaky testleri yok saymak:** Ekibin pipeline sonuçlarına güvenini bitirir.
8. **Limitsiz yetki:** Ele geçirilmiş bağımlılık veya script'in zarar alanını büyütür.
9. **Çok uzun pipeline:** Geliştiriciyi CI sonucunu beklemeden ilerlemeye iter.
10. **Rollback planı olmaması:** İlk production hatasında süreç doğaçlamaya dönüşür.
11. **Ortamların çok farklı olması:** “Staging'de çalışıyordu” problemi doğurur.
12. **Veritabanı migration'ını sıradan deploy gibi görmek:** Veri kaybı ve uzun kilit riski yaratır.

### İyi uygulama kontrol listesi

- [ ] Pipeline tanımı repository içinde sürümleniyor.
- [ ] Her pull request otomatik build ve testten geçiyor.
- [ ] Ana dal branch protection ile korunuyor.
- [ ] Hızlı kontroller önce, pahalı kontroller sonra çalışıyor.
- [ ] Bağımsız testler paralel yürütülüyor.
- [ ] Bağımlılık ve SDK sürümleri kontrol altında.
- [ ] Bir kez build edilen artifact tüm ortamlarda kullanılıyor.
- [ ] Artifact commit SHA ve sürümle izlenebiliyor.
- [ ] Secret'lar güvenli depoda ve en az yetkiyle tutuluyor.
- [ ] Production environment için koruma kuralları var.
- [ ] Deploy sonrası health check ve smoke test çalışıyor.
- [ ] Log, metric ve alarm sistemi yayını takip ediyor.
- [ ] Rollback veya roll-forward planı test edilmiş.
- [ ] Veritabanı migration'ları geriye uyumlu tasarlanıyor.
- [ ] Pipeline süreleri ve DORA metrikleri ölçülüyor.

### Pipeline performansını iyileştirme

- Bağımlılık cache'i kullan.
- Değişmeyen modülleri tekrar build etme.
- Unit testleri paralelleştir.
- Matris stratejisini yalnızca gereken sürümler için kullan.
- Docker layer cache kullan.
- Hızlı hata veren kontrolleri başa al.
- E2E/performance testlerini uygun aşamaya ayır.
- Gereksiz eski branch çalışmalarını concurrency ile iptal et.

---

## 18. Araçlar, kavram özeti ve çalışma soruları

### Yaygın CI/CD araçları

| Kategori | Örnekler |
|---|---|
| Kaynak kod ve workflow | GitHub Actions, GitLab CI/CD, Azure Pipelines, Jenkins |
| Artifact/container registry | GitHub Packages, Azure Artifacts, Nexus, Artifactory, container registry'leri |
| Container ve orkestrasyon | Docker, Kubernetes |
| Infrastructure as Code | Terraform, Bicep, CloudFormation, Ansible |
| Kod kalitesi | SonarQube, linter'lar, dil analizörleri |
| Gözlemlenebilirlik | OpenTelemetry, Prometheus, Grafana ve APM araçları |

Araç seçimi ikincildir. Asıl önemli olan pipeline'ın hızlı geri bildirim vermesi, güvenilir artifact üretmesi, güvenli deploy yapması ve hatadan kurtulabilmesidir.

### Kısa kavram sözlüğü

| Kavram | Kısa açıklama |
|---|---|
| Pipeline | Otomatik teslimat iş akışı |
| Workflow | Pipeline'ın tanımı |
| Trigger | Pipeline'ı başlatan olay |
| Runner/Agent | Komutları çalıştıran makine |
| Job | Aynı çalışma bağlamındaki step grubu |
| Step | Tek işlem veya komut |
| Artifact | Build sonucunda üretilen dağıtılabilir çıktı |
| Quality Gate | Devam için geçilmesi gereken kalite koşulu |
| Environment | Development, staging, production gibi hedef ortam |
| Secret | Hassas kimlik bilgisi |
| Rollback | Önceki çalışan sürüme dönme |
| Roll-forward | Düzeltmeyi yeni sürümle ileri taşıma |
| Canary | Yeni sürümü trafiğin küçük bölümüne açma |
| Blue-Green | İki ortam arasında trafik değişimi |
| Feature Flag | Özelliği deploy'dan bağımsız açıp kapatma |

### Örnek mülakat / çalışma soruları

1. CI ile CD arasındaki fark nedir?
2. Continuous Delivery ve Continuous Deployment nasıl ayrılır?
3. Pipeline'da build, test ve deploy hangi sırayla çalışır ve neden?
4. Artifact ile cache arasındaki fark nedir?
5. “Build once, deploy many” ilkesi neden önemlidir?
6. Blue-green ile canary deployment arasındaki fark nedir?
7. Pipeline secret'ları neden kaynak kodda tutulmamalıdır?
8. OIDC, uzun ömürlü erişim anahtarlarına göre ne sağlar?
9. Flaky test nedir ve pipeline güvenini nasıl etkiler?
10. Deploy başarılı görünmesine rağmen uygulama neden bozuk olabilir?
11. Rollback ile roll-forward ne zaman tercih edilir?
12. Veritabanı migration'ında expand–migrate–contract neden kullanılır?
13. DORA metrikleri nelerdir?
14. Self-hosted runner'ın riskleri nelerdir?
15. Branch protection ve required checks ne işe yarar?

### Öğretici mini senaryo

Bir e-ticaret projesinde geliştirici ödeme servisini değiştiriyor:

1. Pull request açılır.
2. CI projeyi derler ve unit testleri çalıştırır.
3. Test container'ındaki veritabanıyla integration test yapılır.
4. Bağımlılık ve secret taraması tamamlanır.
5. Review sonrası kod `main` dalına birleşir.
6. Pipeline, commit SHA etiketli image üretir.
7. Image staging'e dağıtılır ve sahte ödeme ile smoke test yapılır.
8. Canary yöntemiyle trafiğin %5'i yeni sürüme verilir.
9. Ödeme hata oranı ve gecikme izlenir.
10. Değerler normalse trafik kademeli yükseltilir; değilse eski image'a dönülür.

Bu senaryoda CI hatalı kodun birleşmesini önler; CD ise doğrulanmış sürümün tutarlı ve kontrollü biçimde kullanıcılara ulaşmasını sağlar.

---

## Sonuç

CI/CD'nin özü yalnızca “kod push edilince sunucuya göndermek” değildir. Güvenilir bir teslimat sistemi:

1. Değişikliği otomatik olarak doğrular.
2. Tekrarlanabilir ve izlenebilir artifact üretir.
3. Aynı artifact'ı kontrollü ortamlara taşır.
4. Secret ve yetkileri korur.
5. Deploy sonrasında gerçek sistem sağlığını ölçer.
6. Hata durumunda hızlı ve güvenli kurtarma sağlar.

İyi kurulmuş CI/CD sayesinde geliştirici, manuel yayın adımlarına değil yazılımın değerine odaklanır. Küçük ve sık değişiklikler daha erken test edilir, daha düşük riskle yayınlanır ve sorun çıktığında hangi sürümün neden başarısız olduğu hızlıca anlaşılır.

## Resmî kaynaklar

- [GitHub Actions dokümantasyonu](https://docs.github.com/actions)
- [GitHub Actions ile .NET build ve test](https://docs.github.com/actions/automating-builds-and-tests/building-and-testing-net)
- [GitHub Actions deployment environments](https://docs.github.com/actions/deployment/targeting-different-environments/managing-environments-for-deployment)
- [GitHub Actions güvenlik rehberi](https://docs.github.com/actions/security-for-github-actions/security-guides/security-hardening-for-github-actions)
- [Docker GitHub Actions rehberi](https://docs.docker.com/build/ci/github-actions/)
- [DORA metrikleri](https://dora.dev/guides/dora-metrics-four-keys/)

> **Tek cümlelik özet:** CI kodu sürekli doğrular; Continuous Delivery onu her an yayınlanabilir tutar; Continuous Deployment ise kontrolleri geçen değişikliği otomatik olarak kullanıcıya ulaştırır.