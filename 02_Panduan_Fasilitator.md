# Panduan Fasilitator — Mengajar Data Storytelling dengan Dataset Shopee

Panduan untuk mengajarkan Day 2 (Data Communication) memakai kasus nyata "Menutup Kebocoran Pembatalan". Cocok dipakai sebagai contoh yang kamu bawakan di depan kelas **sebelum** peserta mengerjakan capstone mereka sendiri.

---

## A. Kenapa dataset ini bagus untuk mengajar

1. **Nyata dan tidak sempurna.** Ada tanggal kosong (~1.980 baris), status bervariasi, teks Indonesia campur. Ini kesempatan mengajarkan "data alone does not move people" dan pentingnya membersihkan sebelum bercerita.
2. **Punya tension alami.** Pertumbuhan yang bagus + kebocoran 13,6% = konflik klasik "Setup → Tension" tanpa perlu dibuat-buat.
3. **Punya resolusi yang jujur.** Tingkat batal benar-benar turun ke <10% di 2025 H2 — happy ending yang ada di datanya, bukan karangan.
4. **Menegakkan aturan integritas.** Dataset TIDAK punya profit/margin. Ini momen mengajar: jangan mengarang angka hanya supaya cocok dengan contoh "profit turun 8%" di slide. Kita ubah ceritanya agar sesuai data — bukan sebaliknya.

---

## B. Peta ke setiap prinsip Day 2

Gunakan kasus ini untuk mendemokan tiap lesson di deck:

| Prinsip di deck | Ditunjukkan lewat |
|---|---|
| Exploratory vs Explanatory | Tunjukkan profiling mentah (24 bulan, 19 kolom) lalu hanya 6 chart terpilih. "Kita buka 100 oyster, sajikan 6 mutiara." |
| Tiga elemen (Data/Narrative/Visuals) | Angka batal (data) + "1 dari 7 bocor" (narrative) + line hijau (visuals). |
| WHO/CARE/DO | Bandingkan: cerita untuk pemilik toko (uang) vs untuk tim gudang (gagal kirim). Data sama, cerita beda. |
| Big Idea satu kalimat | Kalimat di §2 dokumen kasus. Minta peserta menulis versinya sendiri. |
| SCQA / narrative arc | Tabel alur di §3. |
| Logika horizontal | Baca 6 action title berurutan — harus utuh tanpa lihat chart. |
| Let the message pick the chart | Chart 1 line (tren), Chart 2 bar (bandingkan), Chart 5 bar (kategori). Tidak ada pie. |
| Eliminate clutter | Bandingkan chart "before" penuh gridline vs PNG kita (tanpa gridline, tanpa legend, satu warna). |
| Focus attention (preattentive) | Semua abu-abu, satu bar/line oranye-hijau. |
| Colour with intent | Oranye = masalah/kebocoran, hijau = perbaikan, abu-abu = konteks. Konsisten di 6 chart. |
| Action title vs topic title | "Sales by Region" ❌ vs "Luar Jawa paling rawan batal (18,9%)" ✔ |
| Annotate the one thing | Chart 6: anotasi "Agu–Nov 2025 turun ke 9,4%". |
| Verify every number | Contoh nyata: klaim awal "hampir separuh batal bisa dicegah" ternyata hanya 29% saat dicek ulang — koreksi sebelum tayang. |

---

## C. Alur sesi yang disarankan (± 60–75 menit)

