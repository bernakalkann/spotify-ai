# Spotify AI Playlist Analyzer

Spotify çalma listelerini analiz eden ve ses profillerini görselleştiren bir yapay zeka destekli web uygulaması. Bu proje, Retrieval-Augmented Generation (RAG) mimarisinin gerçek hayattaki bir müzik analizi senaryosuna nasıl uygulanabileceğini göstermek amacıyla geliştirilmiştir.

---

## Yapay Zeka Mimarisi: RAG (Retrieval-Augmented Generation)

RAG, büyük dil modellerinin veya analitik sistemlerin dış bir veri kaynağından bilgi almasını (retrieval), bu bilgiyi mevcut bağlamla zenginleştirmesini (augmentation) ve kullanıcıya anlamlı bir çıktı üretmesini (generation) sağlayan bir mimaridir.

Bu projede RAG şu şekilde çalışır:

### 1. Retrieval — Veri Çekme
Kullanıcı bir Spotify playlist URL'si girer. Python backend, Spotify'ın embed sayfasını `urllib` ile getirir ve sayfanın içine gömülü `__NEXT_DATA__` JSON nesnesini parse eder. Bu nesne, Next.js tarafından sunucu tarafında render edilen ve gerçek şarkı listesini içeren yapılandırılmamış veridir.

```python
# Spotify embed sayfasından __NEXT_DATA__ çıkarımı
match = re.search(r'<script id="__NEXT_DATA__"[^>]*>(.*?)</script>', html, re.DOTALL)
state = json.loads(match.group(1))
```

### 2. Augmentation — Veri Zenginleştirme
Ham şarkı verisi (isim, sanatçı, süre) tek başına analiz için yeterli değildir. Her şarkı için enerji, dans edilebilirlik, pozitiflik (valence), tempo ve akustiklik metrikleri deterministik bir seed fonksiyonu aracılığıyla üretilir. Bu yaklaşım, Spotify'ın resmi Audio Features API'sine ihtiyaç duymadan ses profilini tahmin etmeye benzer bir augmentation katmanı oluşturur.

### 3. Generation — Analiz ve Görselleştirme
Zenginleştirilmiş veri kullanılarak:
- Radar ve bar grafikleri (Chart.js) ile ses profili görselleştirilir
- Listenin genel ruh hali doğal dil olarak özetlenir
- Kullanıcı, listeyi enerji veya duygu durumuna göre sıralayabilir

Bu üç aşama birleşerek ham bir playlist URL'sini, yorumlanabilir bir müzik analiz raporuna dönüştürür.

---

## Teknik Altyapı

| Bileşen | Teknoloji |
|---|---|
| Frontend | HTML5, CSS3, Vanilla JavaScript |
| Grafik | Chart.js (Radar, Bar) |
| Backend | Python 3, `http.server`, `ThreadingMixIn` |
| Veri Kaynağı | Spotify Embed `__NEXT_DATA__` (Next.js SSR state) |
| Sunucu | Multi-threaded HTTP Server (port 3005) |

---

## Kurulum

```bash
python3 server.py
```

Sunucu `http://localhost:3005` adresinde başlar. Ek bağımlılık gerekmez.

---

## Kullanım

1. Spotify'dan herkese açık bir playlist bağlantısı kopyalayın
2. Arama kutusuna yapıştırın — analiz otomatik olarak başlar
3. Şarkı listesi, ses profili grafikleri ve ruh hali özetini inceleyin
4. Sıralama butonlarıyla listeyi melankolik, enerjik veya popülerlik sırasına göre düzenleyin
5. Herhangi bir şarkıya tıklayarak embed Spotify oynatıcısında dinleyin

---

## Öğrenme Hedefleri

Bu projeyi geliştirirken aşağıdaki yapay zeka ve yazılım mühendisliği kavramları incelenmiştir:

- RAG (Retrieval-Augmented Generation) mimarisinin temel katmanları
- Web scraping ile yapılandırılmamış veriden veri çıkarımı
- Deterministik seed fonksiyonlarıyla veri augmentation
- Ses analizi metriklerinin (valence, energy, tempo) anlamı ve yorumlanması
- Multi-threaded sunucu mimarisi ile eşzamanlı istek yönetimi
- Frontend'de dinamik veri görselleştirme

