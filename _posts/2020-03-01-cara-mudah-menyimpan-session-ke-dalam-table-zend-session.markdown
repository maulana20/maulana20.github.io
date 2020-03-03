---
layout: post
title: Cara Mudah Menyimpan Session ke dalam Tabel Session Zend Session
github: https://gitlab.com/maulana20/zf3-table-session
image: https://gitlab.com/maulana20/zf3-table-session/-/raw/master/image/login.PNG
language: php | Zend Framework 3
---
Di beberapa framework mungkin kita mengenal php framework diantaranya laravel, symfony, dll, namun <b>zend framework</b> ini cukup unik dan banyak digunakan oleh kalangan <b><i>enterprise</i></b> karena merupakan <i>web framework</i> yang di rilis oleh tim pengembang <b>inti PHP</b>.

Zend Framework bersifat open source, struktur dan komponen sangatlah <b>fleksibel</b> dan <b>arsitektur</b> yang bisa <b>ditambah</b> sehingga memungkinkan pengembang untuk menggunakan komponen secara <b>individual</b> "Use-At-Will".

Dari awal release 2007 Zend Framework 1 hingga sekarang <b>Zend Framework 3</b> release, perkembangan terus di lakukan dari download bundle library zend (path) hingga melalui composer (psr-4 autoload) sesuai kebutuhan. Zend Framework di kembangkan kembali dan menjadi <b>Laminas Project</b> (fondation community-supported).

Oke lanjut, pastikan kalian sudah menginstall di antaranya :
- php 7
- composer
- mysql phpmyadmin

Lalu ambil repo [link](https://gitlab.com/maulana20/zf3-table-session) tersebut.

Kemudian ambil package yang dibutuhkan pada library zend sesuai yang ada composer.json dengan perintah
```bash
composer install
```
package library tsb kemudian akan di download. Jika sudah, import database ke mysql atau phpmyadmin dengan sql pada folder database/zend_session.sql .

Kemudah jalankan PHP web server.
```bash
php -S 0.0.0.0:4000 -t public public/index.php
```

Route yang di gunakan adalah :
- domain/admin/login
- domain/admin/logout
- domain/user/list

Buka postman dan jalankan

![login](https://gitlab.com/maulana20/zf3-table-session/-/raw/master/image/login.PNG)
{: style="text-align: center;"}
Gambar I.
{: style="color:gray; font-size: 90%; text-align: center;"}

Buka halaman domain/user/list .

Isilah cookie dengan data TESTSESSION=18038305065e5cacce891115e5cacce89114 sesuai response pada login.

![user](https://gitlab.com/maulana20/zf3-table-session/-/raw/master/image/user.PNG)
{: style="text-align: center;"}
Gambar II.
{: style="color:gray; font-size: 90%; text-align: center;"}

Jika tanpa login akan muncul seperti berikut.

![user](https://gitlab.com/maulana20/zf3-table-session/-/raw/master/image/nouser.PNG)
{: style="text-align: center;"}
Gambar III.
{: style="color:gray; font-size: 90%; text-align: center;"}

Dari gambar diatas ada 3 proses yang di jalankan :
- <b>Authentication</b>
- <b>Authorization</b>
- <b>Session</b>

### 1. Authentication
Pada saat login kita memasukan user dan password dengan admin, dimana dengan mengecek user admin pada database.

Library yang di butuhkan.
```bash
"zendframework/zend-db": "^2.10"
```

Ok, kita lewati tutorial dari [https://docs.zendframework.com](https://docs.zendframework.com) , disini mengkoneksikan database terdapat konfigurasi dengan penggabungan <b>Zend TableGateway</b> dan <b>Zend Adapter</b>.

Lihat pada module/application/model/Table_Gateway_Adapter.php .
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
Apa itu <b>TableGateway</b> ? yaitu object yang bertindak untuk action di dalam tabel.

Untuk cek login kita gunakan pada model user apakah user dan passwordnya sudah sesuai.
```bash
$user->isUserPassword($post['user'], $post['password']);
```
Di sini tabel user terhubung dengan tabel group dengan beberapa access role, penjelasan lebih lanjut ada pada step berikutnya.

### 2. Authorization
Setelah login access role akan di setting sesuai group pada user tersebut. Role tersebut kita gunakan <b>Zend Acl</b>.

Library yang di butuhkan.
```bash
"zendframework/zend-permissions-acl": "^2.7"
```
Apa itu <b>Zend Acl</b> ? yaitu penentuan menu apa saja yang bisa di jalankan pada user tersebut.

```html
use Zend\Permissions\Acl\Acl;

// module/administration/controller/AdminController.php action login

$access = $group->getAccess($group_id); // access pada group
$access = unserialize($access);
$this->setRole($access);

// module/application/controller/ParentController.php action setRole

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
Seluruh acl sudah di bentuk, contoh role access menu :
```html
// module/administration/controller/UserController.php action list
$this->checkRole('ADMINISTRATION');
$this->checkRole('USER');
```
Jika tidak ada akses, maka proses tidak akan dilanjutkan. Lihat pada module/application/controller/ParentController.php action checkRole.

Untuk acl di simpan ke dalam session, penjelasan lebih lanjut ada pada step berikutnya.
### 3. Session
Session disini menggunakan <b>Zend Session</b>. Apa itu Zend Session ? yaitu seluruh aktivitas yang berhubungan dengan interaksi user pada sebuah web yang tersimpan di browser.

Library yang di butuhkan.
```bash
"zendframework/zend-session": "^2.8"
```
Setelah login, seluruh aktivitas untuk kebutuhan web di simpan ke dalam session pada browser untuk di panggil kembali.
```html
// module/application/controller/ParentController.php
use Zend\Session\Container;

public $session = NULL;

// method setUp
$this->session = new Container('namespace');

// module/administration/controller/AdminController.php action login
$this->session->user_id = $user_id;
$this->session->user_name = $row['user_name'];
$this->session->group_id = $group_id;
```
ParentController disini sebagai handling untuk tiap controller dari action, menu, access, dan session.
```html
// module/application/controller/ParentController.php method onDispatch
$controller = $event->getTarget();
$controllerClass = get_class($controller);
$moduleNamespace = substr($controllerClass, 0, strpos($controllerClass, '\\'));

if ($moduleNamespace == __NAMESPACE__) {
	$viewModel = $event->getViewModel();
	$viewModel->setTemplate('layout/layout');
}
$this->setUp();
AbstractActionController::onDispatch($event);
```
Jika controller atau actionnya tidak sesuai maka akan di lempar ke layout.

### SIMPAN TABEL SESSION
```bash
// module/application/controller/ParentController.php method __saveSession
Session::save($this->session);
```
Ok, proses akhir di atas dari aktivitas pada session kita akan simpan ke dalam tabel session.

```bash
TESTSESSION=18038305065e5cacce891115e5cacce89114
```
Cookie tersebut sebagai kunci access untuk melakukan aktivitas pada web.

```bash
// module/application/controller/ParentController.php method __initSession
$session_data = null;
$session_data = Session::get($_COOKIE["TESTSESSION"]);

$this->session = $session_data;
```
Jika sesuai, maka aktivitas session sebelumnya di kembalikan sesuai aktivitas akhir yang di lakukan.

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://gitlab.com/maulana20/zf3-table-session) tersebut.
