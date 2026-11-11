# TaskMate PWA – Student Task Management

Aplikasi manajemen tugas mahasiswa berbasis **Progressive Web App (PWA)** yang dibangun menggunakan React JS, Vite, Tailwind CSS, dan IndexedDB.

TaskMate dirancang untuk membantu mahasiswa mengelola tugas perkuliahan, mengatur deadline, memantau status penyelesaian, serta menyimpan data secara lokal. Aplikasi dapat diinstal pada perangkat Android melalui browser dan mendukung penggunaan offline setelah aset aplikasi berhasil di-cache.

---

## 1. Deskripsi Project

TaskMate PWA merupakan proyek praktikum mata kuliah **Aplikasi Perangkat Bergerak**. Proyek ini memperkenalkan konsep Progressive Web App sebagai alternatif pengembangan aplikasi mobile selain Native Mobile Development dan Cross-Platform Mobile Development.

Dengan teknologi PWA, aplikasi web dapat memberikan pengalaman penggunaan menyerupai aplikasi mobile tanpa harus membuat aplikasi Android menggunakan Kotlin, Java, atau Flutter.

### Tujuan Pengembangan

1. Memahami konsep Progressive Web App.
2. Memahami pengembangan frontend menggunakan React JS.
3. Mengimplementasikan CRUD (Create, Read, Update, Delete).
4. Menggunakan IndexedDB sebagai penyimpanan data lokal.
5. Mengimplementasikan Web App Manifest.
6. Memahami Service Worker dan caching.
7. Mengembangkan aplikasi yang mendukung offline mode.
8. Melakukan deployment aplikasi ke internet.

---

## 2. Fitur Aplikasi

| No. | Fitur | Deskripsi |
|---|---|---|
| 1 | Dashboard | Menampilkan ringkasan tugas mahasiswa |
| 2 | Total Tugas | Menampilkan seluruh jumlah tugas |
| 3 | Pending Tasks | Menampilkan jumlah tugas belum selesai |
| 4 | Completed Tasks | Menampilkan jumlah tugas selesai |
| 5 | Tambah Tugas | Menambahkan tugas baru |
| 6 | Edit Tugas | Mengubah informasi tugas |
| 7 | Hapus Tugas | Menghapus tugas |
| 8 | Kategori | Mengelompokkan tugas berdasarkan kategori |
| 9 | Deadline | Menentukan tanggal pengumpulan tugas |
| 10 | Status Tugas | Mengubah status selesai atau belum selesai |
| 11 | Local Database | Menyimpan data menggunakan IndexedDB |
| 12 | Offline Mode | Mengakses aplikasi tanpa koneksi internet setelah caching |
| 13 | Install PWA | Memasang aplikasi pada home screen perangkat |

### Kategori Tugas

- Kuliah
- Praktikum
- UTS
- UAS
- Proyek

---

## 3. Teknologi yang Digunakan

| Teknologi | Fungsi |
|---|---|
| React JS | Library pengembangan antarmuka |
| Vite | Development server dan build tool |
| JavaScript | Bahasa pemrograman |
| Tailwind CSS | Styling dan desain UI |
| Lucide React | Ikon aplikasi |
| Dexie.js | Pengelolaan IndexedDB |
| Dexie React Hooks | Integrasi database dengan React |
| Vite PWA Plugin | Konfigurasi Progressive Web App |
| Git & GitHub | Version control dan penyimpanan kode |
| Vercel | Deployment aplikasi |

---

## 4. Persyaratan Instalasi

Sebelum menjalankan project, pastikan komputer telah memiliki:

1. Node.js versi LTS.
2. NPM.
3. Visual Studio Code.
4. Git Bash.
5. Google Chrome.

Download tools:

- Node.js: https://nodejs.org/
- Visual Studio Code: https://code.visualstudio.com/
- Git: https://git-scm.com/
- Google Chrome: https://www.google.com/chrome/

Periksa instalasi melalui Git Bash:

```bash
node -v
npm -v
git --version
```

---

## 5. Membuat Project dari Awal

### Langkah 1 – Membuat Project React

Jalankan perintah:

```bash
npm create vite@latest taskmate-pwa -- --template react
```

### Langkah 2 – Masuk ke Folder Project

```bash
cd taskmate-pwa
```

