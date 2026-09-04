# Modul 02: Perintah Dasar Git

Setelah melakukan konfigurasi identitas di Modul 01, saatnya kita mempelajari perintah yang akan digunakan setiap hari saat menulis kode.

---

## 1. Inisialisasi Repositori (`git init`)

Untuk mulai melacak sebuah folder proyek menggunakan Git:

```bash
cd /path/ke/folder-proyek
git init
```

Perintah ini akan membuat subfolder tersembunyi bernama `.git`. Folder `.git` inilah database tempat Git menyimpan seluruh riwayat perubahan proyek Anda.

---

## 2. Memeriksa Status (`git status`)

Perintah paling sering dipanggil dalam Git:

```bash
git status
```

Perintah ini memberi tahu Anda:
- Anda sedang berada di branch mana.
- File mana yang baru dibuat (Untracked files).
- File mana yang diubah tetapi belum dimasukkan ke Staging Area (Changes not staged for commit).
- File mana yang sudah siap di-commit (Changes to be committed).

---

## 3. Menambahkan File ke Staging Area (`git add`)

Sebelum menyimpan perubahan (commit), Anda harus menaruh file ke staging area:

```bash
# Menambahkan satu file tertentu
git add index.html

# Menambahkan beberapa file sekaligus
git add index.html style.css

# Menambahkan SELURUH file yang berubah di folder saat ini
git add .
```

---

## 4. Menyimpan Snapshot / Riwayat (`git commit`)

Commit adalah titik penyimpanan (checkpoint / save-point) permanen dalam riwayat proyek.

```bash
git commit -m "feat: membuat struktur dasar halaman utama"
```

> 💡 **Tips Menulis Commit Message yang Baik (Standar Industri):**
> Gunakan format **Conventional Commits**:
> - `feat:` Menambahkan fitur baru (contoh: `feat: tambah tombol checkout`)
> - `fix:` Memperbaiki bug/error (contoh: `fix: perbaiki validasi nomor hp`)
> - `docs:` Mengubah dokumentasi/README (contoh: `docs: perbarui panduan install`)
> - `style:` Format tampilan tanpa mengubah fungsionalitas (contoh: `style: rapikan indentasi`)
> - `refactor:` Mengubah struktur kode tanpa merubah fungsi (contoh: `refactor: pisah fungsi kalkulasi diskon`)
> - `test:` Menambah atau memodifikasi unit test (contoh: `test: tambah test case login`)
> - `chore:` Pemeliharaan rutin/konfigurasi (contoh: `chore: update dependencies`)

---

## 5. Melihat Riwayat Commit (`git log`)

Untuk melihat daftar riwayat commit yang pernah dilakukan:

```bash
# Tampilan standar lengkap (Author, Tanggal, Pesan)
git log

# Tampilan ringkas satu baris per commit
git log --oneline

# Tampilan grafis visual (bagus untuk melihat cabang/branch)
git log --oneline --graph --all --decorate
```

---

## 6. Memeriksa Perbedaan Kode (`git diff`)

Sebelum memasukkan ke staging atau sebelum commit, Anda bisa melihat baris mana yang ditambah (+) atau dihapus (-):

```bash
# Melihat perbedaan file di Working Directory dengan commit terakhir
git diff

# Melihat perbedaan file yang SUDAH di Staging Area dengan commit terakhir
git diff --staged
```

---

## 🧪 Simulasi Praktik Mandiri

Mari kita coba langsung perintah-perintah di atas:

1. Buat file baru bernama `catatan.txt`:
   ```bash
   echo "Belajar Git itu menyenangkan!" > catatan.txt
   ```
2. Cek status:
   ```bash
   git status
   ```
   *(Anda akan melihat `catatan.txt` berwarna merah sebagai untracked file)*

3. Masukkan ke Staging:
   ```bash
   git add catatan.txt
   git status
   ```
   *(Sekarang `catatan.txt` berwarna hijau)*

4. Simpan perubahan ke riwayat Git:
   ```bash
   git commit -m "docs: tambah file catatan awal"
   ```

5. Cek riwayat commit:
   ```bash
   git log --oneline
   ```

Selamat! Anda sudah berhasil membuat commit pertama Anda.

➡️ Lanjut ke: **[Modul 03: Branching dan Merging](03-branching-dan-merging.md)**

