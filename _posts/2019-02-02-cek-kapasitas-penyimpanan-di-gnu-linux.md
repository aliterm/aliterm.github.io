---
layout: post
title: "Cek Kapasitas Penyimpanan Di GNU/Linux"
date: 2019-02-02 21:31:03 +0700
tags: [gnulinux,storage,cli]
category: linux
---

## Latar Belakang

Teman saya pernah bertanya bahwa VPS yang dia kelola ketika ingin diperbarui gagal dan terjadi galat. Ketika saya lihat, informasi galat yang tertera ternyata dia kehabisan ruang penyimpanan.


## Kronologi

Kemudian saya coba periksa dengan perintah:

```bash
$ df -h /
```

Kalau dari tebakan saya ini pasti ada hubungannya dengan log yang menyebabkan kapasitas media penyimpanannya menjadi penuh.
Solusi

Daripada tebak-tebak buah manggis, lebih baik saya pastikan dengan mengecek seluruh direktori menggunakan perintah berikut:

```bash
$ sudo su
# du --max-depth=1 --human-readable / | sort --human-numeric-sort
```

Ternyata tebakan saya salah, justru yang penuh direktori home hahaha 🤣 setelah ditanya, sebelumnya dia sering coba-coba aplikasi dan mengunduh beberapa video yang menyebabkan ruang penyimpanannya menjadi penuh.

Dari kejadian tersebut, saya mencoba memerikasa lebih dalam pada direktori home dengan perintah berikut:

```bash
$ du -d1 -h ~ | sort -h
```

Nah ketahuan deh direktori mana yang bikin penuh.
Kesimpulan

Peristiwa di atas bisa kita simpulkan bahwa, jika ruang penyimpanan penuh, kita dapat melakukan pengecekan seluruh direktori di root dengan perintah:

```bash
$ sudo su
# du --max-depth=1 --human-readable / | sort --human-numeric-sort
```

Atau salah satu direktori yang kalian curigai:

```bash
$ du -d1 -h /direktori/kalian/ | sort -h
```

Semoga bermanfaat.
