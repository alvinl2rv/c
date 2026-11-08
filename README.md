# PROYEK: PERSONAL CLOUD SERVER

Platform Cloud Storage Pribadi Multi-Pengguna Berbasis Ubuntu Server dan Oracle VirtualBox

Bertindaklah sebagai Senior Full-Stack Developer, Backend Engineer, Linux System Administrator, dan Virtualization Engineer.

Tugas Anda adalah merancang, membangun, mengonfigurasi, dan melakukan deployment aplikasi Personal Cloud Server dari nol.

Proyek ini dibuat untuk memenuhi tugas mata kuliah Sistem Operasi di universitas.

Aplikasi akan dikembangkan sendiri dan dijalankan pada Ubuntu Server yang berjalan sebagai Virtual Machine (VM) menggunakan Oracle VirtualBox.

PENTING:

* Seluruh fitur utama aplikasi harus dibuat sendiri.
* Jangan menggunakan Nextcloud, ownCloud, Seafile, atau platform cloud storage siap pakai.
* Jangan hanya memberikan contoh kode. Buat aplikasi yang benar-benar berfungsi.
* Gunakan bahasa Indonesia untuk dokumentasi, instruksi, dan tampilan aplikasi.
* Gunakan istilah teknis pemrograman dan Linux sesuai standar.
* Berikan panduan instalasi dan konfigurasi secara bertahap.
* Pastikan aplikasi dapat berjalan pada Ubuntu Server di Oracle VirtualBox.
* Jangan menghapus atau mengganti konfigurasi VM yang sudah ada tanpa persetujuan pengguna.

⸻

1. TUJUAN PROYEK

Bangun sebuah platform cloud storage pribadi yang memungkinkan banyak pengguna untuk:

* Melakukan registrasi dan login.
* Mengunggah file ke server pusat.
* Mengunduh file dari server.
* Membuat dan mengelola folder.
* Mengubah nama file.
* Menghapus file.
* Membagikan file kepada pengguna lain.
* Mengatur hak akses file.
* Melihat penggunaan kapasitas penyimpanan.
* Mengakses file melalui browser.
* Mengakses data aplikasi melalui REST API.

Server harus dapat diakses oleh beberapa perangkat yang terhubung dalam satu jaringan lokal (LAN/Wi-Fi).

Contoh alamat server:

http://192.168.1.10

Alamat IP harus dapat dikonfigurasi dan tidak boleh ditulis secara permanen di dalam kode aplikasi.

⸻

2. ARSITEKTUR VIRTUALISASI DAN SISTEM

Gunakan Oracle VirtualBox sebagai platform virtualisasi utama.

Arsitektur proyek:

KOMPUTER UTAMA (HOST OS)
|
|
ORACLE VIRTUALBOX
|
|
UBUNTU SERVER 24.04 LTS (GUEST OS)
|
|
PERSONAL CLOUD SERVER
|
|— Python Flask
|— Gunicorn
|— Nginx
|— SQLite Database
|— File Storage
|— REST API
|— Admin Dashboard

Penjelasan:

* Host OS merupakan sistem operasi komputer utama.
* Oracle VirtualBox menjalankan mesin virtual.
* Ubuntu Server menjadi Guest OS.
* Personal Cloud Server merupakan aplikasi yang dikembangkan dan dijalankan di Ubuntu Server.
* HP dan laptop lain dapat mengakses aplikasi melalui jaringan lokal.

Pastikan seluruh rancangan memperhitungkan keterbatasan resource Virtual Machine.

3. KONFIGURASI ORACLE VIRTUALBOX

Sebelum membangun aplikasi, periksa lingkungan VirtualBox yang digunakan.

Jangan langsung membuat VM baru karena pengguna mungkin sudah memiliki Ubuntu Server yang terinstal.

A. Spesifikasi Virtual Machine

Rekomendasi konfigurasi:

Komponen	Spesifikasi
Virtualization	Oracle VirtualBox
Nama VM	Personal-Cloud-Server
Operating System	Ubuntu Server 24.04 LTS
RAM	4 GB
CPU	2 Core
Virtual Disk	40 GB
Disk Format	VDI
Storage Allocation	Dynamically Allocated
Network	Bridged Adapter
Boot	Ubuntu Server ISO

Spesifikasi dapat disesuaikan dengan kemampuan komputer utama.

