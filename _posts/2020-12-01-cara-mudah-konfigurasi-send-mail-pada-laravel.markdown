---
layout: post
title: Cara Mudah Konfigurasi Send Mail Pada Laravel
github: https://www.itsolutionstuff.com/post/how-to-send-mail-in-laravel-6example.html
image: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR8C4p-E16GVw0lX4dbfpKbVB5xUTuiYI1wNw&usqp=CAU
language: php | Laravel
---

### 1. Membuat Konfigurasi
Di sini untuk pertama buat konfigurasi mail yang sudah di sediakan pada .env . Contoh pada mailtrap
```html
MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=user
MAIL_PASSWORD=xxx
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=from@example.com
MAIL_FROM_NAME="${APP_NAME}"
```

### 2. Membuat Mail Class
Pada langkah ini buat mail class untuk mengirim email.
```bash
php artisan make:mail ContactUsMail
```

Kemudian pada app\Mail\ContactUsMail.php ubah seperti ini.
```bash
<?php

namespace App\Mail;

use Illuminate\Bus\Queueable;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Mail\Mailable;
use Illuminate\Queue\SerializesModels;

class ContactUsMail extends Mailable
{
    use Queueable, SerializesModels;
    
    public $details;

    /**
     * Create a new message instance.
     *
     * @return void
     */
    public function __construct($details)
    {
        $this->details = $details;
    }

    /**
     * Build the message.
     *
     * @return $this
     */
    public function build()
    {
        return $this->subject('Masukan Subject')->view('mail.contact-us-mail');
    }
}
```

### 3. Membuat Blade View
Pada langkah ini untuk menulis email yang akan kita kirimkan.

Kemudian pada resources\views\mail\contact-us-mail.blade.php
```bash
<!DOCTYPE html>
<html>
<head>
    <title>{{ $details['title'] }}</title>
</head>
<body>
    <h1>{{ $details['title'] }}</h1>
    <p>{{ $details['body'] }}</p>
    
    <p>Thank you</p>
</body>
</html>
```

### 4. Membuat Send Mail Controller
Pada langkah ini kita akan membuat perintah untuk mengirim email pada controller.
```bash
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class LandingController extends Controller
{
    public function sendContactUs(Request $request)
    {
        if ($request->isMethod('post')) {
            $this->validate(
                $request,
                [
                    'title' => 'required',
                    'body' => 'required',
                ]
            );
            
            $details = [
                'title' => $request->title,
                'body' => $request->body,
            ];
            
            $mail = \Mail::to('your_receiver_email@gmail.com')->send(new \App\Mail\ContactUsMail($details));
            
            return response('Email is Sent.', 200)->header('Content-Type', 'text/plain');
        }
    }
}
```

### Catatan
Jika smpt kalian menggunakan selain mailtrap bisa ubah konfigurasi seperti ini.

DEVELMAIL
```html
MAIL_HOST=smtp.develmail.com
MAIL_PORT=587
```

SENDGRID
```html
MAIL_HOST=smtp.sendgrid.net
MAIL_PORT=587
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://www.itsolutionstuff.com/post/how-to-send-mail-in-laravel-6example.html) tersebut.
