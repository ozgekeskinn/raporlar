# 11. Bellek ve Performans Derinliği

---

## İçindekiler

1. [Bellek (Memory) Nedir?](#1-bellek-memory-nedir)
2. [Stack Bellek](#2-stack-bellek)
3. [Heap Bellek](#3-heap-bellek)
4. [Garbage Collection (GC)](#4-garbage-collection-gc)
5. [Memory Leak](#5-memory-leak)
6. [Performans Derinliği](#6-performans-derinliği)
7. [Dil Bazında Karşılaştırma](#7-dil-bazında-karşılaştırma)
8. [Mülakat Soruları](#8-mülakat-soruları)

---

## 1. Bellek (Memory) Nedir?

Bellek, bir program çalışırken ihtiyaç duyduğu tüm verilerin geçici olarak saklandığı alandır. Bu alan **RAM (Random Access Memory)** olarak adlandırılır.

| Depolama  | Özellik |
|---|---|
| SSD / HDD | Kalıcıdır. Bilgisayar kapansa bile veri kaybolmaz. |
| RAM | Geçicidir. Bilgisayar kapanınca temizlenir. |

### Günlük Hayat Benzetmesi

Bilgisayarı bir ofis olarak düşün:
- **SSD** → Dosya dolabı (kalıcı arşiv)
- **RAM** → Çalışma masası (aktif çalışılan alan)

### CPU ve RAM İlişkisi

CPU saniyede milyarlarca işlem yapabilir. SSD çok yavaş kalır. Bu yüzden veriler önce RAM'e yüklenir.

```
SSD → RAM → CPU
```

### Memory Layout (Bellek Yerleşimi)

Bir process oluşturulduğunda bellekte şu bölümler ayrılır:

```
+----------------------------+
|       Code Segment         |  ← Programın makine kodu (Read Only)
+----------------------------+
|     Global Variables       |  ← Global değişkenler (program boyunca yaşar)
+----------------------------+
|          Heap              |
|           ↓                |  ← Dinamik veriler (aşağıya büyür)
|           ↓                |
+----------------------------+
|        Boş Alan            |
+----------------------------+
|           ↑                |
|           ↑                |  ← Fonksiyon çağrıları (yukarıya büyür)
|          Stack             |
+----------------------------+
```

### Process (Süreç) Nedir?

Bir program çalıştırıldığında işletim sistemi onu **Process** haline getirir. Her process'in kendi Stack'i ve Heap'i vardır; birbirlerinin belleğine doğrudan erişemezler.

```
RAM
├── Chrome  → kendi Stack + Heap
├── Discord → kendi Stack + Heap
└── VSCode  → kendi Stack + Heap
```

---

## 2. Stack Bellek

Stack (Yığın Bellek), fonksiyon çağrılarının ve yerel değişkenlerin tutulduğu, otomatik yönetilen hızlı bir bellek alanıdır.

### Stack'te Ne Tutulur?

- Primitive değerler (`int`, `number`, `boolean`, `char`)
- Fonksiyon parametreleri
- Yerel (local) değişkenler
- Return adresleri
- Execution context bilgisi

### LIFO Mantığı

Stack **Last In First Out** (Son Giren İlk Çıkar) mantığıyla çalışır.

```
Tabak yığını gibi: En üste ekle, en üstten al.

Push(D):        Pop():
D ← yeni        D ← çıkar
C               C
B               B
A               A
```

Bu yüzden Stack çok hızlıdır: sadece Push ve Pop vardır, arama ve aralara ekleme yoktur → **O(1)**

### Stack Frame Nedir?

Bir fonksiyon çağrıldığında Stack'e yalnızca fonksiyon ismi değil, bir **Stack Frame** eklenir. Frame içinde şunlar bulunur:

- Fonksiyon adı
- Parametreler
- Yerel değişkenler
- Return adresi
- Execution context

```javascript
function sum(a, b) {
  let result = a + b;
  return result;
}
sum(3, 5);
```

```
Stack Frame
─────────────────
Function: sum()
a = 3
b = 5
result = 8
Return Address
─────────────────
```

Fonksiyon bitince frame **otomatik olarak** silinir.

### Çoklu Fonksiyon Çağrısı

```javascript
function A() { B(); }
function B() { C(); }
function C() { }
```

```
Başlangıç:  A çağrıldı:  B çağrıldı:  C çağrıldı:  C bitti:    B bitti:    A bitti:
main()      A()          B()          C()          B()         A()         main()
            main()       A()          B()          A()         main()
                         main()       A()          main()
                                      main()
```

### Call Stack ve Execution Context

Call Stack, JavaScript'in hangi fonksiyonun çalıştığını takip ettiği mekanizmadır. Her fonksiyonun kendi **Execution Context**'i vardır — kendi değişkenleri, parametreleri, `this` değeri ve lexical environment'ı.

### Stack Neden Hızlıdır?

```
Bellekte sadece tek yönde büyür ↓
Boş yer aramaz
Adres hesaplaması yoktur
Parçalanma oluşmaz
CPU doğrudan erişir
```

### Stack'in Dezavantajı ve Stack Overflow

Her Stack'in kapasitesi sınırlıdır (genellikle 1–8 MB). Sonsuz recursion varsa Stack dolar:

```javascript
// ❌ Stack Overflow — durma koşulu yok
function test() {
  test(); // Her çağrı yeni Frame ekliyor
}
test();
// → Maximum Call Stack Size Exceeded
```

```javascript
// ✅ Doğru recursion — durma koşulu var
function countdown(n) {
  if (n === 0) return;
  console.log(n);
  countdown(n - 1);
}
countdown(5);
```

**Recursion'da Stack:**

```javascript
factorial(3)
```

```
factorial(3) → factorial(2) → factorial(1) → factorial(0)
                                              ↓ return 1
                              ↓ return 1
              ↓ return 2
↓ return 6
```

### JavaScript'te Her Şey Stack'te mi?

Hayır. Bu önemli bir yanılgıdır:

```javascript
let person = { name: "Ali" };
//  ↑                ↑
// Stack'te          Heap'te
// (referans/adres)  (gerçek obje)
```

---

## 3. Heap Bellek

Heap, program çalışırken büyük, dinamik ve karmaşık verilerin tutulduğu esnek bellek alanıdır.

### Heap'te Ne Tutulur?

- Object, Array, Function
- Class instance
- Date, Map, Set
- DOM elementleri
- Büyük veri koleksiyonları

### Stack vs Heap Temel Fark

```
STACK                          HEAP
──────────────────────         ──────────────────────
Küçük, sabit boyutlu           Büyük, dinamik
Primitive değerler             Object, Array, Function
Fonksiyon çağrıları            Karmaşık yapılar
Otomatik temizlenir            GC tarafından temizlenir
Referans tutar (pointer)       Verinin kendisi burada
Çok hızlı                      Stack'e göre daha yavaş
```

### Referans Mantığı

Stack'te nesnenin **kendisi değil**, Heap'teki **adresi (referansı)** tutulur:

```
STACK                    HEAP
user ─────────────────► 0x001 { name: "Ali", age: 25 }
```

**Günlük hayat:** Ev adresi (Stack) ≠ Evin kendisi (Heap). Aynı adrese sahip iki kişi aynı evi paylaşır.

### Primitive vs Reference Types

**Primitive Types** (değer kopyalanır):
`string`, `number`, `boolean`, `undefined`, `null`, `bigint`, `symbol`

**Reference Types** (referans kopyalanır):
`object`, `array`, `function`, `date`, `Map`, `Set`

```javascript
// Primitive — değer kopyalanır
let a = 10;
let b = a;
b = 20;
console.log(a); // 10 ← etkilenmedi

// Reference — referans kopyalanır
let person1 = { name: "Ali" };
let person2 = person1;
person2.name = "Veli";
console.log(person1.name); // "Veli" ← etkilendi!
```

```
person1 ──┐
           ├──► HEAP 0x001 { name: "Veli" }
person2 ──┘
```

### Shallow Copy (Yüzeysel Kopyalama)

Sadece birinci seviyeyi kopyalar. İç içe object varsa içteki hâlâ ortaktır.

```javascript
let user1 = { name: "Ayşe", address: { city: "Bursa" } };
let user2 = { ...user1 };

user2.name = "Fatma";          // user1.name değişmez ✅
user2.address.city = "İstanbul"; // user1.address.city DE değişir! ❌

// Bellek:
// user1 → 0x001 { name: "Ayşe", address: 0x003 }
// user2 → 0x002 { name: "Fatma", address: 0x003 }  ← aynı address!
// 0x003 → { city: "İstanbul" }
```

**Shallow Copy yöntemleri:**

```javascript
let copy = { ...original };           // Spread operator
let copy = Object.assign({}, original);
let arr  = [...oldArray];             // Array spread
let arr  = oldArray.slice();
```

### Deep Copy (Derin Kopyalama)

Tüm seviyeleri bağımsız olarak kopyalar. Hiçbir ortak referans kalmaz.

```javascript
let user2 = structuredClone(user1);
user2.address.city = "İstanbul";
console.log(user1.address.city); // "Bursa" ← etkilenmedi ✅
```

**Deep Copy yöntemleri:**

```javascript
// 1. structuredClone (modern, önerilen)
let copy = structuredClone(original);

// 2. JSON yöntemi (eski, kısıtlı)
let copy = JSON.parse(JSON.stringify(original));
// ❌ function, undefined, Symbol, Date bozulur!

// 3. Lodash (karmaşık yapılar için)
let copy = _.cloneDeep(original);
```

### Mutability ve Immutability

```javascript
// Mutable — mevcut objeyi değiştirme (React'ta tehlikeli)
user.name = "Veli";

// Immutable — yeni obje oluştur (React'ta önerilen)
let newUser = { ...user, name: "Veli" };
```

### React'ta Referans Mantığı

```javascript
// ❌ Yanlış — referans aynı, React değişikliği algılamaz
user.age = 26;
setUser(user);

// ✅ Doğru — yeni referans, React yeniden render eder
setUser({ ...user, age: 26 });

// ❌ Yanlış
items.push(newItem);
setItems(items);

// ✅ Doğru
setItems([...items, newItem]);
```

### Heap Fragmentation (Parçalanma)

Farklı boyutlarda objeler oluşturulup silinince Heap'te boşluklar kalabilir:

```
HEAP: [Object A][Boş][Object B][Boş][Object C]
```

Toplam boş alan yeterli olsa bile büyük bir obje için yan yana alan bulunamayabilir. Modern GC'ler **compaction** ile bunu çözer — objeleri yan yana taşır.

### Object'ler Ne Zaman Silinir?

```javascript
let user = { name: "Ali" };
let admin = user;  // İkinci referans

user = null;
// ← Obje silinmez! admin hâlâ erişilebilir

admin = null;
// ← Artık hiçbir referans yok → GC adayı
```

### Circular Reference

İki obje birbirini referans gösterdiğinde döngüsel referans oluşur:

```javascript
let a = {};
let b = {};
a.ref = b;
b.ref = a;
```

**Circular reference her zaman memory leak değildir.** Modern GC (Mark and Sweep), root'lardan erişilemeyen circular yapıları temizleyebilir. Sorun, global değişken veya event listener aracılığıyla erişilmeye devam edilen circular yapılardır.

---

## 4. Garbage Collection (GC)

Garbage Collection, program çalışırken artık kullanılmayan nesneleri bellekten otomatik olarak temizleyen mekanizmadır.

### JavaScript'te Bellek Yönetimi Süreci

```
1. Allocation  → let user = {} oluşturuldu, Heap'te alan ayrıldı
2. Usage       → user.name erişildi, kullanıldı
3. Release     → user = null; GC zamanında temizleyecek
```

C/C++'da manuel yapılır (`malloc / free`). JavaScript'te **otomatiktir.**

### Reachability (Erişilebilirlik)

GC'nin temel sorusu:

> "Bu nesneye hâlâ root'lardan ulaşılabiliyor mu?"

- **Reachable** → Canlı, sakla
- **Unreachable** → Çöp, temizle

**Root nedir?**
- Global object (`window` / `global`)
- Aktif fonksiyonların local değişkenleri
- Call Stack içindeki değişkenler
- Closure tarafından erişilen değişkenler
- DOM üzerinden erişilebilen nesneler

```javascript
let user = { name: "Ali" };   // ROOT → user → { name: "Ali" } ✅ reachable
user = null;                   // ROOT → null ... { name: "Ali" } ❌ unreachable → GC adayı
```

### GC Algoritmaları

#### 1. Reference Counting (Referans Sayımı)

Her objenin kaç referansı olduğu sayılır. Sayı 0'a düşünce silinir.

```python
# Python (CPython) bu yöntemi kullanır
a = {}   # ref count = 1
b = a    # ref count = 2
del b    # ref count = 1
del a    # ref count = 0 → hemen silinir
```

**Zayıf yönü — Circular Reference:**

```javascript
let a = {};
let b = {};
a.ref = b;
b.ref = a;
del a; del b;
// Birbirlerine referans var, sayı 0'a düşmez → bellek sızıntısı!
```

#### 2. Mark and Sweep (İşaretle ve Süpür)

Modern JavaScript motorlarının (V8) kullandığı temel algoritma. Circular reference'ı çözer.

**Aşama 1 — Mark:** Root'lardan başlayarak ulaşılabilen TÜM nesneler işaretlenir.

**Aşama 2 — Sweep:** İşaretlenmemiş nesneler silinir.

```
ROOT
 ├──► User {id:1} ✅         Orphan {} ❌
 │      └──► Address {} ✅   [1,2,3]   ❌
 └──► App {} ✅

Sonuç: Orphan ve [1,2,3] temizlenir.
```

**Circular Reference örneği:**

```
Fonksiyon bittikten sonra a ve b root'tan erişilemez
→ Birbirlerine işaret etseler de IKISI DE temizlenir ✅
```

#### 3. Generational GC (Nesil Bazlı)

**Temel fikir:** "Yeni oluşturulan nesnelerin büyük çoğunluğu kısa ömürlüdür."

```
HEAP
┌────────────────────────────────────────┐
│  Young Generation (Genç Nesil)         │
│  ┌──────────┐ ┌──────────┐ ┌────────┐ │
│  │  Eden    │ │Survivor 0│ │Survivor│ │
│  │ (yeni    │ │          │ │   1    │ │
│  │ objeler) │ │          │ │        │ │
│  └──────────┘ └──────────┘ └────────┘ │
│     Minor GC → sık, hızlı (~ms)       │
├────────────────────────────────────────┤
│  Old Generation (Eski Nesil/Tenured)   │
│  ┌──────────────────────────────────┐  │
│  │   Uzun yaşayan objeler           │  │
│  └──────────────────────────────────┘  │
│     Major GC → nadir, yavaş (~100ms+)  │
└────────────────────────────────────────┘
```

**Süreç:**
1. Yeni obje → Eden'e gider
2. Minor GC → Hayatta kalanlar Survivor'a taşınır
3. Birkaç GC'den sonra hâlâ hayattaysa → Old Generation'a "promote" edilir
4. Old Generation dolunca → Major (Full) GC çalışır

```javascript
// ❌ Her döngüde yeni obje → Minor GC baskısı
for (let i = 0; i < 1_000_000; i++) {
  let s = new String("geçici"); // Kısa ömürlü, sürekli GC
}

// ✅ Tek obje genişliyor
let sb = "";
for (let i = 0; i < 1_000_000; i++) {
  sb += "geçici";
}
```

#### 4. Stop-the-World (STW)

GC çalışırken uygulama **kısa süreliğine duraklatılır.** Büyük Heap kullanımında bu fark edilir hale gelebilir.

```
Zaman →
App:  ████████ ░░░░ ████████████ ░░░░░░░ ████████
GC:           ████          ███████
              ↑              ↑
           Minor GC      Major GC
           (~5ms)         (~500ms)
```

**Bu sorunu azaltan yöntemler:**

- **Incremental GC:** GC işini küçük parçalara böler, uzun duraksamaları önler.
- **Concurrent GC:** Bazı GC işleri ana thread'den bağımsız yapılır.
- **Compaction:** Heap'teki objeleri yan yana taşıyarak parçalanmayı azaltır.

### WeakMap ve WeakSet

Normal `Map`'te key olan obje GC tarafından toplanamaz:

```javascript
let map = new Map();
let user = { name: "Ali" };
map.set(user, "admin");
user = null;
// map hâlâ objeyi key olarak tuttuğu için bellekte kalır!
```

`WeakMap`'te key olan objeye başka referans kalmazsa GC temizleyebilir:

```javascript
let weakMap = new WeakMap();
let user = { name: "Ali" };
weakMap.set(user, "admin");
user = null;
// Başka referans yok → GC temizleyebilir ✅
```

**WeakMap özellikleri:**
- Sadece `object` key kabul eder (primitive kabul etmez)
- **Iterable değildir** (elemanlar GC tarafından herhangi zamanda silinebilir)

**Ne için kullanılır?**
- Object'e bağlı metadata saklamak
- Cache (memory leak riski olmadan)
- DOM elementlerine ek bilgi bağlamak

```javascript
// WeakMap ile güvenli cache
let cache = new WeakMap();

function processUser(user) {
  if (cache.has(user)) return cache.get(user);
  let result = { processedName: user.name.toUpperCase() };
  cache.set(user, result);
  return result;
}
// user = null yapılınca cache de otomatik temizlenir ✅
```

**WeakSet:** Object'leri zayıf referansla tutan Set. Daha önce işlenip işlenmediğini takip etmek için kullanılır.

### GC Varsa Memory Leak Nasıl Olur?

GC yalnızca **ulaşılamayan** nesneleri temizler. GC şunu bilemez:

> "Bu veri artık işime yaramıyor."

GC sadece şunu bilir:

> "Bu veriye teknik olarak ulaşılabiliyor mu?"

Eğer evet → silmez. Mantıksal olarak gereksiz ama teknik olarak erişilebilirse → **memory leak.**

---

## 5. Memory Leak

Memory Leak (Bellek Sızıntısı), artık kullanılmaması gereken verilerin hâlâ bir referans üzerinden erişilebilir olduğu için bellekte tutulmaya devam etmesidir.

**Temel problem:**
```
Normal:  Kullan → Referansı kaldır → GC temizler ✅
Leak:    Kullan → Referans yanlışlıkla tutulmaya devam eder → GC temizleyemez ❌
```

**Belirtiler:**
- RAM kullanımı sürekli artar
- Uzun süre açık kalınca uygulama yavaşlar
- Aynı event birden fazla tetikleniyor
- Chrome Task Manager'da memory sürekli yükseliyor
- Tarayıcı sekmesi donuyor

**En riskli uygulamalar:** Dashboard, CRM, chat uygulamaları, oyunlar, finans panelleri — uzun süre açık kalan her şey.

### 5.1 Gereksiz Global Değişkenler

```javascript
// ❌ Kötü — global scope'a sızan değişken
function birSeyYap() {
  kacikDegisken = new Array(1_000_000); // var/let/const yok → window'a gider!
}

// ✅ İyi
function birSeyYap() {
  const lokalDizi = new Array(1_000_000); // Fonksiyon bitince temizlenir
}
```

**Cache'in kontrolsüz büyümesi:**

```javascript
// ❌ Kötü — cache hiç temizlenmiyor
const cache = {};
function getUserData(id) {
  if (cache[id]) return cache[id];
  cache[id] = { id, data: new Array(100_000).fill("data") };
  return cache[id];
}
// Binlerce user için → Heap şişer

// ✅ İyi — sınırlı cache
const cache = new Map();
const MAX = 100;
function setCache(key, value) {
  if (cache.size >= MAX) {
    cache.delete(cache.keys().next().value); // En eski silinir
  }
  cache.set(key, value);
}
```

### 5.2 Temizlenmeyen Event Listener'lar

```javascript
// ❌ Kötü — anonim function, kaldırılamaz
function setup() {
  window.addEventListener("resize", function() {
    console.log(window.innerWidth);
  });
}
// Her setup() çağrısında yeni listener eklenir, hiçbiri kaldırılamaz

// ❌ Kötü — aynı görünen ama farklı referans
window.removeEventListener("resize", function() {}); // Çalışmaz!

// ✅ İyi — named function, kaldırılabilir
function handleResize() {
  console.log(window.innerWidth);
}
window.addEventListener("resize", handleResize);
// iş bitince:
window.removeEventListener("resize", handleResize);
```

**Event listener closure'la büyük veri tutabilir:**

```javascript
// ❌ Tehlikeli
function createListener() {
  const bigData = new Array(1_000_000).fill("data");

  function handleClick() {
    console.log(bigData.length); // closure bigData'yı bellekte tutuyor
  }

  document.addEventListener("click", handleClick);

  return () => document.removeEventListener("click", handleClick); // cleanup döndür
}
```

### 5.3 Temizlenmeyen Timer ve Interval'lar

```javascript
// ❌ Kötü — interval hiç temizlenmiyor
function startProcess() {
  const bigData = new Array(1_000_000).fill("data");
  setInterval(() => {
    console.log(bigData.length); // bigData da bellekte kalır!
  }, 1000);
}

// ✅ İyi — id sakla ve temizle
const intervalId = setInterval(() => { ... }, 1000);
clearInterval(intervalId); // iş bitince

// setTimeout da temizlenmeli
const timeoutId = setTimeout(() => { ... }, 5000);
clearTimeout(timeoutId);
```

### 5.4 Closure Tuzağı

```javascript
// ❌ — closure gereksiz büyük veriyi tutuyor
function buyukVeriIsle() {
  const buyukDizi = new Array(1_000_000).fill("veri");
  const ilkEleman = buyukDizi[0];

  return function() {
    return ilkEleman; // Sadece ilkEleman kullanılıyor
                      // AMA buyukDizi hâlâ closure scope'unda!
  };
}

// ✅ — referansı kes
function buyukVeriIsle() {
  const buyukDizi = new Array(1_000_000).fill("veri");
  const ilkEleman = buyukDizi[0];
  // buyukDizi'ye artık dışarıdan referans yok → GC temizleyebilir

  return function() { return ilkEleman; };
}
```

### 5.5 Detached DOM (Kopuk DOM Elementleri)

DOM'dan kaldırılmış ama JavaScript'te referansı tutulan elementler:

```javascript
// ❌ Kötü
let removedElements = [];

function createAndRemove() {
  const div = document.createElement("div");
  document.body.appendChild(div);
  document.body.removeChild(div);
  removedElements.push(div); // DOM'da yok ama bellekte var!
}

// Bellek:
// DOM Tree: div yok
// JS Heap:  removedElements → div referansı hâlâ var
```

```javascript
// ✅ Çözüm: referansı temizle
removedElements = [];
// veya
div = null;
```

### 5.6 Subscription Leak

```javascript
// ❌ Kötü — her açılışta yeni subscription
function openPage() {
  store.subscribe(() => { console.log("State değişti"); });
}
// 100 kez açılırsa → 100 listener

// ✅ İyi
const unsubscribe = store.subscribe(() => { ... });
unsubscribe(); // iş bitince
```

### 5.7 WebSocket ve Fetch Leak

```javascript
// ❌ Kötü — bağlantı kapatılmıyor
const socket = new WebSocket("wss://example.com");
socket.onmessage = (e) => console.log(e.data);
// sayfa kapanınca socket açık kalır!

// ✅ İyi
socket.close();
```

```javascript
// ❌ Kötü — component unmount sonrası state set ediliyor
useEffect(() => {
  fetch("/api/users")
    .then(res => res.json())
    .then(data => setUsers(data)); // component kapandıysa uyarı!
}, []);

// ✅ İyi — AbortController ile iptal
useEffect(() => {
  const controller = new AbortController();

  fetch("/api/users", { signal: controller.signal })
    .then(res => res.json())
    .then(data => setUsers(data))
    .catch(err => { if (err.name !== "AbortError") console.error(err); });

  return () => controller.abort(); // cleanup
}, []);
```

### 5.8 React useEffect Cleanup

```javascript
// Cleanup fonksiyonu:
// - component unmount olduğunda çalışır
// - dependency değişip effect yeniden çalışmadan önce çalışır

// ✅ Event listener cleanup
useEffect(() => {
  function handleResize() { console.log(window.innerWidth); }
  window.addEventListener("resize", handleResize);
  return () => window.removeEventListener("resize", handleResize);
}, []);

// ✅ Interval cleanup
useEffect(() => {
  const id = setInterval(() => { ... }, 1000);
  return () => clearInterval(id);
}, []);

// ✅ WebSocket cleanup
useEffect(() => {
  const socket = new WebSocket("wss://example.com");
  socket.onmessage = (e) => console.log(e.data);
  return () => socket.close();
}, []);

// ✅ Subscription cleanup
useEffect(() => {
  const unsubscribe = store.subscribe(() => { ... });
  return () => unsubscribe();
}, []);

// ✅ Dependency değişiminde cleanup — örneğin roomId değişince eski socket kapanır
useEffect(() => {
  const socket = new WebSocket(`wss://example.com/room/${roomId}`);
  return () => socket.close();
}, [roomId]);
```

### Memory Leak Tespit Araçları

```
1. Chrome DevTools → Memory sekmesi → Heap Snapshot
   - İlk snapshot al
   - İşlem yap (sayfa aç/kapat)
   - Tekrar snapshot al
   - "Comparison" ile artan objeleri incele

2. Chrome Task Manager (Shift+Esc) → Memory sütununu izle

3. Node.js
```

```javascript
// Node.js bellek izleme
setInterval(() => {
  const mem = process.memoryUsage();
  console.log({
    heapKullanilan: `${Math.round(mem.heapUsed / 1024 / 1024)} MB`,
    heapToplam:    `${Math.round(mem.heapTotal / 1024 / 1024)} MB`,
  });
}, 5000);
```

### Memory Leak Önleme Kontrol Listesi

```
✅ Global değişken kullanımını azalt
✅ Event listener eklediysen kaldır
✅ setInterval → clearInterval
✅ setTimeout → clearTimeout (gerekirse)
✅ WebSocket bağlantılarını kapat
✅ Subscription → unsubscribe
✅ React useEffect cleanup yaz
✅ Cache için maksimum boyut belirle
✅ DOM'dan kaldırılan elementlerin referansını temizle
✅ API isteklerinde AbortController kullan
✅ Closure'da gereksiz büyük veri tutma
```

---

## 6. Performans Derinliği

Performans = **Hız + Bellek Verimliliği + Kullanıcı Deneyimi + Kararlılık**

İyi geliştirici sadece "çalışıyor mu?" değil, "**ne kadar verimli çalışıyor?**" sorusunu da sorar.

### Memory Leak ve Performans Zinciri

```
Gereksiz object oluşturma
        ↓
Heap büyür
        ↓
GC daha sık çalışır
        ↓
CPU kullanımı artar
        ↓
UI donar / Uygulama yavaşlar
```

### CPU vs RAM

| | CPU Yoğun | RAM Yoğun |
|---|---|---|
| **Ne?** | Çok hesaplama | Çok veri tutma |
| **Belirti** | Ana thread bloke | Heap sürekli büyüme |
| **Örnek** | Büyük döngü, karmaşık algo | 1M elemanlı array, büyük cache |
| **Çözüm** | Web Worker, chunking | Referans temizleme, cache sınırı |

### JavaScript Tek Thread ve Blocking Code

JavaScript çoğunlukla **tek ana thread** üzerinde çalışır. Ana thread hem JS çalıştırır hem DOM işlemi yapar hem de kullanıcı etkileşimlerine cevap verir.

```javascript
// ❌ Blocking code — UI doner
function heavyCalc() {
  let result = 0;
  for (let i = 0; i < 1_000_000_000; i++) result += i;
  return result;
}
heavyCalc(); // Bu çalışırken hiçbir şey yapılamaz
```

**Çözüm seçenekleri:** Web Worker, pagination, chunking, lazy loading, virtualization.

### Big O Notasyonu

Algoritmanın veri büyüdükçe nasıl davrandığını gösterir.

| Notasyon | Adı | Örnek |
|---|---|---|
| O(1) | Constant | Array index erişimi `arr[0]` |
| O(log n) | Logaritmik | Binary search |
| O(n) | Linear | Array'i baştan sona gezmek |
| O(n log n) | Linearithmic | İyi sıralama algoritmaları |
| O(n²) | Quadratic | İç içe iki döngü |
| O(2^n) | Exponential | Bazı recursive çözümler |

```javascript
// O(1) — Veri sayısından bağımsız
const users = ["Ali", "Ayşe", "Mehmet"];
console.log(users[0]); // Her zaman tek işlem

// O(n) — Veri ile doğru orantılı
for (let user of users) console.log(user);

// O(n²) — 1000 eleman → 1.000.000 işlem!
for (let i = 0; i < arr.length; i++) {
  for (let j = 0; j < arr.length; j++) {
    // ...
  }
}
```

**Mülakat notu:** Küçük veride fark edilmez. 100.000 elemanda iç içe döngü uygulamayı kilitler.

### Doğru Veri Yapısı Seçimi

```javascript
// ❌ Array ile arama — O(n)
const users = [{ id: 1, name: "Ali" }, { id: 2, name: "Ayşe" }];
const user = users.find(u => u.id === 2); // Tüm diziyi gezebilir

// ✅ Map ile erişim — O(1)
const userMap = new Map();
userMap.set(1, { id: 1, name: "Ali" });
userMap.set(2, { id: 2, name: "Ayşe" });
const user = userMap.get(2); // Direkt erişim

// ❌ Array üyelik kontrolü — O(n)
const ids = [1, 2, 3, 4, 5];
ids.includes(4);

// ✅ Set üyelik kontrolü — O(1)
const idSet = new Set([1, 2, 3, 4, 5]);
idSet.has(4);
```

### Gereksiz Döngü ve Obje Oluşturmaktan Kaçın

```javascript
// Okunabilir ama 2 kez döner (küçük veride sorun değil)
const names = products
  .filter(p => p.price > 1000)
  .map(p => p.name);

// Büyük veri için tek geçiş
const names = [];
for (let p of products) {
  if (p.price > 1000) names.push(p.name);
}
```

```javascript
// ❌ Her render'da yeni obje — child gereksiz re-render
function App() {
  const options = { theme: "dark" }; // Her seferinde yeni referans
  return <Panel options={options} />;
}

// ✅ useMemo ile sabit referans
const options = useMemo(() => ({ theme: "dark" }), []);
```

### Debounce

Kullanıcı yazmayı bitirdikten belirli süre sonra çalışır. **Search input, form validation** için idealdir.

```javascript
function debounce(fn, delay) {
  let timerId;
  return function(...args) {
    clearTimeout(timerId);
    timerId = setTimeout(() => fn(...args), delay);
  };
}

const debouncedSearch = debounce((value) => {
  fetch(`/api/search?q=${value}`);
}, 500);

input.addEventListener("input", (e) => debouncedSearch(e.target.value));

// "react" yazılırken:
// r → timer başlar
// re → timer iptal, yeni timer
// rea → timer iptal, yeni timer
// reac → timer iptal, yeni timer
// react → kullanıcı durdu → 500ms sonra API isteği ✅
```

### Throttle

Belirli zaman aralığında en fazla bir kez çalışır. **Scroll, resize, mousemove** için idealdir.

```javascript
function throttle(fn, delay) {
  let lastTime = 0;
  return function(...args) {
    const now = Date.now();
    if (now - lastTime >= delay) {
      lastTime = now;
      fn(...args);
    }
  };
}

const throttledScroll = throttle(() => {
  console.log("Scroll pozisyonu güncellendi");
}, 1000);

window.addEventListener("scroll", throttledScroll);
// Kullanıcı ne kadar hızlı scroll yapsa da saniyede en fazla 1 kez çalışır
```

### Debounce vs Throttle

| | Debounce | Throttle |
|---|---|---|
| **Mantık** | Kullanıcı durduktan sonra çalışır | Belirli aralıklarla çalışır |
| **Kullanım** | Search input, autocomplete | Scroll, resize, drag |
| **Benzetme** | Yazmayı bitirince cevap ver | Her saniye durumu güncelle |

### DOM Performansı

```javascript
// ❌ Her adımda DOM güncelleniyor — çok pahalı
for (let i = 0; i < 1000; i++) {
  document.body.innerHTML += `<div>${i}</div>`;
}

// ✅ Tek seferinde DOM güncelleme
let html = "";
for (let i = 0; i < 1000; i++) html += `<div>${i}</div>`;
document.body.innerHTML = html;

// ✅ DocumentFragment — en iyi yaklaşım
const fragment = document.createDocumentFragment();
for (let i = 0; i < 1000; i++) {
  const div = document.createElement("div");
  div.textContent = i;
  fragment.appendChild(div);
}
document.body.appendChild(fragment); // Tek DOM işlemi
```

### Reflow ve Repaint

```
HTML parse → DOM → CSS parse → CSSOM → Render Tree → Layout/Reflow → Paint → Composite
```

- **Reflow:** Element boyut/konum yeniden hesaplama. `width`, `height`, `margin`, DOM ekleme/silme tetikler. **Pahalı.**
- **Repaint:** Görsel yeniden çizim. `color`, `background`, `visibility` tetikler. Reflow'dan daha ucuz.

**Layout Thrashing (okuma-yazma karışımı):**

```javascript
// ❌ Kötü — okuma/yazma karışık → tarayıcı sürekli reflow yapar
boxes.forEach(box => {
  const h = box.offsetHeight; // DOM okuma (reflow tetikler)
  box.style.height = h + 10 + "px"; // DOM yazma
});

// ✅ İyi — önce hepsini oku, sonra hepsini yaz
const heights = Array.from(boxes).map(b => b.offsetHeight); // Toplu okuma
boxes.forEach((box, i) => { box.style.height = heights[i] + 10 + "px"; }); // Toplu yazma
```

### Büyük Liste Çözümleri

```
10.000 elemanlı liste:
├── Pagination    → Her sayfada 50 kayıt göster
├── Infinite Scroll → Scroll ettikçe yeni veri yükle (eski verileri temizle!)
└── Virtualization → Sadece ekranda görünen ~20 elementi render et
                     react-window, react-virtualized
```

### Network Performansı

```javascript
// ❌ Her harf yazımında API isteği
input.addEventListener("input", e => fetch(`/api/search?q=${e.target.value}`));

// ✅ Debounce + AbortController
const search = debounce((value, signal) => {
  fetch(`/api/search?q=${value}`, { signal });
}, 500);
```

**Cache ile gereksiz isteği azalt:**

```javascript
const cache = new Map();
async function getUser(id) {
  if (cache.has(id)) return cache.get(id);
  const data = await fetch(`/api/users/${id}`).then(r => r.json());
  cache.set(id, data);
  return data;
}
// ⚠️ Cache sınırsız büyümesin — maksimum boyut koy!
```

### Performans Ölçümü

```javascript
// console.time
console.time("loop");
for (let i = 0; i < 1_000_000; i++) { /* ... */ }
console.timeEnd("loop"); // loop: 12.5ms

// Performance API (daha hassas)
const start = performance.now();
// ... işlem ...
console.log(`${performance.now() - start} ms`);
```

**Araçlar:**
- Chrome DevTools → Performance sekmesi
- Chrome DevTools → Memory sekmesi
- React DevTools Profiler
- Lighthouse
- Chrome Task Manager (Shift+Esc)

### Premature Optimization

```
❌ Yanlış: Önce optimize et, sonra doğru yaz
✅ Doğru:  Önce okunabilir ve doğru yaz → Ölç → Darboğazı bul → Optimize et
```

Tahminle yapılan optimizasyon bazen kodu daha kötü yapar.

**Bundle Size & Lazy Loading:**

```javascript
// ❌ Tüm kütüphaneyi import et
import _ from "lodash"; // Tüm lodash yüklendi

// ✅ Sadece ihtiyacı al (tree shaking)
import debounce from "lodash/debounce";

// ✅ Lazy loading — AdminPage sadece gerekince yüklenir
const AdminPage = React.lazy(() => import("./AdminPage"));

// ✅ Görsel lazy loading
<img src="photo.jpg" loading="lazy" alt="..." />
```

---

## 7. Dil Bazında Karşılaştırma

| Özellik | C/C++ | Java | JavaScript | Python | Go |
|---|---|---|---|---|---|
| **Bellek yönetimi** | Manuel | GC (JVM) | GC (V8) | GC + Ref Count | GC |
| **GC türü** | Yok | Generational | Mark-Sweep + Gen | Ref Count + Cyclic | Mark-Sweep (Tricolor) |
| **Stack overflow** | Segfault | StackOverflowError | RangeError | RecursionError | goroutine panic |
| **Memory leak riski** | Çok yüksek | Orta | Orta | Düşük | Düşük |
| **GC pause (STW)** | Yok | Var (~ms-s) | Var (küçük, ~ms) | Var | Çok küçük (<1ms) |
| **Bellek kontrolü** | Tam kontrol | Az | Az | Az | İyi |

---

## 8. Mülakat Soruları

### Stack ve Heap arasındaki fark nedir?

Stack, fonksiyon çağrılarında kullanılan, LIFO mantığıyla çalışan, otomatik yönetilen, hızlı ama sınırlı boyutlu bir bellek alanıdır. Fonksiyon bitince stack frame otomatik silinir. Heap ise dinamik olarak büyüyebilen, büyük nesnelerin saklandığı alandır; yönetim ya GC'ye ya da programcıya aittir. Stack'te nesnenin kendisi değil referansı tutulur.

---

### Stack Overflow neden oluşur?

Fonksiyon çağrıları Stack'e frame olarak eklenir. Sonsuz recursion durumunda hiçbir frame çıkarılmaz, Stack'in limiti dolar ve `Maximum Call Stack Size Exceeded` hatası alınır.

---

### Garbage Collection nasıl çalışır?

GC, Heap'teki **erişilemeyen (unreachable)** nesneleri temizler. Modern motorlar Generational yaklaşım kullanır: Young Generation'da kısa ömürlü nesneler Minor GC ile sık temizlenir; Old Generation'da uzun yaşayanlar Major GC ile seyrek temizlenir. Stop-the-World, GC çalışırken uygulamanın kısa süre duraklatılmasıdır.

---

### Mark and Sweep ne anlama gelir?

Root'lardan başlayarak ulaşılabilen tüm nesneler **işaretlenir (mark).** Sonra işaretlenmemiş nesneler **silinir (sweep).** Bu yaklaşım circular reference'ı da çözebilir çünkü birbirini referans eden ama dışarıdan erişilemeyen nesneler işaretlenemez ve silinir.

---

### Circular reference her zaman memory leak midir?

Hayır. Modern GC (Mark and Sweep), root'lardan erişilemeyen circular nesneleri temizleyebilir. Sorun yalnızca bu circular yapının global değişken, event listener veya cache gibi yapılar aracılığıyla hâlâ erişilebilir olması durumunda oluşur.

---

### Memory leak nedir? Nasıl oluşur?

Artık kullanılmaması gereken verinin hâlâ bir referans üzerinden erişilebilir olduğu için bellekte kalmaya devam etmesidir. GC sadece erişilemeyen nesneleri temizler; mantıksal olarak gereksiz ama teknik olarak erişilebilir nesnelere dokunamaz. En yaygın sebepler: temizlenmeyen event listener'lar, setInterval'lar, global cache büyümesi, detached DOM, closure tuzağı, temizlenmeyen WebSocket/subscription.

---

### React'ta useEffect cleanup neden önemlidir?

`useEffect` içinde başlatılan event listener, interval, WebSocket, fetch veya subscription gibi dış kaynaklar, component unmount olduğunda da çalışmaya devam eder. Cleanup fonksiyonu bu kaynakları temizler. Temizlenmezse memory leak ve "Can't perform state update on unmounted component" uyarısı oluşur.

---

### Debounce ve Throttle farkı nedir?

Debounce, kullanıcı işlem yapmayı durdurunca belirli bir bekleyiş süresi sonra çalışır (search input için). Throttle ise kullanıcı ne yaparsa yapsın belirli zaman aralığında en fazla bir kez çalışır (scroll event için).

---

### WeakMap neden normal Map'ten farklıdır?

WeakMap, key olarak kullanılan objeyi **zayıf referansla** tutar. Objeye WeakMap dışında başka referans kalmazsa GC onu temizleyebilir. Normal Map'te key olan obje, Map var olduğu sürece bellekte tutulur. WeakMap iterable değildir çünkü elemanlar GC tarafından herhangi bir anda silinebilir.

---

### Premature optimization nedir ve neden kaçınılmalıdır?

Gerçek bir performans problemi ölçülmeden yapılan erken optimizasyondur. Kodu gereksiz karmaşıklaştırır, okunabilirliği düşürür ve çoğu zaman yanlış yeri optimize eder. Doğru yaklaşım: önce doğru ve okunabilir yaz, sonra araçlarla ölç, gerçek darboğazı bul, sadece orada optimize et.

---