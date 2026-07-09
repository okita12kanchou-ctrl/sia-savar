# SIA-SAVAR
### Sistem Informasi Akuntansi – PT Savar Dinamika Teknologi

> **Proyek Praktikum SIA II** | Semester Genap 2026  
> **Mahasiswa:** Fakhry Arief Rahman (11024006)  
> **Dosen Pembimbing:** Apriani Puti Purfini, S.Kom., M.T.

---

## 📋 Tentang Aplikasi

**SIA-SAVAR** adalah aplikasi sistem informasi akuntansi terintegrasi yang dirancang khusus untuk **PT Savar Dinamika Teknologi**, sebuah perusahaan yang bergerak di dua bidang sekaligus:

- **Teknologi & Jasa** – menyediakan layanan pembiayaan tenaga kerja (pinjaman karyawan).
- **Perdagangan** – menjual produk *office* (perlengkapan kantor).

Aplikasi ini mengotomatiskan seluruh siklus akuntansi, mulai dari pencatatan transaksi hingga penyusunan laporan keuangan.

---

## 🛠️ Teknologi yang Digunakan

| Komponen        | Teknologi                     |
|-----------------|-------------------------------|
| **Backend**     | PHP 8.2+, Laravel 11          |
| **Database**    | MySQL 8.0                     |
| **Frontend**    | Blade Template + Bootstrap 5  |
| **Tools**       | Visual Studio Code, CMD / Git Bash |

---

## ✨ Fitur Utama

1. Manajemen Data Master (Akun, Pelanggan, Supplier, Produk, Karyawan)
2. Input Transaksi Dinamis (Penjualan, Pembelian, Kas, Jurnal Penyesuaian, Pinjaman)
3. Mesin Akuntansi Otomatis (Jurnal, Validasi Balance, Buku Besar)
4. Laporan Keuangan Instan (Neraca Saldo, Laba Rugi, Neraca) + Ekspor PDF

---

## 📚 Dokumentasi Lengkap

Untuk detail teknis, silakan buka file dokumentasi berikut:

- 📄 **[Standar Akuntansi & Chart of Accounts (CoA)](docs/STANDAR_AKUNTANSI_COA.md)**
- 🗄️ **[Desain Database & ERD](docs/DATABASE_SCHEMA.md)**

---

## 🚀 Panduan Instalasi

Ikuti langkah-langkah berikut untuk menjalankan aplikasi di lokal:

### Prasyarat
- PHP 8.2+, Composer, MySQL 8.0

### Langkah Instalasi

```bash
# 1. Clone repositori
git clone https://github.com/username-anda/sia-savar.git
cd sia-savar

# 2. Install dependensi
composer install

# 3. Buat file .env dan generate key
cp .env.example .env
php artisan key:generate

# 4. Atur koneksi database di file .env
# DB_DATABASE=db_sia_savar
# DB_USERNAME=root
# DB_PASSWORD=

# 5. Jalankan migrasi
php artisan migrate

# 6. Jalankan server
php artisan serve