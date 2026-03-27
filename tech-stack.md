# FizyoCoach — Teknoloji Stack

## Genel Mimari

```
┌─────────────────────────────────────────────────┐
│              FRONTEND (React SPA)               │
│         fizyo_coach_v5.jsx — Tek dosya          │
└────────────────────┬────────────────────────────┘
                     │ fetch("/api/ai/chat")
                     ▼
┌─────────────────────────────────────────────────┐
│           AI PROXY (Node.js / Express)          │
│         fizyocoach-ai-proxy / server.js         │
│         http://localhost:8787                   │
└────────────────────┬────────────────────────────┘
                     │ x-api-key header
                     ▼
┌─────────────────────────────────────────────────┐
│           ANTHROPIC API                         │
│         claude-sonnet-4-20250514                │
│         /v1/messages endpoint                   │
└─────────────────────────────────────────────────┘
```

---

## Frontend

| Katman | Teknoloji | Versiyon | Kullanım |
|--------|-----------|----------|----------|
| UI Framework | React | 18+ | Komponent yapısı, hooks |
| Dil | JavaScript (JSX) | ES2022+ | Tek .jsx dosyası |
| Stil | Inline styles | — | CSS-in-JS, dinamik stiller |
| Animasyon | requestAnimationFrame | Web API | 30 egzersiz SVG animasyonu |
| Routing | useState tabanlı | — | Screen state makinesi |
| Ses Tanıma | Web Speech API | — | `webkitSpeechRecognition`, tr-TR |
| TTS (Sesli Okuma) | SpeechSynthesis API | — | `SpeechSynthesisUtterance`, tr-TR |
| State Yönetimi | useState + useCallback | React built-in | Auth, egzersiz, ödev state |
| Build/Deploy | Lovable.dev | — | https://fizyocoach.lovable.app |

### React Hook Kullanımı

| Hook | Amaç |
|------|------|
| `useState` | Ekran geçişleri, form state, egzersiz durumu |
| `useEffect` | Timer, animasyon döngüsü, speech recognition init |
| `useRef` | RAF referansı, timer ID, konuşma tanıma nesnesi, chat scroll |
| `useCallback` | nextRep, handleVoice — re-render optimizasyonu |

---

## Animasyon Sistemi

| Bileşen | Teknoloji | Açıklama |
|---------|-----------|----------|
| Motor | `requestAnimationFrame` | 60fps smooth döngü |
| Figür | SVG primitives | `<path>`, `<ellipse>`, `<circle>`, `<rect>` |
| Kas dokusu | Bezier `musclePath()` | İçbükey/dışbükey çift yüzey |
| Hareket | `easeInOut()` + `sin01()` | Doğal organik hareket |
| Figürler | `Head`, `Body`, `Leg`, `Arm`, `Hand`, `Joint` | Anatomik komponentler |
| Efektler | `Glow` (turuncu halo) | Aktif kas grubu vurgusu |
| Egzersiz sayısı | 30 animasyon | id: 1–30, ANIM_MAP tablosu |

---

## Backend — AI Proxy

| Katman | Teknoloji | Versiyon | Kullanım |
|--------|-----------|----------|----------|
| Runtime | Node.js | 18+ | ES Module (`"type": "module"`) |
| Framework | Express | 4.19.2 | HTTP sunucu, routing |
| CORS | cors | 2.8.5 | Cross-origin izin yönetimi |
| Env yönetimi | dotenv | 16.4.5 | `.env` dosyasından config okuma |
| Dil | JavaScript | ES2022 | `import/export`, async/await |

### API Endpointleri

| Method | Path | Açıklama |
|--------|------|----------|
| GET | `/health` | Servis durumu, API key kontrolü |
| POST | `/api/ai/chat` | AI sohbet proxy — Anthropic'e iletir |

### Ortam Değişkenleri

