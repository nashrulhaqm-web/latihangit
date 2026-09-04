# Modul 07: Git Cheatsheet & Troubleshooting

Simpan halaman ini sebagai contekan cepat Anda sehari-hari saat menulis kode.

---

## ⚡ 1. Tabel Contekan Perintah Populer (Cheatsheet)

### Konfigurasi & Inisialisasi
```bash
git config --global user.name "Nama Anda"        # Setel nama
git config --global user.email "email@anda.com"  # Setel email
git init                                        # Inisialisasi repo lokal baru
git clone <url-repo>                            # Kloning repo dari internet
```

### Siklus Kerja Harian
```bash
git status                                      # Cek status file (untracked, staged)
git add <file>                                  # Masukkan file spesifik ke staging
git add .                                       # Masukkan SEMUA perubahan ke staging
git commit -m "feat: pesan commit"              # Simpan snapshot perubahan
git diff                                        # Lihat perbedaan kode belum di-add
git diff --staged                               # Lihat perbedaan kode yang sudah di-add
git log --oneline --graph --all                 # Lihat histori commit rapi & grafis
```

### Percabangan (Branching)
```bash
git branch                                      # Daftar branch lokal
git branch <nama-branch>                        # Buat branch baru
git switch <nama-branch>                        # Pindah ke branch tertentu
git switch -c <nama-branch>                     # Buat dan langsung pindah ke branch baru
git merge <nama-branch>                         # Gabungkan branch ke branch saat ini
git branch -d <nama-branch>                     # Hapus branch yang sudah di-merge
```

### Sinkronisasi Remote & GitHub
```bash
git remote add origin <url-repo>                # Hubungkan ke repo GitHub
git remote -v                                   # Lihat URL remote yang terdaftar
git push -u origin main                         # Push pertama kali & set upstream
git push                                        # Push commit berikutnya
git pull                                        # Tarik perubahan terbaru dari GitHub
git fetch                                       # Unduh riwayat terbaru tanpa auto-merge
```

### Penyelamatan & Pembatalan (Undo)
```bash
git stash                                       # Simpan sementara kerjaan yang belum di-commit
git stash pop                                   # Ambil kembali kerjaan dari stash
git restore <file>                              # Buang perubahan pada file belum di-add
git restore --staged <file>                     # Keluarkan file dari staging area
git commit --amend -m "pesan baru"              # Revisi pesan commit terakhir
git reset --soft HEAD~1                         # Batalkan commit terakhir, kode tetap aman
git revert <hash-commit>                        # Batalkan commit publik secara aman
```

---

## 🆘 2. Troubleshooting: Solusi Masalah Populer di Lapangan

### Masalah 1: "Updates were rejected because the remote contains work..." saat `git push`
**Penyebab:** Ada orang lain (atau Anda sendiri via web) yang sudah push commit baru ke GitHub, sehingga lokal Anda tertinggal.
**Solusi:**
```bash
git pull origin main
# Jika ada konflik, selesaikan konflik lalu commit
git push origin main
```

---

### Masalah 2: "fatal: refusing to merge unrelated histories"
**Penyebab:** Repo lokal dan repo GitHub Anda dibuat secara terpisah sehingga tidak memiliki commit awal yang sama.
**Solusi:**
```bash
git pull origin main --allow-unrelated-histories
```

---

### Masalah 3: Terjebak di "Detached HEAD state"
**Penyebab:** Anda melakukan `git checkout <hash-commit>` ke commit lama alih-alih checkout ke nama branch.
**Solusi:** Cukup kembali ke branch normal Anda:
```bash
git switch main
```

---

### Masalah 4: File Rahasia (`.env`) Tidak Sengaja Ter-commit
**Penyebab:** Anda lupa menambahkan `.env` ke `.gitignore` sebelum melakukan `git add .`.
**Solusi:**
1. Tambahkan `.env` ke dalam file `.gitignore`.
2. Hapus file `.env` dari pelacakan Git (tanpa menghapus file aslinya di laptop):
   ```bash
   git rm --cached .env
   git commit -m "chore: stop tracking file .env"
   ```

---

### Masalah 5: Ingin Keluar dari Tampilan `git log`
Jika terminal Anda macet menampilkan riwayat log bertanda titik dua `:` di pojok bawah:
- Tekan huruf **`q`** di keyboard untuk keluar (*quit*).

---

## 🚀 3. Tips Pro: Menyiapkan Shortcut (Git Alias)

Agar tidak lelah mengetik perintah yang panjang, daftarkan shortcut favorit ini:

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.sw switch
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.lg "log --oneline --graph --decorate --all"
```

Sekarang Anda bisa mengetik:
- `git st` (setara `git status`)
- `git lg` (setara `git log` grafis indah)
- `git sw -c fitur-baru` (setara `git switch -c fitur-baru`)

---

➡️ Siap uji kemampuan? Kerjakan: **[Studi Kasus & Skenario Latihan Mandiri](../latihan/STUDI_KASUS.md)**

