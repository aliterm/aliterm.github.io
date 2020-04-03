---
layout: post
date: 2016-11-06 09:13:31 +0700
tags: [linux,archlinux]
title: "Install Arch Linux Gnome Systemd-Boot Dualboot dengan Windows 10 (Disertai Video)"
---

Melanjuti artikel sebelumnya masih seputar tentang pemasangan Arch Linux dengan metode UEFI. Tutorial kali ini adalah kita dualboot dengan Windows 10 dan dalam Arch Linux kita tidak menggunakan Grub sebagai bootloader melainkan menggunakan systemd-boot. Meskipun seharusnya kalau dualboot itu, ya gunakan Grub tapi tidak untuk tutorial ini. Kita gunakansystemd-boot yang mana ia lebih simpel dan mudah dibandingkan Grub.

Tutorial ini sengaja saya tulis mengingat banyaknya pertanyaan dari teman-teman tentang bagaimana cara pemasangan Arch Linux dualboot dengan Windows 10. Ada berbagai alasan mereka dualboot pertama karena Windows mereka OEM ketika membeli suatu laptop atau PC branded. Yang kedua, karena memang mereka masih butuh Windows jadi tidak bisa singleboot hanya menggunakan GNU/Linux saja.

Langsung saja kita mulai praktek. Langkah-langkah sebelum memulai instalasi Arch Linux beberapa persiapan harus ada di kalian yakni:

- Pastikan kalian sudah mengunduh Arch Linux. Tautan unduh Arch Linux https://www.archlinux.org/download/
- Pastikan kalian sudah membakar (burning) Arch Linux, baik menggunakan DVD ataupun flashdisk. Jika kalian ingin menggunakan flashdisk gunakan aplikasiddatau image writer
- Pastikan kalian sudah terhubung dengan internet. Ini sangat wajib, jika tidak proses instalasi Arch Linux tidak akan berjalan dengan sebagaimana mestinya.

Jika sudah langsun kalian booting Arch Linux kalian, melalui CD/DVD atau flashdisk. Begitu sudah masuk langsung ketik cfdisk:

```bash
# cfdisk
```

## Persiapan Partisi

Asumsi kalian memiliki storage sebesar 20 GB, kita bagi paling sedikit 2 buah partisi yang wajib kalian buat yakni partisi `ESP` dan `Root`. Di sini saya mencontohkan kita buat 4 buah partisi yakni `ESP`, `Swap`, `Root` dan `Home`.

Adapun skema besaran partisi yang saya siapkan adalah sebagai berikut:

- 1 GB, ESP (EFI System Partition)
- 2 GB, Swap
- 10 GB, root
- 7 GB, /home

![Skema Partisi](/img/install-arch-linux-gnome-systemd-boot-dualboot-dengan-windows-10-disertai-video-1.png)

## Tahap Format

Sekarang kita format 4 partisi tadi dengan perintah di bawah ini:

```bash
# mkfs.fat -F 32 /dev/sda5
# mkswap /dev/sda6
# mkfs.ext4 /dev/sda7 -L "ArchLinux"
# mkfs.ext4 /dev/sda8 -L "Home"
```

> Perhatian!!, jangan sampai salah pilih `/dev/sda` nya.

## Tahap Mount

Kemudian setelah di format, kita `mount` semua partisi di atas dan aktifkan pula `swap` -nya.

```bash
# mount /dev/sda7 /mnt
# mkdir /mnt/{boot,home}
# mount /dev/sda5 /mnt/boot
# swapon /dev/sda6
# mount /dev/sda8 /mnt/home
```

## Persiapan Mirror dan Pemasangan Base

Setelah semua tahap `mount`, langkah selanjutnya kita persiapakan `mirror`. Saya sarankan gunakan `mirror` lokal untuk mempercepat proses instalasi.

__Update 2018__
Saya biasa memakasi `mirror` Singapore dan Indonesia. Kita bisa gunakan `reflector`

```bash
# pacman -S reflector
# reflector --country Singapore --country Indonesia --protocol http --portocol https --sort rate --save /etc/pacman.d/mirrorlist
```

Jika semua sudah, langsung kita `pacstrap`.

```bash
# pacman -Syy
# pacstrap /mnt base base-devel
```

Tunggu sampai proses instalasi selesai, lama atau cepatnya tergantung koneksi internet kalian.

Jika sudah selesai, langsung kita buat `fstab`, yang mana digunakan untuk `mount` seluruh partisi penting diawal `booting`.

```bash
# genfstab -L -p -P /mnt > /mnt/etc/fstab
```

## Chroot dan Pengaturan Sistem

Base dari Arch Linux sudah terpasang, langkah selanjutnya kita atur sistem Arch Linux kita, dikarenakan Arch Linux belum berjalan, kita manfaatkan chroot untuk mengatur Arch Linux tersebut, adapun perintahnya sebagai berikut:

```bash
# arch-chroot /mnt
```

## Pengaturan Hostname, Locale dan Zoneinfo

### Membuat hostname:

```bash
# echo "Arch-Linux" > /etc/hostname
```

### Pengaturan Locale

```bash
# nano /etc/locale.gen
```

Uncomment pada `en_US.UTF-8 UTF-8` dan `id_ID.UTF-8 UTF-8` . Kemudian kita buat berkas `locale.conf`:

```bash
# nano /etc/locale.conf
```

