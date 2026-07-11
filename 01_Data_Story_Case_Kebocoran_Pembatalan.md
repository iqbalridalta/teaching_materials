# Studi Kasus Data Storytelling: "Menutup Kebocoran Pembatalan"

**Dataset:** `all_months_clean.csv` — 20.848 pesanan toko perlengkapan rumah tangga (celengan, mangkok sambal, aksesoris pintu, nampan, rak, dll.) di Shopee, Des 2023 – Nov 2025.
**Audiens:** Pemilik / pengelola toko (lensa operasional + komersial).
**Dipakai untuk:** Capstone Day 2 — ubah satu dashboard menjadi cerita data 3 menit yang bisa ditindaklanjuti.

> Catatan integritas data: seluruh angka di bawah dihitung langsung dari dataset. Kolom turunan (harga satuan, estimasi nilai hilang, kelompok wilayah, kelompok alasan batal) bersifat *derived*, bukan mengarang baris/angka baru. Ini sesuai "Golden rules for using AI honestly" di deck Day 2: *ground it in your data, verify every number.*

---

## 1. Masalah bisnis (business problem)

Toko sudah tumbuh: **Rp 1,05 miliar** GMV dari **17.768 pesanan selesai** dalam 24 bulan. Tapi ada kebocoran yang jarang dilihat pemilik toko karena tidak muncul di laporan "penjualan": **13,6% pesanan batal (2.830 pesanan)**. Pesanan batal tidak menghasilkan rupiah, tetapi tetap memakan biaya — waktu packing, slot stok, dan ongkos kirim yang gagal.

Estimasi konservatif nilai yang hilang karena pembatalan: **± Rp 192 juta** (≈ **Rp 8,7 juta/bulan**). Kabar baiknya: sebagian besar penyebabnya ada di dalam kendali toko, dan data 4 bulan terakhir (Agu–Nov 2025) membuktikan angka ini bisa ditekan ke **bawah 10%**.

### Kerangka audiens (dari deck: WHO / CARE / DO)

| Pertanyaan | Jawaban untuk kasus ini |
|---|---|
| **WHO** — siapa audiensnya? | Pemilik toko. Paham operasional, tidak butuh istilah statistik. Butuh angka rupiah dan tindakan konkret. |
| **CARE** — apa yang dia pedulikan? | Uang yang bocor, risiko, dan usaha yang terbuang. Bukan "cancellation rate" sebagai metrik, tapi "berapa rupiah yang bisa saya selamatkan". |
| **DO** — apa yang kita ingin dia lakukan? | Setujui pengetatan proses pembayaran/COD (terutama luar Jawa) untuk mengunci tingkat batal permanen di bawah 10%. |

---

## 2. Big Idea (seluruh pesan dalam satu kalimat)

> **"Satu dari tujuh pesanan kita batal dan menghabiskan sekitar Rp 192 juta nilai penjualan; pemicu terbesar yang bisa kita kendalikan adalah pesanan yang tak dibayar dan gagal kirim (terparah di luar Jawa), dan jika kita perketat verifikasi pembayaran dan kebijakan COD, kita bisa mengunci tingkat batal di bawah 10% seperti yang sudah terbukti pada Agu–Nov 2025."**

Uji: kalimat ini punya (1) sudut pandang — pembatalan adalah kebocoran uang, (2) taruhan — Rp 192 juta, (3) rekomendasi + bukti — perketat proses, sudah terbukti bisa.

---

## 3. Alur narasi (SCQA / Setup–Tension–Resolution)

| Tahap | Isi | Chart pendukung |
|---|---|---|
| **Situation** (setup) | Toko tumbuh sehat, GMV Rp 1,05 M, puncak Sep 2024. | Chart 1 |
| **Complication** (tension) | Tapi 13,6% pesanan batal = ± Rp 192 jt hilang. | Chart 2 |
| **Question** (diagnosa) | Kenapa dan di mana batal terjadi? Pembayaran mana, alasan apa, wilayah mana. | Chart 3, 4, 5 |
| **Answer** (resolusi + ask) | Ini bisa diperbaiki — sudah terbukti turun ke 9,4%. Kunci permanen. | Chart 6 |

Uji **logika horizontal** (baca judul-judul saja, harus bercerita utuh):
1. Penjualan tumbuh ke Rp 1,05 M, tapi melandai di 2025
2. 1 dari 7 pesanan batal — Rp 192 juta menguap
3. Online Payment & pesanan belum dibayar paling rawan
4. 29% pembatalan murni soal proses (belum dibayar & gagal kirim)
5. Risiko batal tertinggi di luar Jawa
6. Kita sudah pernah menekannya ke bawah 10% — kunci permanen

---

## 4. Rencana chart — satu chart, satu pertanyaan bisnis

Setiap chart mengikuti prinsip Cole: **judul = klaim (action title)**, **chart = bukti**, **catatan = so-what**, satu warna aksen, sisanya abu-abu.

### Chart 1 — Tren GMV bulanan  *(SETUP)*
- **Pertanyaan bisnis:** *"Ke mana arah penjualan kita dalam 24 bulan terakhir?"*
- **Tipe chart:** Line chart (tren waktu). File: `charts/01_gmv_trend.png`
- **Action title:** "Penjualan bulanan naik kuat lalu melandai di 2025"
- **So-what:** Bisnisnya nyata dan besar — jadi kebocoran apa pun berdampak rupiah nyata.
- **Di Tableau:** `Waktu Pesanan Dibuat` (MONTH) di Columns, `SUM(Total Pembayaran)` di Rows, filter `Status Pesanan = Selesai`. Anotasi titik puncak.

