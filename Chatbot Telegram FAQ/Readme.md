# workflow_chatbot_faq_telegram_for_school using n8n


# 📚 Chatbot Telegram FAQ Sekolah (n8n + Gemini)

Workflow ini adalah chatbot Telegram berbasis n8n yang menjawab pertanyaan seputar:
- 📖 Peraturan sekolah (guru, siswa, dan staff)
- 📚 Peminjaman buku di perpustakaan sekolah

Chatbot menggunakan Google Gemini AI untuk membaca file peraturan dari Google Drive dan memberikan jawaban sesuai pertanyaan user.

---

## 🚀 Cara Menggunakan

### 1. Persiapan
Sebelum mengimpor workflow ini, pastikan Anda sudah memiliki:
- Akun n8n (self-hosted atau cloud).
- Bot Telegram (buat via [BotFather](https://core.telegram.org/bots#botfather)).
- API Key Google Gemini AI (buat di [Google AI Studio](https://aistudio.google.com/)).
- File peraturan sekolah yang tersimpan di Google Drive.

---

### 2. Import Workflow
1. Download file JSON workflow dari repo ini (folder `workflows/`).
2. Buka n8n.
3. Pilih Import from File dan masukkan file JSON tersebut.

---

### 3. Konfigurasi Credential
Buat credential berikut di n8n:

- Telegram API
  - Gunakan token bot dari BotFather.
- Google Gemini API
  - Masukkan API key Gemini.
- Google Drive
  - Hubungkan dengan akun Google tempat file peraturan sekolah disimpan.

---

### 4. Jalankan Workflow
- Aktifkan workflow di n8n.
- Chatbot Telegram akan otomatis merespons pertanyaan dari user:
  - Guru, siswa, atau staff bisa menanyakan aturan & hukuman.
  - User bisa menanyakan status atau prosedur peminjaman buku perpustakaan.

---

## 📂 Struktur Repo
- `workflows/` → file JSON export dari n8n.
- `docs/` → dokumentasi tambahan jika diperlukan.
- `README.md` → penjelasan project.

---

## ✨ Catatan
- API key dan credential tidak disimpan di workflow JSON.  
  Anda perlu membuat credential baru di n8n masing-masing.  
- Pastikan file peraturan di Google Drive bisa diakses oleh akun yang digunakan di n8n.  

---

## 🛠 Teknologi yang Digunakan
- [n8n](https://n8n.io) → workflow automation
- [Telegram Bot API](https://core.telegram.org/bots/api) → chatbot
- [Google Gemini](https://ai.google.dev) → AI untuk memahami & menjawab pertanyaan
- [Google Drive API](https://developers.google.com/drive) → penyimpanan file peraturan

