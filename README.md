# Moodle dengan MariaDB menggunakan Docker Compose

Repositori ini menyediakan konfigurasi untuk menjalankan [Moodle](https://moodle.org/) bersama [MariaDB](https://mariadb.org/) menggunakan Docker Compose. Konfigurasi ini menggunakan image resmi dari Bitnami.

## 🧾 Layanan yang Digunakan

- **MariaDB**: Server basis data yang digunakan Moodle.
- **Moodle**: Platform pembelajaran daring sumber terbuka.

## 🛠 Prasyarat

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- Jaringan Docker eksternal bernama `ollama-net`

Untuk membuat jaringan eksternal:
```bash
docker network create ollama-net
```

## 🚀 Langkah Menjalankan

1. **Clone repositori ini**:
   ```bash
   git clone https://github.com/ade-karya/moodle.git
   cd moodle-docker-compose
   ```

2. **Pastikan jaringan eksternal sudah dibuat**:
   ```bash
   docker network create ollama-net
   ```

3. **Jalankan layanan**:
   ```bash
   docker-compose up -d
   ```

4. **Akses Moodle di browser**:
   - [http://localhost](http://localhost)

## 🔐 Kredensial Default

| Komponen | Username     | Password                    |
|----------|--------------|-----------------------------|
| Moodle   | `admin`      | `adminpassword123`          |
| MariaDB  | `root`       | `StrongRootPassword123!`    |
| MariaDB  | `bn_moodle`  | `StrongUserPassword456!`    |

> *Kredensial ini bisa disesuaikan di file `docker-compose.yml`.*

## 📂 Volume Docker

Volume yang digunakan untuk menyimpan data secara permanen:

- `mariadb_data`: Menyimpan data database MariaDB
- `moodle_data`: Menyimpan file aplikasi Moodle
- `moodledata_data`: Menyimpan data unggahan Moodle (seperti file tugas, media, dll)

## 📄 Lisensi

Konfigurasi ini dilisensikan di bawah lisensi **Apache 2.0**. Lihat detailnya di [spdx.org/licenses/Apache-2.0](https://spdx.org/licenses/Apache-2.0.html).

---

> Konfigurasi ini menggunakan container dari Bitnami yang dikelola oleh Broadcom.
