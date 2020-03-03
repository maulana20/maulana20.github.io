---
layout: post
title: Cara Mudah Menyimpan Data ke Redis
github: https://gitlab.com/maulana20/redis-demo
image: https://gitlab.com/maulana20/redis-demo/-/raw/master/image/redis-cli.PNG
language: php
---
Apa itu <b>redis</b> ? yaitu salah satu database dari dunia NoSQL yang berbasis key-value store. Redis lebih sekedar cache, karena bersifat sementara apabila di running ulang redis servernya data akan hilang kembali.

Ambil repo pada [link](https://gitlab.com/maulana20/redis-demo) tersebut.

Kemudian ambil package yang dibutuhkan pada library
```bash
composer install
```

Package yang di butuhkan
```bash
"predis/predis": "^1.1"
```

Kemudian download redis for windows [link](https://github.com/dmajkic/redis/downloads). Disini yang kita butuhkan ada 2 yaitu :
- redis-server.exe
- redis-cli.exe