### Langkah 3 – Install Dependency

```bash
npm install
```

### Langkah 4 – Install Library

```bash
npm install lucide-react dexie dexie-react-hooks
```

### Langkah 5 – Install Tailwind CSS

```bash
npm install -D tailwindcss @tailwindcss/vite
```

### Langkah 6 – Install Vite PWA Plugin

```bash
npm install -D vite-plugin-pwa
```

---

## 6. Konfigurasi Project

### A. Konfigurasi vite.config.js

Buka file `vite.config.js`, kemudian ubah menjadi:

```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'
import { VitePWA } from 'vite-plugin-pwa'

export default defineConfig({
  plugins: [
    react(),
    tailwindcss(),
    VitePWA({
      registerType: 'autoUpdate',

      includeAssets: ['favicon.svg'],

      manifest: {
        name: 'TaskMate - Student Task Management',
        short_name: 'TaskMate',
        description: 'Aplikasi manajemen tugas mahasiswa',
        theme_color: '#4f46e5',
        background_color: '#f8fafc',
        display: 'standalone',
        orientation: 'portrait',
        start_url: '/',
        icons: [
          {
            src: '/pwa-192x192.png',
            sizes: '192x192',
            type: 'image/png'
          },
          {
            src: '/pwa-512x512.png',
            sizes: '512x512',
            type: 'image/png'
          }
        ]
      },

      workbox: {
        navigateFallback: '/index.html'
      }
    })
  ]
})
```

### B. Konfigurasi Tailwind CSS

Buka `src/index.css`:

```css
@import "tailwindcss";

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
  background: #f8fafc;
}
```

### C. Konfigurasi Database

Buat file `src/db.js`:

```javascript
import Dexie from 'dexie'

export const db = new Dexie('TaskMateDB')

db.version(1).stores({
  tasks: '++id, title, category, dueDate, completed, createdAt'
})
```

### D. Konfigurasi React

Pastikan file `src/main.jsx` berisi:

```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './index.css'

ReactDOM.createRoot(
  document.getElementById('root')
).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
)
```

### E. Konfigurasi HTML

Ubah bagian `index.html`:

```html
<!doctype html>
<html lang="id">
  <head>
    <meta charset="UTF-8" />

    <meta
      name="viewport"
      content="width=device-width, initial-scale=1.0"
    />

    <meta
      name="theme-color"
      content="#4f46e5"
    />

    <meta
      name="description"
      content="TaskMate adalah aplikasi manajemen tugas mahasiswa."
    />

    <title>TaskMate - Student Task Management</title>
  </head>

  <body>
    <div id="root"></div>

    <script
      type="module"
      src="/src/main.jsx"
    ></script>
  </body>
</html>
```

---

## 7. Struktur Folder Project

Struktur folder akhir:

```text
taskmate-pwa/
│
├── public/
│   ├── favicon.svg
│   ├── pwa-192x192.png
│   └── pwa-512x512.png
│
├── src/
│   ├── App.jsx
│   ├── db.js
│   ├── index.css
│   └── main.jsx
│
├── index.html
├── vite.config.js
├── package.json
├── package-lock.json
└── README.md
```

Keterangan:

- `public/`: menyimpan ikon aplikasi dan aset statis.
- `src/App.jsx`: halaman utama dan fitur aplikasi.
- `src/db.js`: konfigurasi database IndexedDB.
- `src/index.css`: styling aplikasi.
- `src/main.jsx`: entry point React.
- `vite.config.js`: konfigurasi Vite dan PWA.
- `index.html`: dokumen HTML utama.
- `README.md`: dokumentasi project.

---

## 8. Menjalankan Aplikasi

Untuk menjalankan aplikasi dalam mode development:

```bash
npm run dev
```

Buka browser:

```text
http://localhost:5173
```

Untuk menghentikan server:

```bash
CTRL + C
```

---

## 9. Pengujian Production Build

Sebelum deployment, lakukan build:

```bash
npm run build
```

Jika berhasil, Vite akan menghasilkan folder `dist`.

Untuk menguji hasil build:

```bash
npm run preview
```

Buka:

```text
http://localhost:4173
```

Pengujian production penting untuk memastikan service worker dan konfigurasi PWA dapat bekerja.

---

