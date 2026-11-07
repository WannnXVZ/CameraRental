# Camera Rental Platform

Platform penyewaan kamera digital dan perlengkapan fotografi terpadu berbasis web, mobile Android, dan admin dashboard. Seluruh layanan terhubung ke satu backend REST API dan satu database terpusat.

---

## 📁 Struktur Workspace

Workspace ini mengadopsi struktur modular monorepo:

```
CameraRental/
├── backend/              # REST API (Laravel 13, Sanctum, Eloquent, Queue Worker, Scheduler)
├── frontend-customer/    # Customer Web Application (React, TypeScript, Vite, Tailwind CSS, shadcn/ui)
├── frontend-admin/       # Admin Dashboard SPA (React, TypeScript, Vite, Tailwind CSS, shadcn/ui)
├── mobile-customer/      # Customer Android Application (React Native, Expo, TypeScript)
├── shared/               # Shared TypeScript types, DTO contracts, dan spesifikasi OpenAPI
└── docs/                 # Dokumentasi arsitektur, PRD reference, skema database, dan panduan teknis
```

---

## 🛠️ Stack Teknologi

| Komponen | Teknologi | Peran |
|---|---|---|
| **Backend** | Laravel 13, PHP 8.3+, REST API | Business logic, state machine, dan autentikasi |
| **Database** | Supabase PostgreSQL | Relational database dengan exclusion constraints (`btree_gist`) |
| **Storage** | Supabase Storage (S3-compatible) | Bucket publik (katalog) dan privat (dokumen, bukti transfer, invoice) |
| **Customer Web** | React, TypeScript, Vite, Tailwind CSS, shadcn/ui | Antarmuka web pelanggan |
| **Admin Web** | React, TypeScript, Vite, Tailwind CSS, shadcn/ui | Antarmuka dashboard admin |
| **Mobile App** | React Native, Expo, TypeScript | Antarmuka Android pelanggan |
| **Queue & Cron** | Laravel Queue Worker & Scheduler | Job asinkron (email, push notification, auto-expire booking) |

---

## 📖 Dokumentasi & Rencana Implementasi
* [Implementation Plan](docs/IMPLEMENTATION_PLAN.md)
* [System Architecture](docs/architecture/system-architecture.md)
* [Double Booking Prevention Strategy](docs/architecture/double-booking-prevention.md)
* [Database Schema Design](docs/database/schema-design.md)
