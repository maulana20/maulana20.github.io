---
layout: post
title: Cara Mudah Export Excel Pada Laravel
github: https://docs.laravel-excel.com/3.1/exports/from-view.html
image: data:image/jpeg;base64,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
language: php | Laravel
---

### 1. Instalasi
Di sini perlu untuk menginstall beberapa kebutuhan package dan beberapa yang berhubungan dengan <i>PhpSpreadsheet</i>.
```html
composer require maatwebsite/excel
```

Registrasi pada ServiceProvider config/app.php .
```bash
'providers' => [
    /*
     * Package Service Providers...
     */
    Maatwebsite\Excel\ExcelServiceProvider::class,
]
```

Dan juga pada bagian bawah.
```bash
'aliases' => [
    ...
    'Excel' => Maatwebsite\Excel\Facades\Excel::class,
]
```

Publish pada config dengan menjalankan perintah ini.
```bash
php artisan vendor:publish --provider="Maatwebsite\Excel\ExcelServiceProvider" --tag=config
```

### 2. Membuat Export Class
Pada langkah ini buat export class untuk mengexport excel.
```bash
php artisan make:export DeliveryOrderDetailExport
```

Kemudian pada app\Exports\DeliveryOrderDetailExport.php ubah seperti ini.
```bash
<?php

namespace App\Exports;

use Maatwebsite\Excel\Concerns\FromCollection;
use Illuminate\Contracts\View\View;
use Maatwebsite\Excel\Concerns\FromView;

class DeliveryOrderDetailExport implements FromView
{
    public function __construct($data)
    {
        $this->data = $data;
    }
    
    /**
    * @return \Illuminate\Support\Collection
    */
    public function collection()
    {}
    
    public function view(): View
    {
        return view('exports.delivery-order-detail-export')->with('data', $this->data);
    }
}
```

### 3. Membuat Blade View
Pada langkah ini untuk menulis excel yang akan kita buat.

Kemudian pada resources\views\exports\delivery-order-detail-export.blade.php
```bash
<table>
    <thead>
    <tr>
        <th>No</th>
        <th>Nama Supplier</th>
        <th>No DO</th>
        <th>Status</th>
    </tr>
    </thead>
    <tbody>
    @foreach($data as $row)
        <tr>
            <td>{{ $row['no'] }}</td>
            <td>{{ $row['name'] }}</td>
            <td>{{ $row['do'] }}</td>
            <td>{{ $row['status'] }}</td>
        </tr>
    </tbody>
</table>
```

### 4. Memanggil Export Excel Controller
Pada langkah ini kita akan membuat perintah untuk mengexport excel pada controller.
```bash
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

use Excel;
use App\Exports\DeliveryOrderDetailExport;

class DeliveryOrderController extends Controller
{
    public function export()
    {
        $data = [
            [
                'no' => 1,
                'name' => 'PT Maju Mundur',
                'do' => 'DO-01',
                'status' => 'aktif',
            ],
            [
                'no' => 2,
                'name' => 'PT Bintang Kejora',
                'do' => 'DO-02',
                'status' => 'aktif',
            ],
        ];
        
        return Excel::download(new DeliveryOrderDetailExport($data), 'delivery-order-detail-' . $id . '.xlsx');
    }
}
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://docs.laravel-excel.com/3.1/exports/from-view.html) tersebut.
