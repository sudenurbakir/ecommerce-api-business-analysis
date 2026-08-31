# Product API Analizi (İş Analisti Bakış Açısı)

## 1. Bu API Ne İşe Yarar?

Product API, e-ticaret sisteminde **ürünlerle** ilgili tüm işlemleri yönetir.

Tipik iş ihtiyaçları:
- Ürünleri listelemek
- Tek bir ürünün detayını görmek
- Yeni ürün eklemek (genelde admin)
- Ürün güncellemek
- Ürün silmek / pasife almak
- Filtreleme, arama, sayfalama

---

## 2. Sık Görülen Endpoint’ler

| Method | Endpoint                     | Ne İş Yapar?                        | Kim Kullanır?      |
|--------|------------------------------|-------------------------------------|--------------------|
| GET    | /api/products                | Ürün listesini getirir              | Herkes (public)    |
| GET    | /api/products/{id}           | Tek ürün detayını getirir           | Herkes (public)    |
| POST   | /api/products                | Yeni ürün ekler                     | Admin / Yetkili    |
| PUT    | /api/products/{id}           | Ürünü tamamen günceller             | Admin / Yetkili    |
| PATCH  | /api/products/{id}           | Ürünün bir kısmını günceller        | Admin / Yetkili    |
| DELETE | /api/products/{id}           | Ürünü siler veya pasife alır        | Admin / Yetkili    |

---

## 3. BA Olarak Nelere Dikkat Etmelisin?

### Listeleme (GET /api/products)
- Sayfalama var mı? (`page`, `pageSize`)
- Filtreleme var mı? (kategori, fiyat aralığı, marka, stok durumu)
- Arama var mı? (`search` veya `q`)
- Sıralama var mı? (`sortBy`, `sortDirection`)
- Dönen alanlar iş ihtiyacını karşılıyor mu? (isim, fiyat, stok, görsel, kategori…)

### Detay (GET /api/products/{id})
- Hangi alanlar dönüyor?
- Stok bilgisi anlık mı?
- Varyant / seçenek bilgisi var mı? (renk, beden vs.)
- 404 durumu net mi?

### Ekleme / Güncelleme (POST – PUT – PATCH)
- Zorunlu alanlar neler?
- Fiyat ve stok validasyonları nasıl?
- Kategori zorunlu mu?
- Aynı isimde ürün eklenebilir mi? (409 riski)

### Silme (DELETE)
- Soft delete mi (pasife alma), hard delete mi?
- Siparişi olan ürün silinebilir mi?

---

## 4. Önemli Status Code’lar (Product için)

| Kod | Ne Zaman Dönar?                              |
|-----|----------------------------------------------|
| 200 | Listeleme veya detay başarılı                |
| 201 | Yeni ürün başarıyla eklendi                  |
| 400 | Eksik / hatalı veri gönderildi               |
| 401 | Login olunmamış (özellikle yazma işlemlerinde) |
| 403 | Yetki yok (admin olmayan kullanıcı)          |
| 404 | Ürün bulunamadı                              |
| 409 | Çakışma (örneğin aynı barkod / sku)          |

---

## 5. BA Kontrol Listesi

Bir Product API’sini incelerken şu soruları sorabiliriz:

- [ ] Listeleme endpoint’inde sayfalama ve filtreleme var mı?
- [ ] Detay endpoint’inde ihtiyaç duyulan tüm alanlar dönüyor mu?
- [ ] Yazma işlemleri (POST/PUT/PATCH) authentication istiyor mu?
- [ ] Zorunlu alanlar net mi?
- [ ] Stok ve fiyat validasyonları düşünülmüş mü?
- [ ] 404 ve 409 senaryoları tanımlı mı?
- [ ] Soft delete mi hard delete mi kararlaştırılmış mı?

---

## 6. Özet

Product API, e-ticaretin kalbidir.  
BA olarak burada işimiz sadece “ürün listelensin” demek değil;  
**nasıl listeleneceğini, hangi alanların döneceğini, hangi hataların yönetileceğini** netleştirmektir.
