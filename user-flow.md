# FizyoCoach — User Flow

## Genel Bakış
FizyoCoach iki farklı kullanıcı tipine sahip bir fizyoterapi rehber platformudur.
Her iki kullanıcı da aynı giriş ekranından başlar, PIN + Ad ile kendi akışına yönlendirilir.

---

## 1. Kimlik Doğrulama Akışı

```
[ Uygulama Açılır ]
        │
        ▼
[ Karşılama Ekranı ]
  ⚕ FizyoCoach logosu
  "Giriş tipini seçin"
        │
   ┌────┴────┐
   │         │
   ▼         ▼
[👨‍⚕️ Fzt.]  [🧑‍💼 Hasta]
   │         │
   ▼         ▼
[ Ad + PIN Girişi ]
   │         │
   ▼         ▼
[Fzt. Paneli] [Hasta Paneli]
```

**Hata durumu:** Yanlış PIN veya ad → "Ad veya PIN hatalı" uyarısı, tekrar dene.

---

## 2. Fizyoterapist Akışı

```
[ Fzt. Dashboard ]
  → Hasta listesi (ad, yaş, tanı, % tamamlama)
        │
        ▼
[ Hasta Detay Sayfası ]
  → Hasta profili (ad, yaş, tanı)
  → Aktif ödevler + ilerleme çubuğu
  → Toplam tamamlanan set sayısı
        │
   ┌────┴────┐
   │         │
   ▼         ▼
[Ödevleri Görüntüle]  [+ Yeni Ödev Ata]
                             │
                             ▼
                    [ Ödev Oluşturma Ekranı ]
                      1. Kategori filtrele
                         (Bel, Karpal, Diz,
                          Boyun, Omuz, Pediatri,
                          Kardiyopulmoner, Sporcu,
                          Nöroloji, El Reha)
                      2. Egzersizleri seç (✓ işaretle)
                      3. Hasta notu yaz
                      4. Son tarih belirle
                      5. "Ödev Ata" butonuna bas
                             │
                             ▼
                    [ Hasta Detaya Geri Dön ]
                      → Yeni ödev listede görünür
```

---

## 3. Hasta Akışı

```
[ Hasta Ana Sayfası ]
  → "Merhaba [Ad]!" + tanı bilgisi
  → Fizyoterapistinden Ödevler bölümü (varsa)
  → Egzersiz Kütüphanesi (10 kategori)
        │
   ┌────┴──────────────┐
   │                   │
   ▼                   ▼
[📋 Ödevlerim]    [📚 Kütüphane]
   │                   │
   ▼                   ▼
[Ödev Kartı]      [Kategori Seç]
  - Fzt. adı           │
  - Not                ▼
  - Son tarih     [Egzersiz Listesi]
  - İlerleme %         │
  - Egzersiz listesi   │
        │               │
        └──────┬────────┘
               ▼
      [ Egzersiz Detay Sayfası ]
        → Canlı SVG animasyonu (oynat/durdur)
        → Açıklama metni
        → Doğru form ipuçları (3 madde)
        → Zorluk / süre / set bilgisi
        → "Ödevde" rozeti (varsa)
               │
          ┌────┴────┐
          │         │
          ▼         ▼
      [▶ Başlat]  [🤖 AI Koça Sor]
          │
          ▼
      [ Antrenman Ekranı ]
        → Halka sayacı (conic-gradient)
        → "SET X / Y" veya "DİNLENME" rozeti
        → Mini canlı animasyon
        → Form ipucu kartı
        → Sesli komutlar aktif
          ┌──────────────┐
          │ Sesli Komutlar│
          │ "Başla"       │
          │ "Dur"         │
          │ "Sonraki"     │
          │ "İpucu"       │
          └──────────────┘
          │
          ▼ (tüm setler bitti)
      [ Tamamlandı Ekranı ]
        → 🎉 Tebrik
        → Seans özeti
        → "Ödev tamamlandı" mesajı (varsa)
        → "Ana Sayfaya Dön" butonu
```

---

## 4. AI Koç Akışı

```
[ AI Koç Ekranı ]
  → Yazarak soru sor
  → 🎤 Sesle soru sor
  → Hızlı soru önerileri (3 buton)
        │
        ▼
  [ Claude API isteği ]
    sistem prompt:
    - Hasta adı
    - Aktif egzersiz
    - Fizyoterapi uzmanı rolü
        │
        ▼
  [ Cevap baloncuğu ]
  [ Cevap sesli okunur (TTS) ]
```

---

## 5. İlerleme Takibi Akışı

```
[ Takip Ekranı ]
  → Tamamlanan egzersiz sayısı
  → Toplam set sayısı
  → Ödev ilerleme çubuğu (her ödev için)
  → Bölge bazlı ilerleme (10 kategori, %)
  → Son aktiviteler listesi (zaman damgalı)
```

---

## 6. Veri Akışı (Client-Side State)

```
[Giriş] → currentUser, userType
[Egzersiz Bitince] → completed[], sessionLog[], patientProgress{}
[Ödev Atama] → assignments{patientId: [{ids, note, dueDate}]}
[Fzt. Paneli] → patientProgress okur, ilerleme % hesaplar
```

---

## Navigasyon Yapısı (Alt Bar — Hasta)

| Tab | Ekran | Açıklama |
|-----|-------|----------|
| 🏠 Ana | patHome | Ödevler + kütüphane |
| 🏋️ Egzersiz | exlist | Kategori filtreyle liste |
| 📊 Takip | tracker | İlerleme grafikleri |
| 🤖 AI Koç | ai | Chat arayüzü |

---

## Navigasyon Yapısı (Alt Bar — Fzt.)

| Ekran | Açıklama |
|-------|----------|
| dashboard | Hasta listesi |
| patientDetail | Seçili hasta profili + ödevler |
| assign | Yeni ödev oluşturma |
