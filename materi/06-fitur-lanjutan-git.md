# Modul 06: Fitur Lanjutan & Membatalkan Perubahan (Undo)

Dalam dunia nyata, developer sering kali salah ketik, kelupaan memasukkan file, atau tiba-tiba harus beralih tugas mendesak di tengah pengerjaan fitur. Git menyediakan alat canggih untuk mengatasi situasi ini.

---

## 1. Mengabaikan File dengan `.gitignore`

Tidak semua file perlu dilacak oleh Git. File seperti password/kredensial (`.env`), folder dependensi raksasa (`node_modules/`, `venv/`), atau file sistem OS (`.DS_Store`) **wajib diabaikan**.

Cukup buat file bernama `.gitignore` di root proyek Anda, lalu tulis nama file/folder yang ingin diabaikan:
```gitignore
# Abaikan folder dependensi
node_modules/
venv/

# Abaikan file konfigurasi rahasia
.env
*.pem

# Abaikan file sistem OS
.DS_Store
Thumbs.db
```

---

## 2. Menyimpan Sementara Perubahan (`git stash`)

Bayangkan Anda sedang asyik membuat fitur baru (belum selesai dan belum siap di-commit), tiba-tiba atasan meminta Anda segera memperbaiki bug kritis di `main`. Jika Anda langsung berpindah branch, Git akan menolaknya atau perubahan Anda terbawa.

Solusinya: gunakan **`git stash`** (kantong ajaib untuk menyimpan pekerjaan sementara).

```bash
# 1. Simpan perubahan yang belum selesai ke dalam stash
git stash save "pengerjaan fitur navbar belum selesai"

# 2. Sekarang working directory Anda bersih! Anda bebas pindah branch
git switch main
# (Lakukan perbaikan bug, commit, push...)

# 3. Kembali ke branch fitur Anda
git switch fitur-navbar

# 4. Lihat daftar perubahan yang tersimpan di stash
git stash list

# 5. Kembalikan perubahan tadi dan keluarkan dari stash
git stash pop
```

Perintah stash lainnya:
- `git stash apply`: Mengembalikan perubahan tanpa menghapusnya dari daftar stash.
- `git stash drop`: Menghapus satu simpanan stash.
- `git stash clear`: Menghapus seluruh riwayat stash.

---

## 3. Memperbaiki Commit Terakhir (`git commit --amend`)

Jika Anda baru saja melakukan commit, lalu sadar:
- Ada saltik (typo) pada pesan commit.
- Ada satu file kecil yang kelupaan di-`git add`.

Cukup tambahkan filenya, lalu jalankan:
```bash
git add file-ketinggalan.txt
git commit --amend -m "feat: pesan commit yang sudah diperbaiki"
```
*(Perintah ini akan menggantikan commit terakhir tanpa membuat commit baru)*

---

## 4. Berbagai Cara Membatalkan Perubahan (Undo)

| Kondisi Masalah | Perintah Solusi | Penjelasan |
| :--- | :--- | :--- |
| File diedit, belum di-`add`, ingin kembali ke versi semula | `git restore <nama-file>` | Membatalkan perubahan di working directory. |
| File sudah di-`add` (ada di Staging), ingin dikeluarkan dari Staging | `git restore --staged <nama-file>` | Mengembalikan file dari Staging ke Working Directory. |
| Sudah di-commit lokal, ingin batalkan commit tapi KODE TETAP ADA di editor | `git reset --soft HEAD~1` | Mundur 1 commit, file tetap ada di Staging Area. |
| Sudah di-commit lokal, ingin BUANG SEMUA KODE dan balik ke commit sebelumnya | `git reset --hard HEAD~1` | ⚠️ **Hati-hati**: Kode yang belum di-commit akan hilang permanen! |
| Kode sudah di-PUSH ke GitHub publik, ingin membatalkan fiturnya | `git revert <hash-commit>` | Membuat commit baru yang isinya kebalikan dari commit lama (Aman untuk tim). |

### Mengapa Harus `revert`, Bukan `reset` untuk Kode yang Sudah Dipush?
Jika commit sudah berada di GitHub dan ditarik oleh anggota tim lain:
- Melakukan `git reset` akan mengubah sejarah Git, menyebabkan konflik fatal di komputer rekan tim Anda.
- Melakukan `git revert` tidak menghapus sejarah lama, melainkan menambahkan commit baru yang menetralisir perubahan sebelumnya.

---

## 5. Mengambil Commit Tertentu (`git cherry-pick`)

Jika Anda berada di branch `main`, dan hanya ingin mengambil **satu commit tertentu** dari branch `fitur-eksperimen` tanpa harus men-merge seluruh isi branch tersebut:

```bash
# 1. Cari hash commit yang diinginkan dari branch fitur
git log --oneline fitur-eksperimen

# 2. Terapkan commit tersebut ke branch saat ini
git cherry-pick a1b2c3d
```

---

➡️ Lanjut ke: **[Modul 07: Git Cheatsheet & Troubleshooting](07-git-cheatsheet.md)**

