---
title: "Memperbaiki Grub GNU/Linux Dengan Chroot"
date: 2019-02-09 21:25:00 +0700
layout: post
tags: [gnulinux,chroot]
category: "linux"
---

## Introduksi

Pernah kah kalian mengalami GNU/Linux tiba-tiba tidak bisa masuk pada saat di-restart?

Atau tiba-tiba `grub` hilang setelah kita memasang Windows untuk dual-boot?

Jika iya, kalian tidak sendirian. Saya pun pernah mengalami hal demikian. Karena pengalaman itulah yang membuat saya ingin menuliskannya, siapa tahu ini menjadi berguna bagi kalian pembaca setia situsali.

## Persyaratan

- Memiliki USB Bootable GNU/Linux. Jika kalian belum punya sebaiknya buat dulu, caranya ada di blog ini, kalian bisa cari.
- Koneksi Internet. Ini dibutuhkan pada saat pemasangan beberapa aplikasi menggunakan manajer paket.

## Masuk GNU/Linux

Boot komputer kalian menggunakan USB Bootable Live GNU/Linux. Jika kalian sudah masuk. Lakukan pengecekan di mana kalian memasang GNU/Linux, ada dua cara yakni:

```bash
$ lsbk
```

atau

```bash
$ sudo fdisk -l
```

Saya asumsikan kalian memasang GNU/Linux di `/dev/sda1`. Jika kalian pengguna UEFI kalian perlu tahu juga letak `/boot` atau `/boot/efi`, saya asumsikan lagi terletak di `/dev/sda2` .

Kita sudah tahu letak `/` dan `/boot/efi` selanjutnya tinggal kita mount dengan perintah berikut:

```bash
$ sudo mkdir /media/recovery/
$ sudo mount /dev/sda1 /media/recovery/
```

Khusus pengguna UEFI kalian wajib melakukan ini:

```bash
$ sudo mount /dev/sda2 /media/recovery/boot/efi
```

## Pemasangan Grub

Setelah semua sudah di-mount langsung saja kita pasang `grub`-nya.

### Khusus penggunan BIOS

```bash
$ sudo grub-install /dev/sda --root-directory=/media/recovery/ --target=i386-pc
```

### Khusus pengguna UEFI

```bash
$ grub-install --target=x86_64-efi --efi-directory=/media/recovery/boot/efi/ --bootloader-id=GRUB
```

## Chroot

Cukup panjang juga ya caranya? Kalian jangan menyerah dulu ya.. 😀 karena kita baru saja memulai.

Untuk masuk `chroot` kita perlu me- `mount`

```bash
$ cd /media/recovery
$ sudo mount -t proc proc proc/
$ sudo mount -t sysfs sys sys/
$ sudo mount -o bind /dev dev/
$ sudo mount -t devpts pts dev/pts/
```

Kemudian langsung kita `chroot` dengan perintah di bawah ini:

```bash
$ sudo chroot /media/recovery /bin/bash
```

Kalau sudah masuk `chroot`, kalian sudah seperti masuk dalam GNU/Linux yang berada dalam media penyimpanan / diska kalian. Tinggal langkah selanjutnya kita update `grub` config dengan perintah:

```bash
# grub-mkconfig -o /boot/grub/grub.cfg
```

Sip mudah kan? Mudah banget…😎

## Penutup

Sebenarnya jika kita sudah masuk `chroot` kita bisa melakukan apapun, seperti pemasangan aplikasi atau bahkan merubah kata sandi root tapi karena topik bahasan kita hanya pada perbaikan `grub` maka kita sampai di sini dulu ya. Nanti kita lanjut lagi dalam studi kasus lainnya menggunakan `chroot`.

Semoga bermanfaat 😉
