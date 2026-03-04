# Test Repo
TUGAS 1 — Deteksi Anomali Data
a.no_bpjs NULL

Masalah:
Terdapat beberapa pasien yang tidak memiliki nomor BPJS (nilai NULL).

Mengapa ini anomali:

Nomor BPJS merupakan identitas penting dalam sistem rumah sakit.

Data yang kosong menyebabkan informasi tidak lengkap.

Berpotensi mengganggu proses klaim asuransi dan pelaporan.

Dampak:

Gagal klaim BPJS.

Data pasien tidak valid untuk kebutuhan administratif.

Laporan pasien BPJS menjadi tidak akurat.

Solusi Perbaikan:

Validasi input agar no_bpjs wajib diisi jika pasien menggunakan BPJS.

Tambahkan constraint NOT NULL (jika memang wajib).

Lakukan pengecekan di level aplikasi sebelum menyimpan data.

b. no_bpjs Duplikat

Masalah:
Terdapat nomor BPJS yang digunakan oleh lebih dari satu pasien.

Mengapa ini anomali:

Nomor BPJS bersifat unik (unique identifier).

Satu nomor tidak boleh dimiliki oleh dua pasien berbeda.

Dampak:

Riwayat medis bisa tercampur.

Klaim asuransi dapat salah orang.

Pelanggaran integritas data.

Potensi masalah hukum.

Solusi Perbaikan:

Tambahkan constraint UNIQUE pada kolom no_bpjs.

Bersihkan data duplikat dengan verifikasi manual.

Tambahkan validasi di aplikasi agar tidak bisa memasukkan BPJS yang sudah terdaftar.

c. tgl_lahir Tidak Valid (Masa Depan)

Masalah:
Terdapat tanggal lahir yang lebih besar dari tanggal hari ini.

Mengapa ini anomali:

Secara logika, tidak mungkin seseorang lahir di masa depan.

Menunjukkan tidak adanya validasi input.

Dampak:

Perhitungan umur menjadi negatif.

Statistik demografi menjadi tidak akurat.


TUGAS 2 — Perbaikan N+1 Query
📌 Identifikasi Masalah

Masalah terjadi ketika sistem mengambil data rekam_medis, lalu di dalam loop melakukan query tambahan untuk mengambil data dokter.

Ini menyebabkan pola:

1 query utama + N query tambahan

Jika terdapat 70 data rekam medis, maka:

1 query ambil rekam medis

70 query ambil dokter

Total = 71 query

Sistem asuransi atau laporan bisa error.

Solusi Perbaikan:

Tambahkan validasi bahwa tgl_lahir tidak boleh melebihi tanggal saat ini.

Tambahkan CHECK constraint (jika DB mendukung).

Validasi di sisi aplikasi sebelum penyimpanan data.

TUGAS 3 — Query Laporan Agregasi
📌 Kebutuhan Laporan

Menampilkan:

Nama dokter

Jumlah pasien unik

Total kunjungan

Total biaya

Diurutkan dari total biaya tertinggi

📌 Konsep yang Digunakan

JOIN → Menghubungkan rekam_medis dengan dokter

COUNT(DISTINCT) → Menghitung jumlah pasien unik

COUNT() → Menghitung total kunjungan

SUM() → Menghitung total biaya

GROUP BY → Mengelompokkan per dokter

ORDER BY → Mengurutkan berdasarkan total biaya

📌 Tujuan Laporan

Mengetahui dokter dengan kontribusi biaya tertinggi.

Menganalisis beban kerja dokter.

Membantu manajemen dalam pengambilan keputusan.

Mendukung evaluasi performa.
