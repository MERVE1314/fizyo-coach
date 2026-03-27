# Feature: Antrenman Zamanlayıcısı

## Özet
Egzersiz başlatıldığında devreye giren, set/dinlenme fazlarını otomatik yöneten
görsel + sesli zamanlayıcı sistemi.

## Faz Yapısı

```
[ Egzersiz Fazı ] ──→ [ Dinlenme Fazı ] ──→ [ Egzersiz Fazı ] ──→ ... ──→ [ Bitti ]
    duration sn            restTime sn
```

## Görsel Bileşenler

| Bileşen | Açıklama |
|---------|----------|
| Halka sayacı | `conic-gradient` ile dolup boşalan daire |
| Renk | Egzersiz fazı: #00d4aa (teal) · Dinlenme: #ffd166 (altın) |
| Büyük sayı | Kalan saniye (0'a kadar geri sayım) |
| Set rozeti | "SET 2 / 3" veya "⏸ DİNLENME" |
| Mini animasyon | Egzersiz figürü antrenman sırasında oynar |
| Form ipucu | Her sette dönen ipucu metni |

## Kontroller

| Buton | Davranış |
|-------|----------|
| ⏭ Sonraki | Seti atla / dinlenmeye geç |
| ⬛ Dur | Antrenmanı iptal et, listeye dön |
| 🎤 Mikrofon | Sesli komut dinlemeye başla |

## Sesli Komutlar (Web Speech API — tr-TR)

| Komut | Eylem |
|-------|-------|
| "Başla" | Egzersizi başlatır |
| "Dur" | Durdurur |
| "Sonraki" | Sete geçer |
| "İpucu" | İlk form ipucunu TTS ile okur |
| Diğer metin | AI koça gönderilir |

## Sesli Bildirimler (TTS)

| Tetikleyici | Söylenen |
|-------------|----------|
| Egzersiz başlangıcı | "[Egzersiz adı] başlıyor." |
| Dinlenme başlangıcı | "Dinlenme. [X] saniye." |
| Yeni set | "[X]. set başlıyor!" |
| 4 saniye kala | "Bitiyor..." / "Hazır ol!" |
| Tamamlandı | "Harika! Tamamlandı!" |

## Timer Mantığı

```js
useEffect(() => {
  if (isRunning && timeLeft > 0) {
    timer = setTimeout(() => setTimeLeft(t => t - 1), 1000)
    if (timeLeft === 4) speak(...)
  } else if (isRunning && timeLeft === 0) {
    nextRep()  // faz geçişi
  }
}, [isRunning, timeLeft])
```

## Tamamlandı Ekranı

- 🎉 animasyonu
- Egzersiz adı
- Seans özeti (bu oturumda tamamlananlar)
- "Ödev tamamlandı" özel mesajı (fzt. tarafından atandıysa)
- İlerleme kaydedilir (`patientProgress` state güncellenir)
- "Ana Sayfaya Dön" butonu
