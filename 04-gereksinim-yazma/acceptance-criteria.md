# Acceptance Criteria Örnekleri (E-Ticaret + API Odaklı)

## 1. Acceptance Criteria Nedir?

Acceptance Criteria (Kabul Kriterleri), bir User Story’nin **ne zaman tamamlanmış sayılacağını** netleştiren maddelerdir.

Kısaca:
- User Story → Ne isteniyor?
- Acceptance Criteria → Nasıl anlaşılacak ki doğru yapılmış?

İyi yazılmış Acceptance Criteria:
- Test edilebilir olur
- Geliştiriciye net yol gösterir
- BA ile Developer arasında “ben öyle dememiştim” tartışmasını azaltır

---

## 2. Önerilen Yazım Formatı 

En çok kullanılan format: **Given / When / Then**

- **Given** → Başlangıç durumu
- **When** → Kullanıcının yaptığı aksiyon
- **Then** → Beklenen sonuç

---

## 3. Örnekler

### US-04: Sepete Ürün Ekleme

**Acceptance Criteria:**

1. Given kullanıcı giriş yapmış durumda  
   When geçerli bir ürünü sepete ekler  
   Then ürün sepete eklenir ve sepet tutarı güncellenir

2. Given ürünün stoku 0  
   When kullanıcı bu ürünü sepete eklemeye çalışır  
   Then sistem 409 döner ve “Stok yetersiz” mesajı gösterilir

3. Given kullanıcı giriş yapmamış  
   When sepete ürün eklemeye çalışır  
   Then sistem 401 döner ve login sayfasına yönlendirilir

4. Given sepette aynı üründen 1 adet varken  
   When kullanıcı aynı ürünü tekrar ekler  
   Then ürün adedi 1 artar (yeni satır oluşmaz)

---

### US-09: Sipariş Oluşturma

**Acceptance Criteria:**

1. Given kullanıcının sepetinde en az 1 ürün var ve stoklar yeterli  
   When kullanıcı siparişi onaylar  
   Then sipariş oluşturulur, stok düşer, sepet temizlenir ve sipariş numarası döner

2. Given sepet boşken  
   When kullanıcı sipariş oluşturmaya çalışır  
   Then sistem 400 döner ve “Sepetiniz boş” mesajı verilir

3. Given stok son anda yetersiz kalırsa  
   When sipariş oluşturulmaya çalışılır  
   Then sistem 409 döner ve sipariş oluşturulmaz

4. Given kullanıcı giriş yapmamış  
   When sipariş oluşturmaya çalışır  
   Then sistem 401 döner

---

### US-07: Kullanıcı Girişi

**Acceptance Criteria:**

1. Given geçerli email ve şifre girildiğinde  
   When kullanıcı login olur  
   Then sistem 200 döner ve access token verir

2. Given hatalı şifre girildiğinde  
   When kullanıcı login olmaya çalışır  
   Then sistem 401 döner ve “Email veya şifre hatalı” mesajı gösterilir

3. Given 5 kez üst üste hatalı giriş yapıldığında  
   When tekrar denendiğinde  
   Then hesap geçici olarak kilitlenir (403)

---

### US-01: Ürün Listeleme

**Acceptance Criteria:**

1. Given ürünler sistemde mevcutken  
   When kullanıcı ürün listesini ister  
   Then sistem 200 döner ve sayfalanmış ürün listesini getirir

2. Given kategori filtresi uygulandığında  
   When istek atılır  
   Then sadece o kategoriye ait ürünler döner

3. Given sayfa ve sayfa boyutu parametreleri gönderildiğinde  
   When istek atılır  
   Then ilgili sayfadaki ürünler döner

---

## 4. İyi Acceptance Criteria Yazma Detayları

- Hem mutlu yolu (happy path) hem hata senaryolarının yazılması
- Status code’ları mümkün olduğunca belirtmemiz (200, 401, 409…)
- İş kurallarını net koyulması (stok yetersizse ne olacak gibi)
- Teknik implementasyon detayına girilmemesi (hangi tablo, hangi class vs.)
- Test edilebilir maddeler yazılması

---

## 5. Özet

Acceptance Criteria = User Story’nin “tamamlandı” sayılması için gereken net şartlar.

BA olarak projenin en net çıktılarından biri budur.  
Doğru yazıldığında hem geliştirme hem test süreci çok daha sağlıklı ilerler.
