# Instalasi Laravel

Berikut adalah langkah instalasi Laravel pada WSL2 / Linux / macOS. Pada tutorial kali ini akan menggunakan Ubuntu 20.04 pada WSL2 di Windows 11.

## Prerequisites

- Windows dengan WSL2 / Linux dengan [distro berbasis Debian](https://en.wikipedia.org/wiki/Category:Debian-based_distributions)
- Koneksi internet
- [PHP 8.0+](../Instalasi%20PHP%208/) untuk Laravel 9 atau PHP 7.3+ untuk Laravel 8
- [Composer](../Instalasi%20Composer/)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop) (macOS / Windows) atau [Docker](https://docs.docker.com/engine/install/debian/) dan [Docker Compose](https://docs.docker.com/compose/install/) untuk Linux
- [nginx-proxy](https://github.com/dptsi/nginx-proxy)

## Instalasi

### Instalasi PHP extension

Sebelum melakukan instalasi, perlu dilakukan pemasangan ekstensi PHP yang diperlukan oleh composer

```bash
sudo apt install php8.1-zip php8.1-bcmath php8.1-curl \
php8.1-mbstring php8.1-xml unzip
```

### Inisiasi Project Laravel

Buat folder baru untuk project yang akan diinisiasi

```bash
mkdir project-baru
cd project-baru
```

![Pembuatan folder baru](https://media.discordapp.net/attachments/769183322147389460/951341064277594152/unknown.png)

Buka folder tersebut dengan Visual Studio Code

```bash
code .
```

Buat berkas bernama `docker-compose.yml` berisi sebagai berikut:

```yaml
version: "3.8"
services:
  nama-service:
    container_name: nama-container
    image: pilih-image
    volumes:
      - ./src:/var/www/html
    env_file: .env
    dns:
      - 1.1.1.1
      - 1.0.0.1
    extra_hosts:
      - "host.docker.internal:host-gateway"
    networks:
      - nginx-proxy-network

networks:
  nginx-proxy-network:
    external: true
```

Penjelasan dari `docker-compose.yml` lebih lengkap dapat dilihat pada [Compose file version 3 reference | Docker Documentation](https://docs.docker.com/compose/compose-file/compose-file-v3/), namun untuk memasang 1 container Laravel maka yang perlu diganti adalah sebagai berikut:

- `nama-service` dan `nama-container`: Bisa diberi nama bebas, untuk mempermudah bisa diberi nama yang sama, contoh: `proyek-laravel`
- `image`: Dapat menggunakan `dptsi/laravel-web-dev`

Berikutnya buat berkas `.env` yang isinya berupa konfigurasi dari `nginx-proxy`

```env
VIRTUAL_HOST=laravel.local
VIRTUAL_PORT=8080
SELF_SIGNED_HOST=laravel.local
```

Kemudian, tambahkan domain serta private IP address PC development di /etc/hosts atau C:\Windows\System32\drivers\etc\hosts (menggunakan HostsMan).

Setelah itu, jalankan perintah berikut untuk memasang Laravel

```bash
composer create-project laravel/laravel src
```

Berikutnya, jalankan perintah `docker compose up -d` dan akses `laravel.local` melalui browser.

### Troubleshoots

### Mendapatkan exception UnexpectedValueException

```bash
UnexpectedValueException
The stream or file "/var/www/html/storage/logs/laravel.log" could not be opened in append mode: Failed to open stream: Permission denied
```

Masuk ke docker container sebagai root dengan `docker exec -it nama-container sh` kemudian lakukan perintah sebagai berikut di folder /var/www/html.

```bash
chown -R www-data:www-data storage
```

### Mendapatkan exception MissingAppKeyException

```php
Illuminate\Encryption\MissingAppKeyException
No application encryption key has been specified.
```

Masuk ke docker container sebagai root dengan `docker exec -it nama-container sh` kemudian lakukan perintah sebagai berikut di folder /var/www/html.

```bash
php artisan key:generate
```

## Referensi

- [dptsi/nginx-proxy: A docker compose configuration for web development using nginx-proxy and self signed proxy companion.](https://github.com/dptsi/nginx-proxy)
- [Installation - Laravel - The PHP Framework For Web Artisans](https://laravel.com/docs/9.x/)
