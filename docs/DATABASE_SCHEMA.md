# Desain Database & ERD
## SIA-SAVAR – PT Savar Dinamika Teknologi

**Normalisasi:** 3NF (Third Normal Form)  
**DBMS:** MySQL 8.0  
**Total Tabel:** 10 tabel utama

---

## 🏢 Alur Bisnis & Departemen

| Tahap | Aktivitas | Departemen |
|-------|-----------|------------|
| 1 | Konsumen request produk | Sales & Marketing |
| 2 | Pembuatan Quotation & syarat pembayaran | Sales & Marketing |
| 3 | Konfirmasi pembayaran | Finance / Keuangan |
| 4 | Diskusi & pembuatan desain spesifikasi | Desain & Engineering |
| 5 | Serah terima kriteria ke produksi | Sales → Produksi |
| 6 | Pengerjaan & laporan progres mingguan | Produksi & Manufaktur |

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
| `name` | VARCHAR(100) | Nama pelanggan |
| `address` | TEXT | Alamat |
| `phone` | VARCHAR(15) | Telepon |
| `email` | VARCHAR(50) | Email |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 3. Tabel `suppliers` (Supplier Bahan Baku)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `name` | VARCHAR(100) | Nama supplier |
| `address` | TEXT | Alamat |
| `phone` | VARCHAR(15) | Telepon |
| `email` | VARCHAR(50) | Email |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 4. Tabel `products` (Master Produk/Jasa)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `name` | VARCHAR(100) | Nama produk/jasa (misal: Custom Office Chair, Interior Design) |
| `sku` | VARCHAR(50) | Kode produk |
| `base_price` | DECIMAL(15,2) | Harga dasar (untuk referensi) |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 5. Tabel `sales_orders` (Pesanan Penjualan)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `order_number` | VARCHAR(20) | Nomor pesanan (unik, misal: SO-2026-001) |
| `customer_id` | BIGINT UNSIGNED | FK ke `customers` |
| `order_date` | DATE | Tanggal pesanan masuk |
| `status` | ENUM | `request`, `quoted`, `design`, `production`, `completed`, `cancelled` |
| `total_amount` | DECIMAL(15,2) | Total nilai pesanan |
| `notes` | TEXT | Catatan khusus |
| `created_by` | BIGINT UNSIGNED | FK ke `users` |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 6. Tabel `sales_order_items` (Detail Pesanan)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `sales_order_id` | BIGINT UNSIGNED | FK ke `sales_orders` |
| `product_id` | BIGINT UNSIGNED | FK ke `products` (nullable, jika produk custom bisa null) |
| `description` | TEXT | Deskripsi barang/jasa yang dipesan (untuk custom) |
| `quantity` | INT | Jumlah |
| `unit_price` | DECIMAL(15,2) | Harga per unit |
| `subtotal` | DECIMAL(15,2) | `quantity * unit_price` |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 7. Tabel `quotations` (Penawaran Harga & Syarat Pembayaran)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `sales_order_id` | BIGINT UNSIGNED | FK ke `sales_orders` |
| `quotation_number` | VARCHAR(20) | No. Penawaran (unik) |
| `payment_terms` | TEXT | Syarat pembayaran (misal: DP 50%, pelunasan sebelum kirim) |
| `valid_until` | DATE | Batas berlaku penawaran |
| `approved_by` | BIGINT UNSIGNED | FK ke `users` (Sales yang membuat) |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 8. Tabel `payments` (Konfirmasi Pembayaran)
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

### 9. Tabel `design_specifications` (Spesifikasi Desain)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `sales_order_id` | BIGINT UNSIGNED | FK ke `sales_orders` |
| `design_details` | JSON / TEXT | Detail desain (ukuran, warna, material, dll) |
| `file_attachment` | VARCHAR(255) | Path file gambar/desain (opsional) |
| `submitted_by` | BIGINT UNSIGNED | FK ke `users` (Divisi Desain) |
| `submitted_at` | DATETIME | Waktu penyerahan desain ke produksi |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 10. Tabel `work_orders` (Perintah Kerja Produksi)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `sales_order_id` | BIGINT UNSIGNED | FK ke `sales_orders` |
| `work_order_number` | VARCHAR(20) | No. Perintah Kerja (unik) |
| `assigned_to_team` | VARCHAR(50) | Nama tim/divisi produksi |
| `start_date` | DATE | Tanggal mulai pengerjaan |
| `deadline` | DATE | Batas waktu selesai |
| `status` | ENUM | `pending`, `in_progress`, `completed` |
| `created_by` | BIGINT UNSIGNED | FK ke `users` |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 11. Tabel `work_order_progress` (Laporan Progres Mingguan)
| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `work_order_id` | BIGINT UNSIGNED | FK ke `work_orders` |
| `week_number` | INT | Minggu ke- (1, 2, 3, ...) |
| `progress_percentage` | TINYINT | Persentase (30, 60, 100) |
| `progress_date` | DATE | Tanggal laporan progres |
| `notes` | TEXT | Catatan progres (misal: kendala, pencapaian) |
| `reported_by` | BIGINT UNSIGNED | FK ke `users` (Tim Produksi) |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

## 🔗 Relasi Antar Tabel (ERD)

| Relasi | Kardinalitas | Keterangan |
|--------|--------------|------------|
| `customers` → `sales_orders` | **1 to M** | Satu pelanggan bisa punya banyak pesanan |
| `sales_orders` → `sales_order_items` | **1 to M** | Satu pesanan punya banyak item |
| `sales_orders` → `quotations` | **1 to 1** | Satu pesanan punya satu penawaran |
| `sales_orders` → `payments` | **1 to M** | Satu pesanan bisa punya banyak pembayaran (DP + pelunasan) |
| `sales_orders` → `design_specifications` | **1 to 1** | Satu pesanan punya satu desain |
| `sales_orders` → `work_orders` | **1 to 1** | Satu pesanan punya satu perintah kerja |
| `work_orders` → `work_order_progress` | **1 to M** | Satu perintah kerja punya banyak laporan progres mingguan |
| `products` → `sales_order_items` | **1 to M** | Satu produk bisa dipesan di banyak item |

---

