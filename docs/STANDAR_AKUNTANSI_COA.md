
---

### 2. File Dokumentasi CoA: `docs/STANDAR_AKUNTANSI_COA.md`

Buat folder `docs` terlebih dahulu, lalu buat file ini di dalamnya.

```markdown
# Standar Akuntansi & Chart of Accounts (CoA)
## SIA-SAVAR – PT Savar Dinamika Teknologi

**Standar Akuntansi:** SAK ETAP (Entitas Tanpa Akuntabilitas Publik)  
**Format Kode Akun:** 3 digit numerik (mengacu pada standar perusahaan jasa & dagang)

---

## Daftar Chart of Accounts (CoA)

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

## Catatan Penting

- Kode akun **111–143** masuk dalam kelompok **Aset** (Debit).
- Kode akun **211–222** masuk dalam kelompok **Kewajiban** (Kredit).
- Kode akun **311–313** masuk dalam kelompok **Ekuitas** (Kredit, kecuali Prive).
- Kode akun **411–412** masuk dalam kelompok **Pendapatan** (Kredit).
- Kode akun **511–523** masuk dalam kelompok **Beban** (Debit).