| Değişken | Varsayılan | Açıklama |
|----------|------------|----------|
| `ANTHROPIC_API_KEY` | — | Zorunlu — Anthropic API anahtarı |
| `PORT` | 8787 | Sunucu portu |
| `ALLOWED_ORIGIN` | `*` | CORS izin verilen origin |
| `ANTHROPIC_MODEL` | `claude-sonnet-4-20250514` | Kullanılacak model |

---

## AI Entegrasyonu

| Özellik | Detay |
|---------|-------|
| Model | `claude-sonnet-4-20250514` |
| API | Anthropic Messages API v1 |
| max_tokens | 1000 |
| Sistem prompt | Hasta adı + aktif egzersiz + rol tanımı |
| Dil | Türkçe, maks 3 cümle, kısa ve motive edici |
| Bağlantı | Proxy üzerinden (API key frontend'de yok) |

---

## Veri Mimarisi

> Şu an tüm state client-side `useState` ile tutulmaktadır.
> Kalıcı depolama yok — sayfa yenilenince sıfırlanır.

```
AUTH
  currentUser: { id, name, pin, specialty | diagnosis, patients[] }
  userType: "physio" | "patient"

ASSIGNMENTS (in-memory, başlangıç demo verisi ile)
  assignments: {
    [patientId]: [
      {
        ids: number[],       // egzersiz ID listesi
        note: string,        // fizyoterapist notu
        dueDate: string,     // son tarih
        assignedBy: string,  // fzt. adı
        assignedAt: string,  // atama tarihi
      }
    ]
  }

PATIENT PROGRESS (in-memory)
  patientProgress: {
    [patientId]: {
      completed: number[],   // tamamlanan egzersiz ID'leri
      lastActive: string,    // son aktif tarih
      totalSets: number,     // toplam set
    }
  }
```

---

## Demo Kullanıcılar

### Fizyoterapistler (6 kişi)

| Ad | PIN | Uzmanlık |
|----|-----|----------|
| Fzt. Ayşe Kaya | 1234 | Ortopedik FTR |
| Fzt. Mehmet Demir | 5678 | Nörolojik FTR |
| Fzt. Elif Çelik | 9012 | Kardiyopulmoner FTR |
| Fzt. Can Öztürk | 3456 | Sporcu Fizyoterapisti |
| Fzt. Selin Arslan | 7890 | Pediatrik FTR |
| Fzt. Murat Yıldız | 2468 | El Rehabilitasyonu |

### Hastalar (8 kişi)

| Ad | PIN | Tanı |
|----|-----|------|
| Ali Yılmaz | 0001 | L4-L5 disk hernisi |
| Fatma Şahin | 0002 | Karpal tünel sendromu |
| Ahmet Çelik | 0003 | Sağ diz osteoartriti |
| Zeynep Arslan | 0004 | İnme sonrası spastisite |
| Hasan Koca | 0005 | KOAH — efor intoleransı |
| Burak Aydın | 0006 | ACL rekonstrüksiyon sonrası |
| Aylin Kaya | 0007 | Gelişimsel kalça displazisi |
| Nilüfer Demir | 0008 | Fleksör tendon tamiri sonrası |

---

## Deployment

| Ortam | Platform | URL |
|-------|----------|-----|
| Frontend (prod) | Lovable.dev | https://fizyocoach.lovable.app |
| AI Proxy (local) | Node.js / localhost | http://localhost:8787 |
| AI Proxy (prod önerisi) | Railway / Render / Fly.io | — |

---

## Gelecek Stack Önerileri

| İhtiyaç | Öneri |
|---------|-------|
| Kalıcı veri | Supabase (PostgreSQL + Auth) |
| Gerçek zamanlı | Supabase Realtime |
| Dosya depolama | Supabase Storage |
| Auth | Supabase Auth veya Clerk |
| Prod proxy | Railway veya Render (ücretsiz tier) |
| Video/animasyon | Lottie veya rive.app |
