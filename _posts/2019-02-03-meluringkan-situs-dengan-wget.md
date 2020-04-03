---
title: "Meluringkan Situs Dengan Wget"
date: 2019-02-03 21:27:17 +0700
layout: post
tags: [wget,gnulinux]
category: linux
---

## Prakata

Terkadang kita perlu menyalin suatu situs yang kita anggap penting dan bermanfaat dengan meluringkannya, guna untuk membacanya kembali semisal kita berada dalam situasi yang mana kita tidak dapat terkoneksi dengan internet.

## Persiapan

Yakni menggunakan aplikasi wget. Jika kalian pengguna GNU/Linux, berbahagialah karena wget pada beberapa distro tertentu sudah menjadi asali. Kalaupun belum ada, kita bisa memasanganya dengan manajer paket sesuai dengan distro yang kita pakai.

Contoh untuk penguna Ubuntu beserta derivatifnya:

```bash
$ sudo apt install wget
```

Lalu bagaimana jika bukan pengguna GNU/Linux mungkin kalian perlu mengompilnya yang bisa kalian ambil kode sumbernya dari situs resmi GNU:

<https://www.gnu.org/software/wget/>

Oh iya, kalau kalian pengguna macOS kalian juga bisa pasang wget dengan brew.
Cara Menggunakan

Sedangkan perintah untuk meluringkan situs adalah sebagai berikut:

```bash
$ wget --mirror --convert-links --adjust-extension --page-requisites --no-parent --no-check-certificate https://contoh.com/
```

Atau kita bisa gunakan perintah yang lebih singkat:

```bash
$ wget -mkEpnp --no-check-certificate https://contoh.com/
```

Mudahkan? Semoga bermanfaat.😁