## 10. Pengujian Database IndexedDB

Untuk memastikan data tersimpan:

1. Jalankan aplikasi.
2. Buka Google Chrome.
3. Tekan F12.
4. Pilih tab Application.
5. Buka bagian Storage.
6. Pilih IndexedDB.
7. Pilih database `TaskMateDB`.
8. Buka tabel `tasks`.

Data tugas yang ditambahkan akan tersimpan pada IndexedDB browser.

Data tetap tersedia setelah halaman di-refresh selama data browser tidak dihapus.

---

## 11. Pengujian Progressive Web App

### A. Pengujian Manifest

Periksa apakah manifest sudah terdeteksi:

1. Buka Chrome DevTools.
2. Pilih Application.
3. Pilih Manifest.
4. Periksa nama aplikasi, ikon, theme color, dan display mode.

### B. Pengujian Service Worker

1. Buka Chrome DevTools.
2. Pilih Application.
3. Pilih Service Workers.
4. Pastikan service worker berhasil terdaftar.

### C. Instalasi Aplikasi

Pada Android:

1. Buka URL aplikasi melalui Chrome.
2. Klik menu tiga titik.
3. Pilih Install app atau Add to Home screen.
4. Konfirmasi instalasi.
5. Buka TaskMate melalui ikon di home screen.

### D. Pengujian Offline Mode

1. Buka aplikasi melalui browser.
2. Pastikan aplikasi sudah selesai dimuat.
3. Buka Chrome DevTools.
4. Pilih tab Network.
5. Aktifkan mode Offline.
6. Refresh halaman.
7. Periksa apakah aplikasi masih dapat dibuka.

Aplikasi harus sudah pernah dimuat secara online agar aset yang diperlukan tersedia di cache.

Data transaksi dan tugas tetap dapat dikelola menggunakan IndexedDB ketika offline.

---

## 12. Upload Project ke GitHub

### Langkah 1 – Membuat Repository

1. Login ke GitHub.
2. Klik New Repository.
3. Masukkan nama `taskmate-pwa`.
4. Pilih Public atau Private.
5. Klik Create Repository.

### Langkah 2 – Inisialisasi Git

```bash
git init
```

### Langkah 3 – Konfigurasi Identitas Git

Jika belum dikonfigurasi:

```bash
git config --global user.name "Nama Mahasiswa"
git config --global user.email "email@example.com"
```

### Langkah 4 – Menambahkan File

```bash
git add .
```

### Langkah 5 – Membuat Commit

```bash
git commit -m "Initial TaskMate PWA"
```

### Langkah 6 – Mengatur Branch

```bash
git branch -M main
```

### Langkah 7 – Menghubungkan Repository

```bash
git remote add origin https://github.com/USERNAME/taskmate-pwa.git
```

Ganti `USERNAME` dengan username GitHub masing-masing.

### Langkah 8 – Push ke GitHub

```bash
git push -u origin main
```

### Jika Ada Perubahan Kode

Gunakan:

```bash
git add .
git commit -m "Update TaskMate PWA"
git push origin main
```

---

## 13. Deployment ke Vercel

TaskMate dapat dipublikasikan secara online menggunakan Vercel.

### Langkah 1

Buka:

https://vercel.com/

### Langkah 2

Login menggunakan akun GitHub.

### Langkah 3

Pilih Add New Project.

### Langkah 4

Import repository `taskmate-pwa`.

### Langkah 5

Pastikan konfigurasi:

| Pengaturan | Nilai |
|---|---|
| Framework Preset | Vite |
| Build Command | npm run build |
| Output Directory | dist |
| Install Command | npm install |

### Langkah 6

Klik Deploy.

Setelah proses deployment selesai, Vercel memberikan URL aplikasi.

Contoh:

```text
https://taskmate-pwa.vercel.app
```

URL tersebut dapat diakses melalui browser komputer maupun smartphone.

---

## 14. Daftar Perintah Git Bash

Seluruh perintah utama dari awal sampai upload GitHub:

