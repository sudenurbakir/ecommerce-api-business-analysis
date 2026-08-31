# Auth & JWT Analizi 

## 1. Bu API Ne İşe Yarar?

Auth API, kullanıcının **kimliğini doğrulama** ve sisteme **giriş yapma** işlemlerini yönetir.

Temel işleri:
- Kullanıcı girişi (Login)
- Kullanıcı kaydı (Register)
- Token alma
- Token yenileme (Refresh)
- Çıkış yapma (Logout)
- Şifre sıfırlama / değiştirme

E-ticarette sepet, sipariş, adres gibi birçok işlem bu kimlik doğrulamasına bağlıdır.

---

## 2. JWT Nedir? 

**JWT (JSON Web Token)** = Kullanıcının giriş yaptığını kanıtlayan dijital bir bilet.

Basit mantık:
1. Kullanıcı email + şifre ile giriş yapar
2. Sistem ona bir **Token** verir
3. Sonraki isteklerde bu token’ı gönderir
4. Sistem token’a bakarak “bu kullanıcı giriş yapmış” der

Token yoksa veya geçersizse → **401 Unauthorized** döner.

---

## 3. Sık Görülen Endpoint’ler

| Method | Endpoint                        | Ne İş Yapar?                          |
|--------|---------------------------------|---------------------------------------|
| POST   | /api/auth/login                 | Kullanıcı girişi yapar, token döner   |
| POST   | /api/auth/register              | Yeni kullanıcı kaydı oluşturur        |
| POST   | /api/auth/refresh               | Eski token ile yeni token alır        |
| POST   | /api/auth/logout                | Çıkış yapar / token’ı geçersiz kılar  |
| POST   | /api/auth/forgot-password       | Şifre sıfırlama isteği gönderir       |
| POST   | /api/auth/reset-password        | Yeni şifre belirler                   |

---

## 4. BA Olarak Nelere Dikkat Edilmeli

### Login
- Hangi bilgilerle giriş yapılıyor? (email + şifre, telefon + şifre, vs.)
- Başarılı olunca ne dönüyor? (sadece token mi, yoksa kullanıcı bilgisi de mi?)
- Hatalı girişte ne oluyor? (kaç yanlış denemeden sonra kilitleniyor?)
- Token’ın ömrü ne kadar? (15 dakika, 1 saat, 1 gün?)

### Register
- Hangi alanlar zorunlu?
- Email / telefon doğrulaması var mı?
- Aynı email ile ikinci kayıt denenirsa ne oluyor? (409?)

### Token
- Access Token ve Refresh Token ayrı mı?
- Token süresi dolunca kullanıcı tekrar login mi olmak zorunda?
- Token çalınırsa ne yapılacak? (logout / blacklist var mı?)

### Genel
- Misafir kullanıcı bazı işlemleri yapabiliyor mu?
- Sosyal login var mı? (Google, Apple vs.)
- Çıkış yapınca token gerçekten geçersiz oluyor mu?

---

## 5. Önemli Status Code’lar (Auth için)

| Kod | Ne Zaman Döner?                                      |
|-----|------------------------------------------------------|
| 200 | Login / işlem başarılı                               |
| 201 | Yeni kullanıcı başarıyla oluşturuldu                 |
| 400 | Eksik veya hatalı veri                               |
| 401 | Hatalı email/şifre veya geçersiz token               |
| 403 | Hesap kilitli / yetkisiz                             |
| 404 | Kullanıcı bulunamadı                                 |
| 409 | Email veya telefon zaten kayıtlı                     |

---

## 6. BA Kontrol Listesi

- [ ] Login başarılı olunca hangi bilgiler dönüyor?
- [ ] Token’ın süresi net mi?
- [ ] Hatalı giriş denemelerinde hesap kilitlenme var mı?
- [ ] Register’da email/telefon unique mi kontrol ediliyor?
- [ ] Refresh token mekanizması var mı?
- [ ] Logout sonrası token geçersiz oluyor mu?
- [ ] 401 ve 409 senaryoları tanımlı mı?

---

## 7. Özet

Auth & JWT, e-ticaret sisteminin kapı görevlisidir.  
BA olarak buradav netleştirmemiz gereken şey:

> “Kullanıcı nasıl giriş yapacak, token ne kadar geçerli olacak, hatalı girişte ve çıkışta sistem ne yapacak?”
