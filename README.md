# 🥤 Aplikasi Kasir UMKM Jus — Vue + Pinia + JSON Server

Selamat datang di **Aplikasi Kasir Jus**!  
Aplikasi ini dirancang khusus untuk membantu **UMKM (Usaha Mikro Kecil Menengah)** seperti kios jus, stand minuman sehat, atau kafe kecil dalam mengelola transaksi penjualan jus dengan tampilan segar dan ramah pengguna.

---

## 🍃 Teknologi yang Digunakan

- ✅ **Vue 3**
- ✅ **Pinia** (state management)
- ✅ **Tailwind CSS** (styling hijau segar)
- ✅ **Vue Router**
- ✅ **JSON Server** (mock backend API)

---

## 🍹 Fitur Unggulan

### 1. 🌿 Transaksi
- Menampilkan daftar menu jus dalam tampilan segar
- Fitur **pencarian menu** cepat
- Tambahkan item ke **keranjang**
- Lencana jumlah item di keranjang selalu update

### 2. 🧺 Keranjang
- Tampilkan semua item pesanan
- Hapus item dengan mudah
- **Checkout** otomatis menyimpan transaksi ke backend

### 3. 📜 Riwayat Transaksi
- Daftar transaksi yang sudah dilakukan
- Rincian lengkap per pesanan
- Tanggal dan total belanja yang jelas

### 4. 📈 Laporan Penjualan
- Menampilkan **total transaksi**
- Menghitung **total pemasukan**
- Rekap semua transaksi secara ringkas

---

## ✅ Masalah yang Diselesaikan

| Masalah                                                                  | Solusi                                                                 |
|--------------------------------------------------------------------------|------------------------------------------------------------------------|
| Pelaku UMKM sulit mencatat transaksi harian                              | Transaksi otomatis disimpan ke database                               |
| Tidak tahu berapa total pemasukan tiap hari/bulan                        | Fitur laporan menyediakan rekap jumlah & nilai transaksi              |
| Terlalu banyak menu sulit dikelola                                       | Menu tampil dalam grid dan mudah dicari dengan fitur pencarian        |
| Sistem kasir mahal dan rumit                                             | Aplikasi ini ringan, gratis, dan mudah dijalankan di laptop/PC lokal  |

---

## 🌐 Routing Vue

| Path           | Komponen        | Deskripsi                                          |
|----------------|------------------|-----------------------------------------------------|
| `/`            | `Transaksi.vue` | Halaman utama untuk memilih menu dan menambah pesanan |
| `/keranjang`   | `Keranjang.vue` | Tampilkan isi keranjang dan lanjut ke checkout     |
| `/riwayat`     | `Riwayat.vue`   | Riwayat transaksi yang telah dilakukan             |
| `/laporan`     | `Laporan.vue`   | Ringkasan pemasukan dan jumlah transaksi           |

---

## 🔗 Endpoint API (JSON Server)

Pastikan Anda menjalankan server di:  
`http://localhost:3000`

### 📦 Menu
```http
GET    /menu            # Ambil semua data menu jus
GET    /transaksi       # Ambil semua riwayat transaksi
POST   /transaksi       # Simpan transaksi baru

