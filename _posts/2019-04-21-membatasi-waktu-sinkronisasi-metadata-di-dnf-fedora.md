---
title: "Membatasi Waktu Sinkronisasi Metadata Di Dnf Fedora"
date: 2019-04-21 21:51:01 +0700
layout: post
tags: [fedora,gnulinux]
category: linux
---

Fedora setiap kali kita ingin melakukan pemasangan ataupun pencarian paket aplikasi dari `dnf`,  ia akan selalu melakukan sinkronisasi metadata. Perlu diketahui bahwa metadata dibutuhkan `dnf` sebagai indeksi berkas pada repositori. Simpelnya, metadata itu pangkalan data dari `dnf`.

## Pokok Masalah

Sinkronisasi metadata sangatlah penting, karena pada saat kita ingin melakukan pemasangan paket, `dnf` akan mengecek paket tersebut pada metadata di lokal dan memastikan semuanya sama dengan peladen repositori. Jika tidak, tentu kita akan mendapati galat 404 karena berkas tidak ada dalam peladen.

Fedora secara asali menerapkan sinkronisasi metadata selama 48 jam atau 2 hari. Jadi jika sudah lebih dari dua hari, kalian ingin memasang aplikasi, maka `dnf` akan memperbaharui metadata-nya.

![Contoh Pembaruan Metadata](/img/membatasi-waktu-sinkronisasi-metadata-di-dnf-fedora-1.png)

Gambar di atas hanya contoh pembaruan metadata. Kalau metadata berukuran kecil (filesize), mungkin tidak akan menjadi masalah. Lainhal jika berukuran hingga puluhan megabyte akan sangat menjengkelkan, terlebih lagi bagi para pengguna internet berkecepatan rendah dan dibatasi kuota. Ini akan sangat menyiksa. Kebetulan juga saya salah satu yang merasakan itu 🤣.

## Solusi

Saya ada sedikit solusi yang mungkin akan membantu kalian. Yakni dengan kita membatasi `metadata_expire`. Kalian bisa memperpanjang masa kadaluarsanya sebanyak satu minggu atau satu bulan. Tapi saya saya lebih baik jangan diberi kadaluarsa, mengapa? Karena kita bisa memperbarui metadata secara manual dari `dnf`.

Berikut ini solusinya. Pertama-tama kalian sunting berkas `/etc/dnf/dnf.conf`

```bash
$ vim /etc/dnf/dnf.conf
```

Lalu tambahkan `metadata_expire=never` dan `metadata_timer_sync=0` dibaris paling bawah seperti gambar berikut:

![Metadata](/img/membatasi-waktu-sinkronisasi-metadata-di-dnf-fedora-2.png)

Kalau kalian ingin menganti menjadi 6 hari misalnya. Tinggal ganti kata `never` dengan `6h` atau `86400`.

Kemudian pastikan semua repositori tidak ter-override dengan masing-masing konfigurasinya.  Kita bisa cek dengan cara berikut:

```bash
$ grep -r /etc/yum.repos.d/ -e 'metadata_expire'
```

![Metadata](/img/membatasi-waktu-sinkronisasi-metadata-di-dnf-fedora-3.png)

Kalian lihat beberapa repositori ada yang tertimpa dengan konfigurasinya. Ada yang kadaluarsa 6 jam ada juga yang 7 hari. Oleh karena itu kita harus merubahnya menjadi `expired`. Sebelum diubah cek dulu repositori mana saja yang dipakai, dengan perintah berikut:

```bash
$ grep -Ril /etc/yum.repos.d/ -e 'enabled=1'
```

![Metadata](/img/membatasi-waktu-sinkronisasi-metadata-di-dnf-fedora-4.png)

Nah, itu dia repostori yang aktif. Sekarang tinggal kita ubah satu persatu berkas seperti di atas.

Langkah terakhir ketika kita ingin memasang aplikasi pastikan ditambah parameter `--cacheonly`. Contoh

```bash
$ sudo dnf install vlc --cacheonly
```

Semoga bermanfaat 😉