```bash
# Membuat project
npm create vite@latest taskmate-pwa -- --template react

# Masuk folder
cd taskmate-pwa

# Install dependency
npm install

# Install library
npm install lucide-react dexie dexie-react-hooks

# Install Tailwind CSS
npm install -D tailwindcss @tailwindcss/vite

# Install PWA Plugin
npm install -D vite-plugin-pwa

# Menjalankan aplikasi
npm run dev

# Build production
npm run build

# Preview production
npm run preview

# Inisialisasi Git
git init

# Konfigurasi Git
git config --global user.name "Nama Mahasiswa"
git config --global user.email "email@example.com"

# Menambahkan seluruh file
git add .

# Commit
git commit -m "Initial TaskMate PWA"

# Mengatur branch
git branch -M main

# Menghubungkan GitHub
git remote add origin https://github.com/USERNAME/taskmate-pwa.git

# Upload ke GitHub
git push -u origin main
```

---

## 15. Troubleshooting

| Permasalahan | Solusi |
|---|---|
| npm is not recognized | Instal Node.js |
| Tailwind tidak berfungsi | Periksa konfigurasi Vite dan CSS |
| Ikon tidak muncul | Periksa instalasi Lucide React |
| Database tidak muncul | Periksa konfigurasi Dexie |
| Data hilang setelah refresh | Periksa IndexedDB |
| PWA tidak dapat diinstal | Periksa manifest, ikon, dan HTTPS |
| Service Worker tidak aktif | Periksa production build dan registrasi |
| Offline mode tidak berfungsi | Periksa cache Service Worker |
| Git push ditolak | Periksa autentikasi dan konfigurasi repository |
| Deployment gagal | Periksa build log Vercel |

---

## 16. Batasan Aplikasi

Versi awal TaskMate memiliki beberapa batasan:

1. Tidak menggunakan sistem login.
2. Data disimpan secara lokal pada browser masing-masing pengguna.
3. Data tidak otomatis tersinkronisasi antarperangkat.
4. Tidak menggunakan backend maupun database server.
5. Offline mode bergantung pada aset yang telah tersimpan dalam cache.
6. Push notification belum diimplementasikan.
7. Aplikasi belum dipublikasikan melalui Google Play Store.

Batasan tersebut merupakan bagian dari ruang lingkup pengembangan versi praktikum.

---

## 17. Pengembangan Selanjutnya

Beberapa fitur yang dapat dikembangkan pada versi berikutnya:

- Autentikasi pengguna.
- Integrasi REST API.
- Sinkronisasi data ke server.
- Push notification untuk pengingat deadline.
- Kalender akademik.
- Filter dan pencarian tugas.
- Export data tugas ke PDF.
- Dark mode.

---

## 18. Tugas Praktikum Mahasiswa

Setelah berhasil membuat TaskMate, mahasiswa diminta untuk:

1. Mengembangkan aplikasi sesuai tutorial.
2. Memastikan seluruh fitur CRUD berfungsi.
3. Mengimplementasikan penyimpanan IndexedDB.
4. Mengaktifkan fitur instalasi PWA.
5. Menguji aplikasi dalam kondisi offline.
6. Melakukan deployment ke Vercel.
7. Mengunggah source code ke GitHub.
8. Membuat dokumentasi project.
9. Melakukan presentasi hasil pengembangan.

### Ketentuan Pengumpulan

| Komponen | Keterangan |
|---|---|
| Source Code | Repository GitHub |
| README | Dokumentasi project |
| Deployment | URL Vercel |
| Pengujian | Bukti instalasi dan offline mode |
| Presentasi | Demo aplikasi |

---

## 19. Kesimpulan

TaskMate PWA merupakan proyek pembelajaran yang memperkenalkan mahasiswa pada konsep Progressive Web App melalui React JS dan teknologi web modern.

Melalui proyek ini, mahasiswa diharapkan memahami bahwa aplikasi mobile tidak selalu harus dikembangkan menggunakan bahasa pemrograman native. Teknologi web juga dapat dimanfaatkan untuk menghasilkan aplikasi yang dapat diinstal, memiliki penyimpanan lokal, dan mendukung penggunaan offline.

---

**Mata Kuliah:** Aplikasi Perangkat Bergerak  
**Program Studi:** S1 Teknik Informatika  
**Project:** TaskMate – Student Task Management  
**Platform:** Progressive Web App (PWA)  
**Framework:** React JS + Vite  
**Database:** IndexedDB  
**Deployment:** Vercel

**Developed for Learning Purpose – Mobile Application Development.**