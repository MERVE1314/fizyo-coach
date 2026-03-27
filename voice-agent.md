[voice-agent.md](https://github.com/user-attachments/files/26305592/voice-agent.md)
# Agent: Sesli Komut Sistemi (Voice Agent)

## Kimlik

```
Ad:       FizyoCoach Ses Ajanı
API:      Web Speech API (tarayıcı built-in)
Dil:      tr-TR
Mod:      continuous: false · interimResults: false
```

## Mimari

```
🎤 Mikrofon
    │
    ▼
SpeechRecognition (webkitSpeechRecognition)
    │ tr-TR · single utterance
    ▼
Transkript (lowercase string)
    │
    ▼
Komut Eşleştirme (includes tabanlı)
    │
    ├─── "başla"   ──→ startEx(selEx)
    ├─── "dur"     ──→ stopEx()
    ├─── "sonraki" ──→ nextRep()
    ├─── "ipucu"   ──→ speak(tips[0])
    └─── diğer     ──→ sendToAI(transcript)
         (len > 3)
```

## Sesli Giriş (STT)

| Özellik | Değer |
|---------|-------|
| API | `window.webkitSpeechRecognition` |
| Dil | `tr-TR` |
| Sürekli dinleme | `false` (tek ifade) |
| Ara sonuçlar | `false` |
| Tetikleyici | 🎤 butonuna basılınca |

## Sesli Çıkış (TTS)

| Özellik | Değer |
|---------|-------|
| API | `window.speechSynthesis` |
| Dil | `tr-TR` |
| Hız | `rate: 0.92` |
| İptal | Her yeni konuşmada `cancel()` çağrılır |

## Komut Tablosu

| Kullanıcı Söyler | Tetiklenen Eylem | Ekran |
|-----------------|-----------------|-------|
| "başla" | `startEx(selEx)` | Herhangi |
| "dur" / "durdur" | `stopEx()` | Antrenman |
| "sonraki" / "geç" | `nextRep()` | Antrenman |
| "ipucu" | `speak(selEx.tips[0])` | Herhangi |
| Diğer (>3 harf) | `sendToAI(transcript)` | Herhangi |

## TTS Tetikleyici Olaylar

| Olay | Söylenen |
|------|----------|
| Egzersiz başlar | "[Ex adı] başlıyor." |
| Dinlenme | "Dinlenme. [X] saniye." |
| Yeni set | "[X]. set başlıyor!" |
| 4 sn kala (egzersiz) | "Bitiyor..." |
| 4 sn kala (dinlenme) | "Hazır ol!" |
| Bitti | "Harika! Tamamlandı!" |
| AI yanıtı | [AI metnini okur] |
| İpucu komutu | [tips[0] metnini okur] |

## Durum Göstergesi

```
🎤 → dinlemiyor (gri/teal renk)
🔴 → aktif dinleme (kırmızı pulse)
"[transkript]" → voiceStatus alanında 3 sn gösterilir
```

## Hata Durumları

| Hata | Davranış |
|------|----------|
| `onerror` | `isListening = false`, sessizce hata |
| `onend` | `isListening = false` |
| Tarayıcı desteklemiyor | Mikrofon butonu çalışmaz (hata yok) |

## Tarayıcı Desteği

| Tarayıcı | Destek |
|----------|--------|
| Chrome / Edge | ✅ Tam destek |
| Safari (iOS) | ✅ webkit prefix ile |
| Firefox | ❌ Desteklenmiyor |
| Samsung Browser | ✅ webkit ile |

## Gelecek Geliştirmeler

- Komutları genişlet: "tekrar et", "yavaşlat", "kategori göster"
- `continuous: true` ile sürekli dinleme modu
- Wake word desteği: "Hey Fizyo" ile aktifleştirme
- Komut geri bildirimi: tanınan komut sesli onaylanır
