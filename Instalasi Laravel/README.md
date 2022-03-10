# Instalasi Laravel

Berikut adalah langkah instalasi Laravel pada WSL2 / Linux / macOS. Pada tutorial kali ini akan menggunakan Ubuntu 20.04 pada WSL2 di Windows 11.

## Prerequisites

- Windows dengan WSL2 / Linux dengan [distro berbasis Debian](https://en.wikipedia.org/wiki/Category:Debian-based_distributions)
- Koneksi internet
- [PHP 8.0+](../Instalasi%20PHP%208/) untuk Laravel 9 atau PHP 7.3+ untuk Laravel 8
- [Composer](../Instalasi%20Composer/)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop) (macOS / Windows) atau [Docker](https://docs.docker.com/engine/install/debian/) dan [Docker Compose](https://docs.docker.com/compose/install/) untuk Linux

## Instalasi

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
version: '3.8'
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
      - 'host.docker.internal:host-gateway'
    networks:
      - nginx-proxy-network

networks:
  nginx-proxy-network:
    external: true
```

Penjelasan dari `docker-compose.yml` lebih lengkap dapat dilihat pada [Compose file version 3 reference | Docker Documentation](https://docs.docker.com/compose/compose-file/compose-file-v3/), namun untuk memasang 1 container Laravel maka yang perlu diganti adalah sebagai berikut:

- `nama-service` dan `nama-container`: Bisa diberi nama bebas, untuk mempermudah bisa diberi nama yang sama, contoh: `proyek-laravel`
- `image`: Dapat menggunakan `dptsi/laravel-web-dev` untuk Laravel 8 atau `zydhanlinnar11/laravel-docker-image` untuk Laravel 9

Berikutnya buat berkas `.env` berisi konfigurasi dari `nginx-proxy`

```env
# Docker compose variables
VIRTUAL_HOST=laravel.local
VIRTUAL_PORT=8080
SELF_SIGNED_HOST=laravel.local
```

TODO: melanjutkan

## Referensi

-
