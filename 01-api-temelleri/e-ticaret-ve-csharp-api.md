# E-Ticaret ve C# Perspektifinden API Nedir?

## 1. API Nedir? (İş Analisti Gözüyle)

API (Application Programming Interface), sistemlerin birbiriyle **konuşmasını** sağlayan arayüzdür.

E-ticaret dünyasında API’yi şöyle düşünebiliriz;

> “Frontend (web sitesi / mobil uygulama) ile Backend (iş kuralları, veritabanı) arasında çalışan bir **anlaşma / sözleşme**.”

Bu sözleşme şunları belirler:
- Hangi bilgi istenebilir?
- Bilgi nasıl istenir?
- Cevap nasıl döner?
- Hata durumunda ne olur?

---

## 2. Neden API Bu Kadar Önemli?

E-ticaret sistemlerinde genellikle şu katmanlar vardır:

- **Frontend** → Kullanıcının gördüğü ekranlar (React, Angular, mobil uygulama vs.)
- **Backend** → İş kuralları (C# / ASP.NET Core)
- **Veritabanı** → Ürünler, siparişler, kullanıcılar

API, Frontend ile Backend arasındaki köprüdür.

### Tipik E-ticaret Senaryoları:

| İş İhtiyacı              | API’nin Rolü                          |
|--------------------------|---------------------------------------|
| Ürünleri listele         | Ürün listesini getirir                |
| Sepete ürün ekle         | Sepeti günceller                      |
| Sipariş oluştur          | Siparişi kaydeder ve süreci başlatır  |
| Kullanıcı girişi yap     | Kimlik doğrulama yapar                |
| Ödeme al                 | Ödeme servisiyle konuşur              |
| Stok kontrolü yap        | Anlık stok bilgisini döner            |

---

## 3. REST API Nedir?

E-ticarette en yaygın kullanılan API tarzı **REST**’tir.

REST’in temel prensibi:
- Kaynaklar (Resources) vardır → Ürün, Sepet, Sipariş, Kullanıcı
- Bu kaynaklara **HTTP Method**’ları ile işlem yapılır.

### Temel HTTP Method’ları (BA’nın bilmesi gerekenler)

| Method | Anlamı                  | E-ticaret Örneği                     | Ne zaman kullanılır?      |
|--------|-------------------------|--------------------------------------|---------------------------|
| GET    | Veri getir              | Ürün listesini getir                 | Sadece okuma              |
| POST   | Yeni kayıt oluştur      | Yeni sipariş oluştur                 | Yeni bir şey yaratma      |
| PUT    | Tam güncelleme          | Sepeti tamamen güncelle              | Tüm bilgiyi değiştirme    |
| PATCH  | Kısmi güncelleme        | Sadece ürün adedini güncelle         | Bir alanı değiştirme      |
| DELETE | Sil                     | Sepetten ürün çıkar                  | Silme işlemi              |

---

## 4. Temel Kavramlar

### Endpoint (Uç Nokta)
API’nin adresidir.

Örnek:
- `/api/products` → Ürünler
- `/api/products/15` → 15 numaralı ürün
- `/api/carts` → Sepetler
- `/api/orders` → Siparişler

### Request (İstek)
Frontend’in API’ye gönderdiği mesajdır.

İçinde genellikle şunlar olur:
- URL (endpoint)
- Method (GET, POST vs.)
- Header’lar (örneğin Authorization)
- Body (POST/PUT/PATCH’te gönderilen veri)

### Response (Cevap)
API’nin geri döndürdüğü cevaptır.

Genellikle **JSON** formatındadır.

### Status Code (Durum Kodu)
İşlemin başarılı olup olmadığını söyler.

| Kod  | Anlamı                        | BA Açısından Önemi                     |
|------|-------------------------------|----------------------------------------|
| 200  | Başarılı                      | Her şey yolunda                        |
| 201  | Oluşturuldu                   | Yeni kayıt başarıyla eklendi           |
| 400  | Hatalı istek                  | Frontend yanlış veri göndermiş         |
| 401  | Yetkisiz                      | Kullanıcı giriş yapmamış / token yok   |
| 403  | Yasak                         | Yetkisi yok                            |
| 404  | Bulunamadı                    | İstenen kayıt yok                      |
| 500  | Sunucu hatası                 | Backend’de beklenmeyen hata            |

---

## 5. C# / ASP.NET Core Tarafı 

Ekiplerde backend genellikle **ASP.NET Core Web API** ile yazılır.

Burada bilinmesi gereken noktalar;

- Her endpoint genelde bir **Controller** içinde yer alır.
- Örnek: `ProductsController`, `OrdersController`, `CartsController`
- Dokümantasyon genellikle **Swagger** ile otomatik üretilir.
- Authentication çoğu zaman **JWT Token** ile yapılır.

Önemli olan:
> “Bu endpoint ne iş yapıyor, hangi veriyi alıyor, hangi veriyi dönüyor, hangi hataları fırlatabilir?”

Kodun nasıl yazıldığı değil, **sözleşmenin** ne olduğu önemlidir.

---

## 6. Özet – BA Olarak Akılda Kalması Gerekenler

1. API = Sistemler arası sözleşme
2. E-ticarette en çok REST kullanılır
3. Method’lar işi belirler (GET, POST, PUT, PATCH, DELETE)
4. Endpoint = Adres
5. Status Code = Sonucun durumu
6. C# tarafında genelde ASP.NET Core + Swagger + JWT kullanılır
7. Bizim işimiz: Bu sözleşmeyi anlamak, dokümante etmek ve doğru gereksinim yazmak

---
