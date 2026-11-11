# Tanya Fiqh Sunnah – Versi AI Live (Gemini, hybrid)

Cara kerja:
1. Pertanyaan dicocokkan dulu dengan **basis data terverifikasi** (17 topik) di frontend.
2. Kalau tidak ada yang cocok, atau tombol **🤖 Tanya AI** ditekan, pertanyaan dikirim ke backend `/api/ask`.
3. Backend menambahkan aturan ketat (hanya Al-Qur'an, hadits shahih/hasan, manhaj salaf, jangan mengarang dalil) lalu memanggil **Google Gemini API** secara streaming.
4. Jawaban AI selalu diberi label "belum diverifikasi ulama" dan tautan rujukan.

## Dapatkan API key gratis
1. Buka https://aistudio.google.com/apikey lalu login dengan akun Google.
2. Buat API key, salin ke `.env`.

## Menjalankan di komputer
Butuh Node.js 20.6 atau lebih baru.

```bash
npm install
cp env.example .env      # lalu isi GEMINI_API_KEY
npm run dev
```
Buka http://localhost:3000

## Deploy
Cocok di Render, Railway, Fly.io, atau VPS yang menjalankan Node.js.
- Build command: `npm install`  |  Start command: `npm start`
- Isi environment variable `GEMINI_API_KEY` (opsional: `MODEL`, `RATE_LIMIT`, `DAILY_CAP`) di dashboard hosting.
- Pakai HTTPS. Jangan taruh API key di file HTML.

## Hal penting soal paket gratis
- **Batas gratis berubah-ubah.** Lihat batas terbaru proyek Anda di Google AI Studio (halaman rate limit). Atur `DAILY_CAP` dan `RATE_LIMIT` di `.env` di bawah batas itu. Jika kuota habis, website menampilkan pesan sopan.
- **Nama model bisa berubah.** Default `gemini-2.5-flash`. Kalau model diganti atau dihentikan Google, ubah `MODEL` di `.env` sesuai daftar di AI Studio.
- **Privasi:** pada paket gratis, menurut ketentuan Google, isi pertanyaan dapat dipakai untuk meningkatkan produk Google. Beri tahu pengunjung agar tidak menulis data pribadi di pertanyaan.
- Pembatas per IP tersimpan di memori server, jadi reset saat server restart.

## Memperbarui basis data terverifikasi
Edit array `DB` di `public/index.html`. Tambahkan entri hanya setelah dalil dan nomor haditsnya dicek ke kitab atau Dorar.net.

## Catatan penting
AI bisa keliru mengutip walau sudah diberi aturan ketat, dan model gratis cenderung lebih rawan daripada yang besar. Karena itu jawaban AI diberi label dan peringatan. Sebaiknya ada ustadz yang mereview secara berkala.
