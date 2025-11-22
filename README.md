# Pengaturan Moodle dengan Docker

Repositori ini menyediakan cara yang efisien untuk menginstal dan menjalankan Moodle menggunakan Docker dan Docker Compose. Ini dirancang untuk pengembangan lokal, pengujian, atau lingkungan produksi awal yang cepat.

## Daftar Isi
- [Pengaturan Moodle dengan Docker](#pengaturan-moodle-dengan-docker)
  - [Daftar Isi](#daftar-isi)
  - [File yang Disertakan](#file-yang-disertakan)
  - [Memulai](#memulai)
    - [Prasyarat](#prasyarat)
    - [Petunjuk Pengaturan](#petunjuk-pengaturan)
  - [Konfigurasi](#konfigurasi)
  - [Mengakses Moodle](#mengakses-moodle)
  - [Menghentikan Lingkungan](#menghentikan-lingkungan)
  - [Penyelesaian Masalah](#penyelesaian-masalah)
  - [Kontribusi](#kontribusi)
  - [Lisensi](#lisensi)

## File yang Disertakan

-   `apache-moodle.conf`: Konfigurasi server web Apache yang khusus disesuaikan untuk Moodle.
-   `config.php`: File konfigurasi utama Moodle, yang akan dipasang ke dalam kontainer Moodle. Anda mungkin perlu menyesuaikan detail database di sini.
-   `docker-compose.yml`: Mendefinisikan aplikasi Docker multi-kontainer, termasuk server aplikasi Moodle, database, dan layanan lain yang diperlukan.
-   `moodle.ini`: Pengaturan PHP `ini` yang dioptimalkan untuk kebutuhan Moodle.

## Memulai

### Prasyarat

Sebelum Anda memulai, pastikan Anda telah menginstal yang berikut ini di sistem Anda:

-   **Docker Desktop**: Termasuk Docker Engine, Docker CLI, Docker Compose, dan Kubernetes.
    -   [Unduh Docker Desktop](https://www.docker.com/products/docker-desktop)

### Petunjuk Pengaturan

1.  **Klon Repositori (jika berlaku)**:
    Jika Anda belum melakukannya, klon repositori ini ke mesin lokal Anda:
    ```bash
    git clone https://github.com/ade-karya/moodle.git
    cd moodle
    ```
    Jika Anda sudah memiliki file-file ini, pastikan semuanya berada dalam satu direktori.

2.  **Mulai Lingkungan Moodle**:
    Navigasi ke direktori utama proyek ini tempat `docker-compose.yml` berada dan jalankan:
    ```bash
    docker-compose up -d
    ```
    Perintah ini akan:
    -   Membangun (jika perlu) dan memulai semua layanan yang didefinisikan dalam `docker-compose.yml` dalam mode terpisah (di latar belakang).
    -   Ini biasanya mencakup server web (Apache/Nginx), database (MySQL/PostgreSQL), dan aplikasi Moodle.

## Konfigurasi

Anda dapat menyesuaikan pengaturan Moodle Anda dengan mengedit file-file berikut sebelum memulai kontainer:

-   **`config.php`**: Sesuaikan pengaturan koneksi database, URL Moodle, jalur direktori data, dan konfigurasi inti Moodle lainnya.
-   **`apache-moodle.conf`**: Modifikasi pengaturan khusus Apache seperti virtual host, konfigurasi SSL, atau arahan kustom.
-   **`moodle.ini`**: Sesuaikan pengaturan PHP seperti `memory_limit`, `max_execution_time`, `upload_max_filesize`, dll., agar sesuai dengan kebutuhan instansi Moodle Anda.

## Mengakses Moodle

Setelah `docker-compose up -d` selesai dan semua kontainer berjalan, Anda dapat mengakses instansi Moodle Anda:

-   Buka peramban web Anda dan navigasi ke: `http://localhost` (atau port spesifik yang dikonfigurasi di `apache-moodle.conf` dan `docker-compose.yml` jika berbeda dari port 80).
-   Ikuti petunjuk instalasi Moodle di layar untuk menyelesaikan proses pengaturan.

## Menghentikan Lingkungan

Untuk menghentikan dan menghapus semua layanan, jaringan, dan volume yang dibuat oleh `docker-compose up`:

```bash
docker-compose down
```
Jika Anda hanya ingin menghentikan kontainer tanpa menghapusnya:
```bash
docker-compose stop
```
Untuk memulai ulang kontainer yang dihentikan:
```bash
docker-compose start
```

## Penyelesaian Masalah

-   **Periksa Log Kontainer**: Jika Anda mengalami masalah, periksa log kontainer yang berjalan untuk mengidentifikasi kesalahan:
    ```bash
    docker-compose logs -f <nama_layanan>
    # Contoh: docker-compose logs -f web
    ```
-   **Alokasi Sumber Daya**: Pastikan Docker Desktop memiliki alokasi CPU dan memori yang cukup, terutama untuk instansi Moodle yang lebih besar.
-   **Konflik Port**: Verifikasi bahwa tidak ada aplikasi lain yang menggunakan port yang dibutuhkan oleh layanan Docker Anda (misalnya, port 80, 443, 3306).
-   **Kesalahan Instalasi Moodle**: Jika penginstal web Moodle menunjukkan kesalahan, periksa kembali pengaturan `config.php` dan konektivitas database Anda.

## Kontribusi

Jangan ragu untuk memfork repositori ini, melakukan perbaikan, dan mengirimkan permintaan pull.

## Lisensi

Proyek ini bersifat open-source dan tersedia di bawah ![License](https://img.shields.io/badge/license-MIT-brightgreen).