Dan isikan seperti berikut:

```bash
LC_COLLATE=C
LANG=en_US.UTF-8
LC_TIME=id_ID.UTF-8
```

Jika sudah langsun kita generate `locale` tersebut:

```bash
# locale-gen
```

Kemudian buat symbolic link zone kita:

```bash
# ln -sf /usr/share/zoneinfo/Asia/Jakarta /usr/localtime
```

## Pemasangan Kebutuhan Jaringan

```bash
# pacman -S bash-completion
# pacman -S ntfs-3g wpa_supplicant dialog
```

## Pembutan User dan Sudo

Agar kita tidak menggunakan user root, maka perlu membuat user biasa yang dengan fungsi `sudo` agar dapat menjalakan aplikasi yang mana membutuhkan root untuk menjalankannya.

Pertama-tama kita buat dulu group `sudo`:

```bash
# groupadd sudo
```

Kemudian kita buat user dengan memasukan sebagaian dari grup sudo.

```bash
# useradd -m -U -G sudo,power,storage,audio,video Namakalian
```

Jangan lupa kita sunting `sudoers`.

```bash
# nano /etc/sudoers
```

Kemdian tambahkan atau uncomment berikut:

```bash
%sudo ALL=(ALL)
```

Dan yang terakhir kita buat password untuk `root` dan `user` yang sebelumnya telah kita buat.

```bash
# passwd Namakalian
# passwd root
```

## Pembuatan Bootloader

Pertama-tama kita buat dulu initramfs:

```bash
# mkinitcpio -p linux
```

Kemudian khusus bagi kalian pengguna prosesor Intel, pasang pula `intel-ucode`.

```bash
# pacman -S intel-ucode
```

Dan langsung kita buat `bootloader` dengan `systemd-boot` dengan perintah berikut:

```bash
# bootctl install
```

Jangan lupa buat entri `systemd-boot` kita di `/boot/loader/entries/`:

```bash
# nano /boot/loader/entries/archlinux.conf
```

Lalu isikan seperti berikut:

```bash
title Archlinux
linux /vmlinuz-linux
initrd /intel-ucode.img
initrd /initramfs-linux.img
options root=/dev/sdaX rw
```

Pada `initrd /intel-ucode.img` itu khusus bagi kalian pengguna prosesor Intel, jika buka hilangkan perintah tersebut. Kemduain pastikan `/dev/sdX` kalian sudah mengetahui di mana letak partisi `root` kalian, dalam contoh kasus di sini berarti di `/dev/sda7`.

Jika sudah langsung saja ketik `exit`, dan `reboot`.

## Tahap Pemasangan Gnome

Sehabis `reboot` kalian masuk Arch Linux kalian dengan `username` yang telah dibuat sebelumnya. Kemudian, langkah selanjutnya, koneksikan dahulu internet kita, jika kalian pengguna `dhcp` dengan kabel LAN, bisa langsung gunakan perintah berikut:

```bash
$ sudo systemctl start dhcpcd
```

Jika kalian pengguna IP statis sebagai koneksi internet, dapat menggunakan dhcpcd juga atau dengan ip atau dengan systemd-network, silahkan baca: <https://wiki.archlinux.org/index.php/Network_configuration#dhcpcd_2>

Jika kalian menggunakan WiFi sebagai koneksi internet, kalian bisa menggunakan perintah:

```bash
$ sudo wifi-menu
```

Untuk memasatikan kalian sudah terkoneksi dengan internet atau belum, gunakan ping.

```bash
$ ping -c 2 google.com
```

Jika sudah langsung kita pasang `xorg-server` terlebih dahulu:

```bash
$ sudo pacman -S xorg-server mesa mesa-demos
```

Ketikan kalin tekan `ENTER` maka akan keluar pilihan `mesa-lib` atau `nvidia-lib`.

Pilih `mesa-lib` jika kalian pengguna Intel atau AMD, jika kalian penguna Nvidia pilih `nvidia-lib`. Atau bisa juga kalian pengguna Nvidia memilih `mesa-lib`, dikarenakan `mesa-lib` ini mendukung hampir seluruh grafis.
Pemasangan Driver VGA

Pasang driver VGA, pastikan kalian mengetahuinya. Untuk mengecek dapat menggunakan cara:

```bash
# lspci | grep VGA
```

### Pengguna VGA Standard

```bash
$ sudo pacman -S xf86-video-vesa mesa mesa-demos
```

### Pengguna Intel

```bash
$ sudo pacman -S xf86-video-intel
```

### Pengguna Nvidia

```bash
$ sudo pacman -S xf86-video-nouveau
```

### Pengguna AMD/ATI

```bash
$ sudo pacman -S xf86-video-ati
```

## Pemasangan DE

```bash
$ sudo pacman -S gnome gedit firefox file-roller gnome-tweak-tool
```

Kemudian kita aktifkan `NetworkManager` dan `GDM`:

```bash
$ sudo systemctl enable NetworkManager
$ sudo systemctl enable gdm
```

Keluar tahap instalasi dan `restart`.

```bash
$ sudo reboot
```

## Video Tutorial

Berikut ini video tutorial praktek dari cara instalasi di atas, untuk mempermudah kalian memahami tulisan saya di atas. Video berikut ini saya mempraktekannya di Virtual Box:

<iframe width="640" height="360" src="https://www.youtube.com/embed/LV5u4FkiVXM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
