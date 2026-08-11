# Data Dictionary — Retail Transactions Raw Dataset (2020–2025)

**File:** `retail_transactions_raw_2020_2025.csv` (dikompres: `.csv.gz`)
**Jumlah baris:** 3.030.001 (3.000.000 baris dasar + ±30.000 baris duplikat yang sengaja disisipkan sebagai bagian dari "data kotor")
**Jumlah kolom:** 50
**Periode:** 2020-01-01 s.d. 2025-12-31
**Tujuan:** Dataset simulasi untuk latihan/portofolio *data cleaning & preprocessing*. Semua nama pelanggan, email, dan nomor telepon adalah data sintetis (bukan data asli).

> ⚠️ Dataset ini **sengaja dibuat sangat mentah** — jangan langsung dipakai untuk analisis tanpa proses cleaning terlebih dahulu.

## Daftar Kolom & Masalah Kualitas Data

| # | Kolom | Deskripsi | Masalah yang disengaja |
|---|-------|-----------|--------------------------|
| 1 | TransactionID | ID unik transaksi | ~0.5% kehilangan prefix "TRX-" |
| 2 | OrderID | ID pesanan | - |
| 3 | OrderDate | Tanggal pesanan | 5 format berbeda (YYYY-MM-DD, DD/MM/YYYY, dll), ~1% tanggal tidak valid, ~4% missing |
| 4 | OrderTime | Waktu pesanan (HH:MM:SS) | ~10% missing |
| 5 | Year | Tahun transaksi | ~2% ditulis 2 digit ("20" bukan "2020") |
| 6 | Month | Bulan transaksi (1–12) | - |
| 7 | DayOfWeek | Nama hari (Bahasa Indonesia) | Kapitalisasi tidak konsisten, ~15% missing |
| 8 | CustomerID | ID pelanggan | ~3% kehilangan prefix "CUST-" |
| 9 | CustomerName | Nama pelanggan | Kapitalisasi tidak konsisten, spasi berlebih, ~6% missing |
| 10 | CustomerEmail | Email pelanggan | ~5% format tidak valid, ~8% missing |
| 11 | CustomerPhone | No. telepon | 4 format berbeda (08xx, +628xx, 62-8xx, 0xx), ~12% missing/placeholder |
| 12 | Gender | Jenis kelamin | 10 varian penulisan (M/F/Male/L/P/Laki-laki/dst), ~10% missing |
| 13 | Age | Usia pelanggan | Outlier (negatif, 0, >150), ~9% missing |
| 14 | City | Kota | Typo (huruf hilang), kapitalisasi tidak konsisten, ~5% missing |
| 15 | Province | Provinsi | ~7% missing |
| 16 | Country | Negara | Kapitalisasi tidak konsisten |
| 17 | PostalCode | Kode pos | Beberapa "00000" tidak valid, ~15% missing |
| 18 | CustomerSegment | Segmen pelanggan (Retail/Wholesale/dst) | ~5% missing |
| 19 | ProductID | ID produk | - |
| 20 | ProductName | Nama produk | Typo huruf, kapitalisasi tidak konsisten, ~2% missing |
| 21 | Category | Kategori produk (8 kategori) | - |
| 22 | Brand | Merek produk | ~20% missing |
| 23 | SupplierID | ID pemasok | - |
| 24 | SupplierName | Nama pemasok | ~10% missing |
| 25 | UnitPrice | Harga satuan | 4 format berbeda (angka polos, "Rp x.xxx", "x,xxx.xx", desimal), sebagian negatif, ~5% missing |
| 26 | Quantity | Jumlah unit dibeli | Outlier (0, negatif, 999), ~4% missing |
| 27 | DiscountPct | % diskon | ~25% missing |
| 28 | DiscountAmount | Nominal diskon | ~51% missing (tidak selalu dihitung) |
| 29 | TaxAmount | Nominal pajak | ~44% missing |
| 30 | ShippingCost | Biaya pengiriman | ~10% missing |
| 31 | TotalAmount | Total transaksi | ~15% nilainya **tidak konsisten** dengan Quantity × UnitPrice (kesalahan hitung yang disengaja), ~35% missing |
| 32 | Currency | Mata uang | Variasi penulisan (IDR/Rp/idr/RP/USD) |
| 33 | PaymentMethod | Metode pembayaran | Kapitalisasi tidak konsisten, ~5% missing |
| 34 | PaymentStatus | Status pembayaran | ~4% missing |
| 35 | OrderStatus | Status pesanan | ~3% missing |
| 36 | ShippingMethod | Metode pengiriman | ~12% missing |
| 37 | WarehouseID | ID gudang | ~8% missing |
| 38 | StoreID | ID toko | - |
| 39 | StoreType | Tipe toko (Online/Offline/Marketplace) | - |
| 40 | SalesChannel | Kanal penjualan | ~5% missing |
| 41 | PromoCode | Kode promo | ~85% missing (wajar, tidak semua transaksi pakai promo) |
| 42 | LoyaltyMember | Status member loyalitas | 10 varian penulisan (Yes/No/Y/N/1/0/true/false), ~10% missing |
| 43 | LoyaltyPoints | Poin loyalitas | ~30% missing |
| 44 | ReviewRating | Rating ulasan (1–5) | Beberapa nilai di luar rentang (0, 6, -1, 10), ~55% missing (wajar, tidak semua transaksi diulas) |
| 45 | ReviewText | Teks ulasan | ~75% missing |
| 46 | DeliveryDate | Tanggal pengiriman | Format tanggal beragam, sebagian **lebih awal dari OrderDate** (data error), ~25% missing |
| 47 | DeliveryStatus | Status pengiriman | ~15% missing |
| 48 | ReturnFlag | Status retur | Variasi penulisan (Yes/No/Y/N/0/1) |
| 49 | ReturnReason | Alasan retur | ~90% missing (hanya relevan jika retur) |
| 50 | EmployeeID | ID staf penjualan | ~18% missing |

## Ringkasan Isu Data (untuk latihan cleaning)

1. **Missing values** — tersebar di hampir semua kolom dengan tingkat 2%–90% (kolom yang secara alami jarang terisi seperti PromoCode/ReviewText memang didesain lebih tinggi).
2. **Inkonsistensi format tanggal** — 5 format berbeda di `OrderDate` dan `DeliveryDate`, termasuk tanggal tidak valid.
3. **Inkonsistensi kategori/teks** — kapitalisasi campur (UPPER/lower/Title), spasi berlebih, typo pada `City`, `ProductName`.
4. **Inkonsistensi tipe data** — `UnitPrice` tersimpan sebagai angka, teks dengan simbol mata uang, maupun format ribuan/desimal berbeda.
5. **Duplikat** — ±1% baris duplikat murni disisipkan ke tiap batch data.
6. **Outlier / nilai tidak masuk akal** — `Age` negatif/>150, `Quantity` negatif/0/999, `ReviewRating` di luar 1–5.
7. **Inkonsistensi logika bisnis** — `TotalAmount` yang tidak sama dengan `Quantity × UnitPrice`, `DeliveryDate` yang lebih awal dari `OrderDate`.
8. **Encoding boolean tidak konsisten** — `LoyaltyMember` dan `ReturnFlag` memakai kombinasi Yes/No, Y/N, 1/0, True/False.

Dataset ini cocok digunakan untuk melatih skill: `pandas` data cleaning, deteksi & penanganan missing value, standardisasi format, deduplikasi, validasi rentang nilai (outlier handling), dan rekonsiliasi kolom turunan (misalnya menghitung ulang `TotalAmount`).
