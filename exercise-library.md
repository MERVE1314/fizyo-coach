# Feature: Egzersiz Kütüphanesi

## Özet
30 egzersizden oluşan, 10 klinik kategoriye bölünmüş animasyonlu kütüphane.
Her egzersiz gerçek zamanlı SVG animasyonu, form ipuçları ve anatomik kas vurgusu içerir.

## Kategoriler (10 Uzmanlık Dalı)

| ID | Kategori | Renk | Egzersiz Sayısı | Uzmanlık |
|----|----------|------|-----------------|----------|
| `bel` | Bel Ağrısı | #3b82f6 | 5 | Ortopedik FTR |
| `karpal` | Karpal Tünel | #10b981 | 5 | El Rehabilitasyonu |
| `diz` | Diz Sorunları | #f59e0b | 3 | Ortopedik FTR |
| `boyun` | Boyun & Omuz Kuşağı | #8b5cf6 | 3 | Ortopedik FTR |
| `omuz` | Omuz Sorunları | #ef4444 | 4 | Ortopedik FTR |
| `pediatri` | Pediatri | #06b6d4 | 2 | Pediatrik FTR |
| `kardio` | Kardiyopulmoner | #f43f5e | 2 | Kardiyopulmoner FTR |
| `sporcu` | Sporcu FTR | #a855f7 | 2 | Spor Fizyoterapisi |
| `noro` | Nöroloji | #14b8a6 | 2 | Nörolojik FTR |
| `el` | El Rehabilitasyonu | #f97316 | 2 | El Rehabilitasyonu |

## Egzersiz Veri Yapısı

```js
{
  id: number,           // benzersiz ID (1–30)
  condition: string,    // kategori ID
  name: string,         // Türkçe egzersiz adı
  duration: number,     // saniye (10–300)
  reps: number,         // set sayısı
  restTime: number,     // dinlenme süresi (saniye)
  difficulty: string,   // "Kolay" | "Orta" | "Zor"
  description: string,  // nasıl yapılır
  tips: string[],       // 3 madde — doğru form ipuçları
}
```

## Animasyon Sistemi

Her egzersizin benzersiz SVG animasyonu bulunur. Animasyonlar:

- **Motor:** `requestAnimationFrame` ile 60fps
- **Figür bileşenleri:** `Head`, `Body`, `Leg`, `Arm`, `Hand`, `Joint`
- **Kas dokusu:** `musclePath()` — Bezier eğrili çift yüzey
- **Hareket eğrisi:** `easeInOut()` doğal organik hareket
- **Kas aktivasyonu:** Turuncu `Glow` efekti (aktif bölge)
- **Sinir izi:** Sarı stipple çizgi (karpal tünel / nöroloji)

## Egzersiz Detay Sayfası Özellikleri

- Canlı demo animasyonu (oynat / durdur kontrolü)
- Kategori, süre, set, zorluk rozetleri
- Açıklama metni
- Numbered form ipuçları (3 madde)
- "Ödevde" rozeti (fzt. tarafından atandıysa)
- "Başlat" butonu → antrenman ekranına geçiş
- "AI Koça Sor" butonu → AI chat'e geçiş

## Liste Görünümü Özellikleri

- Kategori filtresi (yatay kaydırmalı chip bar)
- Her kart: küçük animasyon preview + ad + zorluk + süre
- Tamamlanan egzersizlerde ✓ ikonu
- Ödev olarak atananlarda "Ödev" rozeti (altın rengi)

## Zorluk Seviyeleri

| Seviye | Renk | Kullanım |
|--------|------|----------|
| Kolay | #00d4aa (yeşil) | Başlangıç, yaşlı, pediatri |
| Orta | #ffd166 (altın) | Genel rehabilitasyon |
| Zor | #ff6b6b (kırmızı) | Sporcu, ileri seviye |
