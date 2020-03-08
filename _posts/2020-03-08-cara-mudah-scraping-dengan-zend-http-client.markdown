---
layout: post
title: Cara Mudah Scraping dengan Zend Http Client
github: https://gitlab.com/maulana20/zf3-scrapping
image: https://gitlab.com/maulana20/zf3-scrapping/-/raw/master/screen/scrapper.PNG
language: php | Zend Framework 3
---
Apa itu <b>Scraping</b> ? yaitu pengambilan sebuah dokumen berupa halaman web dengan tujuan untuk menganalisis dokumen untuk di ambil data tertentu.

Kita lanjut untuk mencoba scraping. Sekarang ambil ambil [repo](https://gitlab.com/maulana20/zf3-scrapping) tersebut. Kemudian ambil library yang di butuhkan dengan composer.
```bash
composer install
```
Library yang di butuhkan.
```bash
"zendframework/zend-http": "^2.11"
```
Kemudian jalankan PHP web server.
```bash
php -S 0.0.0.0:4000 -t public public/index.php
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://gitlab.com/maulana20/zf3-scrapping) tersebut.
