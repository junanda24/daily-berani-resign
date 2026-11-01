# Berani Resign?

**Kalau kamu resign sekarang, uangmu bertahan berapa lama?** "Berani Resign?"
menjawab pertanyaan itu dengan jujur: hitung runway dari tabungan dan
pengeluaranmu, bandingkan dengan target dana darurat, nilai kesiapanmu lewat
checklist, lalu — kalau verdictnya keluar — terima draf surat pengunduran diri
yang tinggal salin. Dibuat untuk pekerja Indonesia yang tiap Senin pagi
diam-diam memikirkan hal yang sama.

Bagian dari program **1 Hari 1 Project** (1 November 2026). Web app static,
100% client-side: tanpa login, tanpa backend, tanpa data yang dikirim ke mana
pun. Angka gaji dan tabunganmu tidak pernah meninggalkan perangkatmu.

## Kenapa ide ini dipilih

Kalkulator finansial biasanya membosankan dan generik. Yang ini berani masuk
ke keputusan hidup yang emosional — resign — dan menutupnya dengan artefak
nyata: draf surat resign. Verdict "Jangan dulu" sama pentingnya dengan "Gas",
karena kejujuran itulah yang membuat alat ini bisa dipercaya. Efek kejutnya:
dari kalkulator menjadi "suratnya sudah jadi" dalam satu alur.

## Fitur

- **Input Rupiah berformat** — tabungan siap pakai, pengeluaran wajib bulanan,
  pemasukan sampingan/pasif (boleh 0), dan profil tanggungan (Lajang / Menikah
  tanpa anak / Menikah + 1 anak / Menikah + 2 anak atau lebih / Freelance).
- **Runway** — defisit bulanan = pengeluaran − pemasukan sampingan; runway =
  tabungan ÷ defisit (1 desimal) plus perkiraan bulan uang habis. Bila defisit
  ≤ 0, aplikasi menyatakan runway tidak terbatas dari sisi arus kas beserta
  alasannya (bukan angka tak hingga).
- **Target dana darurat** — kelipatan pengeluaran: Lajang 6x, Menikah tanpa
  anak 6x, Menikah + 1 anak 9x, Menikah + 2 anak atau lebih 12x, Freelance 12x
  (ujung atas yang konservatif dari panduan umum 3–12x; panduan OJK menyebut
  3–6x untuk lajang). Ditampilkan target (Rp), selisih, dan persentase
  tercapai.
- **Skor kesiapan** — checklist 8 item (dana darurat mencapai target, terisi
  otomatis; pemasukan pengganti; tawaran/pipeline; BPJS-asuransi mandiri;
  utang terkendali; skill/portofolio siap jual; rencana 3 bulan; dukungan
  keluarga). Skor = item tercentang ÷ 8.
- **Verdict gaya stempel** — "Jangan dulu" (runway < 3 bulan atau skor < 40%),
  "Napas pendek — siapin dulu" (3–6 bulan), "Siap, dengan rencana" (6–12 bulan
  dan skor ≥ 60%), "Gas, tapi tetap pakai rencana" (≥ 12 bulan dan skor
  ≥ 60%). Bila sinyal berlawanan, yang paling konservatif menang dan
  dijelaskan dalam satu kalimat.
- **Simulasi live** — slider pangkas pengeluaran 0–50% yang menghitung ulang
  runway, dan input "nabung Rp X per bulan" yang menghitung berapa bulan
  sampai target dana darurat tercapai.
- **Draf surat resign** — surat pengunduran diri Bahasa Indonesia formal dan
  sopan di atas kertas bergaris, dari nama, perusahaan, dan tanggal terakhir
  kerja (default 30 hari dari hari ini). Tombol "Salin surat" menyalin teks
  dan menampilkan "Tersalin!".
- **Bar runway animasi** dan stempel verdict dengan animasi scale-in;
  menghormati `prefers-reduced-motion`.

## Cara pakai (untuk orang awam)

