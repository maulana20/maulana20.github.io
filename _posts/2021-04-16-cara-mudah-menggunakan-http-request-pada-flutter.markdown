---
layout: post
title: Cara Mudah Menggunakan Http Request Pada Flutter
github: https://medium.com/swlh/how-to-make-http-requests-in-flutter-d12e98ee1cef
image: https://miro.medium.com/max/700/1*YcF4X4FFw-p59uFTiS8gQQ.png
language: dart | flutter
---

### 1. Menambahkan Package Manager
Pada `pubspec.yaml`
```bash
dependencies:
  flutter:
    sdk: flutter
  //
  http: any
```

Kemudian run
```bash
flutter pub get
```

### 2. Membuat Fungsi Pada Http
```bash

import 'package:http/http.dart' as http;

Map<String, String> headers = {'Content-Type': 'application/json'};
http.Response response = await http.get('http://domain', headers: headers);

Map<String, dynamic> result = jsonDecode(response.body);
```

#### Contoh
```bash
import 'dart:async';
import 'dart:convert';

import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

void main() => runApp(MyApp());

class MyApp extends StatefulWidget {
    @override
    _MyAppState createState() => new _MyAppState(appTitle: 'Http Demo');
}

class _MyAppState extends State<MyApp> {
    _MyAppState({ this.appTitle });
    
    String appTitle;
    Map<String, dynamic> currencies;
    
    final JsonDecoder _decoder = new JsonDecoder();
    
    Future<Map> getCurrencies() async {
        Map<String, String> headers = {'Content-Type': 'application/json'};
        http.Response response = await http.get('http://www.floatrates.com/daily/idr.json', headers: headers);
        
        print('Response GET: ${response.body}');
        Map<String, dynamic> result = jsonDecode(response.body);
        
        return result;
    }
    
    initCurrencies() async {
        currencies = await getCurrencies();
    }
    
    @override
    void initState() {
        super.initState();
        initCurrencies();
    }
    
    @override
    Widget build(BuildContext context) {
        return MaterialApp(
            title: appTitle,
            home: Scaffold(
                appBar: AppBar(
                    title: Text(appTitle),
                ),
                body: !["", null, false, 0].contains(currencies) ? dataResult() : errorResult(),
            ),
        );
    }
    
    Widget errorResult() {
        return Center(
            child: new Text('Data not load, please press r [Hot reload] !'),
        );
    }
    
    Widget dataResult() {
        return ListView(
            children: <Widget> [
                CurrencyTile('USD', 'IDR', currencies['usd']),
                CurrencyTile('JPY', 'IDR', currencies['jpy']),
                CurrencyTile('MYR', 'IDR', currencies['myr']),
            ],
        );
    }
    
    ListTile CurrencyTile(String from, String to, dynamic currency) {
        return ListTile(
            title: Row(
                mainAxisAlignment: MainAxisAlignment.spaceBetween,
                children: [
                    Row(
                        mainAxisSize: MainAxisSize.min,
                        children: [
                            Text(from),
                            SizedBox(width: 5.0),
                            Icon(Icons.arrow_forward_outlined, size: 14.0),
                            SizedBox(width: 5.0),
                            Text(to),
                        ],
                    ),
                    Text('${currency['inverseRate']}')
                ],
            ),
        );
    }
}
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://medium.com/swlh/how-to-make-http-requests-in-flutter-d12e98ee1cef) tersebut.
