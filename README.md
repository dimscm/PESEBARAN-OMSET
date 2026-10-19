# Pesebaran Omset Outlet

Web untuk melihat **pesebaran omset outlet di peta**. Web ini membawa **data bawaan** dari
`LOKASI_3_2_1.xlsx` (Grosir Minuman Jaktim, `data/lokasi.js`) yang langsung tampil saat dibuka. Omset yang dipakai adalah **omset per minggu (rata-rata 26 minggu)**.
Anda tetap bisa **unggah file Excel lain** untuk menggantinya, jadi daerah mana pun bisa memakai web yang sama.

> Repositori ini publik, jadi isi `data/lokasi.js` (nama toko, salesman, omset) bisa dilihat siapa pun
> yang tahu alamatnya. Untuk mengganti data bawaan, timpa file itu; untuk menghapusnya, hapus file itu
> dan web kembali ke data contoh.

## Cara pakai

1. Buka `index.html` (klik dua kali, atau lewat alamat web kalau sudah di-hosting).
2. Klik **Pilih file Excel** atau tarik file `.xlsx` / `.xls` / `.csv` ke kotak unggah.
3. Peta langsung terisi dengan file Anda menggantikan data bawaan. Tanpa `data/lokasi.js`, web
   menampilkan **data contoh** sampai file diunggah.

File Anda diproses **di browser Anda sendiri**. Tidak ada data yang dikirim ke server mana pun.

## Kolom yang dibaca

Baris judul kolom dicari otomatis (tidak harus di baris pertama):

| Kolom | Nama lain yang juga dikenali |
| --- | --- |
| Kecamatan | Kec, District |
| Kelurahan | Kel, Desa, Village |
| No Outlet | Kode Outlet, Outlet ID |
| Nama Outlet | Nama Toko, Nama, Outlet Name, Pelanggan |
| Channel | Chanel, Kanal, Tipe Outlet |
| Alamat | Address |
| Omset | Omzet, Penjualan, Sales, Revenue, Nilai (kolom omset per minggu seperti `Omset / Week (avg 26WK)` diutamakan) |
| Salesman | Nama Salesman |
| Status | — |
| Long | Longitude, Lng, Bujur, X |
| Lat | Latitude, Lintang, Y |

Angka bergaya Indonesia (`17.450.000`) maupun internasional (`17,450,000`) sama-sama terbaca.
Baris yang koordinatnya kosong atau `0` tidak bisa dipetakan — jumlahnya ditampilkan di panel
dan daftarnya bisa diunduh untuk diperbaiki.

## Aturan warna titik

| Warna | Channel |
| --- | --- |
| 🔵 Biru muda | Gromin (mis. `123-GM - GROMIN BEV`, `127-GMM GROMIN`) |
| 🔴 Merah | Star Outlet (mis. `122-SO - STAR OUTLET BEV`, `126-SL - STAR OUTLET LM`) |
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
- **Omset** — rentang omset, juga ada di panel Toko terdekat (keduanya selalu sama). Di panel Toko terdekat
  batasnya bisa **diisi sendiri** (*Dari* / *Sampai*), mis. kosong – `4jt` untuk di bawah 4 juta; format `500rb`,
  `1,5jt`, `4000000` terbaca, dan angka polos di bawah 1000 dibaca juta. Bila file punya kolom
  omset per minggu (mis. `Omset / Week (avg 26WK)`), kolom itu yang dipakai dan rentangnya:
  < 250 rb / 250–500 rb / 500 rb–1 jt / 1–2 jt / 2–4 jt / ≥ 4 jt per minggu. Tanpa kolom mingguan:
  < 10 jt / 10–25 jt / 25–50 jt / 50–100 jt / 100–200 jt / ≥ 200 jt.
- **Pencarian** nama outlet, alamat, atau nomor outlet
- Klik baris di **Warna channel** untuk menyembunyikan/menampilkan satu kelompok warna

## Toko terdekat dari saya

Panel paling atas. Pilih **Kelurahan** (atau biarkan *Semua kelurahan*), lalu tekan
**Cari toko terdekat dari lokasi saya**. Daftar toko diurutkan dari yang paling dekat dengan posisi
Anda, lengkap dengan jarak garis lurus, kelurahan, dan omset; daftarnya ikut diperbarui saat Anda
bergerak dan saat filter diubah. Klik nama toko untuk terbang ke titiknya, atau **Rute** untuk membuka
petunjuk arah di Google Maps. Popup setiap titik juga punya tombol **Rute ke sini** dan **Buka di Maps**.

Pilihan kelurahan di panel ini sama dengan checklist Kelurahan di bagian Filter — mengubah salah
satunya ikut mengubah yang lain.

## File tersimpan di browser

File yang terakhir diunggah disimpan di browser itu sendiri (IndexedDB), jadi saat web dibuka lagi
di HP/komputer yang sama datanya langsung tampil tanpa unggah ulang. Tidak ada yang dikirim ke server.
Tombol **Kembali ke data bawaan** di panel Sumber data menghapusnya.

## Lokasi saya

Tombol **Lokasi saya** di kanan atas menandai posisi Anda sekarang dengan titik **ungu** berlabel "Anda" —
warna yang tidak dipakai channel mana pun, jadi tidak tertukar dengan outlet —
beserta lingkaran perkiraan akurasinya. Peta langsung terbang ke titik itu, dan klik titiknya untuk
melihat koordinat, akurasi, serta **outlet terdekat** beserta jaraknya. Posisi ikut bergerak selama
tombolnya menyala — klik sekali lagi untuk berhenti.

Browser akan meminta izin lokasi saat pertama kali dipakai. Fitur ini hanya jalan lewat alamat
`https://` (seperti GitHub Pages) atau `localhost`; kalau `index.html` dibuka langsung dari file di
komputer, browser memblokir layanan lokasi.

## Peta dasar

Pilihan peta dasar ada di ikon lapisan kanan atas: **Abu-abu terang**, **Abu-abu gelap**
(keduanya dari Esri), **Peta jalan** (OpenStreetMap), dan **Satelit** (Esri). Peta abu-abu dipilih
otomatis mengikuti tema terang/gelap.

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
gambar peta dasar (Esri/OpenStreetMap) — tanpa internet, titik-titiknya tetap tampil di atas latar
kosong.
