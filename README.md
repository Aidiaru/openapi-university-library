# Üniversite Kütüphane Sistemi API

Bu proje, üniversite kütüphanesi için tasarlanmış RESTful API'nin OpenAPI 3.0 spesifikasyonunu içermektedir.

## 📋 Proje Hakkında

Bu API, üniversite öğrencilerinin kütüphane sistemini kullanarak kitap ödünç alma işlemlerini yönetmelerini sağlar. Sistem, kitapların, öğrencilerin ve ödünç alma kayıtlarının yönetimini kapsar.

## 🚀 Özellikler

- **Kitap Yönetimi**: Kitap ekleme, güncelleme, silme ve listeleme
- **Öğrenci Yönetimi**: Öğrenci kaydı oluşturma, güncelleme ve yönetim
- **Ödünç Alma Sistemi**: Kitap ödünç alma ve iade işlemleri
- **Sayfalama**: Büyük veri setleri için sayfalama desteği
- **Doğrulama**: Veri formatı doğrulamaları (ISBN, email, UUID)
- **Hata Yönetimi**: Detaylı hata mesajları ve durum kodları

## 📁 Dosya Yapısı

```
/
├── openapi.yaml        # OpenAPI 3.0 API tanımı
├── README.md          # Bu dosya
└── DELIVERY.md        # Ödev teslim raporu
```

## 🛠️ API Endpoints

### Kitaplar (Books)
- `GET /books` - Tüm kitapları listele (sayfalama destekli)
- `GET /books/{id}` - Belirli bir kitabın detaylarını getir
- `POST /books` - Yeni kitap ekle
- `PUT /books/{id}` - Kitap bilgilerini güncelle
- `DELETE /books/{id}` - Kitap sil

### Öğrenciler (Students)
- `GET /students` - Tüm öğrencileri listele
- `GET /students/{id}` - Belirli bir öğrencinin detaylarını getir
- `POST /students` - Yeni öğrenci ekle
- `PUT /students/{id}` - Öğrenci bilgilerini güncelle
- `DELETE /students/{id}` - Öğrenci sil

### Ödünç Alma (Loans)
- `GET /loans` - Tüm ödünç alma kayıtlarını listele
- `GET /loans/{id}` - Belirli bir ödünç alma kaydının detaylarını getir
- `POST /loans` - Yeni ödünç alma kaydı oluştur
- `PATCH /loans/{id}/return` - Kitap iade et

## 📊 Veri Modelleri

### Book (Kitap)
```yaml
- id: UUID
- title: string
- author: string
- isbn: string (ISBN-13 format)
- publisher: string
- pageCount: integer
- stock: integer
```

### Student (Öğrenci)
```yaml
- id: UUID
- name: string
- studentNumber: string
- email: string (email format)
- isActive: boolean
```

### Loan (Ödünç Alma)
```yaml
- id: UUID
- studentId: UUID
- bookId: UUID
- loanDate: date
- returnDate: date (nullable)
- status: enum [ongoing, returned, late]
```

## 🔧 Kullanım

### Swagger Editor ile Test

1. [Swagger Editor](https://editor.swagger.io) sayfasını açın
2. `openapi.yaml` dosyasının içeriğini kopyalayın
3. Editöre yapıştırın
4. Sağ tarafta API dokümantasyonunu inceleyin

### Örnek İstekler

**Kitap Ekleme:**
```bash
POST /books
Content-Type: application/json

{
  "title": "Suç ve Ceza",
  "author": "Fyodor Dostoyevski",
  "isbn": "978-3-16-148410-0",
  "publisher": "İş Bankası Kültür Yayınları",
  "pageCount": 687,
  "stock": 5
}
```

**Ödünç Alma:**
```bash
POST /loans
Content-Type: application/json

{
  "studentId": "550e8400-e29b-41d4-a716-446655440001",
  "bookId": "550e8400-e29b-41d4-a716-446655440002",
  "loanDate": "2024-01-15"
}
```

## 🔐 Güvenlik

API iki farklı kimlik doğrulama yöntemi destekler:
- **Bearer Token (JWT)**: Authorization header ile JWT token gönderimi
- **API Key**: X-API-Key header ile API anahtarı gönderimi

## 📝 Notlar

- Tüm ID'ler UUID v4 formatındadır
- ISBN numaraları ISBN-13 standardına uygun olmalıdır
- Tarihler ISO 8601 formatında (YYYY-MM-DD) gönderilmelidir
- Sayfalama parametreleri: `page` (0'dan başlar) ve `size` (varsayılan: 20)

## 🎓 Akademik Kullanım

Bu proje, Açık Kaynak Kodlu Yazılımlar dersi kapsamında OpenAPI tasarımı öğrenmek amacıyla geliştirilmiştir.

## 📄 Lisans

Bu proje eğitim amaçlı olup, MIT lisansı altında sunulmaktadır.

## 👤 İletişim

Sorularınız için ders hocanızla iletişime geçebilirsiniz.

---

**Ders:** Açık Kaynak Kodlu Yazılımlar  
**Konu:** OpenAPI Tasarımı  
**Yıl:** 2024