B. Pemeriksaan VirtualBox

Jika Claude Code memiliki akses ke komputer host, periksa ketersediaan VirtualBox melalui:

VBoxManage –version

Jika tersedia, periksa daftar VM:

VBoxManage list vms

Periksa VM yang sedang berjalan:

VBoxManage list runningvms

Jika tidak memiliki akses ke komputer host, minta pengguna melakukan pemeriksaan secara manual melalui antarmuka VirtualBox.

Jangan menganggap Claude Code yang berjalan di dalam Guest OS otomatis memiliki akses untuk mengatur VirtualBox di Host OS.

C. Konfigurasi Network Adapter

Berikan panduan konfigurasi VirtualBox secara terperinci:

1. Buka Oracle VirtualBox.
2. Pilih VM Ubuntu Server.
3. Buka Settings.
4. Pilih Network.
5. Buka Adapter 1.
6. Pilih Bridged Adapter.
7. Pilih adapter Wi-Fi atau Ethernet komputer utama.
8. Aktifkan Cable Connected.
9. Simpan konfigurasi.
10. Jalankan kembali VM.

Tujuannya agar Ubuntu Server mendapatkan alamat IP pada jaringan lokal yang sama dengan perangkat lain.

Jika Bridged Adapter tidak tersedia atau tidak berfungsi, berikan alternatif:

* NAT dengan Port Forwarding.
* Host-only Adapter untuk pengujian lokal.

Jelaskan kelebihan dan kekurangan setiap mode jaringan.

D. Pemeriksaan Ubuntu Server

Setelah VM berjalan, periksa:

Versi Ubuntu:

lsb_release -a

Alamat IP:

hostname -I

Informasi jaringan:

ip addr

Penggunaan RAM:

free -h

Kapasitas disk:

df -h

Versi kernel:

uname -r

Gunakan hasil pemeriksaan untuk menentukan langkah konfigurasi selanjutnya.

E. Pengelolaan Virtual Machine

Berikan panduan untuk:

* Menyalakan VM.
* Mematikan Ubuntu Server dengan aman.
* Restart VM.
* Membuat snapshot.
* Memeriksa kapasitas RAM.
* Mengatur CPU.
* Mengatur virtual disk.
* Memeriksa status VM.
* Melakukan backup VM sebelum perubahan besar.

Jangan menghapus VM, disk virtual, snapshot, atau data yang sudah ada.

⸻

4. TEKNOLOGI YANG DIGUNAKAN

Backend:

* Python 3
* Flask
* Flask-SQLAlchemy
* Flask-Login
* Flask-WTF
* Werkzeug

Frontend:

* HTML5
* CSS3
* JavaScript
* Bootstrap 5 atau CSS khusus
* Font Awesome atau Lucide Icons

Database:

* SQLite untuk implementasi awal.
* Rancang lapisan database agar dapat dikembangkan menggunakan PostgreSQL.

Deployment:

* Ubuntu Server 24.04 LTS
* Gunicorn
* Nginx
* systemd

Pengujian:

* Pytest
* Postman
* curl

Semua teknologi tersebut digunakan untuk membangun aplikasi sendiri, bukan mengganti aplikasi utama dengan layanan cloud siap pakai.

⸻

5. HAK AKSES PENGGUNA

Buat dua jenis pengguna.

ADMIN

Administrator memiliki hak untuk:

* Melihat semua pengguna terdaftar.
* Membuat akun pengguna.
* Menonaktifkan dan mengaktifkan akun.
* Melihat metadata seluruh file.
* Memantau penggunaan penyimpanan.
* Melihat riwayat aktivitas.
* Mengelola pengaturan sistem.

USER

Pengguna biasa memiliki hak untuk:

* Registrasi dan login.
* Mengunggah file.
* Mengunduh file pribadi.
* Membuat folder.
* Mengubah nama file.
* Menghapus file pribadi.
* Membagikan file kepada pengguna lain.
* Melihat file yang dibagikan kepadanya.
* Melihat penggunaan penyimpanan pribadi.
* Mengelola profil.

Terapkan Role-Based Access Control (RBAC).

⸻

6. FITUR UTAMA APLIKASI

A. Sistem Autentikasi

Buat fitur:

