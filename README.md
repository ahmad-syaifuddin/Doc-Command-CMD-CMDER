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

# Buka folder di File Explorer dari CMD
start .                    # Buka folder saat ini
start nama_folder          # Buka folder tertentu
start D:\Project\SIDESA    # Buka folder dengan path lengkap

# Buka file dengan aplikasi default
start index.html           # Buka di browser
start document.pdf         # Buka di PDF reader
start image.jpg            # Buka di image viewer
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

## 🔥 Command Tersembunyi yang Jarang Diketahui

### Buka Aplikasi & Folder Cepat

```bash
# Buka folder saat ini di File Explorer
start .

# Buka folder tertentu
start D:\Project\SIDESA

# Buka website di browser default
start https://github.com

# Buka file dengan aplikasi default
start index.html              # Browser
start README.md               # Text editor
start song.mp3                # Media player

# Buka Control Panel & System Settings
control                       # Control Panel
control system                # System Properties
control userpasswords2        # User Accounts
control printers              # Printers & Devices
control folders               # Folder Options

# Buka aplikasi Windows
calc                          # Calculator
notepad                       # Notepad
mspaint                       # Paint
explorer                      # File Explorer
taskmgr                       # Task Manager
```

### Command untuk Development

```bash
# Buka VSCode dari CMD
code .                        # Buka folder saat ini
code nama_file.php            # Buka file tertentu
code -r .                     # Buka di window VSCode yang sudah ada

# Buka dengan editor lain
notepad++ nama_file.php       # Notepad++ (jika installed)
sublime_text .                # Sublime Text (jika installed)
atau
subl .

# Install dependencies dengan cepat
composer install              # Install PHP dependencies
npm install                   # Install Node dependencies
npm install && composer install  # Install keduanya sekaligus

# Jalankan multiple commands sekaligus
npm run dev & php artisan serve  # Jalankan NPM dev + Laravel serve bersamaan
```

### Network & System Info

```bash
# Cek IP Address
ipconfig                      # Info network detail
ipconfig /all                 # Info lengkap semua adapter
ipconfig /release             # Release IP DHCP
ipconfig /renew               # Renew IP DHCP

# Cek koneksi internet
ping google.com               # Test ping ke Google
ping 8.8.8.8                  # Test ping ke DNS Google
tracert google.com            # Trace route ke Google

# Info system
systeminfo                    # Info lengkap sistem
hostname                      # Nama komputer
whoami                        # Username saat ini
ver                           # Versi Windows

# Cek port yang digunakan
netstat -ano                  # Semua koneksi aktif
netstat -ano | findstr :8000  # Cek siapa yang pakai port 8000
```

### File Search & Management

```bash
# Cari file dengan nama tertentu
dir /s nama_file.txt          # Cari file di folder dan subfolder
where php                     # Cari lokasi executable PHP

# Cari teks dalam file
findstr /s /i "password" *.php         # Cari kata "password" di semua file PHP
findstr /s /i "DB_HOST" .env*          # Cari config database

# Tree view folder
tree                          # Tampilkan struktur folder
tree /f                       # Tampilkan struktur + file
tree /f > structure.txt       # Save struktur ke file

# Compare files
fc file1.txt file2.txt        # Bandingkan 2 file
```

### Command untuk Laravel Developer

```bash
# Generate Key & Link Storage
php artisan key:generate
php artisan storage:link

# Maintenance Mode
php artisan down              # Maintenance mode ON
php artisan up                # Maintenance mode OFF
php artisan down --secret="rahasia123"  # Maintenance dengan bypass token

# Create Controller, Model, Migration sekaligus
php artisan make:model Penduduk -mcr
# -m = migration
# -c = controller
# -r = resource controller

# Route & Config
php artisan route:list        # Lihat semua route
php artisan config:cache      # Cache config untuk production
php artisan view:cache        # Cache views

# Queue & Jobs
php artisan queue:work        # Jalankan queue worker
php artisan queue:listen      # Listen queue (auto reload)
php artisan queue:failed      # Lihat failed jobs
php artisan queue:retry all   # Retry semua failed jobs

# Tinker (Laravel Console)
php artisan tinker
>>> App\Models\User::count()  # Cek jumlah user
>>> DB::table('users')->get() # Query langsung
```

### Productivity Hacks

