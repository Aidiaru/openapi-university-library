# OpenAPI Tasarımı Ödevi Teslim Raporu

## 👤 Öğrenci Bilgileri
- **Ad Soyad**: Orçun Samet Tatar
- **Öğrenci Numarası**: 170422014

---

## 📂 OpenAPI YAML Dosyası

- **openapi.yaml** dosyasını projenizin GitHub reposuna yükleyiniz.
- Swagger Editor ile test ettiğinizden emin olunuz.

### 🔗 GitHub Repo Linki
https://github.com/Aidiaru/openapi-university-library

---

## 📝 API Açıklaması

Aşağıda tasarladığınız API’nin genel yapısını ve önemli noktalarını açıklayınız:
- Hangi varlıklar (entities) yer almaktadır?
- CRUD işlemleri hangi endpoint’lerle sağlanmaktadır?
- `components/schemas`, `parameters`, `responses` gibi bölümleri nasıl kullandınız?
- Sayfalama ve hata durumları nasıl ele alındı?


API'nin Genel Yapısı ve Önemli Noktaları
🔹 Varlıklar (Entities)
API'de 3 ana varlık bulunmaktadır:

books (Kitaplar)

id: UUID formatında benzersiz tanımlayıcı
title: Kitap başlığı
author: Yazar adı
isbn: ISBN-13 formatında kitap numarası
publisher: Yayınevi
pageCount: Sayfa sayısı
stock: Stok adedi


students (Öğrenciler)

id: UUID formatında benzersiz tanımlayıcı
name: Öğrenci adı soyadı
studentNumber: 11 haneli öğrenci numarası
email: Email adresi (email formatında)
isActive: Öğrencinin aktif/pasif durumu


loans (Ödünç Alma Kayıtları)

id: UUID formatında benzersiz tanımlayıcı
studentId: Ödünç alan öğrencinin ID'si
bookId: Ödünç alınan kitabın ID'si
loanDate: Ödünç alma tarihi
returnDate: İade tarihi (nullable)
status: Ödünç durumu (ongoing/returned/late)



🔹 CRUD İşlemleri ve Endpoint'ler
Books (Kitaplar):

GET /books → Tüm kitapları listele (sayfalama destekli)
GET /books/{id} → Belirli bir kitabın detayları
POST /books → Yeni kitap ekleme
PUT /books/{id} → Kitap bilgilerini güncelleme
DELETE /books/{id} → Kitap silme

Students (Öğrenciler):

GET /students → Tüm öğrencileri listele
GET /students/{id} → Belirli bir öğrencinin detayları
POST /students → Yeni öğrenci ekleme
PUT /students/{id} → Öğrenci bilgilerini güncelleme
DELETE /students/{id} → Öğrenci silme

Loans (Ödünç İşlemleri):

GET /loans → Tüm ödünç kayıtlarını listele (durum filtrelemesi mevcut)
GET /loans/{id} → Belirli bir ödünç kaydının detayları
POST /loans → Yeni ödünç alma işlemi
PATCH /loans/{id}/return → Kitap iade işlemi

🔹 Components Kullanımı
1. schemas:

Her varlık için hem response (Book, Student, Loan) hem de request (BookRequest, StudentRequest, LoanRequest) şemaları tanımlandı
LoanStatus enum tipi ayrı bir şema olarak tanımlandı
Error şeması tüm hata yanıtları için ortak yapı sağlıyor
Tüm şemalarda required alanlar, format tanımlamaları ve example değerleri mevcut

2. parameters:

BookId, StudentId, LoanId path parametreleri merkezi olarak tanımlandı
Bu sayede aynı parametre tanımı birden fazla endpoint'te $ref ile kullanıldı
Her parametre için açıklama, format ve örnek değerler eklendi

3. responses:

BadRequest (400), NotFound (404), InternalServerError (500) yanıtları merkezi olarak tanımlandı
Her hata yanıtı detaylı Error şeması kullanıyor
Tekrar kullanılabilirlik için $ref referansları ile endpoint'lerde kullanıldı

🔹 Sayfalama ve Hata Durumları
Sayfalama:

GET /books endpoint'inde query parametreleri ile implementasyon:

page: Sayfa numarası (0'dan başlar, varsayılan: 0)
size: Sayfa başına kayıt sayısı (1-100 arası, varsayılan: 20)


Response'da sayfalama metadata'sı:

content: Mevcut sayfadaki kayıtlar
totalElements: Toplam kayıt sayısı
totalPages: Toplam sayfa sayısı
number: Mevcut sayfa numarası
size: Sayfa başına kayıt sayısı



Hata Durumları:

400 Bad Request: Validasyon hataları için detaylı mesajlar

Hatalı alan adı, gönderilen değer ve beklenen format bilgisi


404 Not Found: Kaynak bulunamadığında

Hangi ID'nin bulunamadığı bilgisi


500 Internal Server Error: Sunucu hataları için

Genel hata mesajı



Her hata yanıtı şu yapıda:
{
  "code": "ERROR_CODE",
  "message": "Açıklayıcı hata mesajı",
  "details": { /* Ek detaylar */ }
}
Bu tasarım, OpenAPI 3.0 standartlarına uygun, bakımı kolay ve genişletilebilir bir API yapısı sunmaktadır.

---

## 🧪 Test Notları (Opsiyonel)

Swagger Editor üzerinden test ettiğiniz örnek istek/yanıtları özetleyebilirsiniz:
- `GET /books` çağrısında ne döner?
- `POST /students` için örnek `requestBody` nedir?
- Hatalı bir istek için dönen `400` örneği var mı?

---

## 📌 Ek Açıklamalar

Varsa proje hakkında ekstra notlarınızı buraya ekleyebilirsiniz.
