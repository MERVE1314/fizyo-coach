# FizyoCoach — Renk Paleti

## Ana Renkler (Dark Theme)

```css
:root {
  --bg:          #060b16;  /* Ana arka plan — derin lacivert siyah */
  --surface:     #0b1322;  /* Yüzey — kartların altı */
  --card:        #0f1c2e;  /* Kart arka planı */
  --border:      #122030;  /* Kenarlık */
  --text:        #dce8f4;  /* Ana metin — açık mavi beyaz */
  --muted:       #455a78;  /* İkincil metin — soluk mavi */

  --accent:      #00d4aa;  /* Ana vurgu — teal yeşil */
  --accent-dim:  #00d4aa14; /* Vurgu yarı şeffaf */
  --success:     #22c55e;  /* Başarı — yeşil */
  --gold:        #ffd166;  /* Altın — ödev / dinlenme */
  --warn:        #ff6b6b;  /* Uyarı — kırmızı */
  --physio:      #7c3aed;  /* Fizyoterapist moru */
  --patient:     #0891b2;  /* Hasta mavisi */
}
```

## Kategori Renkleri

| Kategori | Renk | Hex |
|----------|------|-----|
| Bel Ağrısı | Mavi | `#3b82f6` |
| Karpal Tünel | Yeşil | `#10b981` |
| Diz Sorunları | Sarı | `#f59e0b` |
| Boyun & Omuz | Mor | `#8b5cf6` |
| Omuz Sorunları | Kırmızı | `#ef4444` |
| Pediatri | Cyan | `#06b6d4` |
| Kardiyopulmoner | Pembe-kırmızı | `#f43f5e` |
| Sporcu FTR | Menekşe | `#a855f7` |
| Nöroloji | Teal | `#14b8a6` |
| El Rehabilitasyonu | Turuncu | `#f97316` |

## Figür Renkleri (Animasyon)

```css
--skin:       #e8c4a0;  /* Ten rengi açık */
--skin-dark:  #c8864e;  /* Ten gölge */
--skin-light: #f0d4b8;  /* Ten highlight */
--cloth:      #2a4a7f;  /* Kıyafet lacivert */
--cloth-dark: #1a3060;  /* Kıyafet koyu */
--cloth-hi:   #3a6aaf;  /* Kıyafet highlight */
--hair:       #2a1a0a;  /* Saç koyu kahve */
--bone:       #e8dfc8;  /* Kemik rengi */
--floor:      #0f1e35;  /* Zemin */
--glow:       #ff9f43;  /* Aktif kas turuncu */
--nerve:      #ffd166;  /* Sinir izi sarı */
```

## Gradient Kullanımları

```css
/* Başlık logo */
background: linear-gradient(135deg, #00d4aa, #3b82f6);

/* Fizyoterapist giriş kartı */
background: linear-gradient(135deg, #180830, #2a1260);

/* Hasta giriş kartı */
background: linear-gradient(135deg, #001828, #002e48);

/* Başlat butonu */
background: linear-gradient(135deg, #00d4aa, #0088cc);

/* Fizyoterapist butonu */
background: linear-gradient(135deg, #7c3aed, #7c3aedaa);

/* Timer halka — egzersiz */
background: conic-gradient(#00d4aa {progress}%, #122030 0);

/* Timer halka — dinlenme */
background: conic-gradient(#ffd166 {progress}%, #122030 0);

/* İlerleme çubuğu */
background: linear-gradient(90deg, #ffd166, #f59e0b);
```

## Zorluk Renk Kodları

| Seviye | Renk | Hex |
|--------|------|-----|
| Kolay | Teal | `#00d4aa` |
| Orta | Altın | `#ffd166` |
| Zor | Kırmızı | `#ff6b6b` |

## Gece/Gündüz

> FizyoCoach yalnızca **dark theme** kullanmaktadır.
> Açık tema planlanmamıştır.
