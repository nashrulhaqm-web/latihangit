# Modul 04: Menangani Merge Conflict

Banyak pemula merasa panik ketika melihat pesan **Merge Conflict**. Padahal, konflik adalah hal yang normal dan wajar terjadi dalam kerja tim.

---

## 1. Apa itu Merge Conflict?

Merge conflict terjadi ketika:
1. Dua branch berbeda mengedit **baris yang sama pada file yang sama** dengan isi yang berbeda.
2. Satu orang mengedit sebuah file sementara orang lain menghapus file tersebut.

Git cukup pintar untuk menggabungkan kode secara otomatis jika perubahannya berada di baris atau file yang berbeda. Namun jika barisnya sama persis, Git tidak tahu versi mana yang benar, sehingga Git meminta Anda (manusia) untuk memutuskan.

---

## 2. Mengenal Tanda Konflik (Conflict Markers)

Saat terjadi konflik, Git akan menyisipkan penanda khusus langsung ke dalam file kode:

```javascript
<<<<<<< HEAD (Current Change)
const warnaTombol = "biru";
=======
const warnaTombol = "merah";
>>>>>>> fitur-tombol-merah (Incoming Change)
```

Penjelasannya:
- `<<<<<<< HEAD`: Kode yang saat ini ada di branch aktif Anda (misalnya `main`).
- `=======`: Garis pemisah antara kedua perubahan yang bertentangan.
- `>>>>>>> [nama-branch]`: Kode dari branch yang ingin Anda gabungkan (*incoming change*).

---

## 🧪 3. Simulasi Praktik: Membuat dan Menyelesaikan Konflik

Mari kita buat konflik secara sengaja agar Anda terbiasa menyelesaikannya!

### Langkah 1: Buat kondisi awal di `main`
```bash
git switch main
echo "Judul Aplikasi: Toko Kopi Jaya" > judul.txt
git add judul.txt
git commit -m "docs: tambah judul aplikasi"
```

### Langkah 2: Buat branch `desain-modern` dan ubah teksnya
```bash
git switch -c desain-modern
# Ubah judul.txt
echo "Judul Aplikasi: Coffee Shop Modern 2026" > judul.txt
git add judul.txt
git commit -m "feat: perbarui judul gaya modern"
```

### Langkah 3: Kembali ke `main` dan ubah teks yang sama dengan kata berbeda
```bash
git switch main
# Ubah judul.txt dengan versi lain
echo "Judul Aplikasi: Warkop Tradisional Nusantara" > judul.txt
git add judul.txt
git commit -m "feat: perbarui judul gaya tradisional"
```

### Langkah 4: Coba gabungkan branch `desain-modern` ke `main`
```bash
git merge desain-modern
```

⚠️ **Terminal akan menampilkan pesan:**
```text
Auto-merging judul.txt
CONFLICT (content): Merge conflict in judul.txt
Automatic merge failed; fix conflicts and then commit the result.
```

---

## 4. Cara Menyelesaikan Konflik

1. Buka file yang berkonflik (`judul.txt`) menggunakan text editor / VS Code Anda. Isinya akan tampak seperti ini:
   ```text
   <<<<<<< HEAD
   Judul Aplikasi: Warkop Tradisional Nusantara
   =======
   Judul Aplikasi: Coffee Shop Modern 2026
   >>>>>>> desain-modern
   ```

2. Tentukan keputusan Anda:
   - Mau pakai versi `HEAD` saja? Hapus versi branch dan tanda pemisahnya.
   - Mau pakai versi `desain-modern` saja? Hapus versi HEAD dan tanda pemisahnya.
   - Atau gabungkan keduanya?

   *Contoh penyelesaian gabungan:*
   ```text
   Judul Aplikasi: Toko Kopi Nusantara Modern
   ```
   *(Pastikan tanda `<<<<<<<`, `=======`, dan `>>>>>>>` **dihapus bersih**!)*

3. Simpan file `judul.txt`.

4. Tandai bahwa konflik sudah diselesaikan:
   ```bash
   git add judul.txt
   ```

5. Lakukan commit untuk menyelesaikan proses merge:
   ```bash
   git commit -m "merge: selesaikan konflik judul aplikasi"
   ```

### Tips: Membatalkan Merge Jika Buntu
Jika Anda berada di tengah merge conflict yang sangat rumit dan ingin membatalkan keadaan kembali ke sebelum merge dijalankan:
```bash
git merge --abort
```

---

➡️ Lanjut ke: **[Modul 05: Kolaborasi dengan GitHub](05-kolaborasi-dengan-github.md)**

