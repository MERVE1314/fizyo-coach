# Feature: Kimlik Doğrulama (Authentication)

## Özet
Kullanıcılar ad + 4 haneli PIN ile iki farklı rolle giriş yapar.
Rol tespiti otomatiktir — aynı giriş formu hem fzt. hem hasta için çalışır.

## Kullanıcı Rolleri

| Rol | Erişim |
|-----|--------|
| `physio` | Hasta yönetimi, ödev atama, ilerleme takibi |
| `patient` | Ödevler, egzersizler, AI koç, kişisel takip |

## Giriş Akışı

1. Ana ekranda "Fizyoterapist Girişi" veya "Hasta Girişi" seçilir
2. Ad (kısmi eşleşme) + PIN girilir
3. `DEMO_PHYSIOS` veya `DEMO_PATIENTS` dizisinde aranır
4. Eşleşirse `currentUser` ve `userType` state'e yazılır
5. İlgili panel açılır

## Hata Durumları

- Yanlış ad veya PIN → "Ad veya PIN hatalı" uyarısı
- Boş giriş → Butona basılınca hata gösterilir

## Çıkış

- Her iki panelde "Çıkış" butonu mevcuttur
- Tüm state (`currentUser`, `userType`, form alanları) sıfırlanır
- Giriş ekranına yönlendirilir

## Demo Hesaplar

```
Fizyoterapist: "Ayşe Kaya" / 1234
Fizyoterapist: "Can Öztürk" / 3456
Hasta:         "Ali Yılmaz" / 0001
Hasta:         "Burak Aydın" / 0006
```

## Teknik Notlar

- PIN kontrolü: `p.pin === pinInput`
- Ad kontrolü: `p.name.toLowerCase().includes(nameInput.toLowerCase())`
- State: `useState(null)` — sayfa yenilenince oturum kapanır
- Gelecek: Supabase Auth ile kalıcı oturum önerilir
