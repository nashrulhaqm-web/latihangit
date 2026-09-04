# Modul 01: Pengenalan dan Konfigurasi Git

## 1. Apa itu Git & Version Control System (VCS)?

**Version Control System (VCS)** adalah sistem yang merekam perubahan pada satu atau sekumpulan file dari waktu ke waktu, sehingga Anda dapat memanggil kembali versi tertentu di kemudian hari.

Tanpa Git, sering kali orang menyimpan file seperti ini:
```
skripsi_final.docx
skripsi_final_revisi.docx
skripsi_final_revisi_beneran.docx
skripsi_final_fix_banget_bismillah.docx
```
Dengan Git, Anda hanya memiliki satu file proyek yang rapi, namun memiliki catatan sejarah (history) lengkap: siapa yang mengubah, kapan diubah, apa yang diubah, dan mengapa diubah.

---

## 2. Perbedaan Git dan GitHub

| Pembeda | Git | GitHub |
| :--- | :--- | :--- |
| **Sifat** | Software / Alat (Command Line Tool) | Layanan berbasis web (Cloud Platform) |
| **Lokasi** | Berjalan secara lokal di komputer Anda | Berada di server internet milik Microsoft |
| **Koneksi** | Bekerja secara *offline* (tanpa internet) | Membutuhkan koneksi internet |
| **Fungsi Utama** | Melacak histori revisi kode | Tempat menyimpan repository Git, kolaborasi tim, Code Review, CI/CD |

> **Analogi:** Git itu seperti kamera (alat pembuat foto/rekaman), sedangkan GitHub itu seperti Instagram (platform cloud untuk memamerkan dan berbagi rekaman tersebut ke orang lain).

---

## 3. Konsep 3 Area Utama Git (Git Architecture)

Sebelum menjalankan perintah apapun, Anda wajib memahami 3 zona kerja Git:

```
+-------------------+      git add       +-------------------+     git commit     +-------------------+
|                   |  --------------->  |                   |  --------------->  |                   |
| Working Directory |                    |   Staging Area    |                    | Repository (Git)  |
| (Tempat edit file)|  <---------------  | (Area seleksi)    |                    | (Histori tersimpan|
+-------------------+     git restore    +-------------------+                    | secara permanen)  |
                                                                                  +-------------------+
```

1. **Working Directory:** Folder lokal tempat Anda membuat, mengedit, atau menghapus file secara nyata.
2. **Staging Area (Index):** Area persiapan atau "keranjang belanja". Anda memilih file mana saja yang ingin disertakan ke dalam commit berikutnya.
3. **Repository (Local Commit):** Database Git (`.git/`) yang menyimpan snapshot perubahan secara permanen setelah di-commit.

---

## 4. Konfigurasi Awal (Wajib Setelah Install Git)

Sebelum membuat commit pertama, kenalkan identitas Anda kepada Git. Identitas ini akan menempel pada setiap catatan commit yang Anda buat.

Buka terminal dan jalankan:

```bash
# 1. Atur Nama Lengkap Anda
git config --global user.name "Nama Lengkap Anda"

# 2. Atur Email (Gunakan email yang sama dengan akun GitHub Anda)
git config --global user.email "emailanda@example.com"

# 3. Atur nama default branch utama menjadi 'main' (standar modern industri)
git config --global init.defaultBranch main

# 4. Atur penanganan baris baru (CRLF/LF)
# Untuk pengguna macOS / Linux:
git config --global core.autocrlf input
# (Jika di Windows gunakan: git config --global core.autocrlf true)
```

### Memeriksa Konfigurasi:
Untuk memastikan konfigurasi sudah tersimpan dengan benar:

```bash
git config --list
```
Atau cek spesifik nama dan email:
```bash
git config user.name
git config user.email
```

---

## 🎯 Ringkasan Langkah
1. Pahami bahwa Git berjalan lokal tanpa butuh internet.
2. Ingat siklus: **Edit File** -> **Add ke Staging** -> **Commit ke Repository**.
3. Pastikan `user.name` dan `user.email` sudah tersetel.

➡️ Lanjut ke: **[Modul 02: Perintah Dasar Git](02-perintah-dasar-git.md)**

