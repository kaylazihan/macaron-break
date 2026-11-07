# PLAN.md — Universal 2D Arcade Game Roadmap (Untuk Siswa)

Dokumen ini adalah rencana kerja universal dan log perkembangan proyek pembuatan game arcade 2D dalam 1 file `index.html`. Dokumen ini diperbarui secara otomatis oleh AI setiap kali ada perubahan kode sebelum push ke GitHub.

---

## 1. Ikhtisar Game

- **Judul Game**: **Macaron Break** (tema pastel lembut, kontrol keyboard + sentuh/mouse)
- **Struktur Permainan**: 5 level bertingkat — bola makin cepat, baris balok bertambah, bonus poin per level
- **Genre**: 2D Arcade Game
- **Format**: Single-File HTML (`index.html`) tanpa dependensi eksternal
- **Platform**: Web Browser (Desktop & Mobile Responsive)
- **Audio**: Web Audio API Sintetis
- **Penyimpanan**: LocalStorage (`arcade_leaderboard`, `arcade_last_username`)
- **Kebijakan Caching**: Zero-Cache (`no-cache, no-store, must-revalidate`)
- **Deployment**: GitHub Pages (Branch `main`, path `/`)

---

## 2. Fase Pengembangan Universal

### Phase 0: Brainstorming & Desain Game
- [x] Ide & tema game: **Macaron Break** — pecahkan semua balok pastel.
- [x] Kontrol: Panah Kiri/Kanan atau A/D, gerak mouse, dan drag sentuh. Spasi/Tap = luncurkan bola & Pause.
- [x] Aturan: 3 nyawa, +10 poin per balok, 5 level; bonus 50 × level saat level selesai, menang bila semua level tuntas, kalah bila nyawa habis.
- [x] Gaya visual: **pastel lembut** (latar terang, balok warna macaron, aksen mint).

### Phase 1: Setup Single-File `index.html`
- [x] Kerangka HTML5 + meta tag **Zero-Cache**.
- [x] Kanvas responsif 400x600 (rasio 2:3) yang menyesuaikan tinggi layar.
- [x] Struktur 8 blok modular di JavaScript.
- [x] Game loop utama `requestAnimationFrame` dengan fixed timestep 60 FPS.

### Phase 2: Username & Leaderboard LocalStorage
- [x] Modal input username dengan validasi nama (1–15 karakter, anti-XSS).
- [x] Simpan/baca username dari `arcade_last_username`.
- [x] Simpan + sortir Top 10 di `arcade_leaderboard` (otomatis saat Game Over / Menang).
- [x] Tabel peringkat interaktif di menu (tombol Leaderboard).

### Phase 3: Mekanik Inti Permainan (Core Gameplay)
- [x] Status game `MENU`, `PLAYING`, `PAUSED`, `GAMEOVER`, `WIN`.
- [x] Paddle pemain dengan batas layar.
- [x] 35 balok (5 baris x 7 kolom) dengan 5 warna.
- [x] Tabrakan circle-vs-rect + pantulan sudut paddle + skor.

### Phase 4: Efek Suara & Visual Juice
- [x] Efek suara sintetis: luncurkan, pantul, pecah balok, menang, game over.
- [x] Partikel pecahan berwarna saat balok hancur.
- [x] Screen shake saat game over.

### Phase 5: Publikasi GitHub Pages
- [x] Inisialisasi git dan branch `main`.
- [x] Repo publik: https://github.com/kaylazihan/macaron-break (dibuat via `gh repo create --public`).
- [x] GitHub Pages aktif via `gh api` (branch `main`, path `/`): https://kaylazihan.github.io/macaron-break/
- [x] Snippet perintah terminal tersedia di `AGENTS.md` (bagian Google AI Studio).
- [x] Build Pages terverifikasi: status `building` → HTTP 200 pada percobaan pertama.
- [x] Tes live demo: https://kaylazihan.github.io/macaron-break/ (HTTP 200, judul & palet baru tampil).

### Phase 6: Level & Difficulty Ramp (v0.5.0)
- [x] 5 level dengan `STATE_LEVELCLEAR` di antara level.
- [x] Kecepatan bola mulai **1,2×** kecepatan dasar di level 1, lalu +10% setiap level (`LEVEL_START_SPEED`, `LEVEL_SPEED_STEP`). Kecepatan paddle tetap (7/9 px per langkah).
- [x] Baris balok bertambah 1 mulai level 3, palet warna macaron berganti tiap level.
- [x] Bonus skor 50 × level saat level selesai, rekor dikirim ke leaderboard di level 5.
- [x] Perbaikan bug: kontrol keyboard vs mouse, rotasi layar, sudut pantulan bola.
- [x] Kecepatan paddle diturunkan ke **5 px** (portrait) & **7 px** (landscape) per langkah — sebelumnya 7 & 9 terasa terlalu gesit.
- [x] Uji otomatis Node.js: 41 pemeriksaan (`PASS` semua) sebelum deploy.

---

## 3. Matriks Tugas & Status Pelaksanaan

