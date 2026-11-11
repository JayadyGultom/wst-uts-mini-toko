# Laporan UTS Web Software Tools

**Nama:Jayady Managam Gultom**
**Nomor Induk Mahasiswa:12523027**
**Kelas:Teknik Informatika**
**Tanggal:11 November 2026**

## A. Bukti pemeriksaan masalah
| Masalah | Alat yang digunakan | Bukti pemeriksaan | Perkiraan penyebab | Perbaikan | Hasil setelah perbaikan |
|---|---|---|---|---|---|
| Produk | Pemeriksaan kode dan permintaan API lokal | Frontend meminta `/api/barang` (404); `/api/products` merespons 200 dengan 4 produk. | URL API di frontend tidak sama dengan route pada server. | Mengubah URL fetch menjadi `/api/products`. | Endpoint mengembalikan 4 produk; daftar produk dapat dimuat. |
| Tombol keranjang | Pemeriksaan kode dan simulasi klik | Tombol memakai kelas `.add-button`, tetapi handler mencari `.add-to-cart`; setelah selector disamakan, simulasi klik menambahkan produk dan memperbarui jumlah menjadi `1 barang`. | Selector event tidak sesuai dengan kelas tombol yang dirender. | Mengubah selector menjadi `.add-button`. | Produk berhasil masuk ke keranjang dan jumlah tampil `1 barang`. |
| Total belanja | Tes otomatis `node --test` dan pemeriksaan kode | Tes kuantitas 2 menghasilkan Rp75.000, seharusnya Rp150.000; tes beberapa barang menghasilkan Rp225.000, seharusnya Rp600.000. | `calculateTotal` menjumlahkan harga saja dan mengabaikan kuantitas. | Menghitung `item.price * item.quantity` untuk setiap barang. | Semua 7 tes lulus; lint bersih. |

## B. Hasil pengujian
- Jumlah pengujian sebelum perbaikan total: 5 dari 7 lulus; 2 gagal pada perhitungan kuantitas.
- Jumlah pengujian berhasil setelah perbaikan: 7 dari 7 lulus.
- Catatan perubahan pada fungsi yang diperiksa: URL API disesuaikan menjadi `/api/products`, selector tombol menjadi `.add-button`, dan `calculateTotal` menghitung harga dikalikan kuantitas.

## C. Kualitas kode
- Temuan sebelum perbaikan: Biome memberi peringatan bahwa variabel `discount` tidak digunakan; perhitungan total juga mengabaikan kuantitas.
- Perbaikan yang dilakukan: Menghapus variabel yang tidak digunakan dan menghitung total berdasarkan harga serta kuantitas setiap barang.
- Hasil pemeriksaan ulang: `npm.cmd run lint` memeriksa 2 file tanpa temuan.

## D. Git
- Branch: `main` (tidak membuat branch baru).
- Ringkasan commit terakhir yang terdeteksi: `ba81ebf` — Perbaikan perhitungan total harga pada `calculateTotal` agar mempertimbangkan jumlah produk.
- Hasil pemeriksaan `git status`: Saat diperiksa, hanya `LAPORAN_UJIAN.md` berstatus berubah (`M`); pembaruan laporan ini belum di-commit.

## E. Pemakaian kecerdasan buatan (jika digunakan)
- Nama alat: GitHub Copilot.
- Pertanyaan/instruksi yang diberikan: Menelusuri penyebab dan memperbaiki masalah daftar produk, tombol keranjang, serta total belanja secara bertahap; mencatat bukti dan hasil ke laporan.
- Bagian jawaban yang diterapkan: Penyesuaian endpoint API, selector tombol, rumus total berdasarkan kuantitas, dan rangkuman hasil pada laporan.
- Cara memeriksa apakah saran tersebut benar: Memeriksa route server dan respons API, mensimulasikan klik tombol, menjalankan `npm.cmd run test:once` (7/7 lulus), dan `npm.cmd run lint`.

## F. Refleksi singkat
- Satu pelajaran paling penting dari ujian ini: Gunakan bukti dari kode dan pengujian untuk menemukan penyebab, perbaiki satu masalah pada satu waktu, lalu uji kembali hasilnya.