* Registrasi pengguna.
* Login pengguna.
* Logout pengguna.
* Password hashing.
* Pengelolaan session.
* Otorisasi berdasarkan role.
* Status akun aktif dan nonaktif.
* Perlindungan CSRF.

Jangan menyimpan password dalam bentuk teks biasa.

B. Manajemen File

Buat fitur:

* Upload file.
* Download file.
* Hapus file.
* Ubah nama file.
* Membuat folder.
* Menampilkan daftar file.
* Pencarian file.
* Informasi ukuran file.
* Tanggal upload.
* Jenis file.

Ketentuan:

* Batas awal upload maksimal 100 MB.
* Validasi nama file dan ekstensi.
* Gunakan nama penyimpanan unik.
* Cegah Path Traversal.
* Cegah akses file tanpa izin.
* Simpan file di luar direktori web publik.
* Jangan menampilkan lokasi penyimpanan internal kepada pengguna.

Gunakan struktur:

/srv/personal-cloud/uploads/
user_1/
user_2/
user_3/

C. Sistem Berbagi File

Buat fitur:

* Membagikan file kepada pengguna terdaftar.
* Izin Viewer.
* Izin Editor.
* Melihat daftar file yang dibagikan.
* Mencabut akses berbagi.
* Melacak pemilik file.

Setiap permintaan akses harus memeriksa kepemilikan atau izin berbagi yang masih aktif.

D. Manajemen Penyimpanan

Buat fitur:

* Total kapasitas penyimpanan.
* Penggunaan storage setiap pengguna.
* Jumlah file.
* Batas kapasitas penyimpanan per pengguna.
* Visualisasi penggunaan storage.

Batas kapasitas dapat diatur administrator.

E. Dashboard Administrator

Buat dashboard yang menampilkan:

* Total pengguna.
* Pengguna aktif.
* Total file.
* Total penggunaan storage.
* Aktivitas terbaru.
* Manajemen pengguna.
* Informasi file.
* Pengaturan akun.

Hanya administrator yang dapat mengakses halaman tersebut.

F. REST API

Buat REST API menggunakan Flask.

Endpoint autentikasi:

POST /api/auth/login
POST /api/auth/logout
GET /api/auth/me

Endpoint file:

GET /api/files
POST /api/files
GET /api/files/
GET /api/files//download
PUT /api/files/
DELETE /api/files/

Endpoint folder:

GET /api/folders
POST /api/folders
PUT /api/folders/
DELETE /api/folders/

Endpoint sharing:

POST /api/files//share
GET /api/shared
DELETE /api/shares/

Endpoint administrator:

GET /api/admin/users
POST /api/admin/users
PUT /api/admin/users/
GET /api/admin/statistics
GET /api/admin/logs

Gunakan respons JSON yang konsisten, HTTP status code yang tepat, serta autentikasi dan otorisasi pada endpoint yang dilindungi.

⸻

7. DESAIN DATABASE

Buat model database:

1. User
2. File
3. Folder
4. FileShare
5. ActivityLog
6. SystemSetting

Gunakan SQLAlchemy ORM.

Terapkan:

* Relasi antar tabel.
* Foreign key.
* Validasi integritas data.
* Inisialisasi database.
* Migrasi database atau mekanisme pembuatan skema yang konsisten.
* Prosedur pembuatan administrator pertama yang aman.

Jangan menyimpan password administrator secara permanen di source code.

⸻

8. DESAIN FRONTEND

Buat antarmuka cloud storage modern, bersih, profesional, dan responsif.

Gunakan inspirasi desain Google Drive dan Dropbox tanpa menyalin identitas visual mereka.

Buat halaman:

1. Login.
2. Registrasi.
3. Dashboard pengguna.
4. My Files.
5. Shared Files.
6. Recent Files.
7. Trash.
8. My Account.
9. Admin Dashboard.
10. User Management.

Fitur desain:

* Sidebar navigasi.
* Header dan profil pengguna.
* Tombol upload.
* Grid dan list file.
* Ikon berdasarkan jenis file.
* Informasi penggunaan storage.
* Notifikasi keberhasilan dan kegagalan.
* Drag-and-drop upload.
* Progress upload.
* Responsive layout.

Gunakan bahasa Indonesia pada seluruh tampilan aplikasi.

⸻

9. STRUKTUR FOLDER PROYEK

