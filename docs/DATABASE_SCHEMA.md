# Desain Database & ERD
## SIA-SAVAR – PT Savar Dinamika Teknologi

**Normalisasi:** 3NF (Third Normal Form)  
**DBMS:** MySQL 8.0  
**Total Tabel:** 10 tabel utama

---

## 🏢 Alur Bisnis & Departemen

Perusahaan bergerak di bidang **jasa teknologi informasi (IT)** berbasis proyek, seperti:
- Pembuatan website company profile / e-commerce / custom web app
- Pengembangan aplikasi mobile (Android/iOS)
- Jasa UI/UX Design
- IT Consulting & Maintenance

**Alur Pengerjaan Proyek:**

| Tahap | Aktivitas | Departemen |
|-------|-----------|------------|
| 1 | Konsumen konsultasi & request proyek | Sales & Marketing |
| 2 | Pembuatan Quotation / Proposal & syarat pembayaran | Sales & Marketing |
| 3 | Konfirmasi pembayaran dari konsumen | Finance / Keuangan |
| 4 | Diskusi teknis & pembuatan spesifikasi / SRS (Software Requirement Specification) | Analis Sistem / Project Manager |
| 5 | Penyerahan SRS ke tim pengembang | Project Manager → Divisi Pengembangan |
| 6 | Pengerjaan proyek (sprint/iterasi) & laporan progres mingguan (misal: 30% → 60% → 100%) | Divisi Pengembangan & Teknologi |
| 7 | Serah terima produk jadi (delivery) & maintenance (opsional) | Sales & Divisi Pengembangan |

---

## 📋 Daftar Tabel & Struktur Field

