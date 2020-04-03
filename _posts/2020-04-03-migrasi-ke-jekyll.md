---
title: "Migrasi ke Jekyll"
date: 2020-04-03 09:13:31 +07:00
layout: post
---

Sejak 1 Juli 2019, saya memutuskan untuk memindahkan platform [situsali] dari WordPress ke SSG (Static Site Generator), dengan memilih [hugo] sebagai generatornya.

## Wacana Pindah Platform

Pemindahan platform [situsali] sebetulnya sudah saya wacanakan sejak tahun 2016 lalu. Kebetulan ditahun itu SSG memang sedang naik daun. Akan tetapi, wacana pemindahan dibatalkan, karena saya memiliki banyak pertimbangan seperti:

1. **[situsali] sudah cukup berumur**. Ia dibangun sejak akhir tahun 2013, ditahun 2016 berarti sudah berumur 3 tahun. Jika platform dipindah maka akan perlu banyak effort salah satunya masalah SEO.
2. **Karena static site tidak memiliki semacam** `search page`. Meskipun bisa diakali, SSG tidaklah sama dengan dynamic site. Karena situs dinamis disimpan dalam database sehingga lebih mudah untuk ditemukan dan dapat diolah dari backend. Sedangkan static site, kita harus mengolahnya dengan bantuan `javascript`.
3. **Migrasi artikel**. Meskipun bisa saja kita gunakan import tool, akan tetapi yang namanya pindah platform pasti akan perlu dimodifikasi menyesuaikan platform tersebut.
4. **Komentar Tool**. Situs akan lebih hidup dengan adanya komentar dari pembaca. Kalau di WordPress fitur ini sudah ada secara default, beda dengan Static Site. Kita perlu menyisipkan komentar pihak ketiga. Belum lagi, masalah kendala impor komentar.
5. **Konsultasi kepada para senior**, mereka mengatakan bahwa __"jangan dipindah, karena sayang blog sudah lama"__. Kata-kata tersebut, memang ada betulnya mungkin sama denga poin nomor satu.

## Mencoba Jekyll

Awalnya [situsali] sudah saya buatkan versi ssg nya di subdomain <static.situsali.com> dengan Jekyll. Oh iya, Jekyll ini merupakan SSG pertama yang saya kenal sejak tahun 2014an dan memang sudah pernah coba-coba di GitHub Pages.

## Sudah menggunakan Hugo

Sebelum berpindah seperti biasa, saya melakukan uji coba. Saya buat semacam clone dari [situsali] di subdomain <notes.situsali.com>.

## Pindah ke Domain Dot Id
Pertanggal 17 Juni 2019, [situsali] migrasi domain. Sebelumnya menggunakan domain `situsali.com` kini menjadi `situsali.id`. Pemindahan domain dilakukan berdasarkan atas `harga yang lebih murah`.

Jadi awal mulanya, ketika saya melakukan renewal domain [pegelinux.id], saya terkejut karena harga domain dot id hanya 107 ribu ditambah pph 10% menjadi 117 ribu rupiah. Sangat murah dibandingkan domain dot com saya yang seharga 208 ribu. Lumayan jadi hemat 91 ribu, dan ini setara dengan harga VPS [situsali] selama sebulan.

Saya belum tahu secara pasti bahwa domain id ini sedang promo atau harga 107 itu selamanya. Oleh karenanya, untuk mengantisipasi saya membeli domain langsung 3 tahun. Mumpung sedang murah 😅. Update pertanggal 18 Juli 2019, ternyata ini memang sedang promo.

Pemindahan domain inilah yang menjadikan cikal-bakal mengenai wacana penggantian platform, sembari ada komentar teman di blog yang menyarankan pindah platform.

![Saran Teman](/img/migrasi-ke-hugo-1.png)

Saran teman, menambah yakin saya untuk segera pindah platform.

--- Bersambung ---

[situsali]: https://www.situsali.id
[hugo]: https://gohugo.io
[pegelinux.id]: https://pegelinux.id
