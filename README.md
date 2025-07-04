# AmbuLink - Sistem Informasi Geografis Ambulans

Aplikasi Web GIS untuk menampilkan dan mencari informasi ambulans di seluruh Indonesia.

## Teknologi yang Digunakan

- Frontend:
  - HTML
  - Tailwind CSS
  - JavaScript (Leaflet.js untuk peta)
- Backend:
  - Express.js
  - MySQL

## Struktur Project

```
project-root/
│
├── public/              # Static files
│   ├── index.html      # Halaman utama dengan peta
│   ├── login.html      # Halaman login
│   ├── register.html   # Halaman registrasi
│   ├── tambah.html     # Form tambah ambulans
│   ├── detail.html     # Detail ambulans
│   ├── css/
│   │   └── tailwind.css
│   └── js/
│       └── main.js     # Leaflet + interaksi DOM
│
├── server/             # Backend files
│   ├── app.js         # Express server setup
│   ├── routes/
│   │   └── ambulans.js
│   └── controllers/
│       └── ambulansController.js
│
├── db/                # Database configuration
│   └── connection.js
│
├── .env              # Environment variables
├── package.json
└── tailwind.config.js
```

## Setup Database

1. Buat database MySQL baru:

```sql
CREATE DATABASE gis_ambulans;

USE gis_ambulans;

CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nama VARCHAR(100),
  email VARCHAR(100) UNIQUE,
  password VARCHAR(255)
);

CREATE TABLE ambulans (
  id INT AUTO_INCREMENT PRIMARY KEY,
  penyedia VARCHAR(100),
  kontak VARCHAR(20),
  alamat TEXT,
  kota VARCHAR(50),
  latitude DECIMAL(10, 6),
  longitude DECIMAL(10, 6),
  harga INT,
  status ENUM('gratis', 'berbayar'),
  fasilitas TEXT,
  user_id INT,
  FOREIGN KEY (user_id) REFERENCES users(id)
);
```

## Konfigurasi Environment

Buat file `.env` di root project dengan isi:

```
PORT=3000
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=
DB_NAME=gis_ambulans
SESSION_SECRET=your-secret-key-change-this
```

Sesuaikan nilai-nilai tersebut dengan konfigurasi lokal Anda.

## Instalasi

1. Install dependencies:

```bash
npm install
```

2. Build Tailwind CSS:

```bash
npm run build:css
```

3. Jalankan server:

```bash
npm run dev
```

4. Buka http://localhost:3000 di browser

## Fitur

- 🗺️ Peta interaktif dengan Leaflet.js
- 📍 Tampilkan lokasi user dan ambulans
- 🔍 Filter berdasarkan:
  - Kota
  - Status (gratis/berbayar)
  - Harga maksimal
- 📝 CRUD Ambulans:
  - Tambah
  - Lihat detail
  - Edit (untuk pemilik)
  - Hapus (untuk pemilik)
- 👤 Autentikasi:
  - Register
  - Login
  - Session management
- 📏 Hitung jarak ke ambulans terdekat
- 📱 Responsive design

## Pengembangan

- Gunakan `npm run dev` untuk development dengan auto-reload
- Tailwind CSS dalam mode watch: `npm run build:css`

## Catatan

- Pastikan MySQL server berjalan
- Ubah konfigurasi database di `.env` jika diperlukan
- Ganti `SESSION_SECRET` dengan nilai yang aman untuk production
