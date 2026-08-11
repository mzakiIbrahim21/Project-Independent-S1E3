# Studi Kasus: Analisis & Data Cleaning Transaksi Retail
### PT RetailKu Nusantara — Data Analyst Portfolio Project

---

## 1. Latar Belakang

**PT RetailKu Nusantara** adalah perusahaan retail yang menjual produk lintas kategori (Elektronik, Fashion, Rumah Tangga, Kesehatan & Kecantikan, Makanan & Minuman, Otomotif, Olahraga, Mainan & Hobi) melalui kanal **online** (website, mobile app, marketplace) dan **offline** (toko fisik) di berbagai kota di Indonesia sejak tahun 2020.

Selama 6 tahun beroperasi, seluruh transaksi tercatat di sistem POS (Point of Sale) dan e-commerce backend perusahaan, namun **data tersebut belum pernah dibersihkan atau distandardisasi**. Sistem lama sering berganti vendor, tim entry data manual di beberapa cabang tidak mengikuti format baku, dan integrasi antar kanal penjualan (toko fisik, marketplace, aplikasi) menghasilkan format yang berbeda-beda pada kolom yang sama.

Manajemen (Bos/Direksi) ingin mulai memanfaatkan data ini untuk pengambilan keputusan strategis — namun tim data menyadari bahwa **data mentah (raw data) tidak bisa langsung dianalisis** karena kualitasnya buruk: banyak nilai kosong, format tidak konsisten, duplikasi, outlier, dan kesalahan logika bisnis (misalnya total transaksi yang tidak sesuai perhitungan).

## 2. Peran Anda (Data Analyst)

Anda direkrut sebagai **Data Analyst** untuk membersihkan, menganalisis, dan menyajikan data transaksi retail perusahaan tersebut agar dapat digunakan sebagai dasar pengambilan keputusan oleh manajemen.

## 3. Pernyataan Masalah (Problem Statement)

> "Manajemen PT RetailKu Nusantara membutuhkan pemahaman yang akurat tentang performa penjualan periode 2020–2025 — namun data transaksi yang tersedia sangat mentah dan tidak konsisten, sehingga belum dapat langsung digunakan untuk analisis maupun pelaporan ke jajaran direksi."

## 4. Pertanyaan Bisnis (Business Questions)

1. Berapa banyak produk yang berhasil terjual, dan produk/kategori apa saja yang paling laris?
2. Bagaimana tren pendapatan dan jumlah pelanggan dari tahun ke tahun (2020–2025)?
3. Metode pembayaran apa yang paling banyak digunakan, dan bagaimana pergeserannya dari waktu ke waktu?
4. Seberapa besar tingkat data yang bermasalah (missing value, duplikat, outlier) dalam sistem transaksi perusahaan saat ini?
5. Apa rekomendasi perbaikan proses input data agar masalah kualitas data ini tidak terus berulang?

## 5. Deskripsi Dataset

| Item | Keterangan |
|---|---|
| Nama file | `retail_transactions_raw_2020_2025.csv` |
| Jumlah baris | 3.030.001 transaksi |
| Jumlah kolom | 50 variabel |
| Periode | Januari 2020 – Desember 2025 |
| Granularitas | 1 baris = 1 transaksi produk dalam satu pesanan |
| Cakupan kolom | Informasi transaksi, pelanggan, produk, harga, pembayaran, pengiriman, hingga ulasan |
| Kondisi data | **Mentah** — missing value, format tidak konsisten, duplikat, outlier, kesalahan logika bisnis (lihat `DATA_DICTIONARY.md`) |

## 6. Tujuan & Ruang Lingkup Proyek

**Tujuan:**
- Membersihkan dan menstandardisasi data transaksi mentah menjadi data yang siap dianalisis (*analysis-ready*).
- Menghasilkan insight penjualan yang dapat dipertanggungjawabkan untuk mendukung keputusan bisnis.
- Menyajikan hasil analisis dalam bentuk dashboard/laporan yang mudah dipahami oleh manajemen non-teknis.

**Ruang Lingkup:**
- Data cleaning & preprocessing (bukan membangun sistem baru)
- Exploratory Data Analysis (EDA)
- Visualisasi & pelaporan (dashboard + presentasi eksekutif)
- Rekomendasi bisnis berbasis data

