# ColorCue — Every Color Has a Clue

Asisten visual & auditori cerdas untuk pengguna buta warna (*color vision deficiency*). Kamera ponsel membaca warna objek secara *real-time* dan menyajikan **nama warna, kode HEX/RGB/HSL, pola aksesibilitas visual, suara asisten (TTS), serta analisis cerdas berbasis kebutuhan pengguna**.

---

## 📱 Desain Antarmuka Sesuai Mockup
Desain UI telah dimodernisasi sesuai dengan layout mobile ColorCue:
1. **Layar Onboarding Splash**:
   - Latar gradien biru laut navy `#1B2A4A`.
   - Ikon kacamata ColorCue dengan bracket kuning sudut keemasan (`#E5A800`).
   - *Curved bottom sheet* dengan slogan *"Setiap warna punya petunjuk"* dan tombol pill *"Mulai"*.
2. **Layar Pemilihan Jenis Penglihatan**:
   - Pilihan interaktif: **Deuteranopia** (sulit hijau-merah), **Protanopia** (sulit merah), **Tritanopia** (sulit biru-kuning), dan **Belum tahu / Lainnya**.
   - Indikator radio aktif dengan aksen biru dan border kontras.
3. **Layar Beranda (Home)**:
   - Header aplikasi *"ColorCue"* & sapaan *"Halo! Apa yang ingin kamu kenali hari ini?"*.
   - Banner kartu gelap *"Pindai sekarang"* dengan tombol pill kuning *"Buka Kamera"*.
   - Grid 2×2 Mode: **Buah** 🍊, **Kabel** 🔌, **Diagram** 📊, dan **Pakaian** 👕.
   - Kartu *"Terakhir dipindai"* dengan swatch warna dan status kematangan/detail.
   - Navigasi bawah (*Bottom Navigation Bar*) 4 tab: **Beranda**, **Kamera**, **Riwayat**, dan **Setelan**.

---

## ✨ Fitur-Fitur Lengkap

### 1. Deteksi Warna & Visual Inti
- **Real-Time Color Detection**: Deteksi warna langsung dari umpan video kamera setiap 130ms.
- **Color Information**: Menampilkan nama warna detail dalam Bahasa Indonesia, kode HEX (`#RRGGBB`), nilai `RGB(r, g, b)`, dan tingkat kecocokan.
- **Pattern Replacement**: Menggambar pola garis miring, titik rapat, kotak catur, cincin konsentris, dan garis horizontal langsung di atas area warna untuk membedakan warna yang tampak serupa bagi penyandang buta warna.
- **Color Point Selector**: Retikel bidik (*crosshair*) interaktif yang dapat diketuk atau digeser ke titik mana pun pada layar kamera atau foto.
- **Voice Assistant / Text-to-Speech (TTS)**: Tombol *"Bacakan"* dan mode asisten suara otomatis yang menyuarakan nama warna terdeteksi menggunakan Web Speech API bahasa Indonesia.
- **Upload Image / Gallery**: Fitur memilih dan memuat foto dari galeri HP / file komputer untuk mendeteksi warna di area foto mana pun.

### 2. Mode Khusus Berdasarkan Kebutuhan
- 🍊 **Mode Buah (Fruit Mode)**: Memprediksi jenis buah (pisang, tomat, apel, mangga, alpukat, jeruk) dan mengukur persentase kematangan visual (*ripeness meter*), memberikan status: *Matang*, *Mengkal*, atau *Terlalu Matang*.
- 🔌 **Mode Kabel Listrik (Cable Mode)**: Mengenali fungsi kabel standar instalasi listrik (Fasa/Arus, Netral, Arde/Grounding, DC) disertai peringatan keselamatan kelistrikan.
- 📊 **Mode Diagram (Diagram Mode)**: Membantu membaca grafik/diagram dengan memberikan pola pembeda unik untuk setiap warna area data.
- 👕 **Mode Pakaian (Fashion Matching Mode)**: Memberikan panduan padu padan warna busana yang serasi serta memperingatkan jika terjadi tabrak warna yang mencolok.
- 👓 **Simulasi Buta Warna (Color Blindness Simulation)**: Filter simulasi real-time berbasis matriks SVG feColorMatrix untuk melihat dunia dari sudut pandang *Protanopia*, *Deuteranopia*, *Tritanopia*, dan *Achromatopsia*.

### 3. Fitur Pendukung & Aksesibilitas
- ⚡ **Flashlight / Torch Mode**: Tombol senter untuk menerangi objek saat kondisi pencahayaan gelap (perangkat yang mendukung `torch`).
- 🔍 **Zoom Kamera**: Slider zoom digital dan optik (1x hingga 4x) untuk memperbesar detail objek kecil atau kabel tipis.
- ☀️ **Brightness Adjustment**: Pengatur kecerahan kamera (-50 hingga +50) untuk mengatasi pencahayaan redup atau silau.
- ⚠️ **Confidence Warning**: Indikator keyakinan deteksi warna (Akurat vs Rendah) dengan peringatan jika cahaya kurang memadai.
- 📜 **Scan History**: Riwayat pindaian yang tersimpan lokal dan disinkronkan ke server backend `/api/scans`.
- ⭐ **Favorite Colors**: Menandai warna favorit dengan bintang dan memfilternya di tab Riwayat.
- 🌙 **Dark & Light Mode**: Dukungan mode gelap dan terang yang persisten.
- 🌐 **Language & Accessibility Settings**:
  - Ukuran teks (*Kecil*, *Sedang*, *Besar*).
  - Mode *Kontras Tinggi* (*High Contrast*).
  - Pilihan Bahasa (Bahasa Indonesia / English).
- 📶 **Offline Mode (PWA)**: Aplikasi terdaftar dengan Service Worker (`sw.js`) dan Manifest sehingga dapat diinstal ke layar utama ponsel dan digunakan tanpa koneksi internet.

---

## 🚀 Cara Menjalankan

### 1. Jalankan di Komputer Lokal
```bash
npm install
npm start
```
Buka peramban di: `http://localhost:3000`

> **Catatan Kamera**: Fitur kamera HTML5 membutuhkan konteks aman (**HTTPS** atau `localhost`). Jika dibuka dari perangkat HP lain di jaringan lokal, gunakan terowongan HTTPS:
```bash
npx cloudflared tunnel --url http://localhost:3000
# atau
npx localtunnel --port 3000
```

### 2. Pasang ke Layar Utama (PWA)
- **Android / Google Chrome**: Buka menu tab **Setelan** → Klik tombol **Pasang Aplikasi**, atau melalui menu browser *Tambahkan ke Layar Utama*.
- **iPhone / iOS Safari**: Ketuk tombol **Bagikan (Share)** → Pilih **Tambah ke Layar Utama (Add to Home Screen)**.

---

## 🛠️ Struktur File
```
server.js                 # Backend Node.js Express (REST API /api/scans & static serving)
public/
  ├── index.html          # Seluruh antarmuka aplikasi, visualisasi, dan logika JS
  ├── sw.js               # Service Worker cache offline PWA
  ├── manifest.webmanifest# Konfigurasi PWA mobile
  ├── icon.svg            # Logo vektor kacamata ColorCue
  ├── icon-192.png        # Ikon PWA 192px
  ├── icon-512.png        # Ikon PWA 512px
  └── apple-touch-icon.png# Ikon Safari iOS
```

---

*Dikembangkan untuk Tugas Interaksi Manusia & Komputer (IMK) Semester 5 — Inklusivitas Aksesibilitas Warna.*
