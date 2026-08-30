# Swagger / OpenAPI Nasıl Okunur? (İş Analisti Rehberi)

## 1. Swagger Nedir?

Swagger (şu anki adıyla **OpenAPI**), bir API’nin **canlı dokümantasyonudur**.

ASP.NET Core projelerinde genellikle otomatik olarak üretilir.

BA olarak Swagger’ı şu amaçlarla kullanılır;

- Hangi endpoint’ler var?
- Hangi method kullanılıyor?
- Hangi veriler isteniyor / dönüyor?
- Zorunlu alanlar neler?
- Hata durumları neler olabilir?

Kısaca: **API sözleşmesini okuduğumuz yerdir.**

---

## 2. Swagger Ekranında Neler Görüriz?

Swagger açıldığında genellikle şu bölümler olur:

### 1. Endpoint Listesi
Endpoint’ler gruplar halinde listelenir.

Örnek gruplar:
- Products
- Carts
- Orders
- Users
- Auth

Her grubun altında ilgili endpoint’ler yer alır.

### 2. HTTP Method + Path
Her satırda şunu görürsün:

| Method | Path                     | Açıklama                  |
|--------|--------------------------|---------------------------|
| GET    | /api/products            | Tüm ürünleri getir        |
| GET    | /api/products/{id}       | Tek ürün getir            |
| POST   | /api/products            | Yeni ürün ekle            |
| PUT    | /api/products/{id}       | Ürünü güncelle            |
| DELETE | /api/products/{id}       | Ürünü sil                 |

### 3. Parameters (Parametreler)
Endpoint’e gönderilmesi gereken bilgiler.

İki türü vardır:

- **Path Parameter** → URL içinde yer alır (`{id}` gibi)
- **Query Parameter** → URL’in sonuna eklenir (`page`, `pageSize` gibi)
- **Header** → Genellikle Authorization için kullanılır
- **Body** → POST, PUT, PATCH’te gönderilen JSON veri

### 4. Request Body
POST / PUT / PATCH endpoint’lerinde gönderilecek JSON yapısı burada gösterilir.

Örnek:
```json
{
  "name": "string",
  "price": 0,
  "stock": 0,
  "categoryId": 0
}

Burada dikkat etmemiz gerekenler:

Hangi alanlar zorunlu? (required)
Alanların tipi nedir? (string, number, boolean, object, array)
Varsayılan değer var mı?
