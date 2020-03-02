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

Kemudah jalankan PHP web server
```bash
php -S 0.0.0.0:4000 -t public public/index.php
```

Route yang di gunakan adalah :
- http://localhost:4000/admin/login
- http://localhost:4000/admin/logout
- http://localhost:4000/user/list

Buka postman dan jalankan
![login](https://gitlab.com/maulana20/zf3-table-session/-/raw/master/image/login.PNG)

Buka halaman http://localhost:4000/user/list

isi cookie TESTSESSION=18038305065e5cacce891115e5cacce89114 sesuai response login
![user](https://gitlab.com/maulana20/zf3-table-session/-/raw/master/image/user.PNG)

jika tanpa login
![user](https://gitlab.com/maulana20/zf3-table-session/-/raw/master/image/nouser.PNG)

dari gambar diatas ada 3 proses yang di jalankan :
- authentication
- authorization
- session

### 1. Authentication
Pada saat login kita memasukan user dan password dengan admin, dimana dengan mengecek user admin pada database.

library require yang di gunakan pada composer.json
```bash
"zendframework/zend-db": "^2.10"
```

Ok, kita lewati tutorial dari [https://docs.zendframework.com](https://docs.zendframework.com) , disini mengkoneksikan database terdapat konfigurasi dengan penggabungan <b>Zend TableGateway</b> dan <b>Zend Adapter</b>.

lihat pada Table_Gateway_Adapter.php
```html
use Zend\Db\TableGateway\TableGateway;
use Zend\Db\Adapter\Adapter;

$adapter = new Adapter([
	'hostname'	=> 'localhost',
	'driver'	=> 'mysqli',
	'database'	=> 'zend_session',
	'username'	=> 'root',
	'password'	=> 'gakpakai',
]);

new TableGateway($table, $adapter);
```
apa itu <b>TableGateway</b> ? yaitu object yang bertindak untuk action di dalam tabel.

untuk cek login kita gunakan pada model user apakah user dan passwordnya sudah sesuai 
```bash
$user->isUserPassword($post['user'], $post['password']);
```
di sini tabel user terhubung dengan tabel group dengan beberapa access role, penjelasan lebih lanjut ada pada step berikutnya.

### 2. Authorization
Setelah login access role akan di setting sesuai group pada user tersebut. Setting role tersebut kita gunakan <b>Zend Acl</b>.

library require yang di gunakan pada composer.json
```bash
"zendframework/zend-permissions-acl": "^2.7"
```
apa itu <b>Zend Acl</b> ? yaitu penentuan menu apa saja yang bisa di jalankan pada user tersebut.

```html
use Zend\Permissions\Acl\Acl;

AdminController.php method login

$access = $group->getAccess($group_id); // access pada group
$access = unserialize($access);
$this->setRole($access);

ParentController.php method setRole

$group = new Group();
$acl = new Acl();
$access_all = $group->getAccessAll(); // access pada profile (seluruh access)

foreach ($access_all as $a) {
	$acl->addRole(new Role($a));
}
foreach ($allow as $a) {
	$acl->allow($a);
}

$this->session->acl = serialize($acl);
```
seluruh acl akan di simpan ke dalam session, penjelasan lebih lanjut ada pada step berikutnya.
### 2. Session
test
