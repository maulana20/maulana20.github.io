---
layout: post
title: Cara Mudah Membuat Forgot Password Email Pada Laravel
github: https://laravel.com/docs/6.x/passwords
image: https://www.malasngoding.com/wp-content/uploads/2019/01/reset-password-user-dengan-laravel-1024x384.jpg
language: php | Laravel
---

Perlu di perhatikan pada saat lihat route list sudah di sediakan route untuk reset password.

`$ php artisan route:list`
```bash
|        | POST      | password/email         | password.email    | App\Http\Controllers\Auth\ForgotPasswordController@sendResetLinkEmail  | web,guest  |
|        | POST      | password/reset         | password.update   | App\Http\Controllers\Auth\ResetPasswordController@reset                | web,guest  |
|        | GET|HEAD  | password/reset         | password.request  | App\Http\Controllers\Auth\ForgotPasswordController@showLinkRequestForm | web,guest  |
|        | GET|HEAD  | password/reset/{token} | password.reset    | App\Http\Controllers\Auth\ResetPasswordController@showResetForm        | web,guest  |
```

### 1. Override pada Auth Controller
Membuat form email user ketika submit akan mengirimkan link form reset password ke dalam email.
`App\Http\Controllers\Auth\ForgotPasswordController.php`.
```bash
<?php

namespace App\Http\Controllers\Auth;

use App\Http\Controllers\Controller;
use Illuminate\Foundation\Auth\SendsPasswordResetEmails;
use Illuminate\Support\Facades\Password;
use Illuminate\Http\Request;

class ForgotPasswordController extends Controller
{
    /*
    |--------------------------------------------------------------------------
    | Password Reset Controller
    |--------------------------------------------------------------------------
    |
    | This controller is responsible for handling password reset emails and
    | includes a trait which assists in sending these notifications from
    | your application to your users. Feel free to explore this trait.
    |
    */

    use SendsPasswordResetEmails;
    
    public function __construct()
    {
        $this->middleware('guest');
    }
    
    public function broker()
    {
        return Password::broker('users');
    }
    
    public function showLinkRequestForm()
    {
         return view('auth.password-email');
    }
    
    protected function sendResetLinkResponse(Request $request, $response)
    {
        return redirect()->back()->withSuccess(trans($response));
    }
}
```

note : pada `App\Http\Controllers\Auth\ForgotPasswordController@showLinkRequestForm` merupakan form input email pada view.

Membuat form reset password untuk mengubah password.
`App\Http\Controllers\Auth\ForgotPasswordController.php`.
```bash
<?php

namespace App\Http\Controllers\Auth;

use App\Http\Controllers\Controller;
use App\Providers\RouteServiceProvider;
use Illuminate\Foundation\Auth\ResetsPasswords;
use Illuminate\Support\Facades\Password;
use Illuminate\Support\Facades\Auth;
use Illuminate\Support\Facades\Hash;
use Illuminate\Support\Str;
use \Illuminate\Http\Request;
use Illuminate\Auth\Events\PasswordReset;

class ResetPasswordController extends Controller
{
    /*
    |--------------------------------------------------------------------------
    | Password Reset Controller
    |--------------------------------------------------------------------------
    |
    | This controller is responsible for handling password reset requests
    | and uses a simple trait to include this behavior. You're free to
    | explore this trait and override any methods you wish to tweak.
    |
    */

    use ResetsPasswords;

    /**
     * Where to redirect users after resetting their password.
     *
     * @var string
     */
    protected $redirectTo = RouteServiceProvider::HOME;
    
    public function __construct()
    {
        $this->middleware('guest');
    }
    
    public function broker()
    {
        return Password::broker('users');
    }
    
    public function showResetForm(Request $request, $token = null)
    {
        return view('auth.password-reset')->with(
            ['token' => $token, 'email' => $request->email]
        );
    }
    
    protected function resetPassword($user, $password)
    {
        $user->password = Hash::make($password);

        $user->setRememberToken(Str::random(60));

        $user->save();

        event(new PasswordReset($user));
    }
    
    protected function sendResetResponse(Request $request, $response)
    {
        return redirect()->back()->withSuccess('Password berhasil diganti, silahkan login.');
    }
}
```

note : pada `App\Http\Controllers\Auth\ResetPasswordController@showResetForm` merupakan form reset password dengan token pada view.

### 2. Override sendPasswordResetNotification pada User Model
Di sini kita akan menambahkan notifikasi email pada `app/Models/User.php`.
```bash
use App\Notifications\ResetPasswordNotification;
    
    public function sendPasswordResetNotification($token)
    {
        $this->notify(new ResetPasswordNotification($token));
    }
```

pada `app\Notifications\ResetPasswordNotification.php`.
```bash
    public function toMail($notifiable)
    {
        if (static::$toMailCallback) {
            return call_user_func(static::$toMailCallback, $notifiable, $this->token);
        }

        return (new MailMessage)
            ->subject('Reset Password Request')
            ->line('Hi [User], there is a request to reset your password')
            ->line(new HtmlString('If it’s you, please click this <a href="' . url(route('password.reset', ['token' => $this->token, 'email' => $notifiable->getEmailForPasswordReset()], false)) . '" target="_blank">link</a> to create a new password.'))
            ->line('If it’s not you, please regularly update your password on our website.')
            ->line('Thank you,');
    }
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://laravel.com/docs/6.x/passwords) tersebut.
