---
layout: post
title: Cara Mudah Membuat Verifikasi Email Register Pada Laravel
github: https://medium.com/@neoreids/register-dengan-verifikasi-email-menggunakan-laravel-part-1-c468d859856f
image: https://lh6.googleusercontent.com/K5tbjPh1Enl0C7Gk8-VEXYqu1uHiexakXp4AIc5JrWaDhBMLqQiazgLLcs0RSsmF6ywlM-Xz345xUHn0mdLVl7PQtPPkg8iE6IslmQwOpp82kwfF978MdJkQiOj7mt0m43NqCzj1
language: php | Laravel
---

Disini kita akan membuat verifikasi email setelah melakukan registrasi. Status pada user kita akan kategorikan menjadi 3 : Active, InActive, NotVerified.

### 1. Override pada Auth Controller
Pada saat register, kita akan mengirimkan token untuk verifikasi.
`app/Http/Controllers/Auth/RegisterController.php`.
```bash
    use Ramsey\Uuid\Uuid;
    use App\Models\Verification;
    use App\Mail\AccountVerification;
    use Illuminate\Auth\Events\Registered;
    
    public function register(Request $request)
    {
        $this->validator($request->all())->validate();

        event(new Registered($user = $this->create($request->all())));

        $verification = Verification::create([ 'user_id' => $user->id, 'token' => Uuid::uuid4()->toString() ]);

        \Mail::to($user->email)->send(new AccountVerification($user, $verification->token));

        return redirect()->back()->withSuccess('Akun berhasil dibuat, Mohon periksa email Anda <b>' . $request->email . '</b> untuk melakukan aktivasi.');
    }
    
    protected function create(array $data)
    {
        return User::create([
            'name' => $data['name'],
            'email' => $data['email'],
            'password' => Hash::make($data['password']),
            'status' => Status::NotVerified,
        ]);
    }
    
    public function verification(Request $request)
    {
        $verification = Verification::where('token', $request->token)->first();
        
        if ($verification) {
            $user = Applicant::find($verification->user_id);
            $user->status = Status::Active;
            $user->save();
            
            $verification->delete();
            
            return redirect()->route('login');
        }

        return redirect('/');
    }
```

note : pada `AccountVerification` merupakan email yang akan kita kirimkan dengan template yang sudah disiapkan.

Pada login kita tambahkan untuk pengecekan hanya bisa login dengan status aktif saja.

`app/Http/Controllers/Auth/LoginController.php`.
```bash
    protected function credentials(Request $request)
    {
        return array_merge($request->only($this->username(), 'password'), ['status' => Status:Active]);
    }
```

### 2. Membuat Tabel Verifikasi
Di sini kita akan membuat tabel verifikasi untuk menyimpan token.
```bash
    Schema::create('verifications', function (Blueprint $table) {
        $table->unsignedBigInteger('user_id')->index();
        $table->string('token');
        $table->timestamps();
    });
```

Pada Model Verifikasi tambahkan.
```bash
protected $primaryKey = 'user_id';
```

### 3. Tambahkan Verifikasi Pada Route
`routes/web.php`.
```bash
Route::get('register/verification', '\App\Http\Controllers\Auth\RegisterController@verification')->name('register.verification');
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://medium.com/@neoreids/register-dengan-verifikasi-email-menggunakan-laravel-part-1-c468d859856f) tersebut.