Gunakan struktur modular:

personal-cloud/
│
├── app/
│   ├── init.py
│   ├── models.py
│   ├── auth.py
│   ├── files.py
│   ├── sharing.py
│   ├── admin.py
│   └── api.py
│
├── templates/
│   ├── base.html
│   ├── login.html
│   ├── register.html
│   ├── dashboard.html
│   ├── files.html
│   ├── shared.html
│   └── admin.html
│
├── static/
│   ├── css/
│   ├── js/
│   └── images/
│
├── config.py
├── run.py
├── requirements.txt
├── .env.example
├── .gitignore
└── README.md

Tambahkan file lain jika diperlukan.

Pisahkan backend, frontend, database, konfigurasi, dan file penyimpanan.

⸻

10. KONFIGURASI UBUNTU SERVER

Berikan panduan instalasi secara bertahap:

1. Pemeriksaan versi Ubuntu.
2. Pemeriksaan IP Address.
3. Update dan upgrade sistem.
4. Instalasi Python.
5. Instalasi pip dan virtual environment.
6. Instalasi Git.
7. Instalasi SQLite.
8. Instalasi Nginx.
9. Pembuatan direktori proyek.
10. Konfigurasi hak akses folder.
11. Instalasi dependensi aplikasi.

Gunakan perintah terminal yang dapat langsung dijalankan.

Jelaskan fungsi setiap perintah.

Jangan mengulang instalasi Ubuntu Server jika pengguna sudah memiliki VM yang berjalan.

⸻

11. DEPLOYMENT PADA UBUNTU SERVER

Gunakan:

* Gunicorn sebagai application server.
* Nginx sebagai reverse proxy.
* systemd sebagai pengelola service.

Buat konfigurasi:

* personal-cloud.service
* Konfigurasi Nginx.
* Firewall UFW.
* Environment variables.

Aplikasi harus:

* Berjalan di latar belakang.
* Otomatis aktif ketika Ubuntu dinyalakan.
* Bisa dihentikan dan dijalankan ulang.
* Memiliki log.
* Tidak membutuhkan terminal yang terus terbuka.

Gunicorn hanya boleh menerima koneksi dari localhost. Akses jaringan harus melalui Nginx.

⸻

12. KEAMANAN SISTEM

Implementasikan:

* Password hashing.
* CSRF protection.
* Session security.
* Validasi upload file.
* Perlindungan Path Traversal.
* Pencegahan IDOR.
* Pembatasan ukuran file.
* RBAC.
* Isolasi file antar pengguna.
* Validasi hak akses sharing.
* Proteksi endpoint administrator.
* Penyimpanan file di luar direktori publik.
* Firewall untuk jaringan lokal.

Jangan membuka akses aplikasi ke internet secara otomatis.

⸻

13. BACKUP DAN PEMULIHAN DATA

Buat sistem backup untuk:

* Database.
* File pengguna.
* Metadata file.
* Konfigurasi yang diperlukan.

Sediakan:

* Backup manual.
* Restore.
* Verifikasi backup.
* Dokumentasi lokasi backup.

Jelaskan cara menyimpan backup di perangkat terpisah dari virtual disk utama.

⸻

14. PENGUJIAN APLIKASI DAN VIRTUALBOX

Buat skenario pengujian:

1. Menjalankan VM Ubuntu melalui VirtualBox.
2. Memastikan Ubuntu mendapatkan IP Address.
3. Memastikan aplikasi berjalan.
4. Membuka cloud melalui browser komputer utama.
5. Membuka cloud melalui browser HP.
6. Registrasi pengguna.
7. Login.
8. Upload file.
9. Download file.
10. Membuat folder.
11. Menghapus file.
12. Berbagi file.
13. Menguji isolasi file antar pengguna.
14. Menguji dashboard admin.
15. Menguji REST API menggunakan Postman.
16. Restart service.
17. Reboot Ubuntu Server.
18. Memastikan aplikasi otomatis berjalan kembali.

Buat unit test untuk fungsi autentikasi, otorisasi, upload, download, dan sharing.

⸻

15. KAITAN DENGAN MATA KULIAH SISTEM OPERASI

Jelaskan penerapan konsep:

