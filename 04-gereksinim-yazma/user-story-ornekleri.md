# User Story Örnekleri (E-Ticaret + API Odaklı)

## 1. User Story Nedir? (Kısa Hatırlatma)

User Story, iş ihtiyacını **kullanıcı dilinde** anlatan kısa bir ifadedir.

Klasik format:

**Bir [rol] olarak, [amaç] istiyorum, böylece [fayda] sağlarım.**

Burada yapmamız gereken;
- İhtiyacı net yazmak
- Kabul kriterlerini (Acceptance Criteria) eklemek
- API’nin bu ihtiyacı nasıl karşılayacağını düşünmek

---

## 2. Product API ile İlgili User Story Örnekleri

### US-01: Ürün Listeleme
**Bir müşteri olarak,**  
ürünleri kategoriye ve fiyata göre filtreleyerek listelemek istiyorum,  
**böylece** aradığım ürüne daha hızlı ulaşabileyim.

### US-02: Ürün Detayı Görüntüleme
**Bir müşteri olarak,**  
bir ürünün detay sayfasında stok bilgisini, fiyatını ve görsellerini görmek istiyorum,  
**böylece** satın alma kararı verebileyim.

### US-03: Yeni Ürün Ekleme (Admin)
**Bir admin olarak,**  
sisteme yeni ürün eklemek istiyorum,  
**böylece** katalog güncel kalsın.

---

## 3. Cart API ile İlgili User Story Örnekleri

### US-04: Sepete Ürün Ekleme
**Bir müşteri olarak,**  
beğendiğim ürünü sepete eklemek istiyorum,  
**böylece** daha sonra satın alabileyim.

### US-05: Sepetteki Ürün Adedini Güncelleme
**Bir müşteri olarak,**  
sepetteki ürünün adedini değiştirebilmek istiyorum,  
**böylece** ihtiyacıma göre düzenleme yapabileyim.

### US-06: Sepetten Ürün Silme
**Bir müşteri olarak,**  
sepetimdeki bir ürünü silmek istiyorum,  
**böylece** istemediğim ürünler kalmasın.

---

## 4. Auth / JWT ile İlgili User Story Örnekleri

### US-07: Kullanıcı Girişi
**Bir müşteri olarak,**  
email ve şifremle sisteme giriş yapmak istiyorum,  
**böylece** sepetime ve siparişlerime ulaşabileyim.

### US-08: Üye Olma
**Bir ziyaretçi olarak,**  
sisteme üye olmak istiyorum,  
**böylece** alışveriş yapabileyim ve siparişlerimi takip edebileyim.

---

## 5. Sipariş ile İlgili User Story Örnekleri

### US-09: Sipariş Oluşturma
**Bir müşteri olarak,**  
sepetteki ürünleri siparişe dönüştürmek istiyorum,  
**böylece** satın alma işlemini tamamlayabileyim.

### US-10: Siparişlerimi Görüntüleme
**Bir müşteri olarak,**  
geçmiş siparişlerimi listelemek istiyorum,  
**böylece** ne aldığımı ve durumunu takip edebileyim.

### US-11: Sipariş İptal Etme
**Bir müşteri olarak,**  
henüz kargoya verilmemiş siparişimi iptal etmek istiyorum,  
**böylece** vazgeçtiğim alışverişi geri alabileyim.

---

## 6. İyi User Story Yazarken Dikkat Edilmesi Gereken Noktalar

- Rol net olmalı (müşteri, admin, misafir…)
- Amaç net olmalı (ne yapmak istiyor?)
- Fayda yazılmalı (neden istiyor?)
- Teknik detay yazmamalı (endpoint, JSON vs. Acceptance Criteria adımında yapmalıyız)
- Mümkün olduğunca tek bir ihtiyaca odaklanalım

---

## 7. Özet

User Story = İş ihtiyacının kullanıcı dilindeki hali.

Buradaki dikkat etmemiz gereken adımlar;
1. İhtiyacı doğru yakalayabilmek
2. Temiz bir User Story yazabilmek
3. Sonra bu detayları Acceptance Criteria adımı ile detaylandırmak
