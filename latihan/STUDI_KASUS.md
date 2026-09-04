# 🎯 5 Studi Kasus & Skenario Latihan Mandiri

Gunakan modul ini untuk melatih pemahaman Anda secara langsung. Setiap skenario meniru tugas nyata seorang software engineer di industri.

---

## 📌 Skenario 1: First Commit Proyek Web Sederhana

### Latar Belakang:
Anda baru saja bergabung ke sebuah tim dan diminta untuk menginisialisasi pelacakan Git pada proyek landing page sederhana yang ada di folder `latihan/sample-project/`.

### Tugas Anda:
1. Buka terminal dan masuk ke repositori ini.
2. Periksa status file yang belum terlacak (*untracked*):
   ```bash
   git status
   ```
3. Tambahkan file dokumentasi dan proyek sample ke staging:
   ```bash
   git add README.md .gitignore materi/ latihan/
   ```
4. Lakukan commit pertama dengan format conventional commit:
   ```bash
   git commit -m "feat: inisialisasi modul materi dan sample project"
   ```
5. Periksa histori commit untuk memastikan commit Anda tercatat:
   ```bash
   git log --oneline
   ```

---

## 📌 Skenario 2: Mengembangkan Fitur Baru dengan Branching

### Latar Belakang:
Klien meminta penambahan fitur "Mode Gelap (Dark Mode)" pada file `latihan/sample-project/index.html`. Anda dilarang mengubah langsung di branch `main`.

### Tugas Anda:
1. Buat dan beralih ke branch baru bernama `feat/dark-mode`:
   ```bash
   git switch -c feat/dark-mode
   ```
2. Buka file `latihan/sample-project/style.css` dan tambahkan styling di baris paling bawah:
   ```css
   body.dark-mode {
       background-color: #121212;
       color: #f1f1f1;
   }
   ```
3. Cek perbedaan kode yang baru diubah:
   ```bash
   git diff
   ```
4. Masukkan ke staging dan commit:
   ```bash
   git add latihan/sample-project/style.css
   git commit -m "feat: tambah styling dark mode pada css"
   ```
5. Kembali ke branch `main`:
   ```bash
   git switch main
   ```
   *(Perhatikan bahwa baris dark mode tadi belum ada di branch main)*
6. Gabungkan (*merge*) fitur tersebut ke branch `main`:
   ```bash
   git merge feat/dark-mode
   ```
7. Hapus branch `feat/dark-mode` yang sudah selesai digabung:
   ```bash
   git branch -d feat/dark-mode
   ```

---

## 📌 Skenario 3: Menjinakkan Merge Conflict Dua Pengembang

### Latar Belakang:
Dua developer (Dev A dan Dev B) secara bersamaan mengubah teks tombol call-to-action di `latihan/sample-project/index.html`.

### Tugas Anda:
1. Pastikan Anda berada di branch `main`:
   ```bash
   git switch main
   ```
2. Buat branch simulasi Developer A:
   ```bash
   git switch -c dev-a
   ```
   Ubah teks tombol di `latihan/sample-project/index.html` dari `<button id="btn-cta">Mulai Sekarang</button>` menjadi:
   ```html
   <button id="btn-cta">Daftar Akun Gratis Sekarang</button>
   ```
   Commit perubahan tersebut:
   ```bash
   git add latihan/sample-project/index.html
   git commit -m "feat: perbarui teks tombol versi dev A"
   ```

3. Kembali ke `main`, lalu buat branch simulasi Developer B:
   ```bash
   git switch main
   git switch -c dev-b
   ```
   Ubah baris tombol yang sama menjadi:
   ```html
   <button id="btn-cta">Coba Gratis 14 Hari</button>
   ```
   Commit perubahan tersebut:
   ```bash
   git add latihan/sample-project/index.html
   git commit -m "feat: perbarui teks tombol versi dev B"
   ```

4. Sekarang gabungkan perubahan Dev A ke `main`:
   ```bash
   git switch main
   git merge dev-a
   ```
   *(Proses ini berhasil secara Fast-Forward)*

5. Sekarang coba gabungkan perubahan Dev B ke `main`:
   ```bash
   git merge dev-b
   ```
   💥 **BOOM! Terjadi MERGE CONFLICT!**

6. Buka `latihan/sample-project/index.html` di editor Anda:
   - Bersihkan penanda konflik `<<<<<<<`, `=======`, `>>>>>>>`.
   - Sepakati teks gabungan terbaik, misalnya:
     ```html
     <button id="btn-cta">Daftar Sekarang & Coba Gratis 14 Hari</button>
     ```
7. Simpan file, lalu tuntaskan merge:
   ```bash
   git add latihan/sample-project/index.html
   git commit -m "merge: selesaikan konflik teks tombol CTA"
   ```
8. Bersihkan branch simulasi:
   ```bash
   git branch -d dev-a
   git branch -d dev-b
   ```

---

## 📌 Skenario 4: Darurat Hotfix Saat Pekerjaan Belum Selesai (Menggunakan Stash)

### Latar Belakang:
Anda sedang sibuk merombak JavaScript di branch `refactor-js`. Tiba-tiba ada laporan bug darurat di branch `main` bahwa ada saltik (typo) judul di halaman utama yang harus segera diperbaiki dan dideploy sekarang juga.

### Tugas Anda:
1. Buat branch pekerjaan:
   ```bash
   git switch -c refactor-js
   ```
2. Edit file `latihan/sample-project/app.js` (tambahkan beberapa baris baru, **JANGAN di-commit**).
3. Anda harus segera pindah ke `main`, tapi Git menolak atau Anda tidak ingin perubahan setengah jadi ini berantakan.
4. Simpan sementara perubahan ke stash:
   ```bash
   git stash save "pengerjaan refactor js belum tuntas"
   ```
5. Pindah ke branch `main` dengan aman:
   ```bash
   git switch main
   ```
6. Buat branch hotfix dan perbaiki bug:
   ```bash
   git switch -c hotfix-typo-judul
   # Edit latihan/sample-project/index.html perbaiki typo
   git add latihan/sample-project/index.html
   git commit -m "fix: perbaiki saltik pada heading utama"
   ```
7. Merge hotfix ke `main`:
   ```bash
   git switch main
   git merge hotfix-typo-judul
   git branch -d hotfix-typo-judul
   ```
8. Kembali ke branch fitur Anda dan ambil kembali pekerjaan dari stash:
   ```bash
   git switch refactor-js
   git stash pop
   ```
   *(Pekerjaan refactor Anda kembali tanpa ada yang hilang!)*

---

## 📌 Skenario 5: Menghubungkan ke GitHub Pribadi

### Latar Belakang:
Anda ingin menyimpan seluruh latihan ini di akun GitHub pribadi Anda agar bisa diakses dari mana saja dan mempercantik profil GitHub Anda.

### Tugas Anda:
1. Buka [GitHub](https://github.com), login, buat repo baru bernama `latihan-git` (kosong tanpa README).
2. Tambahkan URL remote GitHub Anda:
   ```bash
   git remote add origin https://github.com/USERNAME-ANDA/latihan-git.git
   ```
3. Verifikasi remote:
   ```bash
   git remote -v
   ```
4. Push seluruh commit lokal ke GitHub:
   ```bash
   git push -u origin main
   ```
5. Buka halaman repository di browser dan periksa riwayat commit serta file Anda!

