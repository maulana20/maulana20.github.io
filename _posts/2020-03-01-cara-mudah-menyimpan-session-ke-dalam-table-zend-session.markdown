---
layout: post
title: Cara Mudah Menyimpan Session ke dalam Tabel Session Zend Session
github: https://gitlab.com/maulana20/zf3-table-session
image: https://gitlab.com/maulana20/zf3-table-session/-/raw/master/image/login.PNG
language: php | Zend Framework 3
---
Di beberapa framework mungkin kita mengenal php framework diantaranya laravel, symfony, dll, namun <b>zend framework</b> ini cukup unik dan banyak digunakan oleh kalangan <b><i>enterprise</i></b> karena merupakan <i>web framework</i> yang di rilis oleh tim pengembang <b>inti PHP</b>.

Zend Framework bersifat open source, struktur dan komponen sangatlah <b>fleksibel</b> dan <b>arsitektur</b> yang bisa <b>ditambah</b> sehingga memungkinkan pengembang untuk menggunakan komponen secara <b>individual</b> "Use-At-Will".

Dari awal release 2007 Zend Framework 1 hingga sekarang <b>Zend Framework 3</b> release perkembangan terus di lakukan dari penggunaan download folder library zend (path) hingga saat ini (Zend Framework 3) mengikuti perkembangan dengan composer (psr-4 autoloading) dan di kembangkan kembali <b>menjadi</b> <b>Laminas Project</b> (fondation community-supported) dan sudah <b>support</b> pada <b>PHP 7</b>.

Oke lanjut, pastikan kalian sudah menginstall di antaranya :
- php 7
- composer
- mysql phpmyadmin

Lalu ambil repo [link](https://gitlab.com/maulana20/zf3-table-session) tersebut.

Kemudian ambil require package library zend sesuai yang ada composer.json dengan perintah
```bash
composer install
```
package library kemudian akan di download. Jika sudah, import database ke mysql atau phpmyadmin dengan sql pada folder database/zend_session.sql .

Kemudah jalankan localhost server
```bash
php -S 0.0.0.0:4000 -t public public/index.php
```

Buka postman dan jalankan
![login](https://gitlab.com/maulana20/zf3-table-session/-/raw/master/image/login.PNG)
![user](https://gitlab.com/maulana20/zf3-table-session/-/raw/master/image/user.PNG)

jika tanpa login
![user](https://gitlab.com/maulana20/zf3-table-session/-/raw/master/image/nouser.PNG)

dari gambar diatas
