# FizyoCoach — İkon ve Sembol Referansı

## Uygulama İkonu

```
⚕   Tıbbi sembol — logo olarak kullanılır
    Kullanım: Header, giriş ekranı, tab bar
```

## Navigasyon İkonları

| Tab | İkon | Açıklama |
|-----|------|----------|
| Ana Sayfa | 🏠 | Hasta ana sayfası |
| Egzersiz | 🏋️ | Egzersiz kütüphanesi |
| Takip | 📊 | İlerleme dashboard |
| AI Koç | 🤖 | Sohbet ekranı |

## Kategori İkonları

| Kategori | İkon | Renk |
|----------|------|------|
| Bel Ağrısı | 🔵 | #3b82f6 |
| Karpal Tünel | 🟢 | #10b981 |
| Diz Sorunları | 🟡 | #f59e0b |
| Boyun & Omuz Kuşağı | 🟣 | #8b5cf6 |
| Omuz Sorunları | 🔴 | #ef4444 |
| Pediatri | 🩵 | #06b6d4 |
| Kardiyopulmoner | ❤️ | #f43f5e |
| Sporcu FTR | ⚡ | #a855f7 |
| Nöroloji | 🧠 | #14b8a6 |
| El Rehabilitasyonu | 🖐 | #f97316 |

## Eylem İkonları

| Eylem | İkon | Kullanım |
|-------|------|----------|
| Başlat | ▶ | Egzersiz başlatma butonu |
| Durdur | ⬛ | Antrenmanı durdur |
| Sonraki | ⏭ | Sete geç |
| Dinleme | 🎤 | Sesli komut aktif değil |
| Dinliyor | 🔴 | Sesli komut aktif |
| Tamamlandı | ✓ | Egzersiz tamamlama |
| Kutlama | 🎉 | Seans sonu |
| Ödev | 📋 | Fizyoterapist ödevi |
| Takip | 📊 | İlerleme verileri |
| Sohbet | 💬 | AI chat boş ekran |
| Profil | 👨‍⚕️ | Fizyoterapist |
| Hasta | 🧑‍💼 | Hasta girişi |

## Durum Göstergesi Renkleri

| Durum | Renk | İkon |
|-------|------|------|
| Tamamlandı | #22c55e | ✓ yeşil |
| Devam ediyor | #ffd166 | ilerleme çubuğu altın |
| Ödev atandı | #ffd166 | "Ödev" rozeti altın |
| Uyarı/Hata | #ff6b6b | metin kırmızı |

## Tip Kullanımı

> Tüm ikonlar sistem emojisidir — harici ikon kütüphanesi kullanılmamaktadır.
> Bu, bundle boyutunu küçük tutar ve platform uyumluluğunu artırır.
>
> **Gelecek öneri:** Heroicons veya Phosphor Icons ile tutarlı SVG ikonlara geçiş.

## Rozet (Badge) Stilleri

```js
badge(color) = {
  background: color + "22",    // %13 opaklık
  color: color,
  borderRadius: 20,            // tam yuvarlak
  padding: "3px 10px",
  fontSize: 11,
  fontWeight: 700,
}
```

Örnek rozetler:
- 🟢 `Kolay` — teal
- 🟡 `Orta` — altın
- 🔴 `Zor` — kırmızı
- 🔵 `Bel Ağrısı` — mavi
- `📋 Ödevde` — altın
- `3 ✓` — oturum sayısı
