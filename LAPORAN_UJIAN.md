# Laporan UTS Web Software Tools

**Nama:** Belum diberikan
**Nomor Induk Mahasiswa:** Belum diberikan
**Kelas:** Belum diberikan
**Tanggal:** 2026-11-11

## A. Bukti pemeriksaan masalah

| Masalah          | Alat yang digunakan                   | Bukti pemeriksaan                                                                                                                                                     | Perkiraan penyebab                                                 | Perbaikan                                                    | Hasil setelah perbaikan                                                              |
| ---------------- | ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------------------------------ |
| Produk           | Pemeriksaan kode dan browser lokal    | `public/app.js` meminta `/api/barang`, sedangkan `server.mjs` menyediakan `/api/products`. Setelah diperbaiki, browser menampilkan 4 produk.                          | URL endpoint frontend tidak cocok dengan route server.             | Mengubah request menjadi `/api/products`.                    | Status menunjukkan 4 produk tersedia dan keempat produk tampil.                      |
| Tombol keranjang | Pemeriksaan kode dan browser lokal    | Tombol hasil render memakai kelas `.add-button`, tetapi listener mencari `.add-to-cart`. Setelah diperbaiki, klik tombol mouse dua kali menghasilkan `2 barang`.      | Selector listener tidak cocok dengan kelas tombol.                 | Listener mencari `.add-button`.                              | Produk masuk keranjang dan kuantitas bertambah saat produk yang sama diklik kembali. |
| Total belanja    | `npm run test:once` dan browser lokal | Sebelum perbaikan hanya 5 dari 7 tes lulus; kuantitas 2 menghasilkan Rp75.000, seharusnya Rp150.000, dan kasus campuran menghasilkan Rp225.000, seharusnya Rp600.000. | Fungsi total menjumlahkan harga satuan tanpa mengalikan kuantitas. | Menghitung `harga × kuantitas` untuk setiap baris keranjang. | 7 dari 7 tes lulus; dua mouse menampilkan total Rp150.000 di browser.                |

## B. Hasil pengujian

- Jumlah pengujian sebelum perbaikan: 7 tes; 5 berhasil dan 2 gagal.
- Jumlah pengujian berhasil setelah perbaikan: 7 dari 7 tes.
- Catatan perubahan pada fungsi yang diperiksa: `loadProducts` menggunakan endpoint server yang benar; `renderProducts` memasang listener pada kelas tombol yang benar; `calculateTotal` mengalikan harga dengan kuantitas. Berkas tes tidak diubah.

## C. Kualitas kode

- Temuan sebelum perbaikan: Biome melaporkan variabel `discount` tidak digunakan dan format `public/app.js` tidak sesuai konfigurasi.
- Perbaikan yang dilakukan: menghapus variabel yang tidak digunakan dan memformat kedua berkas JavaScript yang diperiksa.
- Hasil pemeriksaan ulang: `npm run quality:check` berhasil; kedua berkas JavaScript lolos pemeriksaan lint dan format.

## D. Git

- Branch (jika membuat): `main`, terhubung ke remote `origin` pada repository GitHub yang diberikan.
- Ringkasan commit: `81c62d8 chore: initialize project with UTS fixes` (snapshot kondisi proyek setelah perbaikan; bukan baseline sebelum perbaikan).
- Hasil pemeriksaan `git status`: setelah commit laporan dipush, branch `main` tersinkron dengan `origin/main` dan working tree bersih.

## E. Pemakaian kecerdasan buatan (jika digunakan)

- Nama alat: GitHub Copilot di Visual Studio Code.
- Pertanyaan/instruksi yang diberikan: periksa dan perbaiki masalah daftar produk, tombol keranjang, dan total belanja; lengkapi laporan berdasarkan bukti.
- Bagian jawaban yang diterapkan: penyesuaian endpoint API, selector tombol, dan rumus total berdasarkan kuantitas.
- Cara memeriksa apakah saran tersebut benar: menjalankan 7 tes otomatis serta membuka aplikasi lokal, memastikan 4 produk tampil, lalu menambahkan mouse dua kali dan memeriksa kuantitas serta totalnya.

## F. Refleksi singkat

- Satu pelajaran paling penting dari ujian ini: telusuri kesesuaian kontrak antarbagian aplikasi (endpoint server, selector UI, dan bentuk data), lalu buktikan perbaikan dengan tes dan perilaku aplikasi.
