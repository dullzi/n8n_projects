# workflow_automation_create_blog_and_post_to_dev.to

# 🤖 n8n Workflow: Auto Blog Generator & Dev.to Poster

Workflow ini adalah otomatisasi menggunakan **n8n** dan **Google Gemini AI** untuk membuat artikel blog secara otomatis, lalu mempublikasikannya ke platform **Dev.to**.  

---

## 1. Fitur Utama

1. User mengisi form dengan judul/topik artikel.  
2. Workflow meminta **Gemini AI** untuk:  
   - Membuat **topik** sesuai judul.  
   - Menyusun **outline** artikel.  
   - Mengembangkan **konten lengkap** berdasarkan outline.  
3. Hasil artikel langsung **diposting otomatis ke Dev.to**.  

---

## 2. Persiapan

Sebelum menggunakan workflow ini, pastikan Anda sudah memiliki:  

1. Akun n8n (self-hosted atau cloud).  
2. API Key **Google Gemini AI** (buat di [Google AI Studio](https://aistudio.google.com/)).  
3. API Key **Dev.to** (buat melalui [Dev.to API Settings](https://dev.to/settings/account)).  

---

## 3. Import Workflow

1. Download file JSON workflow dari folder `workflows/`.  
2. Buka n8n.  
3. Pilih **Import from File** dan masukkan file JSON tersebut.  

---

## 4. Konfigurasi Credential

Buat credential berikut di n8n:  

1. **Google Gemini API** → masukkan API key dari Google AI Studio.  
2. **Dev.to API** → gunakan API key dari akun Dev.to Anda.  

---

## 5. Jalankan Workflow

1. User mengisi form dengan judul artikel.  
2. Workflow akan otomatis memproses:  
   - Generate topik dari judul.  
   - Buat outline artikel.  
   - Buat konten lengkap artikel.  
3. Artikel akan diposting otomatis ke **Dev.to** dengan judul sesuai input user.  

---

## 6. Struktur Repo

1. `workflows/` → berisi file JSON export dari n8n.  
2. `docs/` → dokumentasi tambahan jika diperlukan.  
3. `README.md` → penjelasan project.  

---

## 7. Catatan

1. API key dan credential tidak disimpan di workflow JSON.  
   Anda perlu membuat credential baru di n8n masing-masing.  
2. Artikel yang diposting bisa langsung tampil di akun Dev.to Anda.  
3. Sesuaikan format artikel (tags, publish status, dsb.) sesuai kebutuhan di node Dev.to.  

---

## 8. Teknologi yang Digunakan

1. [n8n](https://n8n.io) → workflow automation  
2. [Google Gemini](https://ai.google.dev) → AI untuk generate topik, outline, dan konten  
3. [Dev.to API](https://developers.forem.com/api) → auto publish artikel ke Dev.to  

