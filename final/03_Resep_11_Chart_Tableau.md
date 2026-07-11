# Resep 11 Chart Day 1 di Tableau — pakai data `shopee_enriched.csv`

Setiap jenis chart yang diajarkan Day 1, dibangun di atas dataset Shopee ini, lengkap dengan pertanyaan bisnisnya. Ini adalah "kosakata eksploratori" (semua tipe) — nanti di Day 2 kamu hanya memilih ~6 yang paling penting untuk cerita (eksplanatori).

Kolom yang dipakai sudah ada di data (termasuk turunan): `Metode Pembayaran`, `region_group`, `main_category`, `cancel_reason_group`, `order_month`, `Provinsi`, `Total Pembayaran`, `total_qty`, `lost_gmv_est`, `is_cancel` (1/0). Ditambah dua calculated field di workbook: **Tingkat Batal** = `SUM([is_cancel]) / COUNT([order_id])` dan **Jumlah Pesanan** = `1` (SUM = jumlah pesanan).

Status: 🟢 = sudah jadi worksheet di `Cerita_Data_Shopee_11charts.twbx` · 🔧 = bangun sendiri (butuh field bawaan Tableau: lat/long, bins, atau reference distribution yang tidak bisa ditulis di file mentah).

---

### 1. Bar Chart — 🟢 (sheet "G1 Bar")
**Pertanyaan:** Metode pembayaran mana yang paling banyak dipakai?
Columns: `SUM(Jumlah Pesanan)` · Rows: `Metode Pembayaran` · urutkan menurun. Ingat: sumbu mulai dari 0.

### 2. Line Chart — 🟢 (sheet "G2 Line")
**Pertanyaan:** Bagaimana tren GMV dari bulan ke bulan?
Columns: `Bulan Pesanan` (atau `Waktu Pesanan Dibuat` set continuous MONTH) · Rows: `SUM(Total Pembayaran)`.

### 3. Pie / Donut — 🟢 (sheet "G3 Pie")
**Pertanyaan:** Berapa komposisi pesanan per kelompok wilayah?
Marks = Pie · `region_group` ke Color · `SUM(Jumlah Pesanan)` ke Angle & Label.
*Catatan ajar:* Day 1 mengajarkan pie; Day 2 (Cole) menyarankan bar/treemap. Pakai hanya untuk 2–4 bagian.

### 4. Treemap — 🟢 (sheet "G4 Treemap")
**Pertanyaan:** Kategori produk mana penyumbang GMV terbesar?
Marks = Square · `main_category` ke Color · `SUM(Total Pembayaran)` ke Size & Label. (Temuan: **Seal/Baut/Roof** justru penyumbang GMV terbesar, walau **Celengan** paling banyak jumlah pesanannya.)

### 5. Scatter Plot — 🟢 (sheet "G5 Scatter")
**Pertanyaan:** Apakah makin banyak item, makin besar nilai pesanan?
Columns: `SUM(total_qty)` · Rows: `SUM(Total Pembayaran)` · `order_id` ke Detail (satu titik = satu pesanan) · Marks = Circle. Ingat: korelasi bukan sebab-akibat.

### 6. Map — 🔧
**Pertanyaan:** Di provinsi mana pelanggan kita tersebar?
Pastikan `Provinsi` bericon globe (Geographic role → State/Province; sudah di-set di workbook). Klik dua kali `Provinsi` → Tableau membuat Latitude/Longitude otomatis dan menggambar peta. Lalu `SUM(Jumlah Pesanan)` ke Size (symbol map) atau Color (filled map). *Kenapa bangun sendiri: lat/long adalah field bawaan yang baru muncul setelah Tableau geocode, tidak bisa ditulis di file mentah.*

### 7. Highlight Table / Heat Map — 🟢 (sheet "G7 Heatmap")
**Pertanyaan:** Kombinasi pembayaran × wilayah mana paling rawan batal?
Rows: `Metode Pembayaran` · Columns: `region_group` · `Tingkat Batal` ke Color (skala merah) dan ke Label.

### 8. Histogram — 🔧
**Pertanyaan:** Bagaimana sebaran nilai pesanan pelanggan?
Klik kanan `Total Pembayaran` → Create → Bins (mis. ukuran 10.000). Drag field bins ke Columns, `CNT(Total Pembayaran)` ke Rows. *Bangun sendiri: field Bins dibuat lewat menu Tableau.*

### 9. Box-and-Whisker Plot — 🔧
**Pertanyaan:** Bagaimana sebaran & outlier nilai pesanan per wilayah?
Columns: `region_group` · Rows: `Total Pembayaran` (jadikan continuous, matikan agregasi via Analysis → Aggregate Measures). Dari panel Analytics, drag **Box Plot** ke view. *Bangun sendiri: box plot adalah reference distribution dari Analytics pane.*

### 10. Dual-Axis / Combo — 🔧
**Pertanyaan:** Saat penjualan naik, apakah pembatalan ikut naik?
Columns: `Bulan Pesanan`. Rows: `SUM(Total Pembayaran)` lalu `Tingkat Batal`. Klik kanan sumbu ke-2 → **Dual Axis**. Set Marks: GMV = Bar, Tingkat Batal = Line. *Bangun sendiri: konfigurasi dual-axis sulit ditulis andal di file mentah.*

### 11. KPI / Big Number (BAN) — 🟢 (sheet "G11 BAN")
**Pertanyaan:** Apa angka utama yang harus dilihat sekali pandang?
`SUM(Total Pembayaran)` ke Text, format besar & tebal. Duplikat untuk `Tingkat Batal` dan AOV (`SUM(Total Pembayaran)/SUM(Jumlah Pesanan)`). Ingat: satu angka tanpa pembanding tidak bermakna.

---

## Eksploratori (11) → Eksplanatori (6)

Setelah membangun ke-11, untuk **cerita** kamu hanya memakai 6 yang menjawab Big Idea (lihat `01_Data_Story_Case_Kebocoran_Pembatalan.md`): Line GMV, Bar/nilai hilang, Bar batal per pembayaran, Bar alasan batal, Bar batal per wilayah, dan Line tren batal. Inilah inti pelajaran Day 2: buka semua oyster, sajikan mutiaranya saja.
