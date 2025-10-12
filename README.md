# Command atau Perintah perintah di CMD ataupun di CMDER

## Tujuan
Kamu ingin:
Copy project SIDESA, tapi supaya repo baru (SIDESA Pro) benar-benar independen — bukan fork, bukan cabang, gak punya riwayat git lama.

### 💣 Cara Aman (Langkah Manual, Rapi, Tanpa Bawa Sejarah Git)

Buka folder project lama kamu.
Misal:

```bash
cd D:\Project\SIDESA
```

Copy seluruh isi folder ke folder baru.
Contoh:

```bash
cd ..
xcopy SIDESA SIDESA_PRO /E /I
```

(atau bisa manual lewat File Explorer juga boleh.)

Masuk ke folder baru:

```bash
cd SIDESA_PRO
```

Hapus seluruh riwayat git lama:

```bash
rmdir /s /q .git
```

⚠️ Ini penting banget! Karena kalau gak dihapus, repo-nya masih dianggap “terhubung” dengan repo lama.

Inisialisasi Git baru:

```bash
git init
```

Tambahkan semua file & commit pertama:

```bash
git add .
git commit -m "Initial commit - SIDESA Pro version"
```

Buat repository baru di GitHub:
Misal nama repo-nya sidesa-pro.

Hubungkan ke repo GitHub baru:

```bash
git remote add origin https://github.com/username/sidesa-pro.git
```

Push project-nya:

```bash
git branch -M main
git push -u origin main
```

🎯 Hasil Akhir

SIDESA → tetap di repo lama (public/free version).

SIDESA_PRO → repo baru, tanpa histori commit lama.

Keduanya benar-benar independen, bisa kamu kembangkan secara terpisah.

🧠 Tips Bonus

Kalau nanti kamu mau sync fitur tertentu dari SIDESA ke SIDESA Pro, pakai cara manual aja:

Misal: copy file tertentu.

Atau patch via commit tertentu (kalau kamu masih punya akses ke repo lama).

Kalau kamu mau SIDESA Pro bersifat “private”, atur repo GitHub-nya ke private.


### Kalau kamu mau aku bantu cek apakah folder .git beneran gak ada, jalankan ini:

```bash
dir /a
```

Kalau di situ gak muncul .git, berarti fix udah bersih 🔥

---

# Solusi 3: Periksa background-attachment: fixed
Pastikan benar-benar sudah dihapus dari _hero.blade.php. Buka file dan cari background-attachment:

```bash 
# Di terminal Laravel, cari semua file yang mengandung background-attachment
grep -r "background-attachment" resources/views/
```
Jika masih ada, hapus semua background-attachment: fixed;