* Process Management melalui Gunicorn dan systemd.
* Memory Management melalui penggunaan RAM aplikasi.
* File System melalui penyimpanan file.
* User Management melalui akun pengguna.
* Networking melalui komunikasi client-server.
* Storage Management melalui kapasitas disk.
* Security melalui autentikasi dan hak akses.
* Service Management melalui systemd.
* Virtualization melalui Oracle VirtualBox.

Sediakan perintah Linux untuk pemantauan:

CPU:
top

RAM:
free -h

Storage:
df -h

Service:
systemctl status personal-cloud

Log:
journalctl -u personal-cloud -f

Jelaskan hubungan masing-masing perintah dengan materi Sistem Operasi.

⸻

16. DOKUMENTASI PROYEK

Buat README.md dalam bahasa Indonesia yang berisi:

* Deskripsi proyek.
* Tujuan proyek.
* Fitur aplikasi.
* Teknologi.
* Arsitektur sistem.
* Arsitektur VirtualBox.
* Struktur direktori.
* Cara instalasi.
* Konfigurasi jaringan.
* Cara menjalankan aplikasi.
* Cara membuat administrator pertama.
* Cara mengakses melalui HP dan laptop.
* Daftar REST API.
* Cara deployment.
* Cara backup dan restore.
* Troubleshooting.

⸻

17. ATURAN PENGERJAAN

Ikuti ketentuan berikut:

1. Jangan hanya memberikan potongan kode tanpa konteks.
2. Buat source code yang lengkap dan saling terhubung.
3. Periksa seluruh import dan dependensi.
4. Jangan gunakan placeholder untuk fitur utama.
5. Jangan mengklaim aplikasi berhasil sebelum benar-benar diuji.
6. Periksa kesalahan sintaks dan integrasi.
7. Gunakan struktur kode modular.
8. Berikan komentar pada bagian penting.
9. Gunakan bahasa Indonesia untuk dokumentasi dan tampilan.
10. Jangan mengubah konfigurasi sistem tanpa menjelaskan dampaknya.
11. Jangan menjalankan perintah berisiko tanpa persetujuan.
12. Jangan menghapus VM atau data VirtualBox yang sudah ada.
13. Jangan mengasumsikan Claude Code dapat mengendalikan GUI VirtualBox.
14. Jika konfigurasi harus dilakukan manual, berikan panduan klik secara rinci.
15. Selalu verifikasi hasil setiap tahap sebelum melanjutkan.

⸻

18. TAHAP PENGERJAAN

Kerjakan proyek secara bertahap.

FASE 1: Pemeriksaan Oracle VirtualBox, VM Ubuntu, dan analisis kebutuhan.

FASE 2: Konfigurasi jaringan VirtualBox dan Ubuntu Server.

FASE 3: Pembuatan struktur proyek dan konfigurasi Flask.

FASE 4: Pembuatan database dan autentikasi.

FASE 5: Pembuatan manajemen file dan folder.

FASE 6: Pembuatan sistem file sharing.

FASE 7: Pembuatan REST API.

FASE 8: Pembuatan frontend dan dashboard pengguna.

FASE 9: Pembuatan dashboard administrator.

FASE 10: Implementasi keamanan dan pengujian.

FASE 11: Deployment menggunakan Gunicorn, Nginx, dan systemd.

FASE 12: Backup, dokumentasi, dan persiapan demonstrasi.

Setelah setiap fase:

* Periksa kode dan konfigurasi.
* Jalankan pengujian yang relevan.
* Perbaiki error.
* Jelaskan hasil pekerjaan.
* Berikan instruksi melanjutkan fase berikutnya.

Jangan melompat ke fase berikutnya sebelum fase saat ini selesai dan diverifikasi.

MULAI SEKARANG DENGAN FASE 1.

Pertama, periksa apakah Oracle VirtualBox, Ubuntu Server VM, dan konfigurasi jaringan sudah tersedia.

Karena pengguna kemungkinan sudah menginstal Ubuntu Server di VirtualBox, utamakan melanjutkan konfigurasi yang ada daripada membuat ulang VM.

Jangan langsung membuat aplikasi sebelum lingkungan virtualisasi dan jaringan siap.

Target akhir adalah Personal Cloud Server buatan sendiri yang berjalan stabil pada Ubuntu Server di Oracle VirtualBox dan dapat digunakan oleh banyak pengguna melalui jaringan lokal.
