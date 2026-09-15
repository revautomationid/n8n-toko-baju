# n8n-toko-baju

## Prasyarat (Prerequisites)

Sebelum mengimpor workflow ini, pastikan Anda memiliki kredensial / akun untuk layanan berikut:
1. **WhatsApp Cloud API** (via Meta Developer) untuk *trigger* dan pengiriman pesan.
2. **OpenAI API** (model `gpt-4o` atau model vision yang setara) untuk *AI Agent* dan analisis gambar.
3. **PostgreSQL** untuk *database* pesanan.

## Cara Instalasi

1. Buka workspace n8n Anda.
2. Buat Workflow baru, klik tombol **Import from File** atau *copy-paste* isi file `.json` ke dalam canvas n8n.
3. Setelah terimpor, Anda akan melihat beberapa node memiliki peringatan kredensial (karena kredensial asli telah diamankan). 
4. Hubungkan/buat kredensial baru untuk node berikut:
   - `WhatsApp Trigger`, `Download Media`, `Fetch Image`, `Send Image Reply`, `Send Text Reply`
   - `OpenAI Chat Model`, `Analyze image`
   - `Add to Cart` (PostgreSQL)

## 🗄️ Persiapan Database (PostgreSQL)

Buat tabel `orders` di database PostgreSQL Anda dengan skema berikut agar sinkron dengan node **Add to Cart**:

```sql
CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    customer_phone VARCHAR(50) NOT NULL,
    items TEXT NOT NULL,
    total NUMERIC NOT NULL,
    status VARCHAR(50) DEFAULT 'WAITING_CONFIRMATION',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
