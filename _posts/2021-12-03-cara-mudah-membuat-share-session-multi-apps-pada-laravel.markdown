---
layout: post
title: Cara Mudah Membuat Share Session Multi Apps Pada Laravel
github: https://medium.com/@zsolt.gyure96/how-to-share-sessions-between-two-laravel-applications-4b9d061fa599
image: https://miro.medium.com/max/1400/1*YPeMdgpj9SCeKXmUh338wg.png
language: php | laravel
---

Memungkinkan untuk melakukan share session, cookie pada multi aplikasi pada subdomain yang sama.

### 1. Pada Aplikasi Pertama

#### Buat Table Session
- `$ php artisan session:table`
- `$ php artisan migrate`

#### Ubah Environtment
- `SESSION_DRIVER=database`
- `SESSION_DOMAIN=".example.com"`

### 2. Pada Aplikasi Kedua

#### Buat Connection Baru pada config/database.php
```bash
    'common_database' => [
        'driver' => 'mysql',
        'url' => env('DATABASE_URL'),
        'host' => env('DB_HOST', '127.0.0.1'),
        'port' => env('DB_PORT', '3306'),
        'database' => env('COMMON_DB_DATABASE', 'forge'),
        'username' => env('DB_USERNAME', 'forge'),
        'password' => env('DB_PASSWORD', ''),
        'unix_socket' => env('DB_SOCKET', ''),
        'charset' => 'utf8mb4',
        'collation' => 'utf8mb4_unicode_ci',
        'prefix' => '',
        'prefix_indexes' => true,
        'strict' => true,
        'engine' => null,
        'options' => extension_loaded('pdo_mysql') ? array_filter([
            PDO::MYSQL_ATTR_SSL_CA => env('MYSQL_ATTR_SSL_CA'),
        ]) : [],
    ],
```

#### Ubah Pada Models\User.php
`protected $connection = 'common_database';`

#### Ubah Environtment
- `APP_KEY="copy pada APP_KEY applikasi pertama"`
- `SESSION_DRIVER=database`
- `SESSION_CONNECTION=common_database`
- `SESSION_DOMAIN=".example.com"`

#### Ubah Middleware\Authenticate.php
```bash
    use Session;
    
    class Authenticate extends Middleware
    {
        
        ****
        
        protected function redirectTo($request)
        {
            Session::setId("cookie name dari applikasi pertama");
            
            Session::start();
            
            ****
        }
    }
```

### Note

- Share Session ini hnya berlaku untuk subdomain to subdomain.
- Pada `Session::setId` sesuaikan dengan nama cookie aplikasi pertama, biasanya menggunakan nama dari `Str::slug(env('APP_NAME', 'laravel'), '_').'_session'`

### Reference

- [sumber 1](https://medium.com/@zsolt.gyure96/how-to-share-sessions-between-two-laravel-applications-4b9d061fa599)
- [sumber 2](https://stackoverflow.com/questions/26821648/laravel-share-session-data-over-multiple-domains)

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://medium.com/@zsolt.gyure96/how-to-share-sessions-between-two-laravel-applications-4b9d061fa599) tersebut.
