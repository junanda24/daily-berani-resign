# Proposal: Berani Resign?

## Apa & kenapa

"Berani Resign?" adalah web app client-side (tanpa login, tanpa backend, tanpa
data yang dikirim ke mana pun) yang menjawab pertanyaan yang diam-diam dipikirkan
banyak pekerja Indonesia setiap Senin pagi: **kalau aku resign sekarang, uangku
bertahan berapa lama?**

Pengguna memasukkan tabungan yang siap dipakai, pengeluaran bulanan, pemasukan
sampingan (bila ada), dan tanggungan. Aplikasi menghitung:

1. **Runway** — berapa bulan uang bertahan (tabungan ÷ defisit bulanan) plus
   tanggal kira-kira uang habis.
2. **Target dana darurat** — kelipatan pengeluaran sesuai tanggungan, mengacu
   panduan umum literasi keuangan (OJK: 3–6x untuk lajang; panduan perencana
   keuangan: 6x menikah tanpa anak, 9x satu anak, 12x dua anak/freelance).
3. **Skor kesiapan** — checklist 8 kesiapan non-angka (pemasukan pengganti,
   asuransi/BPJS mandiri, utang terkendali, tawaran atau pipeline, rencana
   3 bulan, dll) yang menghasilkan verdict jujur.
4. **Simulasi** — slider pangkas pengeluaran dan target nabung bulanan: berapa
   bulan lagi sampai target dana darurat tercapai.
5. **Twist (momen delight)** — begitu verdict keluar, aplikasi menyusun draf
   surat pengunduran diri berbahasa Indonesia formal yang sopan, tinggal salin
   (nama, perusahaan, tanggal terakhir kerja bisa diedit). Dari kalkulator
   menjadi "suratnya sudah jadi" — itulah momen "wah, kok kepikiran sih".

## Kenapa ide ini mengejutkan

Kalkulator finansial biasanya membosankan dan generik. Yang ini berani masuk ke
keputusan hidup yang emosional — resign — dan menutupnya dengan artefak nyata
(surat resign) yang biasanya baru dicari orang setelah keputusannya bulat.
Sudut pandangnya provokatif tapi jujur: verdict "Jangan dulu" sama pentingnya
dengan "Gas", dan semua angka ditampilkan sebagai estimasi, bukan janji.

## Kenapa bentuk output ini

Web app static client-side. Hitungannya ringan (pembagian dan perkalian),
tidak butuh data live, tidak butuh akun, dan privasi adalah fitur: angka gaji
dan tabungan orang tidak boleh transit ke server mana pun. Backend hanya akan
menambah risiko privasi tanpa menambah nilai.

## Kenapa tidak pakai backend

Tidak ada data yang perlu disimpan bersama, tidak ada API berbayar, tidak ada
state server. Semua state hidup di browser dan hilang saat reload (sesuai
sifat artifact static) — itu disengaja dan dinyatakan di halaman.

## Anti-AI-slop

Copy memakai Bahasa Indonesia sehari-hari yang natural ("uangmu habis sekitar
bulan…", bukan "optimalkan runway finansial Anda"). Tidak ada emoji di label
fungsional, tidak ada lorem ipsum, tidak ada angka contoh yang diklaim sebagai
data nyata.

## IP check

Semua aset original (CSS + teks). Tidak ada gambar, logo, atau karakter pihak
ketiga. Tidak perlu disclaimer fan-made.

## Kepatuhan

Mengikuti `CODE_STANDARDS.md` dan `ARCHITECTURE.md` bagian web artifact static:
satu objek state, data terpisah dari logika, render murni dari state, handler
tipis, tidak ada god component, tidak ada secret (tidak ada secret sama sekali).
