---
title: "Memperbaiki Grub Yang Tertimpa Setelah Install Windows"
date: 2014-01-17 04:50:54 +0700
image: "/images/Test.jpg"
tags: ["gnu/linux","grub","bootloader"]
layout: "post"
---

## Latar Belakang

Kalian masih suka dengan Windows? Sulit meninggalkan Windows karena ada software atau game kesukaan kalian tidak kompatibel dengan GNU/Linux? Ya tentu saja dengan dualboot menjadikan sebuah alternatif terbaik bagi mereka yang sulit meninggalkan Windows atau memang karena tuntutan pekerjaan sehingga mau-mau tidak mau harus memakai Windows.

Saya sendiri termasuk pengguna GNU/Linux dan Windows (dualboot), tapi saya bekerja lebih sering menggunakan GNU/Linux daripada Windows, malah Windows itu jarang sekali dipakai, saya pakai Windows cuma untuk menggunakan software Microsoft Office 2013 saja, meskipun hanya untuk keperluan kantor.

Ok kembali ke judul artikel ini, melihat situasi dari teman-teman saya yang dualboot sering kali terjadi Grub nya tertipa karena sehabis Install Windows atau juga Grubnya tidak terinstall sehabis Install GNU/Linux.

Pada Artikel kali ini yang saya bahas GNU/Linux itu berarti menyangkut hampir semua distro GNU/Linux baik itu Ubuntu, LinuxMint, Fedora, Arch Linux, dlll. Jadi istilahnya secara universal 😀

## Persiapan
Langsung saja kita praktek, sebelum praktek yang perlu kalian siapkan adalah Live OS terserah mau distro apa, apakah Ubuntu, Arch Linux, Fedora, dll. Tapi saya menyarankan menggunakan LiveOS Arch Linux mengapa? ~~karena alasan klasik Arch Linux ISO nya sudah merangkap 32bit dan 64bit sehingga memudahkan jika menggunakan atau menginstall salah satu GNU/Linux itu baik 32bit atau 64bit.~~ Saat ini hampir semua distro tidak lagi mendukung 32bit, jadi kalian bisa gunakan distro lawas.

## Mount Partisi

Setelah itu, boot PC/Laptop kalian menggunakan LiveOS baik secara CD/DVD ataupun USB Flashdisk yang bisa kalian buat dengan [Rufus]. Kemudian setelah masuk Live pertama-tama `mount` dulu GNU/Linux kalian.

```bash
$ sudo mount /dev/sdX /mnt
```
Untuk `X` pada kata `sdX` di atas, mengidentifikasikan nomor partisi kalian. Oleh karenaitu, kalian harus tahu dimana letak partisi Linux kalian, jika kalian tidak tau atau lupa kalian bisa lihat dengan fdisk, caranya:

```bash
$ sudo fdisk -l
```

Lihat gambar di bawah ini
![fdisk -l](/img/memperbaiki-grub-yg-tertimpa-setelah-install-windows-1.png)

Jika dilihat dari gambar, GNU/Linux terletak pada `sda1`. Nah, kita bisa langsung `mount` dengan cara berikut:

```bash
$ sudo mount /dev/sda1 /mnt
```
## Install Grub

Langkah selanjutnya kita install `grub` dengan perintah di bawah ini.
> Perlu diperhatikan bahwa perintah di bawah hanya berlaku bagi kalian yang menggunakan legacy boot bukan mode UEFI

### Distro Pada Umumnya

```bash
$ sudo grub-install /dev/sda --root-directory=/mnt
```
### Khusus Fedora dan turunannya
```bash
$ sudo grub2-install /dev/sda --root-directory=/mnt
```
[Rufus]:https://rufus.ie
