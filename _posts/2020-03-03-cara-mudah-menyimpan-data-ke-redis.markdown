---
layout: post
title: Cara Mudah Menyimpan Data ke Redis
github: https://gitlab.com/maulana20/redis-demo
image: https://gitlab.com/maulana20/redis-demo/-/raw/master/image/redis-cli.PNG
language: php
---
Apa itu <b>redis</b> ? yaitu salah satu database dari dunia NoSQL yang berbasis key-value store di tempatkan di dalam memori. Redis memiliki sejumlah query yang pastinya mudah untuk digunakan untuk menyimpan mulai data sederhana hingga data kompleks.

Kita lanjut untuk mencoba redis. Sekarang ambil repo pada [link](https://gitlab.com/maulana20/redis-demo) tersebut. Kemudian ambil library yang di butuhkan dengan composer.
```bash
composer install
```

Library yang di butuhkan.
```bash
"predis/predis": "^1.1"
```

Kemudian download redis exe for windows [link](https://github.com/dmajkic/redis/downloads). Disini yang kita butuhkan ada 2 yaitu :
- <b>redis-server.exe</b>
- <b>redis-cli.exe</b>

OK, sekarang kita harus menjalankan redis server terlebih dahulu pada redis-serve.exe .
![redis](https://gitlab.com/maulana20/redis-demo/-/raw/master/image/redis.PNG){: .center-image }

Gambar I.
{: style="color:gray; font-size: 90%; text-align: center;"}

Kemudian jalankan script php seperti berikut.

![run](https://gitlab.com/maulana20/redis-demo/-/raw/master/image/run.PNG)
{: style="text-align: center;"}
Gambar II.
{: style="color:gray; font-size: 90%; text-align: center;"}

Lihat pada run.php .
```html
require_once 'vendor/autoload.php';

use Predis\Client;

$redis = new Client();

$redis->set('nama', 'maulana saputra'); // nb : set key => value
echo $redis->get('nama');
```
Terdapat file <b>autoload.php</b> yang merupakan (PSR-4 Autoloading) pada composer sebagai <b>penghubung</b> <b>library</b> yang ada pada folder vendor. Data dengan key dan value telah dikirimkan ke redis server (lihat pada Gambar I) dan lihat pada redis akan muncul keterangan Accepted 127.0.0.1:55529 .

Jika di jalankan melalui redis-cli.exe .

![redis-cli](https://gitlab.com/maulana20/redis-demo/-/raw/master/image/redis-cli.PNG)
{: style="text-align: center;"}
Gambar III.
{: style="color:gray; font-size: 90%; text-align: center;"}

Bisa kita cek <b>query</b> <b>redis</b> pada <b>command</b> dengan perintah di atas. Data tersebut bersifat sementara apabila redis-server di jalankan ulang, maka data di kembalikan ke semula.

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://gitlab.com/maulana20/redis-demo) tersebut.
