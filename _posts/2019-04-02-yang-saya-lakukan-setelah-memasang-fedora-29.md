---
title: "Yang Saya Lakukan Setelah Memasang Fedora 29"
date: 2019-04-20 22:20:30 +0700
tags: ["fedora","gnulinux"]
category: "linux"
layout: post
---

## Sekata-Kata

Alasan saya memilih Fedora adalah stabilitas dan adanya deltarpm beserta fastestmirror. Lebih-lebih ke deltarpm inilah terpenting bagi saya. Karena saat ini, saya tidak lagi menggunakan layanan internet kabel, melainkan dengan modem atau tethering dari smartphone. Akan sangat berasa manfaatnya menggunakan deltarpm ini, sebagai penghemat kuota.

Kemudian stabiltas, meskipun Fedora merupakan distro ujicoba dari RHEL (RedHat Enterprise Linux) dan setiap 9 bulan berganti versi. Kestabilan Fedora saya akui lebih dibandingkan dengan distro semisal Ubuntu. Oh, iya Ubuntu ini memiliki varian LTS (Long Term Service), yang memungkinkan didukung hingga 5 tahun. Namun menurut pandangan saya, dibandingkan dengan Ubuntu, Fedora ini masih lebih stabil. Ingat ini hanya pendapat pribadi saya! Bisa jadi berbeda dengan kalian. Akan lebih baik, silahkan kalian bandingkan sendiri.

Diartikel ini, saya tidak akan menjelaskan bagaimana proses pemasangan Fedora. Mungkin jika sempat, akan saya buatkan tutorialnya. Karena pemasangan Fedora saya akui agak sedikit tricky dibandingan dengan distro lainnya semisal Ubuntu dan Manjaro. Terutama bagian pemilihan storage. Untuk sementara kalian bisa mencari tutorialnya di blog lain atau dari Youtube.
Setelah Pasang

Agar tidak panjang mengenai alasan saya memasang Fedora, dan tidak keluar dari topik judul. Langsung saja kita mulai.

## Setelah Pasang Fedora

Yang saya lakukan setelah memasang Fedora adalah sebagai berikut:

### Mengaktifkan Fastest Mirror dan Delta RPM

Fedora 29 secara asali tidak mengaktifkan fastestmirror dan deltarpm jika kita ingin memanfaatkan fitur tersebut, perlu diaktifkan terlebih dahulu. Caranya adalah sebagai berikut:

Buka berkas di `/etc/dnf/dnf.conf` :

```bash
$ vim /etc/dnf/dnf.conf
```

Kemudian tambahkan:

```bash
fastestmirror=true
deltarpm=true
```

![fastest mirror](/img/yang-saya-lakukan-setelah-memasang-fedora-29-1.png)

### Pasang RPM Fusion

Fedora sangat ketat dalam hal repositori di dalamnya. Secara asali, aplikasi non-free tidak disertakan dalam repositori. Jadi jangan terkejut jika kalian ingin memasangan ffmpeg atau kebutuhan multimedia lainnya, di Fedora tidak ada. Karena itulah, kita membutuhkan rpmfusion yang mana ia menangani paket aplikasi non-free. Berikut ini cara pemasangannya:

```bash
$ sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
$ sudo dnf install https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

### Memasang Google Chrome

Ini sebetulnya opsional saja. Karena beberapa orang ada yang lebih nyaman dengan berselancar dengan Google Chrome dibandingkan Firefox.

Google Chrome ada dua cara memasangnya, pertama kita bisa langsung pasang dari rpm dari situs resminya, dan yang kedua kita tambahkan repositorinya Google Chrome. Saya lebih menyarankan cara kedua, karena akan lebih mudah pada saat kita memasang tidak perlu lagi mencari dependensinya. Juga pada saat meng-update-nya. Tinggal lakukan melalui dnf.

Menambahkan repositori Google Chrome:

```bash
$ sudo dnf install fedora-workstation-repositories
$ sudo dnf config-manager --set-enabled google-chrome
```

Memasang Google Chrome:

```bash
$ sudo dnf install google-chrome-stable
```

### Memasang Kebutuhan Multimedia

Kalian tentu masih ada yang menyimpan musik mp3? Jika kalian ingin memutar media di Fedora, terlebih dahulu paket multimedianya dipasang. Jangan lupa, untuk melakukan tahapan ini, kalian harus memasang rpmfusion pada langkah ke-2 di atas.

```bash
$ sudo dnf install \
gstreamer-plugins-base \
gstreamer1-plugins-base \
gstreamer-plugins-bad \
gstreamer-plugins-ugly \
gstreamer1-plugins-ugly \
gstreamer-plugins-good-extras \
gstreamer1-plugins-good \
gstreamer1-plugins-good-extras \
gstreamer1-plugins-bad-freeworld \
```

## Penutup

Kita sampai di sini dulu. Untuk aplikasi lainnya semisal kebutuhan gambar dan memanipulasi foto. Misalnya Gimp dan Inkscape. Kalian bisa pasang sendiri aplikasi tersebut melalui dnf.

Semoga tulisan ini bermanfaat.
