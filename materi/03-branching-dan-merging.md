# Modul 03: Branching dan Merging

Branch (cabang) adalah salah satu fitur paling penting dan paling kuat di Git. Branch memungkinkan Anda bekerja pada fitur baru atau perbaikan bug tanpa mengganggu kode utama (`main` / `master`).

---

## 1. Mengapa Kita Butuh Branch?

Bayangkan kode di branch `main` adalah aplikasi yang sudah berjalan di production (digunakan oleh user).

Jika Anda ingin membuat fitur baru atau eksperimen:
- Anda **tidak boleh** langsung mengedit di `main`.
- Anda membuat cabang baru bernama `fitur-keranjang`.
- Jika fitur sudah selesai dan dites dengan baik, cabang tersebut digabungkan kembali (*merge*) ke `main`.
- Jika eksperimen gagal, Anda cukup menghapus cabang tersebut tanpa merusak `main`.

```
        C --- D  (fitur-keranjang)
       /        \
A --- B --------- E (main setelah di-merge)
```

---

## 2. Perintah Dasar Branch

### Melihat Daftar Branch
```bash
git branch
```
Branch yang sedang aktif akan ditandai dengan tanda bintang `*` dan berwarna hijau.

### Membuat Branch Baru
```bash
git branch fitur-navbar
```

### Berpindah ke Branch Lain
Ada dua cara (cara modern menggunakan `git switch`):
```bash
# Cara modern (disarankan):
git switch fitur-navbar

# Cara lama:
git checkout fitur-navbar
```

### Membuat dan Langsung Berpindah ke Branch Baru (Shorthand)
```bash
# Cara modern (disarankan):
git switch -c fitur-footer

# Cara lama:
git checkout -b fitur-footer
```

### Menghapus Branch
Hanya bisa dilakukan jika Anda sedang TIDAK berada di branch tersebut.
```bash
# Hapus branch yang sudah di-merge (aman)
git branch -d fitur-footer

# Hapus paksa branch (meskipun belum di-merge)
git branch -D fitur-footer
```

---

## 3. Menggabungkan Branch (`git merge`)

Untuk menggabungkan perubahan dari branch lain ke branch saat ini:

1. Pindah dulu ke branch tujuan (biasanya `main`):
   ```bash
   git switch main
   ```
2. Jalankan perintah merge dengan menyebutkan nama branch sumber:
   ```bash
   git merge fitur-navbar
   ```

### Jenis-Jenis Merge:
1. **Fast-Forward Merge:** Terjadi jika branch `main` tidak memiliki commit baru sejak branch fitur dibuat. Git hanya memindahkan pointer `main` maju ke depan.
2. **Three-Way Merge (Merge Commit):** Terjadi jika branch `main` dan branch fitur sama-sama memiliki commit baru yang independen. Git akan membuat satu commit baru khusus penggabungan.

---

## 🧪 Simulasi Praktik Mandiri

Mari kita simulasikan alur kerja percabangan:

1. Pastikan Anda berada di branch `main`:
   ```bash
   git switch main
   ```
2. Buat branch baru untuk fitur login:
   ```bash
   git switch -c fitur-login
   ```
3. Buat file baru untuk fitur ini:
   ```bash
   echo "function login() { return true; }" > login.js
   git add login.js
   git commit -m "feat: tambah fungsi login"
   ```
4. Pindah kembali ke branch `main`:
   ```bash
   git switch main
   ```
   *(Periksa folder Anda: file `login.js` menghilang sementara, karena file tersebut hanya ada di branch `fitur-login`)*

5. Gabungkan fitur login ke branch `main`:
   ```bash
   git merge fitur-login
   ```
   *(Sekarang file `login.js` sudah ada di branch `main`!)*

6. Bersihkan branch fitur yang sudah selesai:
   ```bash
   git branch -d fitur-login
   ```

---

Lalu apa yang terjadi jika ada dua branch yang mengubah **baris file yang sama** secara bersamaan? Jawabannya adalah **Merge Conflict**.

➡️ Lanjut ke: **[Modul 04: Menangani Merge Conflict](04-simulasi-merge-conflict.md)**

