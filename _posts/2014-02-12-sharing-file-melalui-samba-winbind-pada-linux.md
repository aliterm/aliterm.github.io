---
layout: post
title: Sharing File Melalui Samba Winbind Pada Linux
date: 2014-02-12 00:00 +0000
tags: [sharing, samba]
---

Pada Artikel kali ini saya ingin membagikan sedikit pemanfaatan Samba pada Linux yang digunakan untuk membangun jaringan kombinasi sistem operasi Windows dengan Linux. Salah satu pemanfaatan Samba adalah Sharing File atau berbagi file antar komputer atau bahkan antar komputer dengan smartphone atau PC tablet.

Sedikit ulasan tentang Samba adalah program yang dapat menjembatani kompleksitas berbagai platform system operasi Linux (UNIX) dengan mesin Windows yang dijalankan dalam suatu jaringan komputer. Samba merupakan aplikasi dari UNIX dan Linux, yang dikenal dengan SMB(Service Message Block) protocol. Banyak sistem operasi seperti Windows dan OS/2 yang menggunakan SMB untuk menciptakan jaringan client/server. Protokol Samba memungkinkan server Linux/UNIX untuk berkomunikasi dengan mesin client yang mengunakan OS Windows dalam satu jaringan (Sumber: Kang Deden).

Kemudian Winbind itu adalah Name Service Switch (NSS) untuk memperbaiki nama dari Server NT. Singkat kata seperti Netbios di Windows, pernah kan Anda ping localhost Anda dengan nama komputer Anda pada jaringan di Windows? Lalu apa fungsinya? Fungsinya adalah menghemat waktu :D, maksudnya jika Anda di rumah menggunakan jaringan DHCP (Dynamic Host Configuration Protocol) pasti Anda akan merasa kesulitan untuk mengetahui IP masing-masing dari komputer yang terhubung dengan router Anda, karena otomatis IP akan berubah-rubah ketika Komputer dimatikan / dihidupkan kembali. Untuk mengatisipasi kendala tersebut kita tidak perlu mengetahui IP dari setiap komputer, cukup tahu nama komputer itu apa, lalu kita ping dengan computer name itu maka kita akan tau IP nya. Seperti halnya juga domain, netbios juga sama.

Contoh ping localhost pada laptop saya:
