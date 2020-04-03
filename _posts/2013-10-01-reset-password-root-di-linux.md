---
title: "Reset Password Root Di GNU/Linux"
date: 2013-10-01 04:50:54 +0700
image: "/images/Test.jpg"
tags: ["gnu/linux","chroot"]
layout: "post"
---

## Introduksi

Kadang karena sibuk, membuat hal terkecil lupa seperti halnya dengan password, baik password email, facebook, forum atau password OS kita sendiri juga ikut lupa 😄, Ya wajar-wajar saja, mungkin karena kebanyakan password. Saya sendiri pun pernah mengalami lupa password. Kalau, password email atapun sosmed lupa, kita bisa manfaatkan fitur `forgot password`, bagaimana jika password sistem operasi kita?

Kali ini saya ingin membagikan sedikit tips, menganai bagaimana cara me-reset password `root` di GNU/Linux.

## Persyaratan

Sebelum memasuki tahap praktek ada kiranya beberapa persyaratan yang harus kalian persiapkan.

1. Sudah membuat GNU/Linux USB/CD bootable. Bebas menggunakan distro apapun. Saran saya gunakan distro yang sudah familiar. Kalau contoh di sini saya menggunakan Arch Linux.

2. Pastikan partisi kalian tidak terenkripsi. Jika memang sudah terenkrip, mohon maaf kalian tidak bisa lanjut. Mungkin nanti akan saya buatkan mengenai hal ini. Tapi tidak janji 😄.

## Proses Reset Password

Jika syarat di atas sudah terpenuhi, mari langsung praktek.

Pertama-tama kalian booting dulu ke GNU/Linux USB atau CD. Selanjutnya. Kalian `mount`. Perintahnya sebagai berikut:

### Mount Drive

Cek di mana GNU/Linux kalian dipasang.

```bash
$ sudo fdisk -l
```
atau gunakan `lsblk`

```bash
$ lsblk
```

Jika sudah ketemu, langsung saja kalian `mount`

```bash
$ sudo mount /dev/sdX /mnt
```
Ingat tanda `X` dari `sdX` di atas yakni nomor urut partisi GNU/Linux kalian dari hasil `lsblk` atau `fdisk`.

### Chroot

Jika root dari partisi kalian sudah di `mount` langsung lakulan perintah `chroot` seperti berikut:

```bash
$ sudo chroot /mnt /bin/bash
```
Jika berhasil kalian akan langsung masuk dalam mode root.

### Ganti Password

Nah, langkah selanjutnya kita bisa gunakan perintah `passwd` untuk membuat password baru:

```bash
# passwd
```
Tulis password baru kalian.

## Kesimpulan

Pengguna GNU/Linux jika kalian lupa password root kalian. Sebetulnya bisa langsung diakali dengan `user` biasa yang diberikan akses `sudo` namun, jika memang tidak bisa baru kalian melakukan metode `chroot`. Caranya pun sangat mudah, cukup boot melalui Live USB/CD dengan syarat partisi kalian tidak terenkripsi.

Semoga bermanfaat 😉


