Kaldığımız yerden devam edelim

### 5. Responses

API’nin dönebileceği cevaplar.

| Status Code | Açıklama         | Dönüş Tipi     |
|-------------|------------------|----------------|
| 200         | Başarılı         | Product        |
| 201         | Oluşturuldu      | Product        |
| 400         | Hatalı istek     | ErrorResponse  |
| 401         | Yetkisiz         | -              |
| 404         | Bulunamadı       | -              |
| 500         | Sunucu hatası    | -              |

---

## 3. BA Olarak Swagger’da Nelere Bakmalıyız

Her endpoint için şu soruları sorabiliriz;

1. **Bu endpoint ne iş yapıyor?**  
   (Açıklama kısmını oku)

2. **Hangi method kullanılmış?**  
   (GET mi, POST mu? İş kuralını etkiler)

3. **Zorunlu alanlar neler?**  
   (Request Body ve Parameters’taki required alanlar)

4. **Hangi veriyi dönüyor?**  
   (Response şemasına bakabiliriz)

5. **Hangi hataları fırlatabilir?**  
   (400, 401, 403, 404, 409, 500 vs.)

6. **Authentication istiyor mu?**  
   (Padlock ikonu varsa genellikle JWT ister)

---

## 4. Pratik Okuma Sırası 

Bir endpoint’i incelerken şu sırayı takip edebiliriz; 

1. Method + Path’in okunması
2. Summary / Description’ı okunması
3. Parameters’a bakılması
4. Request Body’yi incelenmesi
5. Responses’a bakalım (özellikle 200/201 ve hata kodları)
6. Schema’ya tıklayıp detaylı alanları görebiliriz

### 1. Ürün Listeleme
* **Endpoint:** `GET /api/products`
* **Query Parametreleri:** `page`, `pageSize`, `categoryId`, `search`
* **Başarılı Yanıt:** `200 OK` → Ürün listesi
* **Yetkilendirme:** Public (Authentication gerektirmez)

### 2. Sepete Ürün Ekleme
* **Endpoint:** `POST /api/carts/items`
* **Request Body:** `productId`, `quantity`
* **Başarılı Yanıt:** `200 OK` veya `201 Created`
* **Yetkilendirme:** Oturum açmış kullanıcı (`401 Unauthorized` riski)

### 3. Sipariş Oluşturma
* **Endpoint:** `POST /api/orders`
* **Request Body:** Teslimat adresi, ödeme bilgileri vb.
* **Başarılı Yanıt:** `201 Created`
* **Hata Senaryoları:** Yetersiz stok durumunda `400 Bad Request` veya `409 Conflict`
* **Yetkilendirme:** Oturum açmış kullanıcı

---

## 6. Sık Yapılan BA Hataları

- Sadece 200 cevabına bakıp diğer status code’ları görmezden gelmek
- Zorunlu alanları (required) kontrol etmemek
- Path parameter ile Query parameter farkını karıştırmak
- Authentication ihtiyacını atlamak
- Response’daki alanların gerçekten iş ihtiyacını karşılayıp karşılamadığını kontrol etmemek

---

## 7. Özet

Swagger = API’nin canlı sözleşmesi

BA olarak görevin:
- Endpoint’leri anlamak
- İstenen ve dönen veriyi netleştirmek
- Hata senaryolarını görmek
- Bunu User Story ve Acceptance Criteria’ya dökmek




