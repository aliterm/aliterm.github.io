---
title: "Mudah Migrasi Wordpress"
date: 2019-02-06 21:33:52 +0700
layout: post
tags: ["wordpress","migrasi"]
category: "pemrograman"
---

## Prakata

Setelah kalian selesai membangun situs dengan WordPress di `localhost`, dan berencana untuk menaikannya ke peladen (server). Nah, kalian harus mempersiapkan diri untuk menyunting beberapa kode sumber dan pangkalan datanya. Jika tidak, situs kalian tidak akan bisa berjalan seperti halnya di `localhost`.

## Persyaratan

Sebelum memasuki tahap praktek, di sini saya asumsikan kalian menggunakan VPS atau Dedicated Server. Jika kalian menggunakan Shared Hosting yang kalian lakukan adalah:

- Buka File Manager dan buka berkas `wp-config.php`.
- Buka Database Server atau `phpMyAdmin` jika ada.

Nah bagi kalian penggunaa non-shared hosting, kalian bisa langsung buka berkas `wp-config.php` menggunakan `vim` atau `nano`. Perintahnya sebagai berikut:

```bash
$ cd /direktori/wp/kalian/
$ vim wp-config.php
```

Lihat dan catat `DB_USER`, `DB_PASSWORD`, `DB_HOST`, `DB_PASSWORD` dan yang paling penting `$table_prefix` :

```php
define( 'DB_NAME', 'database_name_here' );
define( 'DB_USER', 'username_here' );
define( 'DB_PASSWORD', 'password_here' );
define( 'DB_HOST', 'localhost' );
$table_prefix = 'wp_';
```

## Caranya

Setelah melihat berkas `wp-config.php` langkah selanjutnya yakni kalian masuk ke `mariadb` dengan cara:

```bash
$ sudo mysql -u root
```

Kemudian kita ubah (replace) tautan lama yang di `localhost` kalian dengan tautan baru.

```sql
UPDATE wp_posts SET post_content = REPLACE(post_content, 'http://link.lama', 'http://link.baru');
UPDATE wp_posts SET guid = REPLACE(guid, 'http://link.lama', 'http://link.baru');
```

Perhatian contoh skrip di atas saya menggunakan `wp_posts` karena sebelumnya `$table_prefix` nya adalah `wp_`. Pastikan disesuaikan dengan `$table_prefix` kalian, jika tidak skrip di atas akan terjadi galat.

Kemudian yang terakhir kita ubah juga tautan `options` -nya yang mana tautan ini yang pertama kali dibaca oleh WP saat memuat di awal, jadi pastikan wajib diubah!

```sql
UPDATE wp_options
SET option_value = REPLACE(option_value, 'http://link.lama', 'http://link.baru')
WHERE option_value LIKE '%http://link.lama%';
```

Nah, selesai sudah. Langkah terakhir kita cek apakah situs kita sudah daring atau belum?

Oh iya, sebetulnya saya sudah membahas tentang migrasi WP di artikel sebelumnya kalian bisa baca khusus pengguna shared hosting: <http://www.situsali.id/cara-migrasi-wordpress-dari-localhost-ke-hosting-cpanel-disertai-video/>.

Semoga bermanfaat 😉
