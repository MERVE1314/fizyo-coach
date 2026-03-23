[README.md](https://github.com/user-attachments/files/26194428/README.md)
# FizyoCoach AI Proxy

Bu servis `fizyo_coach_v5.jsx` icin guvenli AI baglanti katmanidir.
API key istemcide tutulmaz, sadece server tarafinda kullanilir.

## Kurulum

1. Klasore gir:
   - `cd /Users/merve/Downloads/fizyocoach-ai-proxy`
2. Bagimliliklari kur:
   - `npm install`
3. Ortam dosyasi olustur:
   - `cp .env.example .env`
4. `.env` icinde `ANTHROPIC_API_KEY` degerini gir.
5. Servisi baslat:
   - `npm start`

Proxy adresi:
- `http://localhost:8787/api/ai/chat`

Saglik kontrolu:
- `http://localhost:8787/health`

## Uygulama tarafi ayari

`fizyo_coach_v5.jsx` varsayilan olarak:
- Dosya `file://` protokolu ile acilirsa `http://localhost:8787/api/ai/chat`
- Web uygulamasi icinden calisiyorsa `/api/ai/chat`

AI ekraninda `AI Ayar` tusundan endpoint/model degistirilebilir.

## Guvenlik notu

- Uretimde `ALLOWED_ORIGIN` degerini `*` yerine kendi domaininiz yapin.
- API key'i sadece `.env` dosyasinda tutun.