1. Buka aplikasinya di browser HP atau laptop.
2. Isi tabungan yang siap dipakai, pengeluaran wajib tiap bulan, pemasukan
   sampingan (kalau ada), dan profil tanggunganmu.
3. Baca hasil: berapa bulan uangmu bertahan, target dana daruratmu, dan
   verdictnya.
4. Centang checklist kesiapan sejujur-jujurnya — skor dan verdict akan ikut
   berubah.
5. Mainkan slider pangkas pengeluaran dan rencana nabung untuk melihat
   skenario "kalau aku lebih hemat / nabung segini".
6. Kalau sudah yakin, isi nama dan perusahaan di bagian surat, lalu tekan
   "Salin surat" dan tempel di email atau dokumenmu. Sesuaikan dulu dengan
   kontrak, masa notice, dan aturan perusahaanmu.

## Cara menjalankan dari source

Tidak perlu build step. File hasil export artifact ada di `src/index.html`
(satu file HTML mandiri). Jalankan server statis apa pun dari folder project,
misalnya:

```bash
cd src
python3 -m http.server 8080
```

Lalu buka `http://localhost:8080` di browser. Atau cukup buka file
`src/index.html` langsung — semua logika berjalan di browser tanpa jaringan.

## Tech stack

- HTML + CSS + JavaScript client-side (hasil export web artifact static Muse)
- Tanpa framework, tanpa backend, tanpa database, tanpa dependency
- Penyimpanan: tidak ada (sengaja — angka finansial tidak disimpan)

## Struktur folder

```
2026-11-01-berani-resign/
├── README.md                 # dokumen ini
├── .gitignore
├── src/
│   └── index.html            # aplikasi lengkap (export artifact)
└── openspec/changes/archive/2026-11-01-berani-resign/
    ├── proposal.md
    ├── specs/berani-resign/spec.md
    ├── design.md
    └── tasks.md
```

## Link hasil

- Aplikasi: artifact web static `berani-resign` (dibuka lewat kartu artifact
  di aplikasi Muse; tidak di-deploy ke Vercel — keputusan deploy ada di Junan)
- Repo: https://github.com/junanda24/daily-berani-resign
- Tanggal rilis: 2026-11-01

## Catatan / temuan saat build

- **Keputusan penting — kelipatan konservatif.** Panduan umum dana darurat
  adalah rentang (3–12x). Aplikasi memakai ujung atas per profil (6/9/12x)
  agar verdict tidak memberi rasa aman palsu, dan menjelaskannya di halaman.
  Pengguna yang lajang dan ingin patokan minimal bisa memakai angka 3x
  sebagai target tahap pertama.
- **Tanggal habis dibulatkan ke bawah** ke bulan penuh, supaya tidak terkesan
  lebih optimistis dari kenyataan.
- **Yang sengaja tidak dibuat:** login/penyimpanan (privasi adalah fitur),
  backend (tidak ada nilai tambah), dan saran finansial personal (hasil
  dinyatakan jelas sebagai estimasi edukasi, bukan saran profesional).
- **Verifikasi build (audit builder):** 0 console error, 0 overflow di lebar
  390px. Probe langsung: Rp 12.000.000 / Rp 5.000.000 / Rp 1.000.000 →
  defisit Rp 4.000.000, runway 3,0 bulan, habis sekitar Februari 2027, target
  Rp 30.000.000 (6x, Lajang), 40% tercapai, kurang Rp 18.000.000, verdict
  "Jangan dulu"; mencentang 1 item → skor 12,5%; slider 25% → runway simulasi
  4,4 bulan; nabung Rp 1.500.000/bulan → 12 bulan sampai target (November
  2027); tombol salin berubah menjadi "Tersalin!". Dua hal yang tidak
  ter-cover probe langsung dan dicatat jujur: isi clipboard tidak dibaca
  balik di sesi audit, dan kasus defisit ≤ 0 (runway tak terbatas)
  diverifikasi dari logika kode, bukan lewat probe.
- **Font Google** terblokir hanya oleh lockdown egress di sesi audit; di
  halaman terbit font akan termuat (fallback sistem tetap terbaca di audit).