### Chart 2 — Nilai terealisasi vs nilai hilang  *(TENSION)*
- **Pertanyaan bisnis:** *"Berapa nilai penjualan yang hilang karena pesanan batal?"*
- **Tipe chart:** Bar (perbandingan 2 kategori). File: `charts/02_lost_gmv.png`
- **Action title:** "Sekitar Rp 192 juta hilang karena 1 dari 7 pesanan batal"
- **So-what:** Ini bukan angka persen abstrak — ini rupiah yang bisa diselamatkan.
- **Di Tableau:** buat field `is_cancel` sudah tersedia; bar `SUM(Total Pembayaran)` pesanan selesai vs `SUM(lost_gmv_est)`.

### Chart 3 — Tingkat batal per metode pembayaran  *(DIAGNOSA)*
- **Pertanyaan bisnis:** *"Metode pembayaran mana yang paling rawan batal?"*
- **Tipe chart:** Bar horizontal. File: `charts/03_cancel_by_payment.png`
- **Action title:** "Online Payment paling rawan batal (18,5%), ShopeePay paling aman (8,7%)"
- **So-what:** COD memang volume terbesar (55%), tapi metode online yang belum dibayar justru bocor lebih besar per pesanan.
- **Di Tableau:** `Metode Pembayaran` di Rows, `AVG(is_cancel)` (format %) di Columns, warnai satu bar tertinggi.

### Chart 4 — Alasan pembatalan  *(DIAGNOSA)*
- **Pertanyaan bisnis:** *"Kenapa pesanan batal — apa akar penyebabnya?"*
- **Tipe chart:** Bar horizontal. File: `charts/04_cancel_reasons.png`
- **Action title:** "29% pembatalan murni soal proses: belum dibayar & gagal kirim"
- **So-what:** Mayoritas batal (68%) memang keputusan pembeli (berubah pikiran, ubah pesanan), tapi 29% ("belum dibayar" + "gagal kirim") adalah masalah proses yang bisa langsung kita tindaklanjuti — itu titik ungkit paling mudah.
- **Di Tableau:** pakai kolom `cancel_reason_group` yang sudah dibuat.

### Chart 5 — Tingkat batal per wilayah  *(DIAGNOSA / PELUANG)*
- **Pertanyaan bisnis:** *"Di mana risiko batal paling tinggi, dan di mana pelanggan kita?"*
- **Tipe chart:** Bar. File: `charts/05_cancel_by_region.png`
- **Action title:** "Luar Jawa paling rawan batal (18,9%) meski hanya 21% pesanan"
- **So-what:** 63% pesanan terpusat di Jabodetabek+Jawa Barat; ekspansi luar Jawa berisiko batal lebih tinggi (sering gagal kirim/COD).
- **Di Tableau:** pakai `region_group`; opsional buat peta (Provinsi → geographic role).

### Chart 6 — Tren tingkat batal + perbaikan  *(RESOLUSI + ASK)*
- **Pertanyaan bisnis:** *"Apakah masalah ini benar-benar bisa diperbaiki?"*
- **Tipe chart:** Line dengan sorotan warna + garis target. File: `charts/06_cancel_trend_win.png`
- **Action title:** "Pembatalan sudah bisa ditekan di bawah 10% — buktinya ada"
- **So-what:** Rata-rata 2024 = 14,5%; Agu–Nov 2025 = 9,4%. Bukan teori, sudah terjadi. Tinggal dikunci.
- **Di Tableau:** line `AVG(is_cancel)` per bulan; highlight 4 bulan terakhir hijau; reference line 10%.

---

## 5. Rekomendasi & ask (penutup presentasi)

**Ask (satu tindakan):** Setujui tiga langkah proses untuk mengunci tingkat batal < 10%:
1. **Verifikasi pembayaran** — ingatkan otomatis pesanan yang belum dibayar sebelum batal otomatis (alasan batal #3 terbesar).
2. **Kebijakan COD luar Jawa** — batas minimum nilai / konfirmasi tambahan untuk COD di wilayah batal tinggi (Luar Jawa 18,9%).
3. **Kunci momentum** — jadikan target < 10% sebagai KPI bulanan; kita sudah membuktikannya empat bulan berturut-turut.

**Nilai yang dipertaruhkan:** menekan batal dari rata-rata ~14% ke ~9% berarti sekitar sepertiga dari Rp 192 juta berpotensi terselamatkan — kira-kira **Rp 2,5–3 juta/bulan** yang sebelumnya menguap.

---

## 6. Angka kunci (untuk verifikasi & catatan pembicara)

| Metrik | Nilai |
|---|---|
| Total pesanan | 20.848 |
| Pesanan selesai | 17.768 |
| Pesanan batal | 2.830 (13,6%) |
| GMV terealisasi | Rp 1.045.550.734 |
| Nilai order rata-rata (AOV) | Rp 58.844 |
| Estimasi nilai hilang (batal) | ± Rp 191.872.343 |
| Estimasi hilang / bulan | ± Rp 8,7 juta |
| Porsi COD | 55,3% |
| Batal — Online Payment | 18,5% (tertinggi) |
| Batal — ShopeePay | 8,7% (terendah) |
| Konsentrasi wilayah inti | 63,2% pesanan |
| Batal Luar Jawa | 18,9% |
| Rata-rata batal 2024 | 14,5% |
| Rata-rata batal Agu–Nov 2025 | 9,4% |
