cat <<EOF > IDEA.md
# 💡 FizyoCoach AI: Akıllı Egzersiz Takip Sistemi

## 📌 Proje Vizyonu
FizyoCoach, fizyoterapi öğrencilerinin ve hastaların ev egzersizlerini klinik bir doğrulukla yapmalarını sağlayan, yapay zeka destekli bir asistan uygulamasıdır. API Proxy katmanı sayesinde veriler güvenli bir şekilde işlenir.

## 🛠 Teknik Altyapı
* **Backend:** Node.js Express Proxy (Anthropic Claude 3.5 Sonnet entegrasyonu aktif).
* **Sunucu:** http://localhost:8787/api/ai/chat.
* **Klinik Mantık:** Squat gibi temel hareketlerin biyomekanik analizi ve takibi.

## 🎯 Temel Özellikler

### 1. Klinik Squat Analizi
* **Diz Kontrolü:** Dizlerin parmak ucunu geçme durumunun takibi.
* **Gövde Pozisyonu:** Omurganın nötral pozisyonunun korunması.
* **Derinlik:** Kalça ve diz eklemi açısının klinik standartlara uygunluğu.

### 2. Yapay Zeka Destekli Geri Bildirim
* **Anlık Uyarılar:** Hatalı form algılandığında proxy üzerinden sesli veya yazılı komutlar (Örn: "Dizlerini dışa doğru it").
* **Gelişim Raporu:** Egzersiz sonrası klinik doğruluk puanlaması.

## 🚀 Buildathon Hedefleri
* **MVP:** Kameradan gelen veriyi AI Proxy üzerinden işleyip anlık feedback vermek.
* **Erişilebilirlik:** Kodlama bilgisi olmayan kullanıcıların dahi kolayca kurabileceği bir yapı.

## 📅 Yol Haritası
1. **Aşama:** AI Proxy'nin görüntü işleme kütüphaneleriyle (MediaPipe vb.) eşleşmesi.
2. **Aşama:** Squat hareketinin klinik kontrol noktalarının Claude 3.5 Sonnet'e öğretilmesi.
3. **Aşama:** Kullanıcı arayüzünün (fizyo_coach_v5.jsx) aktif edilmesi.

---
*Bu belge FizyoCoach Projesi kapsamında Buildathon 2026 için hazırlanmıştır.*
EOF
