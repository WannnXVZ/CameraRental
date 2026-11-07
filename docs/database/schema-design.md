# Database Schema Design

## 1. Konvensi Database
* **Primary Key:** `uuid` (UUIDv7) untuk menjaga privasi ID serta performa indexing yang stabil.
* **Tipe Uang:** `numeric(14,2)` untuk menghindari galat pembulatan floating-point mata uang Rupiah.
* **Waktu & Tanggal:** `timestamptz` (UTC) untuk cap waktu sistem, `date` untuk rentang sewa inklusif harian.
* **Snapshot Pattern:** Nilai transaksi (harga harian, nama kamera, nama/telepon penyewa, alamat pengantaran, rekening pembayaran) disimpan sebagai snapshot saat transaksi dibuat.

## 2. Tabel Inti (31 Tabel)
1. **Identitas & Akses:** `users`, `addresses`, `personal_access_tokens`, `sessions`, `device_tokens`.
2. **Katalog & Unit:** `categories`, `cameras`, `camera_images`, `camera_specifications`, `camera_units`, `unit_maintenances`.
3. **Transaksi & Alokasi:** `bookings`, `booking_items`, `booking_item_units`, `booking_status_histories`.
4. **Verifikasi & Keuangan:** `guarantee_document_types`, `booking_documents`, `payment_methods`, `payments`, `payment_proofs`, `invoices`, `penalties`.
5. **Operasional & Fitur Pendukung:** `fulfillments`, `returns`, `return_items`, `reviews`, `carts`, `cart_items`, `notifications`, `settings`, `audit_logs`, `jobs`, `failed_jobs`.

Semua migrasi dikelola secara eksklusif menggunakan **Laravel Migration** tanpa modifikasi langsung di Supabase Studio.
