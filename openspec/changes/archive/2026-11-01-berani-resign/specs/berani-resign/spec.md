# Spec: Berani Resign?

## Requirements

### R1 — Input keuangan

- SHALL menerima: tabungan siap pakai (Rp), pengeluaran wajib bulanan (Rp),
  pemasukan sampingan/pasif bulanan (Rp, boleh 0), dan profil tanggungan
  (lajang / menikah tanpa anak / menikah + 1 anak / menikah + 2 anak atau lebih
  / freelance).
- WHEN input kosong atau bukan angka positif THEN aplikasi menampilkan pesan
  yang jelas dan TIDAK menampilkan hasil (tidak ada NaN/Infinity di layar).

### R2 — Runway

- SHALL menghitung defisit bulanan = pengeluaran − pemasukan sampingan.
- WHEN defisit > 0 THEN runway (bulan) = tabungan ÷ defisit, ditampilkan dalam
  bulan (1 desimal) beserta tanggal kira-kira uang habis (bulan berjalan +
  runway, dibulatkan ke bulan).
- WHEN defisit ≤ 0 (pemasukan sampingan menutup pengeluaran) THEN aplikasi
  menyatakan runway "tidak terbatas dari sisi arus kas" dan menjelaskan
  alasannya, bukan menampilkan angka tak hingga.

### R3 — Target dana darurat

- SHALL memakai kelipatan: lajang 6x, menikah tanpa anak 6x, menikah + 1 anak
  9x, menikah + 2 anak atau lebih 12x, freelance 12x (rentang panduan umum
  3–12x; nilai yang dipakai adalah ujung atas yang konservatif per profil,
  dan halaman menjelaskannya).
- SHALL menampilkan target (Rp), selisih terhadap tabungan (kurang/lebih),
  dan persentase tercapai.

### R4 — Skor kesiapan & verdict

- SHALL menyediakan checklist 8 kesiapan (dana darurat mencapai target;
  ada pemasukan pengganti; ada tawaran kerja/freelance pipeline; BPJS/asuransi
  mandiri siap; cicilan/utang terkendali; skill atau portofolio siap jual;
  rencana konkret 3 bulan pertama; dukungan keluarga/pasangan).
  Item pertama tercentang otomatis dari hasil R3; sisanya dicentang manual.
- SHALL menghitung skor = item tercentang ÷ 8 dalam persen.
- SHALL menampilkan verdict gabungan dari runway + skor:
  - runway < 3 bulan ATAU skor < 40% → "Jangan dulu" (merah)
  - runway 3–6 bulan → "Napas pendek — siapin dulu" (kuning)
  - runway 6–12 bulan dan skor ≥ 60% → "Siap, dengan rencana" (hijau muda)
  - runway ≥ 12 bulan dan skor ≥ 60% → "Gas, tapi tetap pakai rencana" (hijau)
  - Bila runway dan skor memberi sinyal berlawanan, verdict memakai yang
    paling konservatif dan menjelaskannya dalam satu kalimat.

### R5 — Simulasi

- SHALL menyediakan slider pangkas pengeluaran (0–50%) yang menghitung ulang
  runway secara live.
- SHALL menyediakan input "nabung Rp X per bulan" yang menghitung berapa bulan
  sampai target dana darurat tercapai (bila sudah tercapai, menyatakan
  "target sudah tercapai").

### R6 — Draf surat resign (delight)

- SHALL menghasilkan draf surat pengunduran diri Bahasa Indonesia formal dan
  sopan dari input nama, perusahaan, dan tanggal terakhir kerja (default:
  30 hari dari hari ini).
- WHEN pengguna menekan "Salin surat" THEN teks surat disalin ke clipboard dan
  tombol memberi konfirmasi visual ("Tersalin!").
- SHALL menyatakan jelas bahwa surat ini draf yang perlu disesuaikan (cek
  kontrak, masa notice, dan aturan perusahaan).

### R7 — Transparansi & privasi

- SHALL menampilkan disclaimer: hasil adalah estimasi edukasi, bukan saran
  finansial profesional; angka tidak disimpan atau dikirim ke mana pun.
- SHALL bekerja penuh tanpa jaringan setelah halaman dimuat (tidak ada fetch
  eksternal untuk logika inti).

### R8 — Kualitas

- SHALL mobile-friendly (nyaman di lebar 360px), semua tombol berfungsi,
  tidak ada teks placeholder, tidak ada error console pada alur utama.
- SHALL memakai Bahasa Indonesia natural di semua copy.