```bash
# History command (PowerShell)
doskey /history               # Lihat history command CMD
history                       # Lihat history (PowerShell/Linux)

# Clear screen dengan cepat
cls                           # Clear screen Windows
clear                         # Clear screen Linux/Mac

# Redirect output ke file
dir > files.txt               # Save output dir ke file
php artisan route:list > routes.txt  # Save routes ke file

# Append output ke file
echo "New log entry" >> log.txt

# Command chaining
cd project && composer install && npm install && php artisan serve

# Jalankan command di background (PowerShell)
Start-Process php -ArgumentList "artisan serve" -WindowStyle Hidden

# Kill process by port (Windows PowerShell)
Get-Process -Id (Get-NetTCPConnection -LocalPort 8000).OwningProcess | Stop-Process
```

### Command untuk Handle Large Files

```bash
# Compress folder
# (Butuh 7-Zip installed)
7z a backup.zip D:\Project\SIDESA

# Extract
7z x backup.zip

# Lihat isi tanpa extract
7z l backup.zip

# Split file besar
fsutil file createnew dummy.txt 1048576  # Buat file 1MB
split -b 100M large_file.sql             # Split jadi 100MB per file
```

### Command untuk Git Advanced

```bash
# Git Stash (simpan perubahan sementara)
git stash                     # Simpan perubahan
git stash list                # Lihat daftar stash
git stash apply               # Terapkan stash terakhir
git stash pop                 # Terapkan dan hapus stash
git stash drop                # Hapus stash terakhir

# Git Diff
git diff                      # Lihat perubahan yang belum staged
git diff --staged             # Lihat perubahan yang sudah staged
git diff main develop         # Bandingkan 2 branch

# Git Log Advanced
git log --graph --oneline --all          # Graph semua branch
git log --author="nama"                  # Log by author
git log --since="2 weeks ago"            # Log 2 minggu terakhir
git log --grep="bug fix"                 # Cari di commit message

# Git Blame
git blame nama_file.php       # Lihat siapa yang edit tiap baris

# Git Clean
git clean -n                  # Preview file yang akan dihapus
git clean -fd                 # Hapus untracked files & folders

# Git Revert vs Reset
git revert HEAD               # Undo dengan commit baru
git reset --soft HEAD~1       # Undo commit, keep changes
git reset --hard HEAD~1       # Undo commit, discard changes
```

### Command untuk Database

```bash
# MySQL
mysql -u root -p              # Login ke MySQL
mysqldump -u root -p database_name > backup.sql  # Backup database
mysql -u root -p database_name < backup.sql      # Restore database

# PostgreSQL
psql -U postgres              # Login ke PostgreSQL
pg_dump database_name > backup.sql               # Backup
psql database_name < backup.sql                  # Restore

# SQLite
sqlite3 database.db           # Buka database
.tables                       # Lihat semua table
.schema table_name            # Lihat struktur table
.quit                         # Keluar
```

### Keyboard Shortcuts di CMD

```
Tab                           # Auto-complete nama file/folder
Ctrl + C                      # Stop/cancel command yang running
Ctrl + V                      # Paste (CMD modern)
Ctrl + A                      # Pilih semua text
Ctrl + F                      # Find text
↑ / ↓                         # Navigate command history
F7                            # Lihat history command (popup)
Alt + F4                      # Close CMD window
```

---

## 🎓 Command untuk Pemula (Bonus)

### Setup Project Laravel Baru

```bash
# Step-by-step install Laravel project baru
composer create-project laravel/laravel nama-project
cd nama-project
copy .env.example .env
php artisan key:generate
php artisan storage:link
php artisan serve
```

### Setup Project dari Git

```bash
# Clone dan setup
git clone https://github.com/username/project.git
cd project
composer install
npm install
copy .env.example .env
php artisan key:generate
php artisan migrate
php artisan serve
```

### Daily Development Workflow

```bash
# Pagi - Pull update terbaru
git pull origin main

# Kerja - Buat feature baru
git checkout -b feature/nama-fitur
# ... coding ...
git add .
git commit -m "Add: fitur baru"
git push origin feature/nama-fitur

# Sore - Update dependencies
composer update
npm update

# Malam - Clear cache sebelum pulang
php artisan cache:clear
php artisan config:clear
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

**💖 Happy Coding!**

*Dokumentasi ini dibuat untuk mempermudah workflow development. Jangan lupa backup data penting sebelum menjalankan command yang berbahaya!*
