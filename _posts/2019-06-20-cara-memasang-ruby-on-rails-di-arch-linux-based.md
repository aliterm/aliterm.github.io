---
title: "Cara Memasang Ruby On Rails di Arch Linux Based"
layout: post
date: 2019-06-20 09:13:31 +0700
tags: [ruby, gnulinux, archlinux]
---

Kebetulan lagi memulai belajar Ruby on Rails (RoR) yakni suatu framework untuk membangun aplikasi web dengan bahasa pemrograman ruby.  Dan kebetulan pula, RoR sudah terpasang lama, dikomputer saya yang menggunakan Arch Linux.

Agar tidak lupa, berikut ini  cara saya memasangan Ruby on Rails di Arch Linux based, artinya ini dapat pula digunakan pada distro turunan Arch Linux.

## Pasang Ruby dan NodeJS

Sebelum memasang pertama-tama, pastikan kalian sudah  memasang ruby dan nodejs jika belum, lakukan perintah berikut:

```bash
$ sudo pacman -Sy ruby nodejs
```

## Pasang RoR dari Gem

Setelah ruby terpasang kita tinggal pasang RoR menggunakan paket manager milikruby yakni dengan gem. Berikut perintahnya:

```bash
$ gem install rails
```

## Konfigurasi Gem

Dikarenakan RoR dipasang dari paket manager bukan milik Arch Linux, maka kita tidak bisa langsung memanggilnya.  Kita perlu mengeset $PATH yang berisi binary hasil dari gem agar dapat dieksekusi dari Terminal.

```bash
$ GEM_PATH=$(gem environment | grep "USER INSTALLATION DIRECTORY" | awk '{print $5}')
$ echo "export PATH=$PATH:$GEM_PATH/bin" >> ~/.bashrc && source ~/.bashrc
```

### Penjelasan Perintah

Btw, perintah `GEM_PATH` bla bla bla di atas maksudnya apa? Baiklah akan saya jelaskan sedikit. Jadi, perintah tersebut berfungsi untuk mencari path dari hasil gem dengan mudah. Singkatnya, ketika kalian ketik gem environment maka akan menghasilkan keluaran seperti ini:

```bash
RubyGems Environment:
  - RUBYGEMS VERSION: 3.0.3
  - RUBY VERSION: 2.6.3 (2019-04-16 patchlevel 62) [x86_64-linux]
  - INSTALLATION DIRECTORY: /usr/lib/ruby/gems/2.6.0
  - USER INSTALLATION DIRECTORY: /home/ali/.gem/ruby/2.6.0
  - RUBY EXECUTABLE: /usr/bin/ruby
  - GIT EXECUTABLE: /usr/bin/git
  - EXECUTABLE DIRECTORY: /usr/bin
  - SPEC CACHE DIRECTORY: /home/ali/.gem/specs
  - SYSTEM CONFIGURATION DIRECTORY: /etc
  - RUBYGEMS PLATFORMS:
    - ruby
    - x86_64-linux
  - GEM PATHS:
     - /usr/lib/ruby/gems/2.6.0
     - /home/ali/.gem/ruby/2.6.0
  - GEM CONFIGURATION:
     - :update_sources => true
     - :verbose => true
     - :backtrace => false
     - :bulk_threshold => 1000
     - "gem" => "--user-install"
  - REMOTE SOURCES:
     - https://rubygems.org/
  - SHELL PATH:
     - /usr/local/bin
     - /usr/local/sbin
     - /usr/bin
     - /usr/lib/jvm/default/bin
     - /usr/bin/site_perl
     - /usr/bin/vendor_perl
     - /usr/bin/core_perl
     - /home/ali/.gem/ruby/2.6.0/bin
```

Nah, untuk mempermudah langsung saja kita `grep`.  Jadi `gem environment | grep "USER INSTALLATION DIRECTORY"` hasilnya akan seperti ini:

```bash
- USER INSTALLATION DIRECTORY: /home/ali/.gem/ruby/2.6.0
```

Jika dilihat dari hasil di kita bisa potong agar menghasilkan keluaran `/home/ali/.gem/ruby/2.6.0` dengan `awk` yang berada dalam posisi ke-5 jadi perintahnya seperti ini `gem environment | grep "USER INSTALLATION DIRECTORY" | awk '{print $5}'` .Kemudian baru deh, saya masukan ke dalam variabel `GEM_PATH=$(bla bla bla)`. Dan yang terakhir ditulis diberkas `.bashrc` agar bisa langsung dipergunakan.
Eksekusi RoR

Rails sudah terpasang dan sudah dapat digunakan, kita tinggal jalankan dengan membuat projek baru.

```bash
$ rails new NAMA_ROR_KALIAN
```

Pada saat proses pemasangan akan ada pertanyaan memasukan kata sandi seperti berikut:

```bash
Fetching source index from http://rubygems.org/


Your user account isn't allowed to install to the system Rubygems.
You can cancel this installation and run:

    bundle install --path vendor/bundle

    to install the gems into ./vendor/bundle/, or you can enter your password
    and install the bundled gems to Rubygems using sudo.

    Password:
```

Abaikan saja, Cukup tekan `ENTER`. **Ingat! Jangan pernah menggunakan** `sudo` **untuk paket manager yang bukan milik distro. Karena dikhawatirkan ada skrip jahat yang tidak kita ketahui dari luar, dan bukan tanggung jawab distro**.

Yang hanya perlu kita lakukan adalah seperti yang tertulis dari warning message di atas. Yakni menjalankan perintah `bundle install --path vendor/bundle`. Jadi perintah lengkapnya seperti berikut:

```bash
$ cd nama_ror_kamu
$ bundle install --path vendor/bundle
```

Selesai, jalankan aplikasi RoR kalian dengan perintah berikut:

```bash
$ rails server
```

Langkah selanjutnya? Kita sama-sama belajar RoR, dan insya Allah akan saya tulis pula dasar-dasarnya. Semoga bermanfaat ya kawan-kawan sekalian :D.
