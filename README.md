# Jasa Kelola Dedicated Server Linux, VPS, dan Mikrotik  
Sangat ahli dan berpengalaman.

## Contact Person  
**PURWANTO**  

## Nomor HP  
+62 822-3348-3221  

---

Berikut adalah panduan untuk **menginstal, mengonfigurasi, dan mengoptimalkan CyberPanel** di **AlmaLinux 9**:

---

## **1. Persiapan Awal**
1. **Update Sistem**  
   Jalankan perintah berikut untuk memperbarui paket sistem:
   ```bash
   sudo dnf update -y
   sudo dnf upgrade -y
   ```

2. **Nonaktifkan SELinux** (jika diaktifkan, CyberPanel dapat mengalami masalah saat instalasi):  
   Edit file konfigurasi SELinux:
   ```bash
   sudo nano /etc/selinux/config
   ```
   Ubah baris `SELINUX=enforcing` menjadi:
   ```bash
   SELINUX=disabled
   ```
   Terapkan perubahan:
   ```bash
   sudo setenforce 0
   ```

3. **Pastikan Akses Root**  
   CyberPanel memerlukan akses root untuk instalasi. Jika Anda menggunakan user biasa, gunakan `sudo` untuk semua perintah.

4. **Pastikan Port Firewall Terbuka**  
   Buka port yang dibutuhkan CyberPanel:
   ```bash
   sudo firewall-cmd --permanent --add-port=8090/tcp
   sudo firewall-cmd --reload
   ```

---

## **2. Instalasi CyberPanel**
1. **Unduh dan Jalankan Installer**
   Gunakan skrip bawaan CyberPanel untuk instalasi:
   ```bash
   sudo yum install wget -y
   wget -O installer.sh https://cyberpanel.net/install.sh
   sudo sh installer.sh
   ```

2. **Pilih Opsi Instalasi**
   Selama proses instalasi, Anda akan diminta untuk memilih beberapa opsi. Contohnya:
   - Pilih **CyberPanel** atau **CyberPanel dengan LiteSpeed Enterprise** (pilih sesuai kebutuhan Anda). LiteSpeed OpenLiteSpeed gratis, sementara Enterprise berbayar.
   - Pilih **Full Installation** untuk fitur lengkap.

3. **Konfigurasi Password**
   Anda akan diminta untuk mengatur password admin untuk login CyberPanel. Pastikan menggunakan password yang kuat.

4. **Akses Panel**  
   Setelah instalasi selesai, akses CyberPanel melalui URL:
   ```
   http://IP_SERVER:8090
   ```
   Login menggunakan:
   - Username: `admin`
   - Password: (yang Anda atur selama instalasi)

---

## **3. Konfigurasi Dasar**
1. **Update CyberPanel**  
   Setelah login, periksa dan lakukan pembaruan melalui CLI:
   ```bash
   cyberpanel update
   ```

2. **Tambahkan Domain**  
   Di dashboard CyberPanel:
   - Navigasi ke **Websites > Create Website**.
   - Isi detail domain seperti nama, email, dan package.

3. **Setup SSL (Let’s Encrypt)**  
   Aktifkan SSL untuk domain:
   - Navigasi ke **Websites > SSL > Issue SSL**.
   - Pilih domain, lalu klik **Issue SSL**.

4. **Tambahkan Email Hosting**  
   - Pergi ke **Email > Create Email**.
   - Buat akun email untuk domain.

5. **Konfigurasi Backup dan Restore**  
   - Gunakan fitur bawaan di **Backup > Create Backup**.

---

## **4. Optimasi CyberPanel**
1. **Optimasi OpenLiteSpeed**  
   Masuk ke panel OpenLiteSpeed melalui:
   ```
   http://IP_SERVER:7080
   ```
   Login menggunakan:
   - Username: `admin`
   - Password: (default diatur saat instalasi).
   Optimasi yang bisa dilakukan:
   - **Cache Settings:** Aktifkan LiteSpeed Cache untuk meningkatkan kecepatan situs.
   - **Compression:** Pastikan GZIP atau Brotli diaktifkan.
   - **Tuning:** Sesuaikan parameter seperti *Max Connections* dan *Memory Limit* sesuai kebutuhan server.

2. **Konfigurasi PHP**  
   Di CyberPanel:
   - Navigasi ke **PHP > Edit PHP Configurations**.
   - Sesuaikan nilai seperti `memory_limit`, `upload_max_filesize`, dan `post_max_size`.

3. **Aktifkan ModSecurity**  
   ModSecurity adalah firewall aplikasi web (WAF) untuk melindungi situs:
   - Navigasi ke **Security > ModSecurity Conf**.
   - Aktifkan dan gunakan aturan bawaan atau aturan tambahan seperti OWASP.

4. **Optimasi Database MySQL/MariaDB**  
   Edit file konfigurasi MySQL:
   ```bash
   sudo nano /etc/my.cnf
   ```
   Tambahkan parameter untuk meningkatkan performa:
   ```ini
   [mysqld]
   innodb_buffer_pool_size=1G
   innodb_log_file_size=256M
   query_cache_size=64M
   ```

5. **Gunakan Cache Plugin untuk WordPress**  
   Jika Anda menjalankan WordPress, gunakan LiteSpeed Cache Plugin untuk performa terbaik.

---

## **5. Pemantauan dan Maintenance**
1. **Monitoring Resource**  
   Gunakan fitur **Logs** di CyberPanel untuk memantau penggunaan CPU, RAM, dan disk.

2. **Rutin Backup Data**  
   Otomatiskan backup untuk mencegah kehilangan data.

3. **Update Rutin**  
   Selalu perbarui CyberPanel, OpenLiteSpeed, dan sistem Anda agar tetap aman dan up-to-date.

---

Jika Anda menghadapi masalah spesifik, beri tahu saya untuk panduan lebih lanjut! 😊
