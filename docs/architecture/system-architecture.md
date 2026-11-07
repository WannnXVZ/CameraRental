# System Architecture

## 1. Ikhtisar Arsitektur
Camera Rental dibangun dengan pendekatan decoupled client-server terpusat. Backend Laravel REST API bertindak sebagai *single source of truth* untuk seluruh kalkulasi bisnis, transisi status, otorisasi, dan orkestrasi data.

```mermaid
flowchart LR
    subgraph Clients["Clients Layer"]
        CW["Customer Web (React SPA)"]
        AD["Admin Dashboard (React SPA)"]
        MA["Mobile App (React Native Expo)"]
    end

    subgraph Gateway["API Layer"]
        API["Laravel 13 REST API (/api/v1)"]
        SANCTUM["Laravel Sanctum (SPA Session & PAT)"]
    end

    subgraph Service["Backend Services"]
        BL["Business Logic & Policies"]
        QUEUE["Queue Workers"]
        CRON["Scheduler (Cron)"]
    end

    subgraph StorageLayer["Data & Assets (Supabase)"]
        DB[("PostgreSQL (btree_gist)")]
        PUB_ST["Public Storage (Katalog)"]
        PRIV_ST["Private Storage (KTP, Bukti Bayar)"]
    end

    CW -->|Session Cookie + CSRF| API
    AD -->|Session Cookie + CSRF (Admin)| API
    MA -->|Bearer Token| API
    API --> SANCTUM
    SANCTUM --> BL
    BL --> DB
    BL --> PRIV_ST
    BL --> PUB_ST
    CRON --> QUEUE
    QUEUE --> DB
```

## 2. Prinsip Pemisahan Sesi (Solusi K-01)
1. **Customer Web:** Berjalan pada origin pelanggan (mis. `app.camerarental.com`). Menggunakan cookie session Laravel bawaan (`camerarental_session`).
2. **Admin Dashboard:** Berjalan pada origin terpisah (mis. `admin.camerarental.com`). Menggunakan domain cookie terisolasi atau nama cookie berbeda (`admin_camerarental_session`) untuk mencegah penimpaan sesi pada browser yang sama.
3. **Android Mobile:** Menggunakan Sanctum Personal Access Token (`Authorization: Bearer <token>`) yang disimpan di `Expo SecureStore`.
