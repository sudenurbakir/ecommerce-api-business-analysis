# Sipariş Akışı ve API Eşleştirmesi (İş Analisti Bakış Açısı)

## 1. Sipariş Akışı Nedir?

Sipariş akışı, kullanıcının sepetindeki ürünleri **satın alma** sürecidir.

Tipik adımlar:
1. Kullanıcı sepeti inceler
2. Teslimat adresi seçer / ekler
3. Ödeme yöntemini seçer
4. Siparişi onaylar
5. Sistem stok düşer, ödeme alır, sipariş oluşturur
6. Kullanıcıya sipariş özeti gösterilir

Bu sürecin her adımı bir veya birden fazla API ile konuşur.

---

## 2. Tipik Sipariş Endpoint’leri

| Method | Endpoint                        | Ne İş Yapar?                              |
|--------|---------------------------------|-------------------------------------------|
| POST   | /api/orders                     | Yeni sipariş oluşturur                    |
| GET    | /api/orders                     | Kullanıcının siparişlerini listeler       |
| GET    | /api/orders/{id}                | Tek sipariş detayını getirir              |
| POST   | /api/orders/{id}/cancel         | Siparişi iptal eder                       |
| GET    | /api/orders/{id}/status         | Sipariş durumunu sorgular                 |

---

## 3. Sipariş Oluşturma Sırasında Konuşulan API’ler

Bir sipariş oluşturulurken genelde şu kontroller yapılır:

1. **Kullanıcı giriş yapmış mı?** → Auth / JWT
2. **Sepet dolu mu?** → Cart API
3. **Stok yeterli mi?** → Product API (stok kontrolü)
4. **Adres geçerli mi?** → Address API (varsa)
5. **Ödeme alınabildi mi?** → Payment API
6. **Sipariş kaydı oluşturuldu mu?** → Order API

BA olarak bu adımların sırasını ve hangi API’nin ne zaman devreye girdiğini bilmemiz önemlidir.

---

## 4. BA Olarak Nelere Dikkat Etmeliyiz

### Sipariş Oluşturma (POST /api/orders)
- Sepet otomatik mi siparişe dönüşüyor, yoksa sepet id’si mi gönderiliyor?
- Stok yetersizse ne oluyor? (tüm sipariş mi iptal, yoksa kısmi mi?)
- Ödeme başarısız olursa sipariş kaydı oluşuyor mu?
- Sipariş numarası nasıl üretiliyor?
- Kullanıcıya hangi bilgiler dönüyor? (sipariş no, tahmini teslimat vs.)

### Sipariş Listeleme ve Detay
- Hangi statüler var? (Hazırlanıyor, Kargoda, Teslim Edildi, İptal Edildi…)
- İptal edilebilme kuralları neler? (ne zamana kadar iptal edilebilir?)
- Fatura / irsaliye bilgisi dönüyor mu?

### Hata Senaryoları
- Stok son anda tükenirse ne olacak?
- Ödeme servisi cevap vermezse ne olacak?
- Aynı anda iki cihazdan sipariş verilirse ne olacak? (çift sipariş riski)

---

## 5. Önemli Status Code’lar (Order için)

| Kod | Ne Zaman Döner?                                      |
|-----|------------------------------------------------------|
| 200 | Sipariş listesi / detay başarılı                     |
| 201 | Sipariş başarıyla oluşturuldu                        |
| 400 | Eksik veya hatalı veri                               |
| 401 | Login olunmamış                                      |
| 404 | Sipariş bulunamadı                                   |
| 409 | Stok yetersiz / ödeme çakışması / mükerrer sipariş   |

---

## 6. BA Kontrol Listesi

- [ ] Sipariş oluştururken sepet nasıl bağlanıyor?
- [ ] Stok kontrolü hangi adımda yapılıyor?
- [ ] Ödeme başarısız olursa sipariş ne oluyor?
- [ ] Sipariş statüleri net tanımlanmış mı?
- [ ] İptal kuralları belli mi?
- [ ] 409 (çakışma) senaryoları düşünülmüş mü?
- [ ] Kullanıcıya dönen sipariş özeti yeterli mi?

---

## 7. Özet

Sipariş akışı, e-ticaretin en kritik sürecidir.  
BA olarak burada “sipariş oluşsun” kısmına dikkat etmemeliyiz sadece;

> “Hangi adımda hangi API devreye girecek, stok ve ödeme sorunlarında sistem nasıl davranacak, kullanıcıya ne gösterilecek?”

sorularını netleştirmeliyiz. 
