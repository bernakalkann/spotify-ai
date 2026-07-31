# 🎵 Spotify AI Playlist Analyzer

Spotify çalma listelerini analiz eden, ses profillerini görselleştiren ve Spotify embed oynatıcısıyla entegre çalışan bir web uygulaması.

## Özellikler

- 🎵 Herkese açık Spotify playlist, albüm ve şarkı bağlantılarını analiz eder
- 📊 Enerji, dans edilebilirlik, pozitiflik, tempo ve akustiklik metriklerini gösterir
- 🎨 Dönen plak animasyonlu premium arayüz
- 🔍 Şarkı arama ve sıralama (melankolik, enerjili, popüler, karıştır)
- 🎧 Spotify embed oynatıcı entegrasyonu
- 📈 Radar ve Bar grafikleriyle ses profili görselleştirme

## Kurulum

```bash
python3 server.py
```

Uygulama `http://localhost:3005` adresinde açılır.

## Kullanım

1. Bir Spotify playlist bağlantısı kopyalayın
2. Arama kutusuna yapıştırın (otomatik analiz başlar)
3. Analiz sonuçlarını inceleyin ve şarkıları listeden dinleyin

## Teknolojiler

- **Frontend:** HTML5, CSS3, Vanilla JavaScript, Chart.js
- **Backend:** Python 3 (http.server, multi-threaded)
- **Veri:** Spotify Embed Next.js state parsing
