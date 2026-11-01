# Design: Berani Resign?

## Stack

Web artifact static: satu halaman interaktif client-side (HTML + CSS + JS
yang dibangun oleh artifact builder dari brief ini). Tanpa backend, tanpa
database, tanpa login, tanpa fetch runtime.

## Struktur (mengikuti ARCHITECTURE.md §1, web artifact static)

- `index.html` — struktur + mounting point
- `styles.css` — design token `:root` → komponen → responsive
- `app.js` — pola baku: STATE (satu objek) → DATA (konstanta, kelipatan
  dana darurat, 8 item checklist, template surat) → RENDER (fungsi murni
  state → DOM) → EVENTS (handler tipis) → INIT

Tidak ada import antar-fitur (bukan React), tidak ada god component, tidak
ada secret.

## Keranjang state (lima keranjang ARCHITECTURE.md, dipetakan ke artifact static)

- Lokal: semua input form, checklist, slider simulasi (satu objek state).
- URL: tidak dipakai (angka finansial sensitif tidak boleh masuk URL).
- Server state: tidak ada (tanpa backend).
- Global client UI: status salin ("Tersalin!") dan verdict aktif.
- Form: input angka Rupiah dengan pemformatan ribuan saat diketik.

## Desain visual (mode Operate, prinsip local-impeccable)

- Satu kolom mobile-first, kartu-kartu yang bisa dipindai cepat; hasil
  (runway besar) adalah hierarki pertama, bukan form.
- Palet tegas: tinta gelap, kertas krem, satu aksen hijau untuk "siap" dan
  merah untuk "jangan dulu" — warna hanya sebagai sinyal status, bukan dekor.
- Tipografi besar untuk angka runway; format Rupiah Indonesia (Rp, pemisah
  titik).
- Momen delight: (1) bar runway animasi yang terisi sesuai bulan; (2) verdict
  tampil seperti stempel (cap) yang "ditekankan" dengan animasi scale-in;
  (3) draf surat muncul di kertas bergaris seperti surat sungguhan, dengan
  tombol salin yang memberi konfirmasi visual.
- Tanpa emoji di label fungsional. Copy Bahasa Indonesia natural.

## Animasi / interaksi

- Bar runway: transisi lebar CSS saat angka berubah.
- Verdict stamp: animasi scale + rotate kecil sekali saat verdict berubah.
- Salin surat: feedback instan, tanpa alert browser.
- Semua animasi menghormati `prefers-reduced-motion` (nonaktifkan animasi
  dekoratif bila diminta sistem).

## Edge cases

- Defisit ≤ 0 → runway tak terbatas (R2).
- Tabungan 0 → runway 0 bulan, verdict "Jangan dulu".
- Input negatif / kosong → pesan validasi, hasil disembunyikan.
- Tanggal habis dihitung dari bulan berjalan + runway (pembulatan ke bawah
  ke bulan penuh agar tidak memberi kesan lebih optimistis dari kenyataan).
