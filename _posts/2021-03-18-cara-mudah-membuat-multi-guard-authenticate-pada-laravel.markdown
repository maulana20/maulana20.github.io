---
layout: post
title: Cara Mudah Membuat Multi Guard Authenticate Pada Laravel
github: https://pusher.com/tutorials/multiple-authentication-guards-laravel
image: https://miro.medium.com/max/640/1*32ssDgqEHx3JJM28nf1-0w.png
language: php | Laravel
---

Disini kita akan membuat multi auth dengan sebagai admin dan applicant. Terlebih dahulu untuk admin kita sudah buat sebelumnya pada [link](https://www.itsolutionstuff.com/post/laravel-58-user-roles-and-permissions-tutorialexample.html) tersebut, lalu kita buat tabel applicant serupa dengan tabel user.

### 1. Membuat Guard 
Di sini akan membuat guard pada `config/auth.php`.
```bash
'guards' => [
    [],
    
    'admin' => [
        'driver' => 'session',
        'provider' => 'users',
    ],
    
    'applicant' => [
        'driver' => 'session',
        'provider' => 'applicants',
    ],
],

'providers' => [
    [],
    
    'applicants' => [
        'driver' => 'eloquent',
        'model' => App\Models\Applicant::class,
    ],
],
```

Tambahkan guard name tiap model yang kita gunakan.

`app\Models\User.php`.
```bash
    protected $guard = 'admin';
```

`app\Models\Applicant.php`.
```bash
    protected $guard = 'applicant';
```

### 2. Membuat Auth LoginController
Di sini kita akan membuat Auth LoginController yang berbeda.

`app/Http/Controllers/Admin/Auth/LoginController.php`.
```bash
    protected $redirectTo = '/admin/index';
    
    public function __construct()
    {
        $this->middleware('guest:admin')->except('logout');
    }
    
    public function showLoginForm()
    {
        return view('admin.login');
    }
    
    public function logout(Request $request)
    {
        \Auth::guard('admin')->logout();
        
        return redirect()->route('admin.login');
    }
    
    /**
     * Get the guard to be used during authentication.
     *
     * @return \Illuminate\Contracts\Auth\StatefulGuard
     */
    protected function guard()
    {
        return \Auth::guard('admin');
    }
```

`app/Http/Controllers/Auth/LoginController.php`.
```bash
    protected $redirectTo = '/applicant';
    
    public function showLoginForm()
    {
        return view('applicant.login');
    }
    
    public function logout(Request $request)
    {
        \Auth::guard('applicant')->logout();
        
        return redirect()->route('home');
    }
    
    /**
     * Get the guard to be used during authentication.
     *
     * @return \Illuminate\Contracts\Auth\StatefulGuard
     */
    protected function guard()
    {
        return \Auth::guard('applicant');
    }
```

### 2. Modifikasi Pada Kondisi Authenticate
`app/Http/Controllers/Middleware/RedirectIfAuthenticated.php`.
```bash
    public function handle($request, Closure $next, $guard = null)
    {
        switch ($guard) {
            case 'admin':
                if (Auth::guard($guard)->check()) {
                    return redirect()->route('admin.index');
                }
                break;
            default:
                if (Auth::guard($guard)->check()) {
                    return redirect()->route('applicant.index');
                }
                break;
        }

        return $next($request);
    }
```

`App\Exceptions\Handler.php`.
```bash
    public function render($request, Exception $exception)
    {
        return parent::render($request, $exception);
        
        if ($request->expectsJson()) {
            return response()->json(['message' => $exception->getMessage()], 401);
        }
        
        $guard = array_get($exception->guards(), 0);
        
        switch ($guard) {
            case 'admin' :
                $login = 'admin.login';
                break;
            default:
                $login = 'login';
                break;
        }
        
        return redirect()->route($login);
    }
```

`app/Http/Middleware/Authenticate.php`.
```bash
    protected function redirectTo($request)
    {
        if (! $request->expectsJson()) {
            return route('login');
        }
    }
```

### 3. Sesuaikan Multi Auth Pada Route
`routes/web.php`.
```bash
Route::group(['middleware' => 'auth:admin'], function () {
    // Route Admin
});

Route::prefix('admin')->group(function () {
    // Auth login, logout pada Admin/Auth/LoginController
});

Auth::routes();

Route::group(['middleware' => 'auth:applicant'], function () {
    // Route Applicant
});
```

### Catatan
- Jika kalian ingin check login pada view tiap guard bisa gunakan `Auth::guard('applicant')->check()` contoh detail `Auth::guard('applicant')->user()->full_name`.

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://pusher.com/tutorials/multiple-authentication-guards-laravel) tersebut.
