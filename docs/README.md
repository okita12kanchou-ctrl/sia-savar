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

## 📊 Standar Akuntansi & Chart of Accounts (CoA)

**Standar Akuntansi:** SAK ETAP (Entitas Tanpa Akuntabilitas Publik)  
**Format Kode Akun:** 3 digit numerik (mengacu pada standar perusahaan jasa & dagang)

### 1. ASET (HARTA)

#### Aset Lancar
| Kode | Nama Akun | Normal Saldo |
|------|-----------|--------------|
| 111  | Kas | Debit |
| 112  | Piutang Usaha | Debit |
| 113  | Piutang Karyawan | Debit |
| 114  | Perlengkapan Kantor | Debit |
| 115  | Persediaan Barang Dagang | Debit |
| 116  | Sewa Dibayar di Muka | Debit |
| 117  | Iklan Dibayar di Muka | Debit |

#### Aset Tetap
| Kode | Nama Akun | Normal Saldo |
|------|-----------|--------------|
| 121  | Tanah | Debit |
| 122  | Peralatan Kantor | Debit |
| 123  | Akumulasi Penyusutan Peralatan | Kredit |
| 124  | Gedung/Kantor | Debit |
| 125  | Akumulasi Penyusutan Gedung | Kredit |

#### Aset Tak Berwujud
| Kode | Nama Akun | Normal Saldo |
|------|-----------|--------------|
| 141  | Goodwill | Debit |
| 142  | Hak Paten | Debit |
| 143  | Hak Cipta (Software) | Debit |

---

### 2. KEWAJIBAN (UTANG)

#### Utang Jangka Pendek
| Kode | Nama Akun | Normal Saldo |
|------|-----------|--------------|
| 211  | Utang Usaha | Kredit |
| 212  | Utang Gaji | Kredit |
| 213  | Utang Pajak | Kredit |
| 214  | Utang Bunga | Kredit |
| 215  | Utang Bank | Kredit |

#### Utang Jangka Panjang
| Kode | Nama Akun | Normal Saldo |
|------|-----------|--------------|
| 221  | Utang Obligasi | Kredit |
| 222  | Utang Hipotik | Kredit |

---

### 3. EKUITAS (MODAL)
| Kode | Nama Akun | Normal Saldo |
|------|-----------|--------------|
| 311  | Modal Pemilik | Kredit |
| 312  | Prive Pemilik | Debit |
| 313  | Laba Ditahan | Kredit |

---

### 4. PENDAPATAN
| Kode | Nama Akun | Normal Saldo |
|------|-----------|--------------|
| 411  | Pendapatan Penjualan | Kredit |
| 412  | Pendapatan Jasa (Bunga Pembiayaan) | Kredit |

---

### 5. BEBAN
| Kode | Nama Akun | Normal Saldo |
|------|-----------|--------------|
| 511  | Beban Gaji | Debit |
| 512  | Beban Listrik, Air, Telepon | Debit |
| 513  | Beban Pajak | Debit |
| 514  | Beban Bunga | Debit |
| 515  | Harga Pokok Penjualan (HPP) | Debit |
| 516  | Beban Sewa Gedung | Debit |
| 517  | Beban Asuransi | Debit |
| 518  | Beban Perlengkapan Kantor | Debit |
| 519  | Beban Iklan | Debit |
| 520  | Beban Penyusutan Peralatan | Debit |
| 521  | Beban Penyusutan Gedung | Debit |
| 522  | Beban Administrasi & Umum | Debit |
| 523  | Beban Lain-lain | Debit |

---

## 🗄️ Struktur Database (ERD)

Untuk melihat detail desain database (daftar tabel, field, dan relasi), silakan buka file:  
📄 **[Desain Database & ERD](docs/DATABASE_SCHEMA.md)**

---


## 👥 Kontributor

- **Fakhry Arief Rahman** (11024006) – Pengembang Utama
- **Apriani Puti Purfini, S.Kom., M.T.** – Dosen Pembimbing

---

## 📄 Lisensi

Proyek ini dibuat untuk keperluan akademik **Praktikum Sistem Informasi Akuntansi II**.