---
layout: post
title: Cara Mudah Menyimpan Data ke Redis
github: https://gitlab.com/maulana20/redis-demo
image: https://gitlab.com/maulana20/redis-demo/-/raw/master/image/redis-cli.PNG
language: php
---
Apa itu <b>redis</b> ? yaitu salah satu database dari dunia NoSQL yang berbasis key-value store di tempatkan di dalam memori. Redis lebih sekedar cache, karena bersifat sementara apabila di running ulang redis servernya data akan hilang kembali.

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

OK, untuk menjalankan redis kita jalankan redis-serve.exe
![redis](https://gitlab.com/maulana20/redis-demo/-/raw/master/image/redis.PNG)

Kemudian jalankan script php seperti berikut
```bash
php run.php
```

Maka akan tampil seperti berikut

![run](https://gitlab.com/maulana20/redis-demo/-/raw/master/image/run.PNG)

lihat pada run.php
```html
require_once 'vendor/autoload.php';

use Predis\Client;

$redis = new Client();

$redis->set('nama', 'maulana saputra'); // nb : set key => value
echo $redis->get('nama');
```
terdapat autoload.php yang merupakan penghubung library yang sudah kita download pada composer (PSR-4 Autoloading).

jika di jalankan melalui redis-cli.exe

![redis-cli](https://gitlab.com/maulana20/redis-demo/-/raw/master/image/redis-cli.PNG)
