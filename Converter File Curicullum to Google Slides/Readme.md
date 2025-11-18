# 🚀 Excel to AI Slides Converter - IMPROVED

[](https://opensource.org/licenses/MIT)
[](https://n8n.io/)
[](https://developers.google.com/slides)
[](https://ai.google.dev/)

Alur kerja (workflow) n8n ini mengotomatiskan proses konversi data kurikulum dari *file* Excel menjadi *draft* presentasi Google Slides yang terstruktur dan menarik menggunakan model bahasa besar (LLM) Gemini. Cocok untuk tim pengajar, pengembang kurikulum, atau siapa pun yang perlu membuat materi presentasi cepat dari data terstruktur.

## ✨ Fitur Utama

  * **Pemicu *Form* Web:** Memungkinkan unggahan *file* Excel sederhana melalui antarmuka web.
  * **Penguraian Data Excel:** Secara otomatis membaca dan mengurai data kurikulum (Judul Modul, Tujuan Pembelajaran, Topik Utama, Aktivitas) dari *file* Excel.
  * **Pengelompokan Cerdas:** Mengelompokkan baris-baris Excel menjadi unit-unit modul yang koheren.
  * **Pembuatan *Prompt* AI:** Membuat *prompt* yang kaya konteks (menggunakan data modul) untuk Gemini.
  * **Generasi Konten AI dengan Struktur Ketat:** Menggunakan Gemini (melalui n8n LangChain Agent) dengan instruksi sistem terperinci untuk menghasilkan konten slide dalam format JSON terstruktur (termasuk judul, konten, dan saran gambar).
  * **Integrasi Google Slides:** Secara otomatis menduplikasi *template* Google Slides, membuat slide baru, dan mengisi konten yang dihasilkan AI menggunakan Google Slides API (via HTTP Request Node).
  * **Pemrosesan *Batch*:** Mampu memproses banyak modul sekaligus.

## 🛠️ Persyaratan

Untuk menjalankan alur kerja ini, Anda memerlukan:

1.  **Instalasi n8n** (self-hosted atau n8n Cloud).
2.  **Kredensial API:**
      * **Gemini API Key:** Untuk node `Gemini Model` dan node `AI Generate Slides`.
      * **Google Drive OAuth2 Credential:** Untuk node `Copy Template` (memerlukan scope Drive).
      * **Google Slides OAuth2 Credential:** Untuk node `Slides API` (memerlukan scope Google Slides).
3.  ***Template* Google Slides:** Anda harus memiliki *file* *template* presentasi Google Slides (misalnya, dengan slide cover yang memiliki placeholder `{title}` dan `{body}`). **Ganti `YOUR_TEMPLATE_FILE_ID`** di node `Copy Template` dengan ID *template* Anda.

## 📝 Format Excel Input

*File* Excel harus memiliki kolom-kolom berikut agar node `Group Modules` dapat bekerja dengan benar:

| Nama Kolom | Contoh Data | Deskripsi |
| :--- | :--- | :--- |
| **Judul Modul** | Modul 01: Pengenalan AI (Estimasi Waktu: 4 Jam) | Digunakan untuk judul dan penentuan nomor modul. |
| **Tujuan Pembelajaran** | • Peserta didik dapat mengidentifikasi konsep dasar AI. • Mampu menjelaskan perbedaan Machine Learning dan Deep Learning. | Poin-poin tujuan yang akan dimasukkan ke *prompt* AI. |
| **Topik Utama** | Pengenalan AI Generatif; Arsitektur Model LLM; Etika dalam Pengembangan AI. | Topik yang akan dikembangkan menjadi slide konten. |
| **Aktivitas Praktis/Penilaian** | Mini project: Buat chatbot sederhana dengan RAG. | Poin-poin aktivitas/penilaian. |

## ⚙️ Struktur Alur Kerja (Workflow Architecture)

Alur kerja ini terdiri dari beberapa tahap kunci:

| \# | Node (Nama) | Tipe | Keterangan Fungsi Utama |
| :-: | :--- | :--- | :--- |
| 1 | **Form Upload** | `formTrigger` | Memicu alur kerja dan menerima *file* Excel. |
| 2 | **Parse Excel** | `spreadsheetFile` | Mengurai *file* Excel biner menjadi JSON baris-per-baris. |
| 3 | **Group Modules** | `code` | **Logika Inti:** Mengelompokkan data baris berdasarkan kolom `Judul Modul` dan membersihkan/menyaring poin-poin. |
| 4 | **Loop Modules** | `splitInBatches` | Memulai perulangan untuk setiap modul yang terdeteksi. |
| 5 | **Build Prompt** | `code` | Membuat *prompt* instruksi Gemini terperinci dalam format Markdown. |
| 6 | **AI Generate Slides** | `@n8n/n8n-nodes-langchain.agent` | Memanggil model **Gemini 2.0 Flash (exp)** untuk menghasilkan JSON slide berdasarkan *System Prompt* yang ketat. |
| 7 | **Parse Output** | `code` | Membersihkan *output* JSON dari Gemini dan menangani potensi kesalahan *parsing*. |
| 8 | **Copy Template** | `googleDrive` | Menduplikasi *Template* Google Slides untuk setiap modul. |
| 9 | **Merge Data** | `code` | Menggabungkan ID Presentasi baru dengan data slide. |
| 10 | **Batch Create** | `code` | **Logika Inti Slides API:** Membuat array `requests` JSON untuk Google Slides API (untuk *batch* membuat slide dan mengisi teks). |
| 11 | **Slides API** | `httpRequest` | Melakukan panggilan `presentations:batchUpdate` ke Google Slides API. |
| 12 | **Log Success** | `code` | Mencatat URL presentasi yang berhasil. |
| 13 | **Wait** | `wait` | Menunggu hingga semua perulangan selesai (diperlukan untuk *batching*). |
| 14 | **Final Report** | `code` | Mengumpulkan hasil dari semua modul dan menghasilkan laporan akhir. |

## 💡 System Prompt Gemini (Aturan Konten)

*System Prompt* di node **AI Generate Slides** sangat ketat untuk memastikan *output* yang konsisten.

Beberapa aturan penting yang ditetapkan:

  * **STRUKTUR WAJIB:** Meliputi *Cover*, *Profile Mentor*, *Tujuan Pembelajaran*, *Konten* (dengan pola Header → Konsep → Detail), *Diskusi*, *Mini Project*, *Rubrik*, *Checklist*, *Referensi*, dan *Penutup*.
  * **PANJANG BODY KETAT:** Maksimal **200-400 karakter** per slide untuk menghindari teks padat.
  * **FORMAT KRITIS:** HANYA menggunakan **PLAIN TEXT** (tanpa markdown seperti `**`, `*`, `_`, `\`) dan menggunakan simbol bullet **•** saja.
  * **OUTPUT FORMAT:** HARUS mengembalikan **HANYA JSON** tanpa *backticks* (dikelola oleh Structured Output Parser).

-----

## 💻 Instalasi dan Penggunaan

### 1\. Impor Alur Kerja

1.  Buka antarmuka n8n Anda.
2.  Impor *file* `Converter File to Google Slides.json` yang telah Anda unduh.

### 2\. Konfigurasi Kredensial

Ganti *placeholder* kredensial dengan ID kredensial Anda yang sebenarnya:

  * Node **Gemini Model**
      * `YOUR_GEMINI_CREDENTIAL_ID`
  * Node **Copy Template**
      * `YOUR_DRIVE_CREDENTIAL_ID`
      * Ganti `YOUR_TEMPLATE_FILE_ID` dengan ID Presentasi *Template* Google Slides Anda.
  * Node **Slides API**
      * `YOUR_SLIDES_CREDENTIAL_ID`

### 3\. Eksekusi

1.  Aktifkan (Activate) alur kerja di n8n.
2.  Akses URL Webhook yang dihasilkan oleh node **Form Upload** (`/webhook/excel-slides-converter`).
3.  Unggah *file* Excel kurikulum Anda dan kirimkan formulir.
4.  Alur kerja akan berjalan, dan setelah selesai, node **Final Report** akan menampilkan ringkasan presentasi yang dibuat, termasuk URL Presentasi Google Slides baru.

-----

## ⚖️ Lisensi

Proyek ini dilisensikan di bawah **Lisensi MIT** - lihat *file* [LICENSE](https://www.google.com/search?q=LICENSE) untuk detailnya.

-----

## 🤝 Kontribusi

Saran dan kontribusi selalu diterima\! Silakan ajukan *Pull Request* atau *Issue* jika Anda memiliki perbaikan atau penemuan *bug*.

-----

Apakah Anda ingin saya menambahkan bagian tertentu atau mengubah fokus dari draf README ini?