### 1. Tabel `accounts` (Chart of Accounts)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `code` | VARCHAR(3) | Kode akun (unik), misal: 111, 211 |
| `name` | VARCHAR(100) | Nama akun |
| `type` | ENUM | `aset`, `kewajiban`, `ekuitas`, `pendapatan`, `beban` |
| `normal_balance` | ENUM | `debit` atau `kredit` |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 2. Tabel `customers` (Pelanggan)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `name` | VARCHAR(100) | Nama perusahaan / klien |
| `address` | TEXT | Alamat kantor |
| `phone` | VARCHAR(15) | Telepon |
| `email` | VARCHAR(50) | Email |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 3. Tabel `services` (Katalog Jasa IT)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `name` | VARCHAR(100) | Nama jasa (misal: Web Development, Mobile App, UI/UX Design, IT Maintenance) |
| `sku` | VARCHAR(50) | Kode unik (untuk referensi internal) |
| `base_price` | DECIMAL(15,2) | Harga dasar (sebagai acuan, bisa dinegosiasi per proyek) |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 4. Tabel `sales_orders` (Pesanan Proyek)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `order_number` | VARCHAR(20) | Nomor pesanan/proyek (unik, misal: PROJ-2026-001) |
| `customer_id` | BIGINT UNSIGNED | FK ke `customers` |
| `order_date` | DATE | Tanggal proyek masuk |
| `status` | ENUM | `request`, `quoted`, `design`, `development`, `completed`, `cancelled` |
| `total_amount` | DECIMAL(15,2) | Total nilai proyek |
| `notes` | TEXT | Catatan khusus dari klien |
| `created_by` | BIGINT UNSIGNED | FK ke `users` (Sales yang menerima) |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 5. Tabel `sales_order_items` (Detail Jasa dalam Proyek)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `sales_order_id` | BIGINT UNSIGNED | FK ke `sales_orders` |
| `service_id` | BIGINT UNSIGNED | FK ke `services` (bisa null jika jasa benar-benar custom) |
| `description` | TEXT | Deskripsi spesifik pekerjaan (misal: "Website e-commerce dengan payment gateway") |
| `quantity` | INT | Jumlah unit (biasanya 1 untuk jasa, bisa >1 untuk maintenance bulanan) |
| `unit_price` | DECIMAL(15,2) | Harga per unit (kesepakatan) |
| `subtotal` | DECIMAL(15,2) | `quantity * unit_price` |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 6. Tabel `quotations` (Penawaran Harga & Syarat Pembayaran)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `sales_order_id` | BIGINT UNSIGNED | FK ke `sales_orders` |
| `quotation_number` | VARCHAR(20) | No. Penawaran (unik) |
| `payment_terms` | TEXT | Syarat pembayaran (misal: DP 40%, 30% di tengah, 30% setelah delivery) |
| `valid_until` | DATE | Batas berlaku penawaran |
| `approved_by` | BIGINT UNSIGNED | FK ke `users` (Sales yang membuat) |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 7. Tabel `payments` (Konfirmasi Pembayaran)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `sales_order_id` | BIGINT UNSIGNED | FK ke `sales_orders` |
| `payment_date` | DATE | Tanggal pembayaran |
| `amount` | DECIMAL(15,2) | Jumlah dibayar |
| `payment_method` | ENUM | `cash`, `transfer`, `credit_card` |
| `reference_number` | VARCHAR(50) | No. Bukti transfer / referensi |
| `status` | ENUM | `pending`, `confirmed`, `rejected` |
| `confirmed_by` | BIGINT UNSIGNED | FK ke `users` (Finance yang konfirmasi) |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 8. Tabel `design_specifications` (Spesifikasi Teknis / SRS)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `sales_order_id` | BIGINT UNSIGNED | FK ke `sales_orders` |
| `spec_details` | JSON / TEXT | Spesifikasi teknis (flowchart, database design, fitur, UI reference, dll.) |
| `file_attachment` | VARCHAR(255) | Path file SRS / desain sistem (opsional) |
| `submitted_by` | BIGINT UNSIGNED | FK ke `users` (Analis Sistem / Project Manager) |
| `submitted_at` | DATETIME | Waktu penyerahan spesifikasi ke tim developer |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 9. Tabel `work_orders` (Perintah Kerja / Sprint Assignment)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `sales_order_id` | BIGINT UNSIGNED | FK ke `sales_orders` |
| `work_order_number` | VARCHAR(20) | No. Perintah Kerja (unik) |
| `assigned_to_team` | VARCHAR(50) | Nama tim dev / teknologi yang mengerjakan |
| `start_date` | DATE | Tanggal mulai pengerjaan |
| `deadline` | DATE | Batas waktu delivery |
| `status` | ENUM | `pending`, `in_progress`, `completed` |
| `created_by` | BIGINT UNSIGNED | FK ke `users` (Project Manager) |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 10. Tabel `work_order_progress` (Laporan Progres Mingguan)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `work_order_id` | BIGINT UNSIGNED | FK ke `work_orders` |
| `week_number` | INT | Minggu ke- (1, 2, 3, dst.) |
| `progress_percentage` | TINYINT | Persentase penyelesaian (misal: 30, 60, 100) |
| `progress_date` | DATE | Tanggal laporan progres |
| `notes` | TEXT | Catatan progres (fitur selesai, kendala teknis, revisi klien) |
| `reported_by` | BIGINT UNSIGNED | FK ke `users` (Tim Developer yang melapor) |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

## 🔗 Relasi Antar Tabel (ERD)

| Relasi | Kardinalitas | Keterangan |
|--------|--------------|------------|
| `customers` → `sales_orders` | **1 to M** | Satu klien bisa punya banyak proyek |
| `sales_orders` → `sales_order_items` | **1 to M** | Satu proyek bisa terdiri dari beberapa jasa layanan |
| `sales_orders` → `quotations` | **1 to 1** | Satu proyek punya satu penawaran |
| `sales_orders` → `payments` | **1 to M** | Satu proyek bisa punya banyak termin pembayaran |
| `sales_orders` → `design_specifications` | **1 to 1** | Satu proyek punya satu spesifikasi teknis |
| `sales_orders` → `work_orders` | **1 to 1** | Satu proyek punya satu perintah kerja |
| `work_orders` → `work_order_progress` | **1 to M** | Satu proyek punya banyak laporan progres mingguan |
| `services` → `sales_order_items` | **1 to M** | Satu layanan jasa bisa dipesan di banyak proyek |

---