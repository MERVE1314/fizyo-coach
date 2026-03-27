[animation-engine.md](https://github.com/user-attachments/files/26305570/animation-engine.md)
# Agent: SVG Animasyon Motoru

## Kimlik

```
Ad:      FizyoCoach Animasyon Motoru
Teknoloji: requestAnimationFrame + SVG
FPS:     60
Egzersiz sayısı: 30 animasyon (id: 1–30)
```

## Mimari

```
useAnimFrame(playing: boolean)
    │
    ├─ playing = true  → requestAnimationFrame döngüsü başlar
    │                    t = (timestamp - startTime) / 1000
    │
    └─ playing = false → cancelAnimationFrame, t sıfırlanmaz
         │
         ▼
    ExerciseAnimation({ exerciseId, isPlaying })
         │
         ▼
    ANIM_MAP[exerciseId]  →  AnimasyonKomponent({ t })
         │
         ▼
    SVG (viewBox="0 0 230 220")
```

## Matematik Yardımcıları

| Fonksiyon | Formül | Kullanım |
|-----------|--------|----------|
| `s01(t,spd,off)` | `(sin(t·spd+off)+1)/2` | 0..1 arası smooth döngü |
| `sN(t,spd,amp,off)` | `sin(t·spd+off)·amp` | -amp..amp arası titreşim |
| `L(a,b,f)` | `a+(b-a)·clamp(f,0,1)` | iki değer arası interpolasyon |
| `R(deg)` | `deg·π/180` | derece → radyan |
| `easeInOut(x)` | bezier eğrisi | mekanik hareketi yumuşatır |

## Figür Bileşenleri

| Bileşen | SVG Primitif | Açıklama |
|---------|-------------|----------|
| `Head` | `<ellipse>` + `<circle>` | Saç, yüz, göz, kaş, ağız, kulak, boyun |
| `Body` | `<path>` | Omuz genişliği ve kalça daralması, yaka detayı |
| `Leg` | `musclePath()` + `<circle>` + `<path>` | Uyluk + diz eklemi + baldır + ayak |
| `Arm` | `musclePath()` + `<circle>` | Üst kol + dirsek + ön kol + el |
| `Hand` | `<rect>` + avuç + 4 parmak + başparmak | Tam el anatomisi |
| `Joint` | `<circle>` | Eklem noktası vurgusu |
| `Floor` | `<rect>` x2 | Zemin + gölge |
| `Glow` | `<ellipse>` | Turuncu aktif kas highlight |
| `Spine` | `<path>` Bezier | Sarı omurga izi |

## `musclePath()` Fonksiyonu

```js
// İki nokta arası Bezier eğrili kas yolu
musclePath(x1, y1, x2, y2, width, bulge=1.3)

// Dışbükey sağ yüz → içbükey sol yüz
// Gerçek kas anatomisini simüle eder
```

## Animasyon Kataloğu (30 Egzersiz)

| ID | Ad | Kategori | Hareket Tipi |
|----|----|----------|-------------|
| 1 | Pelvik Tilt | Bel | Sırt üstü, lumbar tilt |
| 2 | Kedi–İnek | Bel | Dört ayak, omurga fleksiyon/ekstansiyon |
| 3 | Kalça Köprüsü | Bel | Sırt üstü, kalça kaldırma |
| 4 | Dead Bug | Bel | Sırt üstü, karşı kol-bacak |
| 5 | Bird Dog | Bel | Dört ayak, karşı uzatma |
| 6 | Bilek Dorsal Germe | Karpal | El + sinir izi |
| 7 | Tendon Kaydırma | Karpal | 5 parmak pozisyonu sekansı |
| 8 | Median Sinir Mob. | Karpal | Kol uzatma + sinir izi |
| 9 | Parmak Abdüksiyonu | Karpal | Parmak açma |
| 10 | Bilek Sirkumdüksiyonu | Karpal | Tam daire dönüş |
| 11 | Quadriceps Germe | Diz | Ayakta topuk-kalça |
| 12 | Terminal Diz Ekst. | Diz | Son derece ekstansiyon |
| 13 | Düz Bacak Kaldırma | Diz | Sırt üstü bacak kaldırma |
| 14 | Chin Tuck | Boyun | Baş retraksiyon |
| 15 | Boyun Lateral Flex. | Boyun | Yan eğme |
| 16 | Skapular Retraksiyon | Boyun | Kürek kemiği çekme |
| 17 | Pendulum | Omuz | Serbest sarkaç |
| 18 | Dış Rotasyon | Omuz | Bant ile dış rotasyon |
| 19 | Wall Slide | Omuz | Duvar kaydırma |
| 20 | Omuz Sirkumdüksiyonu | Omuz | Tam daire |
| 21 | Kurbağa Pozisyonu | Pediatri | Kalça açılma |
| 22 | Top Koordinasyonu | Pediatri | Top tutma-atma |
| 23 | Diyafragmatik Solunum | Kardiyopulmoner | Nefes alma döngüsü |
| 24 | Bisiklet Ergometre | Kardiyopulmoner | Pedal döngüsü |
| 25 | Tek Bacak Squat | Sporcu | Çömelme |
| 26 | Pliometrik Sıçrama | Sporcu | Yerden ayrılma |
| 27 | Frenkel Egzersizi | Nöroloji | Adım sekansı |
| 28 | Spastisite Germe | Nöroloji | Kol nörolojik germe |
| 29 | Parmak Fleksiyon-Ext. | El Reha | Parmak bükme-açma |
| 30 | El Kavrama (Top) | El Reha | Top sıkma |

## Performans Notları

- Her animasyon bileşeni `t` prop alır (saniye cinsinden zaman)
- `playing=false` olduğunda RAF iptal edilir, CPU kullanımı 0'a düşer
- Liste görünümünde: `isPlaying={false}` → statik preview
- Detay sayfasında: `isPlaying={animPlay}` → kontrollü
- Antrenman sırasında: `isPlaying={isRunning && phase==="exercise"}`
