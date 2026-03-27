# Feature: İlerleme Takibi

## Özet
Hastanın tamamladığı egzersizleri, ödev ilerlemesini ve bölge bazlı
gelişimini gösteren görsel takip paneli.

## Hasta Takip Ekranı (📊 Tracker)

### Özet Kartları

```
┌──────────────┐  ┌──────────────┐
│      12      │  │      45      │
│  Egzersiz    │  │  Toplam Set  │
└──────────────┘  └──────────────┘
```

### Ödev İlerleme Bölümü

Her aktif ödev için ayrı çubuk:
```
Ödev 1 · Fzt. Ayşe Kaya          2/3
████████████████░░░░░░░░░░░░░░░░
```

### Bölge İlerleme Çubukları (10 kategori)

```
🔵 Bel Ağrısı               3/5
████████████░░░░░░░░░░░░░░░░

🟢 Karpal Tünel             2/5
████████░░░░░░░░░░░░░░░░░░░░

⚡ Sporcu FTR               1/2
████████████░░░░░░░░░░░░░░░░
```

### Son Aktiviteler Listesi

```
● Pelvik Tilt          14:32
● Kalça Köprüsü        14:25
● Chin Tuck            09:10
```

- Son 8 aktivite gösterilir
- Kategori rengi ile işaretlenir
- Zaman damgası ile

## Fizyoterapist Panelinde Takip

### Hasta Listesi Kartı

```
┌────────────────────────────────┐
│ 👤 Ali Yılmaz                  │
│ L4-L5 disk hernisi             │
│ 45 yaş   [Ödev: 2/3]   Son:... │
│                           62%  │
└────────────────────────────────┘
```

### Hasta Detay Sayfasında İlerleme

```
Ödev İlerlemesi               2/3
████████████████████░░░░░░░░░░

Toplam 18 set tamamlandı
Son aktif: 27.03.2026
```

## Veri Kaynakları

| Metrik | Kaynak |
|--------|--------|
| Tamamlanan egzersizler | `completed[]` state |
| Toplam set | `sessionLog.length` |
| Bölge ilerlemesi | `EXERCISES.filter(condition) + completed` |
| Ödev ilerlemesi | `assignments[id].ids` vs `completed` |
| Son aktiviteler | `sessionLog[]` — reverse slice(0,8) |
| Fzt. görünümü | `patientProgress[patientId]` |

## İlerleme Güncelleme Tetikleyicileri

Egzersiz tamamlandığında (`nextRep()` → son set bitti):

```js
setCompleted([...new Set([...completed, selEx.id])])
setSessionLog([...sessionLog, {
  name, time, reps, cond
}])
setPatientProgress({
  ...prev,
  [currentUser.id]: {
    completed: newCompleted,
    lastActive: "27.03.2026",
    totalSets: prev.totalSets + selEx.reps
  }
})
```

## Renk Kodlaması

| Durum | Renk |
|-------|------|
| Tamamlandı ✓ | #22c55e (yeşil) |
| Devam ediyor | #ffd166 (altın) |
| Başlanmadı | #152030 (koyu) |
| Kategori rengi | Her kategoriye özel |

## Gelecek Özellikler

- Haftalık/aylık grafik (Recharts)
- Ağrı seviyesi takibi (1–10 skala)
- Fzt.'nin hasta için not eklemesi
- PDF rapor çıktısı
- Push notification — "Bugün egzersizini yaptın mı?"
