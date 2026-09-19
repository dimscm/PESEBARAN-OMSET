# Pesebaran Omset Outlet

Web untuk melihat **pesebaran omset outlet di peta**. Data tidak ditanam di dalam web —
Anda **unggah sendiri file Excel**-nya, jadi daerah mana pun bisa memakai web yang sama.

## Cara pakai

1. Buka `index.html` (klik dua kali, atau lewat alamat web kalau sudah di-hosting).
2. Klik **Pilih file Excel** atau tarik file `.xlsx` / `.xls` / `.csv` ke kotak unggah.
3. Peta langsung terisi. Saat pertama dibuka, web menampilkan **data contoh** supaya
   terlihat bentuk akhirnya — data contoh hilang begitu file Anda diunggah.

File Anda diproses **di browser Anda sendiri**. Tidak ada data yang dikirim ke server mana pun.

## Kolom yang dibaca

Baris judul kolom dicari otomatis (tidak harus di baris pertama):

| Kolom | Nama lain yang juga dikenali |
| --- | --- |
| Kecamatan | Kec, District |
| Kelurahan | Kel, Desa, Village |
| No Outlet | Kode Outlet, Outlet ID |
| Nama Outlet | Nama, Outlet Name, Pelanggan |
| Channel | Chanel, Kanal, Tipe Outlet |
| Alamat | Address |
| Omset | Omzet, Penjualan, Sales, Revenue, Nilai |
| Long | Longitude, Lng, Bujur, X |
| Lat | Latitude, Lintang, Y |

Angka bergaya Indonesia (`17.450.000`) maupun internasional (`17,450,000`) sama-sama terbaca.
Baris yang koordinatnya kosong atau `0` tidak bisa dipetakan — jumlahnya ditampilkan di panel
dan daftarnya bisa diunduh untuk diperbaiki.

## Aturan warna titik

| Warna | Channel |
| --- | --- |
| 🔵 Biru muda | Gromin & Star Outlet (mis. `123-GM - GROMIN BEV`, `122-SO - STAR OUTLET BEV`, `126-SL - STAR OUTLET LM`, `127-GMM GROMIN`) |
| 🟢 Hijau | TDP (mis. `158-TDP - RETAIL`, `159-TDP - GROSIR`) |
| ⚪ Abu-abu | Channel lainnya |

Channel `160-TDP - GROMIN` masuk dua kategori sekaligus. Standarnya dihitung sebagai **TDP (hijau)**
karena kode channel-nya TDP; ada saklar di panel **Warna channel** untuk memindahkannya ke
**Gromin (biru muda)** bila cara hitung Anda berbeda.

**Ukuran titik mengikuti besar omset.** Skalanya akar kuadrat terhadap persentil ke-98, supaya satu
outlet raksasa tidak membuat outlet lain menjadi titik yang tak terlihat. Ukuran bisa diperbesar/
diperkecil lewat penggeser *Ukuran titik*.

## Filter

- **Kecamatan** dan **Kelurahan** (pilihan kelurahan menyesuaikan kecamatan yang dipilih)
- **Channel** — per channel asli, lengkap dengan warna dan jumlah outlet
- **Omset minimal** — Semua / ≥ 1 jt / ≥ 5 jt / ≥ 10 jt / ≥ 50 jt
- **Pencarian** nama outlet, alamat, atau nomor outlet
- Klik baris di **Warna channel** untuk menyembunyikan/menampilkan satu kelompok warna

Panel kiri ikut menghitung ulang: jumlah outlet, total omset, rata-rata, median, omset per wilayah,
dan 12 outlet dengan omset tertinggi (klik untuk terbang ke titiknya di peta).
Tombol **Unduh CSV** menyimpan data yang sedang tampil beserta kelompok warnanya.

## Menaruhnya di internet (opsional)

Repositori ini hanya berisi berkas statis, jadi bisa langsung dipakai lewat GitHub Pages:
**Settings → Pages → Source: Deploy from a branch**, pilih branch ini dan folder `/ (root)`.

## Isi repositori

```
index.html   — seluruh aplikasi (tampilan + logika)
vendor/      — Leaflet 1.9.4 (peta) dan SheetJS 0.18.5 (pembaca Excel), beserta lisensinya
```

Pustaka disimpan lokal supaya web tetap jalan tanpa internet; yang tetap butuh internet hanya
gambar peta dasar (OpenStreetMap/CARTO) — tanpa internet, titik-titiknya tetap tampil di atas
latar kosong.
