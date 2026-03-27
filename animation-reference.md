# FizyoCoach — Animasyon Referansı

## Genel Tasarım Kuralları

| Kural | Değer |
|-------|-------|
| ViewBox | `0 0 230 220` — tüm animasyonlarda sabit |
| Arka plan | Şeffaf (transparent) |
| FPS | 60 (requestAnimationFrame) |
| Figür ölçeği | Yetişkin: scale 1.0 · Çocuk: scale 0.85 |
| Zemin | `Floor` bileşeni — `y=188` varsayılan |
| Etiket | `EL` bileşeni — `y=213`, 9px, #506888 |

## Renk Sistemi

| Doku | Renk | Hex |
|------|------|-----|
| Ten açık | SK | `#e8c4a0` |
| Ten gölge | SK2 | `#c8864e` |
| Ten highlight | SK3 | `#f0d4b8` |
| Kıyafet ana | CL | `#2a4a7f` |
| Kıyafet koyu | CL2 | `#1a3060` |
| Kıyafet açık | CL3 | `#3a6aaf` |
| Saç | HR | `#2a1a0a` |
| Vurgu | ACC | `#00d4aa` |
| Aktif kas | — | `#ff9f43` |
| Sinir izi | — | `#ffd166` |
| Zemin | GRD | `#0f1e35` |

## Animasyon Tipleri

### 1. Sırt Üstü (Supine)
Kullanım: Pelvik tilt, Kalça köprüsü, Dead bug, SLR

```
Baş sol tarafta, vücut yatay,
Bacaklar yerde/havada.
Referans noktası: Floor y=188
```

### 2. Dört Ayak (Quadruped)
Kullanım: Kedi–İnek, Bird Dog

```
Sol tarafa bakan profil görünüm,
4 destek noktası (2 el, 2 diz).
Gövde merkezi: ~y=138
```

### 3. Ayakta (Standing)
Kullanım: Quadriceps germe, Terminal diz, Omuz, Boyun egzersizleri

```
Ön cephe görünüm,
Zemin üzerinde dik duruş.
Baş merkez: x=115, y=36-42
```

### 4. El/Bilek Yakın Plan
Kullanım: Bilek germe, Tendon, Parmak egzersizleri

```
Yatay ön kol,
El merkezi: ~x=115, y=140
Sinir izi veya tendon efekti
```

### 5. Oturur/Eğik
Kullanım: Pendulum, Wall slide, Bisiklet

```
Yana eğik veya duvara yaslanmış,
Ortam nesnesi (masa, duvar) eklenir.
```

## Figür Anatomisi ve Boyutlar

```
Head:    r=13-15   (yetişkin), r=15-16 (çocuk)
Body:    hw=15-16, hh=55-84  (omuz genişliği, yükseklik)
Thigh:   length=58*scale
Shin:    length=52*scale
Upper arm: length=44*scale
Forearm: length=38*scale
```

## Hareket Eğrileri

| Eğri | Fonksiyon | Kullanım |
|------|-----------|----------|
| Sinüs 0-1 | `s01(t,spd)` | Sürekli döngüler |
| Sinüs -amp/+amp | `sN(t,spd,amp)` | Salınım |
| EaseInOut | `easeInOut(s01(t))` | Doğal kaldırma/squat |
| Lineer | `t * hız` | Dönme hareketleri |

## Efekt Katmanları

### Kas Aktivasyon (Glow)
```jsx
<Glow cx={110} cy={148} rx={18} ry={12} op={L(0.05, 0.55, p)}/>
```
- Egzersizin doruk noktasında maksimum opaklık
- Resting pozisyonda minimum opaklık

### Sinir İzi
```jsx
<path d={`M... Q... ...`}
  fill="none" stroke="#ffd166" strokeWidth={2}
  strokeDasharray="5 3" opacity={L(0.2, 0.9, ext)}/>
```
- Karpal tünel ve nöroloji egzersizlerinde
- Hareket genişledikçe belirginleşir

### Direniş Bandı
```jsx
<path d={`M${wx} ${wy} L198 ${wy}`}
  stroke={ACC} strokeWidth={3.5} strokeDasharray="7 2"/>
```
- Bant egzersizlerinde görünür

## Küçük Boyut (Liste Görünümü)

```
width: 54px, height: 54px → borderRadius: 11px kutu
isPlaying={false} → statik → t = 0 → ilk frame
```

İlk frame: Figür dinlenme pozisyonunda, s01(0) = 0.5, L sonucu orta değer.

## Büyük Boyut (Detay/Antrenman)

```
Detay:    minHeight: 212px, animBox container
Antrenman: minHeight: 155px, küçük panel
```

## Gelecek Öneriler

| Özellik | Araç |
|---------|------|
| Daha akıcı animasyon | Lottie (.json formatı) |
| 3D görselleştirme | Three.js / rive.app |
| Gerçek video | Cloudinary CDN |
| Kas anatomi haritası | SVG body map + click interaktif |
