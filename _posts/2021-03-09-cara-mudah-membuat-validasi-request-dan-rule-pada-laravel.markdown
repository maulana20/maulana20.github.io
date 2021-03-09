---
layout: post
title: Cara Mudah membuat Validasi Request dan Rule Pada Laravel
github: https://medium.com/@kamerk22/the-smart-way-to-handle-request-validation-in-laravel-5e8886279271
image: https://www.itsolutionstuff.com/upload/laravel-contact-us-form.png
language: php | Laravel
---

### 1. Membuat Request
Di sini akan membuat request dengan perintah.
```bash
php artisan make:request StoreRequest
```

Kemudian ubah pada `app\Http\Requests\StoreRequest.php` seperti di bawah ini.
```bash
<?php

namespace App\Http\Requests;

use Illuminate\Foundation\Http\FormRequest;
use App\Rules\DepartementManagerRule;

class StoreRequest extends FormRequest
{
    /**
     * Determine if the user is authorized to make this request.
     *
     * @return bool
     */
    public function authorize()
    {
        return true;
    }

    /**
     * Get the validation rules that apply to the request.
     *
     * @return array
     */
    public function rules()
    {
        return [
            'title' => 'required|min:5|max:200',
            'body' => 'required',
            'department_manager' => [
                'required',
                new DepartementManagerRule,
             ]
        ];
    }
    
    public function getStore()
    {
        return [
            'title' => $this->title,
            'body' => $this->body,
            'department_manager' => $this->department_manager,
        ];
    }
}
```

### 2. Membuat Rule
Di sini kita akan membuat rule dengan perintah.
```bash
php artisan make:rule DepartementManagerRule
```

Kemudian ubah pada `app\Rules\DepartementManagerRule` seperti di bawah ini.
```bash
<?php

namespace App\Rules;

use Illuminate\Contracts\Validation\Rule;

class DepartementManagerRule implements Rule
{
    /**
     * Create a new rule instance.
     *
     * @return void
     */
    public function __construct()
    {
        //
    }

    /**
     * Determine if the validation rule passes.
     *
     * @param  string  $attribute
     * @param  mixed  $value
     * @return bool
     */
    public function passes($attribute, $value)
    {
        return (empty($value) || empty(\Auth::user()->id) || $value == \Auth::user()->id ? false : true);
    }

    /**
     * Get the validation error message.
     *
     * @return string
     */
    public function message()
    {
        return 'The department Manager must be someone else.';
    }
}
```

### 3. Tambahkan Request pada Controller
Di sini kita akan tambahkan validasi yang kita buat pada controller.
```bash
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Http\Controllers\Controller;
use App\Http\Requests\StoreRequest;
use App\Models\News;

class NewsController extends Controller
{
    public function store(StoreRequest $request)
    {
        News::create($request->getStore());
        
        return redirect()->route('admin.news.index')->with('success', 'News successfully created');
    }
```

### Catatan
- Jika kalian ingin custom message error bisa di tambahkan fungsi `messages()` atau penambahan fungsi lain sesuai kebutuhan kalian pada `StoreRequest.php`.

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://medium.com/@kamerk22/the-smart-way-to-handle-request-validation-in-laravel-5e8886279271) tersebut.
