---
layout: post
title: Cara Mudah Membuat Google Auth Pada Laravel
github: https://jaranguda.com/tutorial-google-authentication-dengan-laravel-6/
image: https://miro.medium.com/max/700/1*4AxSgy4VjvKv9EvJ14VNAQ.png
language: php | laravel
---

Pada kali ini kita akan daftarkan dahulu domain kita untuk bisa akses pada [google](https://console.developers.google.com) untuk mendapatkan credential `client_id` dan `client_secret`.

### 1. Menambahkan Depedency
Di sini kita perlu menginstall depedency pada composer.
```bash
composer require laravel/socialite
```

### 2. Membuat Script pada Controller
```bash
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;
use App\Models\Applicant;
use Socialite;

class GoogleController extends Controller
{
    public function redirect()
    {
        return Socialite::driver('google')->redirect();
    }
    
    public function callback()
    {
        if (Auth::guard('applicant')->check()) {
            return redirect('/home');
        }
        
        $oauthUser = Socialite::driver('google')->user();
        
        $applicant = Applicant::where('google_id', $oauthUser->id)->first();
        
        if ($applicant) {
            Auth::guard('applicant')->loginUsingId($applicant->id);
            
            return redirect('/home');
        } else {
            $applicant = Applicant::where('email', $oauthUser->email)->first();
            $applicant->update([ 'google_id' => $oauthUser->id ]);
            
            Auth::guard('applicant')->login($applicant);
            
            return redirect('/home');
        }
    }
}
```

### 3. Menambahkan Column Google ID
jalankan
```bash
php artisan make:migration add_column_google_id_in_applicants_table
```

`database/migrations/2021_05_07_135025_add_column_google_id_in_applicants_table.php`
```bash
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class AddColumnGoogleIdInApplicantsTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::table('applicants', function (Blueprint $table) {
            $table->string('google_id')->nullable();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::table('applicants', function (Blueprint $table) {
            $table->dropColumn('google_id');
        });
    }
}
```

`app/Models/Applicant.php`
```bash
protected $fillable = [
    'name', 'email', 'password', 'google_id'
];
```

kemudian jalankan
```bash
php artisan migrate
```

### 4. Menambahkan Service Google
`config/services.php`
```bash
'google' => [
    'client_id' => '#CLIENTID',
    'client_secret' => '#CLIENTSECRET',
    'redirect' => 'http://127.0.0.1/google/callback',
],
```

### 5. Menambahkan Pada Route
```bash
Route::get('google', 'GoogleController@redirect')->name('google.redirect');
Route::get('google/callback', 'GoogleController@callback')->name('google.callback');
```

### 6. Menampilkan Pada View
```bash
<div class="form-group m-0">
    <input type="submit" class="btn btn-block btn-primary-dws" onclick="window.open('{{ route('google.redirect') }}')" value="Login with Google">
</div>
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://jaranguda.com/tutorial-google-authentication-dengan-laravel-6/) tersebut.
