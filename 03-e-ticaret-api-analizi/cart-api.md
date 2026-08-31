# Cart API Analizi 

## 1. Bu API Ne İşe Yarar?

Cart API, kullanıcının **sepetini** yönetir.

Tipik iş ihtiyaçları:
- Sepete ürün eklemek
- Sepetten ürün silmek
- Ürün adedini değiştirmek
- Sepeti görüntülemek
- Sepeti tamamen temizlemek
- Sepetteki ürünlerin stok kontrolünü yapmak
- Bazen kupon / indirim uygulamak

---

## 2. Sık Görülen Endpoint’ler

| Method | Endpoint                        | Ne İş Yapar?                          | Kim Kullanır?     |
|--------|---------------------------------|---------------------------------------|-------------------|
| GET    | /api/carts                      | Kullanıcının sepetini getirir         | Login kullanıcı   |
| GET    | /api/carts/{id}                 | Belirli bir sepeti getirir            | Login kullanıcı   |
| POST   | /api/carts/items                | Sepete ürün ekler                     | Login kullanıcı   |
| PUT    | /api/carts/items/{itemId}       | Sepetteki ürün adedini günceller      | Login kullanıcı   |
| PATCH  | /api/carts/items/{itemId}       | Sadece adedi günceller                | Login kullanıcı   |
| DELETE | /api/carts/items/{itemId}       | Sepetten ürün çıkarır                 | Login kullanıcı   |
| DELETE | /api/carts                      | Sepeti tamamen temizler               | Login kullanıcı   |

---

## 3. BA Olarak Nelere Dikkat Etmeliyiz?

### Sepete Ürün Ekleme (POST)
- Aynı ürün tekrar eklenirse ne olur? (adet artar mı, yoksa hata mı verir?)
- Stok yetersizse ne döner? (400 mü, 409 mu?)
- Maksimum adet sınırı var mı?
- Login zorunlu mu?

### Adet Güncelleme
- Adet 0 yapılırsa ürün sepetten silinir mi?
- Negatif adet kabul edilir mi?

### Sepeti Getirme (GET)
- Hangi alanlar dönüyor? (ürün adı, fiyat, görsel, stok, toplam tutar)
- Fiyat değişmişse güncel fiyat mı, ekleme anındaki fiyat mı gösteriliyor?
- Stok tükenmiş ürünler nasıl gösteriliyor?

### Genel Kontroller
- Sepet kullanıcıya mı bağlı, yoksa misafir (guest) sepeti de var mı?
- Sepet ne kadar süre saklanıyor? (session süresi)
- Bir kullanıcının birden fazla sepeti olabilir mi?

---

## 4. Önemli Status Code’lar (Cart için)

| Kod | Ne Zaman Döner?                                      |
|-----|------------------------------------------------------|
| 200 | Sepet başarıyla getirildi / güncellendi              |
| 201 | Ürün sepete başarıyla eklendi                        |
| 400 | Hatalı veri (negatif adet, eksik alan vs.)           |
| 401 | Login olunmamış                                      |
| 404 | Sepet veya ürün bulunamadı                           |
| 409 | Stok yetersiz / çakışma durumu                       |

---

## 5. BA Kontrol Listesi

- [ ] Sepete ekleme işlemi login zorunlu mu?
- [ ] Aynı ürün tekrar eklenince ne oluyor?
- [ ] Stok yetersizse hangi status code dönüyor?
- [ ] Adet 0 yapılınca ürün siliniyor mu?
- [ ] Sepet getirildiğinde güncel fiyat mı dönüyor?
- [ ] Misafir (guest) sepeti destekleniyor mu?
- [ ] Sepet süresi (expiration) tanımlanmış mı?

---

## 6. Özet

Cart API, satın alma sürecinin en kritik ara noktasıdır.  
BA olarak burada netleştirmemiz gereken şey:

> “Kullanıcı ürünü sepete eklediğinde sistem ne yapacak, stok yoksa ne diyecek, fiyat değişirse ne gösterecek?”
