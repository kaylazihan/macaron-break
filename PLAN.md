# PLAN.md — Universal 2D Arcade Game Roadmap (Untuk Siswa)

Dokumen ini adalah rencana kerja universal dan log perkembangan proyek pembuatan game arcade 2D dalam 1 file `index.html`. Dokumen ini diperbarui secara otomatis oleh AI setiap kali ada perubahan kode sebelum push ke GitHub.

---

## 1. Ikhtisar Game

- **Judul Game**: **Macaron Arcade** — 2 permainan dalam satu halaman: **Macaron Break** & **Macaron Match** (tema pastel lembut, kontrol keyboard + sentuh/mouse)
- **Struktur Permainan**: 5 level bertingkat — bola makin cepat, baris balok bertambah, bonus poin per level
- **Power-up**: 4 item jatuh dari balok (paddle lebar, bola ganda, bola lambat, nyawa +1)
- **Macaron Match**: match-3 papan 8×8, 25 langkah, cascade combo, leaderboard terpisah
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

### Phase 7: Power-up & Multi-Bola (v0.6.0)
- [x] Item jatuh dari balok yang hancur, peluang 18% (`POWERUP_DROP_CHANCE`), ditangkap paddle.
- [x] **Paddle Lebar** (W): paddle 1,6× selama 12 detik.
- [x] **Bola Ganda** (M): menambah 2 bola dari posisi bola utama.
- [x] **Bola Lambat** (S): kecepatan 0,65× selama 8 detik (tidak menumpuk).
- [x] **Nyawa +1** (+): maksimal 5 nyawa.
- [x] Bola cadangan dipakai lebih dulu sebelum nyawa berkurang.
- [x] Pill durasi efek di atas papan, item & bola ikut dipindah saat rotasi layar.
- [x] Uji otomatis Node.js: 34 pemeriksaan power-up (`PASS` semua) sebelum deploy.

### Phase 8: Dua Game dalam Satu Halaman (v0.7.0)
- [x] Layar **Home** "Macaron Arcade" untuk memilih permainan; username dipakai bersama.
- [x] **Macaron Match** (match-3): papan 8×8, 6 warna macaron, tukar dua permen bersebelahan.
- [x] Deteksi match horizontal & vertikal 3+, animasi hapus, gravitasi, isi ulang dari atas.
- [x] **Cascade combo**: match beruntun berlipat (skor 10 × combo per permen), teks COMBO muncul.
- [x] **25 langkah** per sesi; skor akhir masuk leaderboard khusus Macaron Match.
- [x] Papan dijamin bebas match awal dan selalu punya langkah valid; papan buntu disusun ulang.
- [x] Leaderboard dengan **tab** per game (data terpisah: `arcade_leaderboard` & `arcade_leaderboard_match`).
- [x] HUD menyesuaikan mode: Nyawa/Level untuk Break, Langkah untuk Match.
- [x] **Home langsung tampil** saat dibuka; nama pemain diisi lewat input di Home (tidak ada lagi tembok modal nama sebelum bisa melihat game).
- [x] **Geser permen (drag/swipe)** ke kiri/kanan/atas/bawah untuk menukar dengan tetangga; klik dua permen tetap didukung.
- [x] Geser yang tidak membentuk match dibatalkan tanpa memakai langkah; geseran kecil (<30% sel) tidak dihitung.
- [x] Uji otomatis Node.js: 56 pemeriksaan gabungan (match-3, navigasi, leaderboard, regresi Break).
- [x] **Fix kritis**: membuka menu Match membuat `gameMode='MATCH'` sebelum papan dibuat → `renderMatch` error tiap frame dan mematikan `requestAnimationFrame` (semua game beku). Papan kini disiapkan di `toMatchMenu()` + guard papan kosong.

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
| **T-11** | Power-up jatuh dari balok & ditangkap paddle | Phase 7 | `DONE` | AI | 4 jenis item, peluang 18% |
| **T-12** | Multi-bola & aturan bola cadangan | Phase 7 | `DONE` | AI | Bola cadangan dipakai sebelum nyawa berkurang |
| **T-13** | Timer efek & pill durasi di papan | Phase 7 | `DONE` | AI | Paddle lebar 12s, bola lambat 8s |
| **T-14** | Uji otomatis power-up | Phase 7 | `DONE` | AI | 34 pemeriksaan, semuanya `PASS` |
| **T-15** | Layar Home & navigasi dua game | Phase 8 | `DONE` | AI | Home → Break / Match, username bersama |
| **T-16** | Engine match-3 (swap, match, gravity) | Phase 8 | `DONE` | AI | Papan 8×8, 6 warna, 25 langkah |
| **T-17** | Cascade combo & leaderboard terpisah | Phase 8 | `DONE` | AI | Tab Break/Match, key LocalStorage berbeda |
| **T-18** | Uji otomatis gabungan dua game | Phase 8 | `DONE` | AI | 56 pemeriksaan, semuanya `PASS` |

*Status: `TODO` | `IN-PROGRESS` | `DONE`*

---

## 4. Changelog & Riwayat Revisi

| Versi | Tanggal | Pelaksana | Ringkasan Perubahan | Referensi Commit |
| :--- | :--- | :--- | :--- | :--- |
| **v0.7.2** | 2026-11-07 | AI | **Tukar permen dengan geser**: drag/swipe ke kiri/kanan/atas/bawah (ambang 30% sel), klik dua permen tetap bisa. Geseran yang tidak menghasilkan match dibatalkan tanpa memakai langkah. Diuji 20 pemeriksaan logika + drag mouse asli di browser (memakai 1 langkah, skor naik, tanpa exception) | `7d0aaaa` |
| **v0.7.1** | 2026-11-07 | AI | **Fix kritis**: membuka Macaron Match membuat seluruh game beku (error `renderMatch` sebelum papan ada → rAF mati). Papan disiapkan saat membuka menu + guard papan kosong. **Home langsung tampil** dengan input nama di dalamnya (modal nama dihapus), favicon ditambahkan. Diuji 40 pemeriksaan + alur klik nyata di browser (tanpa exception) | `962cd5c` |
| **v0.7.0** | 2026-11-07 | AI | **Dua game dalam satu halaman**: layar Home "Macaron Arcade", game kedua **Macaron Match** (match-3 8×8, 25 langkah, cascade combo, gravity + refill, anti-match awal, anti-papan buntu), leaderboard dipisah per game dengan tab. HUD menyesuaikan mode. Diuji 56 pemeriksaan termasuk regresi Break | `bc28f93` |
| **v0.6.0** | 2026-11-07 | AI | **Power-up**: 4 item jatuh dari balok (peluang 18%) — Paddle Lebar 1,6× 12 dtk, Bola Ganda +2 bola, Bola Lambat 0,65× 8 dtk, Nyawa +1 (maks 5). Bola cadangan dipakai sebelum nyawa berkurang, pill durasi di atas papan, item & bola ikut rotasi layar. Diuji 34 pemeriksaan | `b095cac` |
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
