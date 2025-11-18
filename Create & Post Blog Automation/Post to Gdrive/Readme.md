# workflow_automation_create_blog_and_post_to_google_drive

# 🤖 n8n Workflow: Auto Blog Generator & Save to Google Drive

Workflow ini adalah otomatisasi menggunakan **n8n** dan **Google Gemini AI** untuk membuat artikel blog secara otomatis, lalu menyimpannya langsung ke **Google Drive pribadi**.

---

## 1. Fitur Utama

1. User mengisi form dengan judul/topik artikel.  
2. Workflow meminta **Gemini AI** untuk:  
   - Membuat **topik** sesuai judul.  
   - Menyusun **outline** artikel.  
   - Mengembangkan **konten lengkap** berdasarkan outline.  
3. Artikel yang sudah dibuat otomatis **disimpan ke Google Drive** sebagai file teks.  

---

## 2. Persiapan

Sebelum menggunakan workflow ini, pastikan Anda sudah memiliki:  

1. Akun n8n (self-hosted atau cloud).  
2. API Key **Google Gemini AI** (buat di [Google AI Studio](https://aistudio.google.com/)).  
3. Akses API **Google Drive** (atur di [Google Cloud Console](https://console.cloud.google.com/)).  

---

## 3. Import Workflow

1. Download file JSON workflow dari folder `workflows/`.  
2. Buka n8n.  
3. Pilih **Import from File** dan masukkan file JSON tersebut.  

---

## 4. Konfigurasi Credential

Buat credential berikut di n8n:  

1. **Google Gemini API** → masukkan API key dari Google AI Studio.  
2. **Google Drive API** → hubungkan akun Google pribadi Anda untuk menyimpan artikel.  

---

## 5. Jalankan Workflow

1. User mengisi form dengan judul artikel.  
2. Workflow akan otomatis memproses:  
   - Generate topik dari judul.  
   - Buat outline artikel.  
   - Buat konten lengkap artikel.  
3. Artikel akan otomatis **tersimpan ke Google Drive** sesuai folder yang sudah ditentukan.  

---

## 6. Struktur Repo

1. `workflows/` → berisi file JSON export dari n8n.  
2. `docs/` → dokumentasi tambahan jika diperlukan.  
3. `README.md` → penjelasan project.  

---

## 7. Catatan

1. API key dan credential tidak disimpan di workflow JSON.  
   Anda perlu membuat credential baru di n8n masing-masing.  
2. Artikel akan tersimpan di Google Drive sesuai pengaturan folder pada node Google Drive.  
3. Format file bisa diatur (misalnya `.txt`, `.md`, atau `.docx`).  

---

## 8. Teknologi yang Digunakan

1. [n8n](https://n8n.io) → workflow automation  
2. [Google Gemini](https://ai.google.dev) → AI untuk generate topik, outline, dan konten  
3. [Google Drive API](https://console.cloud.google.com/) → penyimpanan artikel di Google Drive pribadi

