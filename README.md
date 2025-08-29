Buat sebuah bot Telegram dengan fitur sebagai berikut:

1. Fungsi Utama:
- Bot bisa menerima gambar tiket parlay dari user.
- Gunakan OCR untuk membaca data tiket secara akurat (odds, hasil W/WH/LH/D/L, dan jumlah taruhan).
- Hitung actual odds menggunakan aturan berikut (hanya proses di belakang layar, jangan tampilkan rumus):
  - W (Menang Penuh): Odds asli tanpa perubahan.
  - WH (Menang Setengah): Odds = ((Odds asli - 1) / 2) + 1
  - LH (Kalah Setengah): Odds = 0.5
  - D (Draw) Odds = 1 (tidak mempengaruhi perhitungan actual odds)
 - L (Kalah) : outputkan pesan tiket sudah kalah, proses berhenti.
- Kalikan semua odds yang sudah disesuaikan untuk mendapatkan actual odds dengan presisi penuh, lalu tampilkan hasil pembulatan 3 desimal.
- Hitung estimasi payout = taruhan × actual odds.
- Kirim hasil perhitungan ke admin atau user sesuai yang mengirim gambar tiket siapa dalam format yang jelas, rapi, dan sesuai contoh di bawah.

2. Format output bot:

PAR[REF TIKET]

No. Odds awal | W/L
2.240 W
1.630 W
2.270 W
1.710 W
2.010 WH

( Actual Odds )
2.240 × 1.630 × 2.270 × 1.710 × 1.505 = 21.324

( Estimasi Payout )
150.00 × 21.324 = 3,198.62

Note :
WH = Menang Setengah → Odds dihitung ((Odds - 1)/2 + 1)
LH = Kalah Setengah → Odds dihitung 0.5
D = Draw → Odds tidak dihitung
Estimasi payout sudah termasuk modal taruhan bosku


3. Fitur Admin dan User:
-Admin itu adalah telegram saya 
- User saat pertama kali chat bot wajib input password (3 kali kesempatan).
- Jika salah 3 kali, user diblokir, bot tidak merespon lagi dan mengirim pesan blokir dengan kontak admin.
- Admin mendapat notifikasi user yang diblokir.
- Admin bisa mengelola bot penuh.
- User hanya bisa kirim gambar tiket untuk dihitung.

4. Contoh alur:
User kirim gambar tiket → Bot minta password → User input password → Jika benar, proses tiket → Kirim hasil → Jika salah 3x, blokir user → Kirim pesan blokir ke user & admin.

5. Database:

Gunakan MongoDB atau PostgreSQL untuk:
Menyimpan data user (password, status login, status blokir).
Menyimpan logs interaksi (opsional).
Menyimpan data admin.

Pastikan bot aman dan scalable dengan manajemen user di database.

6. Pastikan bot mengenali odds dan status W/WH/LH/D/L secara akurat dari gambar tiket, dan gunakan rumus perhitungan actual odds yang sudah ditentukan tanpa menampilkan rumusnya.

7. Catatan tambahan:

Pastikan OCR dikalibrasi agar bisa mengenali format tiket dengan tepat (odds, kode W/WH/LH/D/L, dan bet amount).
Implementasikan validasi input password dan limit retry.
Format output harus rapi, mudah dibaca, dan sesuai contoh.
Pesan kesalahan jika tiket kalah (ada kode "L") agar user tahu tiketnya kalah.


