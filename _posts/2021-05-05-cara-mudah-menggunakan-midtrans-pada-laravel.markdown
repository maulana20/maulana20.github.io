---
layout: post
title: Cara Mudah Menggunakan Midtrans Pada Laravel
github: https://github.com/azishapidin/donasi-midtrans-example
image: https://snap-docs.midtrans.com/images/payment-list.png
language: php | laravel
---

Pada kali ini kita akan daftarkan dahulu domain kita untuk bisa akses pada [midtrans](https://account.midtrans.com/register) untuk mendapatkan `server_key` dan `client_key` nya.

### 1. Menambahkan Depedency
Di sini kita perlu menginstall depedency pada composer.
```bash
composer require veritrans/veritrans-php
```

### 2. Membuat Script pada Controller
```bash
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Veritrans_Config;
use Veritrans_Snap;
use Veritrans_Notification;

class DonationController extends Controller
{
    public function __construct(Request $request)
    {
        $this->request = $request;

        // Set midtrans configuration
        Veritrans_Config::$serverKey = 'server_key';
        Veritrans_Config::$isProduction = false;
        Veritrans_Config::$isSanitized = true;
        Veritrans_Config::$is3ds = true;
    }
    
    public function index(Request $request)
    {}
    
    public function creditCard(Request $request)
    {
        $validator = \Validator::make(request()->all(), [
            'donor_name'  => 'required',
            'donor_email' => 'required|email',
            'amount'      => 'required|numeric'
        ]);

        if ($validator->fails()) {
            return [
              'status'  => 'error',
              'message' => $validator->errors()->first()
            ];
        }
        
        // Buat transaksi ke midtrans kemudian save snap tokennya.
        $payload = [
            'transaction_details' => [
            'order_id'      => rand(),
                'gross_amount'  => $request->amount,
            ],
            'customer_details' => [
                'first_name'    => $request->donor_name,
                'email'         => $request->donor_email,
            ],
            'item_details' => [
                [
                    'id'       => $request->donation_type,
                    'price'    => $request->amount,
                    'quantity' => 1,
                    'name'     => ucwords(str_replace('_', ' ', $request->donation_type))
                ]
            ]
        ];
        
        $snapToken = Veritrans_Snap::getSnapToken($payload);
        
        return response()->json([ 'snap_token' => $snapToken ]);
    }
    
    public function notificationHandler(Request $request)
    {
        $notif = new Veritrans_Notification();
        
        return response()->json($notif);
    }
}
```

### 3. Membuat Form View
```bash
<!doctype html>
<html lang="{{ app()->getLocale() }}">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Simple Donation with Midtrans</title>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
    <style>
        html, body {
            background-color: #fff;
            color: #636b6f;
            font-weight: 200;
            height: 100vh;
            margin: 0;
        }
    </style>
</head>
<body>
    <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
        <a class="navbar-brand" href="#">Online Donation</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav mr-auto">
                <li class="nav-item active"><a class="nav-link" href="#create">Donation</a></li>
                <li class="nav-item"><a class="nav-link" href="#list">Donation List</a></li>
            </ul>
        </div>
    </nav>
    <div class="jumbotron jumbotron-fluid" style="background-color: #74b9ff; color: white;">
        <div class="container">
            <h1 class="display-4">Online Donation</h1>
            <p class="lead">This is just simple donation web with Midtrans.</p>
        </div>
    </div>
    <div class="container">
        <form class="form-horizontal" id="donation" onsubmit="return submitForm();">
            <legend>Donation</legend>
            <div class="row">
                <div class="col-md-4">
                    <div class="form-group">
                        <label class="control-label" for="donor_name">Donor Name</label>
                        <div>
                            <input id="donor_name" name="donor_name" type="text" placeholder="Enter your name.." class="form-control input-md" required="">
                        </div>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="form-group">
                        <label class="control-label" for="donor_email">Donor Email</label>
                        <div>
                            <input id="donor_email" name="donor_email" type="text" placeholder="Enter your email.." class="form-control input-md" required="">
                        </div>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="form-group">
                        <label class="control-label" for="donation_type">Type</label>
                        <div>
                            <select id="donation_type" name="donation_type" class="form-control">
                                <option value="infak_kemanusiaan">Infak Kemanusiaan</option>
                                <option value="infak_pendidikan">Infak Pendidikan</option>
                                <option value="infak_kesehatan">Infak Kesehatan</option>
                            </select>
                        </div>
                    </div>
                </div>
            </div>
            <div class="row">
                <div class="col-md-6">
                    <label for="">Amount</label>
                    <div class="input-group">
                        <div class="input-group-prepend">
                            <span class="input-group-text" id="basic-addon1">Rp</span>
                        </div>
                        <input id="amount" name="amount" class="form-control" placeholder="" type="number" min="1000" max="999999999" required="">
                    </div>
                </div>
                <div class="col-md-6">
                    <div class="form-group">
                        <label class="control-label" for="note">Note (Optional)</label>
                        <div>
                            <textarea class="form-control" id="note" name="note"></textarea>
                        </div>
                    </div>
                </div>
            </div>
            <button id="submit" class="btn btn-success">Submit</button>
        </form>
        <br>
    </div>
    <script src="https://code.jquery.com/jquery-3.3.1.min.js" integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8=" crossorigin="anonymous"></script>
    <script src="https://app.sandbox.midtrans.com/snap/snap.js" data-client-key="client_key"></script>
    <script>
        function submitForm() {
            $.post("{{ route('donation.creditcard') }}",
            {
                _method: 'POST',
                _token: '{{ csrf_token() }}',
                amount: $('input#amount').val(),
                note: $('textarea#note').val(),
                donation_type: $('select#donation_type').val(),
                donor_name: $('input#donor_name').val(),
                donor_email: $('input#donor_email').val(),
            },
            function (data, status) {
                if (data.status == 'error') {
                    alert(data.message);
                } else {
                    snap.pay(data.snap_token, {
                        onSuccess: function (result) {
                            location.reload();
                        },
                        onPending: function (result) {
                            location.reload();
                        },
                        onError: function (result) {
                            location.reload();
                        }
                    });
                }
            });
            return false;
        }
    </script>
</body>
</html>
```

### 3. Menambahkan Pada Route
```bash
Route::post('/donation/creditcard', [ DonationController::class, 'creditCard' ])->name('donation.creditcard');
Route::post('/notification/handler', [ DonationController::class, 'notificationHandler' ])->name('notification.handler');
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://github.com/azishapidin/donasi-midtrans-example) tersebut.
