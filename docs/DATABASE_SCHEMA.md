# Desain Database & ERD
## SIA-SAVAR – PT Savar Dinamika Teknologi

**Normalisasi:** 3NF (Third Normal Form)  
**DBMS:** MySQL 8.0  
**Total Tabel:** 9 tabel utama

---

## Daftar Tabel & Struktur Field

### 1. Tabel `accounts` (Chart of Accounts)

| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key, Auto Increment |
| `code` | VARCHAR(3) | Kode akun (unik), misal: 111, 211 |
| `name` | VARCHAR(100) | Nama akun |
| `type` | ENUM | `aset`, `kewajiban`, `ekuitas`, `pendapatan`, `beban` |
| `normal_balance` | ENUM | `debit` atau `kredit` |
| `created_at` | TIMESTAMP | Otomatis |
| `updated_at` | TIMESTAMP | Otomatis |

---

### 2. Tabel `customers` (Pelanggan)

| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `name` | VARCHAR(100) | Nama pelanggan |
| `address` | TEXT | Alamat |
| `phone` | VARCHAR(15) | Nomor telepon |
| `email` | VARCHAR(50) | Email (opsional) |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 3. Tabel `suppliers` (Supplier/Vendor)

| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `name` | VARCHAR(100) | Nama supplier |
| `address` | TEXT | Alamat |
| `phone` | VARCHAR(15) | Nomor telepon |
| `email` | VARCHAR(50) | Email (opsional) |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 4. Tabel `products` (Barang Dagangan)

| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `name` | VARCHAR(100) | Nama produk office |
| `sku` | VARCHAR(50) | Kode unik produk |
| `purchase_price` | DECIMAL(15,2) | Harga beli |
| `selling_price` | DECIMAL(15,2) | Harga jual |
| `stock` | INT | Stok tersedia |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 5. Tabel `employees` (Karyawan – untuk pembiayaan)

| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `name` | VARCHAR(100) | Nama karyawan |
| `nik` | VARCHAR(20) | NIK/NIP |
| `position` | VARCHAR(50) | Jabatan |
| `phone` | VARCHAR(15) | Telepon |
| `address` | TEXT | Alamat |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 6. Tabel `transactions` (Header Transaksi)

| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `transaction_date` | DATE | Tanggal transaksi |
| `type` | ENUM | `sale`, `purchase`, `cash_in`, `cash_out`, `journal`, `loan` |
| `reference` | VARCHAR(50) | No. Invoice / Bukti Kas |
| `description` | TEXT | Keterangan transaksi |
| `total_amount` | DECIMAL(15,2) | Total nilai transaksi |
| `customer_id` | BIGINT UNSIGNED | FK ke `customers` (nullable) |
| `supplier_id` | BIGINT UNSIGNED | FK ke `suppliers` (nullable) |
| `employee_id` | BIGINT UNSIGNED | FK ke `employees` (nullable) |
| `created_by` | BIGINT UNSIGNED | FK ke `users` (created_by) |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 7. Tabel `transaction_details` (Jurnal Detail)

| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `transaction_id` | BIGINT UNSIGNED | FK ke `transactions` |
| `account_id` | BIGINT UNSIGNED | FK ke `accounts` |
| `debit` | DECIMAL(15,2) | Nominal Debit (default 0) |
| `credit` | DECIMAL(15,2) | Nominal Kredit (default 0) |
| `description` | TEXT | Deskripsi per baris jurnal |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 8. Tabel `sale_items` (Detail Penjualan)

| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `transaction_id` | BIGINT UNSIGNED | FK ke `transactions` (type = sale) |
| `product_id` | BIGINT UNSIGNED | FK ke `products` |
| `quantity` | INT | Jumlah barang |
| `unit_price` | DECIMAL(15,2) | Harga jual per unit |
| `subtotal` | DECIMAL(15,2) | `quantity * unit_price` |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

### 9. Tabel `purchase_items` (Detail Pembelian)

| Field | Tipe Data | Keterangan |
|-------|-----------|------------|
| `id` | BIGINT UNSIGNED | Primary Key |
| `transaction_id` | BIGINT UNSIGNED | FK ke `transactions` (type = purchase) |
| `product_id` | BIGINT UNSIGNED | FK ke `products` |
| `quantity` | INT | Jumlah barang |
| `unit_price` | DECIMAL(15,2) | Harga beli per unit |
| `subtotal` | DECIMAL(15,2) | `quantity * unit_price` |
| `created_at` | TIMESTAMP | |
| `updated_at` | TIMESTAMP | |

---

## Relasi Antar Tabel (ERD)

Berikut adalah hubungan antar tabel (kardinalitas):

| Relasi | Kardinalitas | Keterangan |
|--------|--------------|------------|
| `transactions` → `transaction_details` | **1 to M** | Satu transaksi punya banyak jurnal detail |
| `transactions` → `sale_items` | **1 to M** | Satu transaksi penjualan punya banyak item |
| `transactions` → `purchase_items` | **1 to M** | Satu transaksi pembelian punya banyak item |
| `customers` → `transactions` | **1 to M** | Satu pelanggan punya banyak transaksi |
| `suppliers` → `transactions` | **1 to M** | Satu supplier punya banyak transaksi |
| `employees` → `transactions` | **1 to M** | Satu karyawan punya banyak transaksi pinjaman |
| `products` → `sale_items` | **1 to M** | Satu produk muncul di banyak item penjualan |
| `products` → `purchase_items` | **1 to M** | Satu produk muncul di banyak item pembelian |
| `accounts` → `transaction_details` | **1 to M** | Satu akun muncul di banyak detail jurnal |

---

## Catatan Teknis untuk Migrasi Laravel

Gunakan foreign key `constrained()` pada migration, contoh:

```php
Schema::create('transaction_details', function (Blueprint $table) {
    $table->id();
    $table->foreignId('transaction_id')->constrained()->onDelete('cascade');
    $table->foreignId('account_id')->constrained()->onDelete('restrict');
    $table->decimal('debit', 15, 2)->default(0);
    $table->decimal('credit', 15, 2)->default(0);
    $table->text('description')->nullable();
    $table->timestamps();
});