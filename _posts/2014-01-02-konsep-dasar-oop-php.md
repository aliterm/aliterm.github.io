---
date: 2014-01-02 09:13:31 +0700
layout: post
tags: [php,oop]
title: "Konsep dasar OOP di PHP"
---

## Introduksi

PHP merupakan bahasa pemrograman yang cukup banyak digunakan untuk membuat web dinamis. Seiring perjalanan waktu PHP terus dikembangkan dan PHP sejak versi PHP 5 telah mendukung Object Oriented Programming atau OOP secara penuh.

Di PHP Object di sini didefinisikan dalam sebuah class. Kemudian Properti object didefinisikan menggunakan kata yang tersisipi var. Sedangkan method dari object berbentuk sebuah function.

## Class dan Object

Class merupakan struktur dasar atau sebuah kerangka yang digunakan untuk membentuk sebuah object. Sedangakan Object adalah instance dari class-nya, dengan demikian object itu bisa dikatakan data yang telah terstruktur sesuai dengan yang didefinisikan dalam sebuah class. Jadi di PHP jika kalian ingin membuat object, maka harus mendefinisikan kata class kemudian nama class-nya dibuka dan ditutup menggunakan kurung kurawal `{}`.

Contoh:

```php
<?php

class Makanan {
}
```
Lalu object diimplementasikan dengan variabel dan dikuti kata `new` kemudian nama class-nya.

```php
<?php

class Makanan {
}

$makanan = new Makanan;
```
