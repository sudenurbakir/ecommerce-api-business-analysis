# Postman ile API Test Rehberi (İş Analisti İçin)

## 1. Postman Nedir?

Postman, API’leri **test etmek** ve **incelemek** için kullanılan en yaygın araçtır.

BA olarak Postman’i şu amaçlarla kullanırız;
- Endpoint’lerin gerçekten çalışıp çalışmadığını görmek
- Request / Response yapısını anlamak
- Status code’ları gözlemlemek
- Hata senaryolarını test etmek
- Geliştiriciye “şu durumda böyle dönüyor” diye net geri bildirim vermek

---

## 2. Temel Ekran Alanları

| Alan              | Ne İşe Yarar?                                      |
|-------------------|----------------------------------------------------|
| Method            | GET, POST, PUT, PATCH, DELETE seçtiğin yer         |
| URL               | Endpoint adresini yazdığın yer                     |
| Params            | Query parametrelerini girdiğin yer                 |
| Authorization     | Token / giriş bilgisini girdiğin yer               |
| Headers           | Ek başlık bilgileri                                |
| Body              | POST / PUT / PATCH’te gönderilecek JSON verisi     |
| Send              | İsteği gönder butonu                               |
| Response          | API’nin döndüğü cevap (status code + body)         |

---

## 3. Basit Test Senaryoları

### Senaryo 1: Ürünleri Getirme

1. Method olarak **GET** seçelim
2. Adres kısmına ürün listesi endpoint’ini yazalım
3. **Send** butonuna bas
4. Sonuç: 200 dönmeli ve ürünler gelmeli

---

### Senaryo 2: Sepete Ürün Ekleme

1. Method olarak **POST** seç
2. Adres kısmına sepete ekleme endpoint’ini yazalım
3. Authorization kısmına token’ını yapıştıralım
4. Body kısmına ürün bilgilerini yazalım
5. **Send** butonuna basalım
6. Sonuç: 200 veya 201 dönmeli

---

### Senaryo 3: Token Olmadan İstek Atma

1. Aynı sepete ekleme isteğini deneyelim
2. Bu sefer token’ı **kaldır**alım
3. **Send** butonuna basalım
4. Sonuç: 401 dönmeli

---

### Senaryo 4: Stok Yetersizken Ekleme

1. Stoğu az olan bir ürünü yüksek adetle eklemeye çalışalım
2. **Send** butonuna basalım
3. Sonuç: 409 dönmeli

## 4. BA Olarak Postman Kullanırken Dikkat Edilecekler

- Hem mutlu yolu hem hata senaryolarını test etmek
- Status code’u mutlaka kontrol etmek 
- Response’da dönen alanların iş ihtiyacını karşılayıp karşılamadığına bakılması
- Zorunlu alanları eksik göndererek 400 hatasını gözlenmesi
- Token’lı ve token’sız istekleri karşılaştırılması

---

## 5. Pratik Tavsiyeler

- Sık kullandığımız istekleri **Collection** olarak kaydetmek
- Ortam (Environment) kullanarak farklı adresleri (test / canlı) kolay yönetebilmek
- Response’u güzel görmek için “Pretty” ve “JSON” seçili olması
- Geliştiriciye hata bildirirken:  
  “Şu endpoint’e, şu body ile istek attım → 409 döndü” diye net söyleyebilmek

---

## 6. Özet

Postman, BA’nın API’yi elle tutup anlamasını sağlayan en iyi araçtır.

Sadece dokümantasyona bakmadan,
Gerçek istek atıp, gerçek cevapları görmek konuyu netleştirir. 
