# Backend API - Camera Rental

REST API terpusat untuk platform Camera Rental.

## 📌 Spesifikasi
* **Framework:** Laravel 13 (PHP 8.3+)
* **Autentikasi:** Laravel Sanctum (SPA Session Cookie & Bearer Personal Access Token)
* **Database:** Supabase PostgreSQL (`btree_gist` enabled)
* **Storage:** Supabase Storage (S3-compatible)
* **Arsitektur:** Controller tipis, Form Request Validation, Action/Service classes, Eloquent API Resources, Laravel Policies.

## 🚀 Perintah Dasar (Setelah Inisialisasi Fase 1)
```bash
composer install
php artisan migrate
php artisan db:seed
php artisan serve
```
