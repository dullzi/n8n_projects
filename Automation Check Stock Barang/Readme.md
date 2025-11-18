
# workflow_automation_check_inventory_product_-_chatbot_telegram_reminder using n8n

# 📦 Inventory Stock Checker & Telegram Reminder

## 1. Deskripsi
Workflow ini berfungsi untuk melakukan pengecekan stok barang yang tersimpan di Google Spreadsheet, lalu mengirimkan pengingat otomatis melalui **Telegram Bot** setiap hari pada jam 07:00 (kecuali hari Sabtu & Minggu).  
Tujuannya adalah agar admin atau staff gudang dapat langsung mengetahui stok barang yang berada di bawah batas minimal (*minimal stock*).

## 2. Alur Workflow
1. **Trigger Schedule**  
   - Workflow dijalankan secara otomatis setiap hari pukul **07:00 WIB**, kecuali weekend (Sabtu & Minggu).
2. **Ambil Data dari Google Spreadsheet**  
   - Data stok barang diambil dari spreadsheet yang berisi kolom seperti:
     - Nama Barang  
     - Stok Saat Ini  
     - Minimal Stok  
3. **Filter Barang di Bawah Minimal Stok**  
   - Workflow akan memfilter data untuk mendapatkan list barang yang stoknya lebih rendah dari minimal.
4. **Kirim Reminder ke Telegram**  
   - Daftar barang yang stoknya kurang dari minimal akan dikirim melalui **chatbot Telegram** kepada grup/akun terkait.

## 3. Komponen Workflow
1. **Schedule Trigger**  
   - Untuk menjalankan workflow otomatis setiap jam 07:00 (weekday).
2. **Google Sheets Node**  
   - Mengambil data stok barang dari spreadsheet.
3. **Function / IF Node**  
   - Mengecek kondisi apakah stok < minimal stok.
4. **Telegram Bot Node**  
   - Mengirimkan pesan ke Telegram dengan daftar barang yang stoknya kurang.

## 4. Persiapan
1. **Google Spreadsheet**  
   - Siapkan spreadsheet dengan format minimal:  
     - `Nama Barang`  
     - `Stok`  
     - `Minimal Stok`
2. **Google Cloud Console**  
   - Buat API Credential untuk mengakses Google Sheets dari n8n.
3. **BotFather (Telegram)**  
   - Buat bot di Telegram menggunakan [BotFather](https://t.me/BotFather).  
   - Simpan API Token dari bot yang dibuat.
   - Tambahkan bot ke grup/akun target dan berikan izin agar bisa mengirim pesan.

## 5. Cara Import
1. Download file JSON workflow ini.  
2. Masuk ke dashboard n8n.  
3. Klik **Import from File** dan pilih file JSON.  
4. Atur Credential untuk:
   - Google Sheets
   - Telegram Bot  
5. Simpan dan aktifkan workflow.

## 6. Catatan
- Pastikan server n8n berjalan 24/7 agar jadwal trigger bekerja.  
- Workflow hanya berjalan pada hari **Senin - Jumat**.  
- Format spreadsheet harus konsisten agar data bisa terbaca dengan baik.  

---
✨ Dengan workflow ini, manajemen stok lebih efisien karena admin gudang selalu mendapat pengingat otomatis sebelum stok benar-benar habis.