1. **(10 mnt) Tunjukkan data mentah.** Buka CSV. Tanya kelas: "Apa ceritanya?" — biarkan mereka kewalahan. Itu poinnya: data mentah tidak bercerita.
2. **(10 mnt) Bangun Big Idea bersama.** Tulis di papan. Uji dengan 3 komponen (sudut pandang, taruhan, rekomendasi).
3. **(15 mnt) Storyboard di sticky note.** Susun 6 kartu judul. Acak urutannya, minta kelas menatanya sampai logika horizontal jalan.
4. **(20 mnt) Bedah tiap chart.** Untuk tiap chart tanyakan: pertanyaan bisnisnya apa? kenapa tipe chart ini? mana satu hal yang harus terlihat? Tunjukkan versi decluttered.
5. **(10 mnt) Latihan action title.** Beri peserta topic title, minta ubah jadi action title.
6. **(10 mnt) Bahas integritas.** Kenapa kita TIDAK memakai contoh "profit turun" dari slide. Aturan emas AI.

---

## D. Kesalahan umum peserta (dan cara mengoreksi)

- **Menumpuk semua 6 chart di satu slide.** → Ingatkan: satu ide per slide.
- **Judul topik, bukan aksi.** "Pembatalan per Wilayah" → dorong ke klaim + angka.
- **Pakai pie chart untuk metode pembayaran.** → Bar lebih mudah dibaca; Cole melarang pie.
- **Mengarang margin/profit** karena meniru contoh slide. → Puji kalau mereka sadar datanya tidak punya itu, dan mengubah cerita.
- **Membaca angka tanpa "so-what".** "13,6% batal" → "artinya Rp 192 juta hilang, dan sebagian bisa dicegah."
- **Warna pelangi.** → Satu aksen, sisanya abu-abu.
- **Klaim sebab-akibat berlebihan.** Data menunjukkan korelasi (Online Payment lebih sering batal), bukan sebab pasti. Ajari bahasa hati-hati: "paling rawan", bukan "menyebabkan".

---

## E. Rubrik penilaian (selaras capstone deck)

| Kriteria | 1 (kurang) | 3 (cukup) | 5 (bagus) |
|---|---|---|---|
| Big Idea tunggal & jelas | Tidak ada / kabur | Ada tapi bertele-tele | Satu kalimat, ada taruhan + ask |
| Chart tepat untuk pesan | Salah tipe (mis. pie) | Tipe benar, kurang rapi | Tepat & mendukung klaim |
| Slide bersih (declutter) | Penuh gridline/legend | Cukup bersih | Sangat bersih, 1 aksen warna |
| Action title | Topik semua | Campur | Semua action title, bercerita |
| Delivery 3 menit + ask | Membaca slide | Lancar tanpa ask | Percaya diri, tutup dengan ask |

---

## F. Contoh naskah presentasi 3 menit (untuk dicontohkan)

> "Toko kita tumbuh sehat — Rp 1,05 miliar dalam dua tahun. *(jeda)* Tapi ada yang tidak kelihatan di laporan penjualan: satu dari tujuh pesanan kita batal. Itu sekitar **Rp 192 juta** yang menguap. *(jeda pada angka)*
>
> Kenapa? Sebagian memang pembeli berubah pikiran. Tapi 29% murni soal proses — pesanan belum dibayar dan gagal kirim — dan itu bisa kita perbaiki. Risikonya paling tinggi di luar Jawa, 18,9%.
>
> Kabar baiknya: ini bisa diperbaiki. Lihat empat bulan terakhir — kita sudah menekannya ke bawah 10%. Kita sudah membuktikannya.
>
> Yang saya minta: kunci angka ini permanen dengan tiga langkah — verifikasi pembayaran otomatis, kebijakan COD luar Jawa, dan target < 10% sebagai KPI bulanan. Itu sekitar Rp 2,5–3 juta per bulan yang berhenti bocor."

---

## G. Berkas dalam paket ini

- `01_Data_Story_Case_Kebocoran_Pembatalan.md` — studi kasus lengkap (business problem, Big Idea, rencana chart).
- `02_Panduan_Fasilitator.md` — dokumen ini.
- `shopee_enriched.csv` — data siap Tableau (kolom turunan sudah ditambahkan).
- `charts/01..06_*.png` — enam chart contoh gaya Cole (decluttered).
- `metrics.json` — semua angka mentah untuk verifikasi.
