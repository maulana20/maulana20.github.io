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

Buka pada browser dan buat folder log. Pilih menu scrapper dan pilih jadwal penerbangan kemudian cari.

![scrapper](https://gitlab.com/maulana20/zf3-scrapping/-/raw/master/screen/scrapper.PNG){: .center-image }
Gambar I.
{: style="color:gray; font-size: 90%; text-align: center;"}


Maka akan muncul jadwal penerbangan dengan jadwal yang kita inginkan. Kemudian lihat pada folder log, maka akan tampil screen page html. Page tersebut merupakan hasil dari scraping yang akan kita ambil datanya.

Lihat pada model Citilink.php, terdapat 2 class diantaranya :
- Scrapper
- Citilink

### Scrapper
Model disini sebagai pembentuk client pada <b>Zend_Http_Client</b>. Model di buat abstract class untuk berperan sebagai kerangka dasar untuk turunan kelas lainnya.
```html
abstract class Scrapper
{
	protected $url;
	protected $client;
	
	protected function createClient()
	{
		$this->client = new Client($this->url);
		
		$this->client->setOptions([ // set option ]);
		$this->client->setHeaders([ "Connection" => "keep-alive" ]);
	}
}
```

### Citilink
Kelas turunan dari model Scrapper, disini model tersebut sebagai maskapai yang akan kita scraping. Perlu kita ketahui, client berkomunikasi melalui HTTP yang merupakan protokol yang berbicara menggunakan request dan response menjadikan aplikasi web bergantung kepada siklus ini untuk menghasilkan dokumen yang ingin diakses oleh pengguna.

![inspect](https://gitlab.com/maulana20/zf3-scrapping/-/raw/master/screen/inspect.png){: .center-image }
Gambar II.
{: style="color:gray; font-size: 90%; text-align: center;"}

Gambar di atas merupakan halaman yang berjalan pada HTTP browser. Ambil request saat buka halaman awal hingga pencarian jadwal.
```html
// pada method loginClient yaitu mengambil halaman awal
$client->setUri($host);
$client->setHeaders(["Connection" => "keep-alive"]);

$response = $client->send();
$result = $response->getBody();
$this->logResponse('log/CitilinkIndex.html', $result);

// pada method search yaitu mengambil halaman pencarian jadwal
$data = [];
$data['Page'] = 'Select'; // $data sesuai HTTP request

$client->setUri($host . '/Search.aspx');
$client->setMethod('GET');
$client->setParameterGet($data);

$response = $client->send();
$result = $response->getBody();

$this->logResponse('log/CitilinkSearch.html', $result);
```
Simpan screen page tersebut ke dalam log, kemudian ambil data yang di butuhkan pada result body dan olah data (saya menyebutnya mapping). Olah data tersebut akan di kirim ke front-end untuk di tampilkan hingga seperti pada Gambar I.

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://gitlab.com/maulana20/zf3-scrapping) tersebut.
