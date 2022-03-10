# Instalasi Composer

Berikut adalah langkah instalasi Composer pada WSL2 / Linux. Pada tutorial kali ini akan menggunakan Ubuntu 20.04 pada WSL2 di Windows 11.

## Prerequisites

- Windows dengan WSL2 / Linux dengan [distro berbasis Debian](https://en.wikipedia.org/wiki/Category:Debian-based_distributions)
- Koneksi internet
- [PHP 8.0+](../Instalasi%20PHP%208/)

## Hapus versi lama

Sebelum memasang Composer, anda disarankan untuk menghapus composer yang lain untuk meminimalisir konflik.

```bash
sudo apt remove composer
```

## Instalasi

Berikut command untuk mengunduh Composer:

```bash
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '906a84df04cea2aa72f40b5f787e49f22d4c2f19492ac310e8cba5b96ac8b64115ac402c8cd292b8a03482574915d1a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```

Setelah diunduh, akan ada berkas `composer.phar` pada current directory yang perlu dipindahkan ke PATH agar dapat dieksekusi dari folder manapun.

```bash
sudo mv composer.phar /usr/local/bin/composer
```

Periksa apakah composer sudah terpasang dengan menjalankan `composer -V`

![Composer sudah terpasang](https://media.discordapp.net/attachments/769183322147389460/951337570137145374/unknown.png)

## Referensi

- [Composer](https://getcomposer.org/download/)
