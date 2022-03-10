# Instalasi PHP 8

Berikut adalah langkah instalasi PHP 8.1 pada WSL2 / Linux. Pada tutorial kali ini akan menggunakan Ubuntu 20.04 pada WSL2 di Windows 11.

## Prerequisites

- Windows dengan WSL2 / Linux dengan [distro berbasis Debian](https://en.wikipedia.org/wiki/Category:Debian-based_distributions)
- Koneksi internet

## Hapus versi lama

Sebelum memasang PHP 8.1, anda disarankan untuk menghapus PHP yang lain untuk meminimalisir konflik.

```bash
sudo apt remove php*
```

## Instalasi menggunakan repository PPA

Tambahkan repository ondrej/php ke sistem (Khusus selain Ubuntu 22.04).

```bash
sudo add-apt-repository ppa:ondrej/php
sudo apt update
sudo apt upgrade
```

Install PHP 8.1.

```bash
sudo apt install php8.1-fpm
```

Periksa status instalasi PHP dengan `php -v`

![PHP versi 8.1 terpasang](https://media.discordapp.net/attachments/769183322147389460/951333418065592380/unknown.png)

## Referensi

- [How To Install PHP 8.1 on Ubuntu 22.04|20.04|18.04 | ComputingForGeeks](https://computingforgeeks.com/how-to-install-php-on-ubuntu-linux-system/)
