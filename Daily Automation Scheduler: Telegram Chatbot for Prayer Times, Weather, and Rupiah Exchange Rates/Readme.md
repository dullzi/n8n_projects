# workflow_automation_schedule_Chatbot_Telegram_Harian-Jadwal-Sholat-Cuaca-Kurs-Rupiah-Harga-Bitcoin using n8n 

# 🕌 Telegram Chatbot Harian (Jadwal Sholat, Cuaca, Kurs Rupiah, Harga Bitcoin)

## 1. Deskripsi
Workflow ini berfungsi sebagai **chatbot Telegram otomatis** yang mengirimkan informasi penting setiap pagi, meliputi:
1. Jadwal Sholat harian  
2. Perkiraan Cuaca hari ini  
3. Nilai tukar Rupiah terhadap USD  
4. Harga terkini Bitcoin (BTC/IDR atau BTC/USD)

Pengiriman pesan dilakukan secara terjadwal pada pagi hari, sehingga pengguna langsung mendapatkan informasi utama untuk aktivitas sehari-hari.

## 2. Alur Workflow
1. **Trigger Schedule**  
   - Workflow dijalankan otomatis setiap pagi pada jam yang ditentukan (misal 06:00 WIB).
2. **Ambil Data Jadwal Sholat**  
   - Mengambil jadwal sholat harian berdasarkan lokasi tertentu.
3. **Ambil Data Cuaca**  
   - Mengambil data cuaca harian dari API cuaca.
4. **Ambil Kurs Rupiah – USD**  
   - Mengambil nilai tukar Rupiah terhadap USD dari API keuangan.
5. **Ambil Harga Bitcoin**  
   - Mengambil harga terkini Bitcoin dari API crypto.
6. **Format Pesan**  
   - Semua data dikompilasi menjadi 1 pesan ringkas & rapi.
7. **Kirim ke Telegram**  
   - Pesan dikirim ke akun/grup Telegram menggunakan bot.

## 3. Komponen Workflow
1. **Schedule Trigger** – untuk menjalankan workflow otomatis setiap pagi.  
2. **HTTP Request Node** – untuk mengambil data dari API:  
   - API Jadwal Sholat  
   - API Cuaca  
   - API Kurs Rupiah–USD  
   - API Bitcoin  
3. **Function / Set Node** – untuk memformat data menjadi pesan.  
4. **Telegram Bot Node** – untuk mengirimkan pesan ke Telegram.

## 4. Persiapan
1. **BotFather (Telegram)**  
   - Buat bot di Telegram melalui [BotFather](https://t.me/BotFather).  
   - Simpan API Token dari bot.  
   - Tambahkan bot ke grup/akun target & beri izin kirim pesan.  

2. **API Key**  
   - **Cuaca**: dapatkan API key dari [OpenWeather](https://openweathermap.org/api).  
   - **Kurs Rupiah–USD**: gunakan API keuangan (misal [ExchangeRate API](https://exchangerate.host/) atau [CurrencyFreaks](https://currencyfreaks.com/)).  
   - **Bitcoin**: gunakan API crypto (misal [CoinGecko](https://www.coingecko.com/en/api)).  
   - **Jadwal Sholat**: gunakan API publik seperti [api.myquran.com](https://api.myquran.com/).  

3. **n8n**  
   - Import workflow JSON.  
   - Atur credential masing-masing API & Telegram Bot.  

## 5. Cara Import
1. Download file JSON workflow ini.  
2. Masuk ke dashboard n8n.  
3. Klik **Import from File** lalu pilih file JSON.  
4. Atur API key & Telegram Bot di menu credential.  
5. Simpan & aktifkan workflow.  

## 6. Catatan
- Workflow dijalankan setiap pagi sesuai waktu yang ditentukan.  
- API key disimpan di **credential n8n**, tidak tersimpan dalam file JSON.  
- Data dapat disesuaikan sesuai kebutuhan (misalnya kurs tambahan, harga crypto lain, atau lokasi cuaca berbeda).  

---
✨ Dengan workflow ini, kamu akan selalu mendapat informasi penting setiap pagi langsung lewat Telegram, praktis dan otomatis!