| ID | Tugas / Fitur | Fase | Status | Pelaksana | Catatan |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **T-00** | Pembuatan template `AGENTS.md` & `PLAN.md` untuk Siswa | Fondasi | `DONE` | AI | Template standar single model siap |
| **T-01** | Brainstorming Ide & Konsep Game Spesifik | Phase 0 | `DONE` | Siswa | Macaron Break, tema pastel, 3 nyawa, +10/balok |
| **T-02** | Pembuatan Skeleton `index.html` & Meta Zero-Cache | Phase 1 | `DONE` | AI | 8 blok modular + loop fixed timestep |
| **T-03** | Modul Input Username & Leaderboard Top 10 | Phase 2 | `DONE` | AI | LocalStorage CRUD, sanitasi XSS, tabel Top 10 |
| **T-04** | Logika Pergerakan, Rintangan & Tabrakan | Phase 3 | `DONE` | AI | Paddle, 35 balok, collision, skor, pause |
| **T-05** | Efek Suara Synth Web Audio API & Partikel | Phase 4 | `DONE` | AI | SFX sintetis, partikel, screen shake |
| **T-06** | Deployment GitHub Pages via GitHub CLI (`gh`) | Phase 5 | `DONE` | AI | Live: https://kaylazihan.github.io/macaron-break/ |
| **T-07** | Sistem 5 level & difficulty ramp | Phase 6 | `DONE` | AI | Bola mulai 1,2× lalu +10%/level, paddle tetap, bonus 50×level |
| **T-08** | Perbaikan bug kontrol & rotasi layar | Phase 6 | `DONE` | AI | Keyboard vs mouse, snapshot proporsional + auto-pause |
| **T-09** | Perbaikan sudut pantulan bola | Phase 6 | `DONE` | AI | Batas minimum 22% `vx` / 30% `vy`, kecepatan tetap |
| **T-10** | Uji otomatis logika game (Node.js) | Phase 6 | `DONE` | AI | 41 pemeriksaan, semuanya `PASS` |

*Status: `TODO` | `IN-PROGRESS` | `DONE`*

---

## 4. Changelog & Riwayat Revisi

| Versi | Tanggal | Pelaksana | Ringkasan Perubahan | Referensi Commit |
| :--- | :--- | :--- | :--- | :--- |
| **v0.5.3** | 2026-11-07 | AI | Paddle diperlambat: **5 px/langkah** (portrait) & **7 px** (landscape), sebelumnya 7 & 9. Menyeberang layar ~1,07 detik (dulu ~0,9). Kecepatan bola tidak diubah. Diuji 7 pemeriksaan termasuk simulasi AI paddle di level 5 (0 bola terlewat) | `2ee3944` |
| **v0.5.2** | 2026-11-07 | AI | Koreksi kecepatan: bola mulai **1,2×** dasar (bukan 1,5× karena terasa terlalu kencang) → 1,2 / 1,3 / 1,4 / 1,5 / 1,6. Paddle (alas) sengaja tidak dipercepat, tetap 7 px (portrait) & 9 px (landscape) per langkah. Diuji 11 pemeriksaan | `f910a5f` |
| **v0.5.1** | 2026-11-07 | AI | Kecepatan bola dinaikkan: mulai **1,5×** kecepatan dasar di level 1 (sebelumnya 1,0×), tetap +10% per level → 1,5 / 1,6 / 1,7 / 1,8 / 1,9. Lintasan layar penuh kini ~1,7 detik (dulu ~2,5 detik). Diuji 11 pemeriksaan, aman dari tembus objek | `083fd06` |
| **v0.5.0** | 2026-11-07 | AI | Sistem **5 level**: kecepatan bola +10%/level, baris balok bertambah mulai level 3, bonus 50×level, palet warna berganti, overlay Level Selesai. Perbaikan 3 bug: paddle terkunci mouse, rotasi layar menghapus progres, bola nyangkut di sudut datar | `b0efcb6` |
| **v0.4.0** | 2026-10-31 | AI | Tema pastel hijau-cokelat (cream, sage, mocha), layout otomatis potret di HP & lanskap di laptop, render tajam (DPR), judul **Macaron Break**, deploy GitHub Pages | `01327ee` |
| **v0.3.0** | 2026-10-31 | AI | Menyelesaikan game Brick Breaker: leaderboard LocalStorage, rendering neon, game loop fixed timestep, pause, sanitasi username, HUD mobile, uji otomatis 23 check | *(belum di-commit)* |
| **v0.2.2** | 2026-10-24 | AI | Menambahkan panduan alur integrasi khusus Google AI Studio & penegasan repo wajib Public | `07475fb` |
| **v0.2.1** | 2026-10-24 | AI | Menambahkan panduan detail aktivasi GitHub Pages (CLI gh api & Web UI visual) serta troubleshooting | `3aaf671` |
| **v0.2.0** | 2026-10-24 | AI | Konfigurasi ulang ke Single Model AI untuk siswa, modularisasi 8 blok kode, dan penyesuaian matriks tugas | `2954bb0` |
| **v0.1.0** | 2026-10-24 | AI | Inisialisasi awal file sistem `AGENTS.md` dan universal blueprint `PLAN.md` | `47aa88e` |
