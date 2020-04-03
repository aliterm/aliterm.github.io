---
title: "Menjalankan php 5.6 dan php 7.2 dengan Apache Di MacOS"
date: 2018-11-02 16:48:52 +07:00
subtitle: ""
tags: [apache, php, macos]
category: "system-tools"
layout: post
---

Tutorial sebelumnya saya telah menulis mengenai cara menjalankan php5.6 dan php7.2 secara bersamaan khusus untuk pengguna GNU/Linux distro Ubuntu. Sekarang giliran macOS.

## Kebutuhan

* Sudah memasang brew atau homebrew (https://brew.sh/).
* Sistem Operasi macOS 10.11 (EL Capitan) atau lebih.
  Dalam praktek di sini, saya menggunakan macOS HighSierra.

## Persiapan

1. Koneksi internet.

2. vim dan paham dasar penggunaannya.
3. Secara asali HighSierra sudah terdapat php71 dan apache mereka perlu dinonaktifkan.
   kita cukup gunakan php dan apache bawaan dari brew. Adapun caranya sebagai berikut:
   ```bash
   $ sudo apachectl stop
   $ sudo launchctl unload -w /System/Library/LaunchDaemons/org.apache.httpd.plist 2>/dev/null
   ```

4. Buat direktori `Web` dan `logs` di Home kalian. Caranya:
   ```bash
   $ mkdir -p ~/Web/logs
   ```

5. Mengetahui User dan Group yang kalian gunakan. Caranya sebagai berikut:
   ```bash
   $ ls -l ~/
   ```
   Hasilnya seperti gambar berikut:
   ![img](/img/situsali-macOS-terminal-ls.png)

   Terlihat hasil di atas bahwa user yang digunakan adalah `ali` sedangkan group-nya adalah `staff`.

## Pemasangan
