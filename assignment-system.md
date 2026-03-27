# Feature: Ödev Atama Sistemi

## Özet
Fizyoterapistin hastaya kişiselleştirilmiş egzersiz programı atayabildiği,
hastanın ise bu programı takip edebildiği çift taraflı sistem.

## Fizyoterapist Tarafı

### Ödev Oluşturma Akışı

1. **Hasta seç** → Dashboard'dan hasta kartına tıkla
2. **"+ Yeni Ödev Ata"** butonuna bas
3. **Kategori filtrele** → 10 kategoriden filtre uygula
4. **Egzersizleri seç** → Checkbox ile işaretle (çoklu seçim)
5. **Not yaz** → Hastaya özel talimat (opsiyonel)
6. **Son tarih belirle** → Date picker
7. **"Ödev Ata"** butonuna bas → Kayıt oluşur

### Ödev Görüntüleme

- Hasta detay sayfasında tüm aktif ödevler listelenir
- Her ödev için: atama tarihi, son tarih, egzersiz listesi, not
- İlerleme çubuğu: kaç egzersiz tamamlandı / toplam
- Toplam tamamlanan set sayısı

## Hasta Tarafı

### Ana Sayfa Ödev Kartı

```
┌─────────────────────────────────┐
│ Fzt. Ayşe Kaya         Son: ... │
│ 💬 "Sabah uyandığınızda 10 dk" │
│ İlerleme: ████░░ 2/3           │
│                                 │
│ ○ Pelvik Tilt        [✓]       │
│ ○ Kedi–İnek          [✓]       │
│ ○ Kalça Köprüsü      [ ]       │
└─────────────────────────────────┘
```

### Ödev Egzersizine Tıklama

- Direkt egzersiz detay sayfasına gider
- "📋 Ödevde" rozeti görünür
- Antrenman bitince "✓ Ödevinizi tamamladınız!" mesajı

### Egzersiz Listesinde Ödev Göstergesi

- Altın renkli "Ödev" rozeti
- Altın kenarlı kart arka planı

## Veri Yapısı

```js
assignments: {
  "h1": [
    {
      ids: [1, 2, 3],           // egzersiz ID'leri
      note: "Sabah 10 dk yap", // fzt. notu
      dueDate: "2026-03-28",   // son tarih
      assignedBy: "Fzt. Ayşe Kaya",
      assignedAt: "23.03.2026",
    }
  ]
}
```

## İlerleme Hesaplama

```js
const assignedIds = assignments[patientId].flatMap(a => a.ids)
const doneIds = patientProgress[patientId].completed
  .filter(id => assignedIds.includes(id))
const percent = Math.round(doneIds.length / assignedIds.length * 100)
```

## Fizyoterapist Panelinde İlerleme Göstergesi

- Her hasta kartında `%` tamamlama oranı
- 100% olunca yeşil renk
- Takip ekranında "Son aktif tarih" bilgisi
- Toplam tamamlanan set sayısı

## Teknik Notlar

- State: `useState` ile in-memory (demo veri ile başlangıç)
- Gelecek: Her ödev `assignments` tablosuna Supabase'e yazılacak
- Birden fazla ödev atanabilir (array yapısı)
- Ödev silinemiyor (şimdilik) — gelecek özellik
