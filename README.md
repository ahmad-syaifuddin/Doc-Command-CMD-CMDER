# 📚 Dokumentasi Command CMD/CMDER

> Kumpulan perintah-perintah penting untuk development dan manajemen project

---

## 📋 Daftar Isi

- [Copy Project Tanpa Git History](#copy-project-tanpa-git-history)
- [Command Dasar Git](#command-dasar-git)
- [Command Dasar File Management](#command-dasar-file-management)
- [Troubleshooting Laravel](#troubleshooting-laravel)

---

## 🚀 Copy Project Tanpa Git History

### Tujuan
Membuat project baru (SIDESA Pro) yang benar-benar independen dari project lama (SIDESA) tanpa membawa riwayat git, bukan fork, dan bukan cabang.

### ✅ Langkah-langkah

#### 1️⃣ Masuk ke Folder Project Lama

```bash
cd D:\Project\SIDESA
```

#### 2️⃣ Copy Seluruh Isi ke Folder Baru

```bash
cd ..
xcopy SIDESA SIDESA_PRO /E /I
```

**Keterangan:**
- `/E` - Copy semua subdirektori termasuk yang kosong
- `/I` - Jika tujuan tidak ada, anggap sebagai direktori

> 💡 **Alternatif:** Bisa juga copy manual lewat File Explorer

#### 3️⃣ Masuk ke Folder Baru

```bash
cd SIDESA_PRO
```

#### 4️⃣ Hapus Riwayat Git Lama

```bash
rmdir /s /q .git
```

**Keterangan:**
- `/s` - Hapus folder beserta isinya
- `/q` - Mode quiet (tidak minta konfirmasi)

> ⚠️ **PENTING:** Langkah ini wajib dilakukan agar repo tidak terhubung dengan repo lama!

#### 5️⃣ Verifikasi Penghapusan Git

```bash
dir /a
```

> ✅ Pastikan folder `.git` tidak muncul dalam list

#### 6️⃣ Inisialisasi Git Baru

```bash
git init
```

#### 7️⃣ Tambahkan Semua File & Commit Pertama

```bash
git add .
git commit -m "Initial commit - SIDESA Pro version"
```

#### 8️⃣ Buat Repository Baru di GitHub

1. Buka [GitHub](https://github.com)
2. Klik **New Repository**
3. Beri nama: `sidesa-pro`
4. Pilih **Private** atau **Public** sesuai kebutuhan
5. **Jangan** centang "Initialize with README"
6. Klik **Create Repository**

#### 9️⃣ Hubungkan ke Repository GitHub

```bash
git remote add origin https://github.com/username/sidesa-pro.git
```

> 📝 Ganti `username` dengan username GitHub kamu

#### 🔟 Push Project ke GitHub

```bash
git branch -M main
git push -u origin main
```

---

## 🎯 Hasil Akhir

| Project | Status | Keterangan |
|---------|--------|------------|
| **SIDESA** | Repo lama | Public/Free version, histori tetap ada |
| **SIDESA Pro** | Repo baru | Private version, tanpa histori commit lama |

✨ Kedua project sekarang **benar-benar independen** dan bisa dikembangkan secara terpisah!

---

## 💡 Tips & Tricks

### Sync Fitur dari SIDESA ke SIDESA Pro

**Metode Manual:**

```bash
# Copy file tertentu
copy D:\Project\SIDESA\app\Controllers\FeatureController.php D:\Project\SIDESA_PRO\app\Controllers\
```

**Metode Git Cherry-Pick:**

```bash
# Tambahkan remote SIDESA lama
git remote add sidesa-old https://github.com/username/sidesa.git

# Fetch commits
git fetch sidesa-old

# Cherry-pick commit tertentu
git cherry-pick <commit-hash>
```

### Setting Repository Private

Di GitHub:
1. Buka repository **sidesa-pro**
2. Klik **Settings**
3. Scroll ke bawah ke bagian **Danger Zone**
4. Klik **Change visibility** → **Make private**

---

## 📦 Command Dasar File Management

### Navigasi Folder

```bash
# Lihat isi folder
dir

# Lihat semua file termasuk hidden
dir /a

# Masuk ke folder
cd nama_folder

# Kembali ke folder parent
cd ..

# Pindah ke drive lain
D:
```

### Copy & Move

```bash
# Copy file
copy source.txt destination.txt

# Copy folder beserta isi
xcopy source_folder dest_folder /E /I

# Pindah file
move source.txt destination.txt

# Rename file
ren old_name.txt new_name.txt
```

### Create & Delete

```bash
# Buat folder
mkdir nama_folder

# Hapus file
del nama_file.txt

# Hapus folder kosong
rmdir nama_folder

# Hapus folder beserta isi (hati-hati!)
rmdir /s /q nama_folder
```

---

## 🔧 Command Dasar Git

### Inisialisasi & Status

```bash
# Init git baru
git init

# Cek status
git status

# Cek history
git log
git log --oneline
```

### Add & Commit

```bash
# Add file spesifik
git add nama_file.php

# Add semua file
git add .

# Commit dengan message
git commit -m "Deskripsi perubahan"

# Add dan commit sekaligus (untuk file yang sudah tracked)
git commit -am "Deskripsi perubahan"
```

### Branch Management

```bash
# Lihat semua branch
git branch

# Buat branch baru
git branch nama_branch

# Pindah branch
git checkout nama_branch

# Buat dan pindah branch sekaligus
git checkout -b nama_branch

# Hapus branch
git branch -d nama_branch

# Rename branch
git branch -M old_name new_name
```

### Remote & Push/Pull

```bash
# Tambah remote
git remote add origin url_repo

# Lihat remote
git remote -v

# Push ke remote
git push origin main

# Push dengan set upstream
git push -u origin main

# Pull dari remote
git pull origin main

# Clone repository
git clone url_repo
```

### Undo Changes

```bash
# Buang perubahan file (belum staged)
git checkout -- nama_file.php

# Unstage file
git reset nama_file.php

# Undo commit terakhir (keep changes)
git reset --soft HEAD~1

# Undo commit terakhir (discard changes)
git reset --hard HEAD~1
```

---

## 🐛 Troubleshooting Laravel

### Cari File dengan Pattern Tertentu

```bash
# Cari semua file yang mengandung teks tertentu
grep -r "background-attachment" resources/views/

# Cari di Windows CMD (alternative)
findstr /s /i "background-attachment" resources\views\*.*
```

### Clear Cache Laravel

```bash
# Clear semua cache
php artisan cache:clear
php artisan config:clear
php artisan route:clear
php artisan view:clear

# Clear semuanya sekaligus
php artisan optimize:clear
```

### Permission Issues (Linux/Mac)

```bash
# Set permission untuk storage dan cache
chmod -R 775 storage bootstrap/cache

# Set ownership
chown -R www-data:www-data storage bootstrap/cache
```

### Database Commands

```bash
# Jalankan migration
php artisan migrate

# Rollback migration
php artisan migrate:rollback

# Fresh migration (hati-hati, hapus semua data!)
php artisan migrate:fresh

# Seed database
php artisan db:seed

# Fresh migration + seed
php artisan migrate:fresh --seed
```

### Development Server

```bash
# Jalankan server
php artisan serve

# Jalankan di port tertentu
php artisan serve --port=8080

# Jalankan dengan host tertentu
php artisan serve --host=192.168.1.100
```

---

## 📌 Command Shortcuts yang Berguna

```bash
# Bersihkan terminal
cls              # Windows
clear            # Linux/Mac

# Keluar dari terminal
exit

# Cek versi Git
git --version

# Cek versi PHP
php -v

# Cek versi Composer
composer -v

# Cek versi Node
node -v

# Cek versi NPM
npm -v
```

---

## 🆘 Masalah Umum & Solusi

### Git: "fatal: not a git repository"

**Solusi:**

```bash
git init
```

### Git: Push ditolak (non-fast-forward)

**Solusi:**

```bash
# Pull dulu, baru push
git pull origin main --rebase
git push origin main

# Atau force push (hati-hati!)
git push -f origin main
```

### Laravel: Class not found

**Solusi:**

```bash
composer dump-autoload
```

### Laravel: Permission denied

**Solusi Windows:**

```bash
# Jalankan CMD/PowerShell sebagai Administrator
```

**Solusi Linux/Mac:**

```bash
sudo chmod -R 775 storage bootstrap/cache
```

---

## 📚 Resources

- [Git Documentation](https://git-scm.com/doc)
- [Laravel Documentation](https://laravel.com/docs)
- [GitHub Guides](https://guides.github.com)

---

**Happy Coding!**

*Dokumentasi ini dibuat untuk mempermudah workflow development. Jangan lupa backup data penting sebelum menjalankan command yang berbahaya!*
