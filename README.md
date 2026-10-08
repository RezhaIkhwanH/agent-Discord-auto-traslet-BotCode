# 🤖 AI Discord MOM (Minutes of Meeting) Bot & Dashboard

Bot Discord pintar berbasis Node.js yang secara otomatis bergabung ke Voice Channel rapat, merekam dan mentranskripsi percakapan peserta, merangkum hasil rapat menjadi dokumen **Minutes of Meeting (MOM)** berformat PDF menggunakan AI, serta menyediakan **Web Dashboard** interaktif untuk melihat dan mengunduh hasil ringkasan rapat.

---

> [!IMPORTANT]
> Repositori ini hanya berisi **kode Bot discord dan dashboard** untuk Bot Notetaker MOM. Kode Agent nya berada pada repositori terpisah.
>
> - **Agent MOM Repo**: [Agent MoM](https://github.com/RezhaIkhwanH/MoM-agent-server-agent)
---

## 🌟 Fitur Utama

- **🎙️ Discord Voice Streaming**: Bergabung ke Voice Channel Discord dan mendengarkan percakapan pengguna secara real-time.
- **⚡ Speech-to-Text (STT) via Groq API**: Mengonversi audio stream (Opus/PCM) ke format WAV 16kHz Mono dan mentranskripsikannya ke Bahasa Indonesia menggunakan model **Whisper Large v3** dari Groq API.
- **🧠 AI MOM Summarizer**: Mengirimkan transkrip percakapan lengkap berstempel waktu (*timestamp*) ke Backend Agent AI untuk merangkum poin-poin utama, keputusan rapat, dan tindakan selanjutnya (*action items*).
- **📄 PDF Generator**: Menggenerasi dokumen PDF profesional secara otomatis berdasarkan hasil ringkasan AI MOM.
- **📊 Interactive Web Dashboard**: Express Server terintegrasi yang menyediakan antarmuka web modern untuk mengelola, melihat, dan mengunduh seluruh file PDF MOM yang telah dibuat.

---

## 📁 Struktur Proyek

```text
agent-Discord-mom-bot/
├── Tools/
│   ├── generatePdf.js      # Utility pembuatan file PDF menggunakan pdfkit
│   └── servicetts.js       # Konversi audio (FFmpeg), Groq STT API, & Agent MOM Service
├── hasil_mom/              # Folder tempat menyimpan hasil file PDF MOM
├── public/
│   └── index.html          # Web Dashboard UI
├── recordings/             # Folder penyimpanan sementara file audio stream (.pcm & .wav)
├── .env                    # Konfigurasi kunci rahasia (Token & API Key)
├── .gitignore              # Daftar berkas/folder yang diabaikan Git
├── index.js                # Entry point utama (Discord Bot Client & Express Web Server)
├── package.json            # Manifest dependensi & skrip proyek
└── README.md               # Dokumentasi proyek
```

---

## 📋 Prasyarat

Sebelum menjalankan proyek ini, pastikan Anda telah menyiapkan:

1. **Node.js** (Versi 18 atau lebih baru).
2. **Discord Bot Token**:
   - Buat aplikasi baru di [Discord Developer Portal](https://discord.com/developers/applications).
   - Aktifkan **Privileged Gateway Intents**:
     - `Server Members Intent`
     - `Message Content Intent`
   - Dapatkan Bot Token.
3. **Groq API Key**:
   - Dapatkan API Key gratis atau berbayar di [Groq Console](https://console.groq.com/).
4. **Backend AI Agent Service**:
   - Layanan Agent MOM yang berjalan secara lokal pada `http://127.0.0.1:8000/agent_MOM/invoke`.

---

## ⚙️ Instalasi & Konfigurasi

1. **Clone repositori ini / Buka folder proyek**:
   ```bash
   cd agent-Discord-mom-bot
   ```

2. **Install dependensi**:
   ```bash
   npm install
   ```

3. **Buat file `.env`**:
   Buat file `.env` di akar direktori proyek dan isi konfigurasi berikut:

   ```env
   DISCORD_TOKEN=your_discord_bot_token_here
   GROQ_API_KEY=your_groq_api_key_here
   PORT=3000
   ```

---

## 🚀 Cara Menjalankan

### Mode Produksi
```bash
npm start
```

### Mode Pengembangan (Auto-reload dengan Node Watch)
```bash
npm run dev
```

Saat berhasil dijalankan, terminal akan menampilkan pesan:
```text
Server Dashboard MOM berjalan di port 3000
Akses: http://localhost:3000
🤖 Bot MOM online sebagai: <NamaBot#0000>
```

---

## 💬 Perintah Bot Discord

| Perintah | Deskripsi |
| :--- | :--- |
| `!join` | Bot masuk ke Voice Channel tempat Anda berada dan mulai merekam/mendengarkan percakapan. |
| `!leave` | Bot keluar dari Voice Channel, mengolah seluruh transkrip percakapan, membuat ringkasan AI, dan menyimpannya dalam format PDF. |

---

## 🌐 Web Dashboard & API

Akses Web Dashboard melalui browser di: `http://localhost:3000`

### API Endpoints
- **`GET /api/moms`**: Mengembalikan daftar seluruh berkas PDF MOM yang tersedia di folder `hasil_mom/`.
- **`GET /hasil_mom/:filename`**: Mengunduh atau menampilkan file PDF MOM yang dipilih.

---

## 🛡️ Keamanan

- File `.env` telah ditambahkan ke `.gitignore` untuk mencegah kebocoran token Discord dan API key Groq. **Jangan pernah mengunggah file `.env` ke repositori publik!**

---
