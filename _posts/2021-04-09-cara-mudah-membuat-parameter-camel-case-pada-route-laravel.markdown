---
layout: post
title: Cara Mudah Membuat Parameter Camel Case Pada Route Laravel
github: https://laravel.com/docs/6.x/controllers#restful-naming-resource-routes
image: https://upload.wikimedia.org/wikipedia/commons/thumb/e/ef/CamelCase.svg/250px-CamelCase.svg.png
language: php
---

Pada `routes\web.php`
```bash
Route::resource('join-us', 'JoinUsController', ['as' => 'admin'])->parameters([
    'join-us' => 'joinUs'
])->except('show');
```

Pada Controller.
```bash
public function edit(JoinUs $joinUs)
{
    // return show
}
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://laravel.com/docs/6.x/controllers#restful-naming-resource-routes) tersebut.