**Di luar ruang lingkup:** prediksi/forecasting menggunakan machine learning, perancangan ulang sistem POS/e-commerce.

## 7. Metodologi / Tahapan Kerja

```
1. Data Understanding
   → Memahami struktur, tipe data, dan konteks bisnis dari 50 kolom

2. Data Cleaning & Preprocessing
   → Menangani missing value (imputasi/penghapusan sesuai konteks)
   → Standardisasi format (tanggal, angka, teks, boolean)
   → Deduplikasi baris
   → Deteksi & penanganan outlier (usia, quantity, rating di luar rentang wajar)
   → Validasi & rekonsiliasi logika bisnis (TotalAmount vs Quantity × UnitPrice,
     DeliveryDate vs OrderDate)

3. Exploratory Data Analysis (EDA)
   → Distribusi penjualan per kategori, produk, wilayah, metode pembayaran
   → Analisis tren tahunan (2020–2025)
   → Analisis pelanggan (jumlah unik, segmentasi)

4. Visualisasi & Reporting
   → Dashboard interaktif / laporan PPT untuk manajemen
   → Ringkasan eksekutif (KPI utama, insight, rekomendasi)

5. Rekomendasi
   → Insight strategis untuk manajemen
   → Rekomendasi perbaikan proses data entry ke depannya
```

## 8. Tools & Tech Stack yang Disarankan

| Kategori | Tools |
|---|---|
| Data Cleaning | Python (Pandas, NumPy) / SQL |
| Analisis | Python (Pandas), atau SQL (Google BigQuery/MySQL) |
| Visualisasi | Power BI / Google Looker Studio / Matplotlib & Seaborn |
| Pelaporan | PowerPoint, atau dashboard interaktif |
| Version Control | Git & GitHub (untuk dokumentasi portofolio) |

## 9. Deliverables (Output yang Dihasilkan)

1. **Cleaned dataset** (`.csv`) — data hasil pembersihan, siap dianalisis
2. **Data cleaning report/notebook** — dokumentasi proses & keputusan cleaning (langkah apa dilakukan dan alasannya)
3. **Dashboard/visualisasi** — ringkasan performa penjualan 2020–2025
4. **Laporan eksekutif (PPT/PDF)** — insight & rekomendasi untuk manajemen
5. **README/Studi kasus** (dokumen ini) — konteks proyek untuk portofolio

## 10. Success Metrics (Definisi "Selesai")

- [ ] Persentase missing value pada kolom kritikal (harga, kuantitas, tanggal) berkurang signifikan setelah cleaning
- [ ] Tidak ada duplikat transaksi tersisa di data final
- [ ] Seluruh nilai `TotalAmount` konsisten dengan `Quantity × UnitPrice − Diskon + Pajak + Ongkir`
- [ ] Format tanggal, teks kategori, dan boolean seragam di seluruh dataset
- [ ] Dashboard/laporan dapat menjawab seluruh pertanyaan bisnis di poin 4

## 11. Catatan untuk Portofolio

Proyek ini cocok ditampilkan di GitHub/LinkedIn sebagai studi kasus **end-to-end data analytics**: mulai dari data mentah berskala besar (3 juta baris), proses cleaning yang terdokumentasi, hingga dashboard dan rekomendasi bisnis. Struktur ini mencerminkan alur kerja nyata seorang Data Analyst di perusahaan retail — bukan hanya kemampuan visualisasi, tetapi juga kemampuan menangani data kotor dari sumber yang tidak ideal (skill yang paling dicari recruiter).

**Struktur folder repo yang disarankan:**
```
retail-data-analysis-project/
├── README.md                          (studi kasus ini)
├── data/
│   ├── raw/retail_transactions_raw_2020_2025.csv
│   └── cleaned/retail_transactions_cleaned.csv
├── notebooks/
│   └── 01_data_cleaning.ipynb
│   └── 02_exploratory_analysis.ipynb
├── dashboard/
│   └── retail_dashboard.pbix / .pdf
├── reports/
│   └── Laporan_Analisis_Penjualan_Retail_2020_2025.pptx
└── DATA_DICTIONARY.md
```
