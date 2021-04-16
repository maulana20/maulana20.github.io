---
layout: post
title: Cara Mudah Menyimpan Data Dalam Aplikasi Pada Flutter
github: https://www.byriza.com/flutter-41-menyimpan-data-dengan-shared-preferences-pada-flutter
image: https://miro.medium.com/max/700/1*d7_x3XnsC6FJXNHNx_seQg.png
language: dart | flutter
---

### 1. Menambahkan Package Manager
Pada `pubspec.yaml`
```bash
dependencies:
  flutter:
    sdk: flutter
  //
  shared_preferences: ^0.5.2+2
```

Kemudian run
```bash
flutter pub get
```

### 2. Membuat Fungsi Pada Preference
```bash
import 'package:shared_preferences/shared_preferences.dart';

SharedPreferences preferences = await SharedPreferences.getInstance();

preferences.setString('nama', 'maulana');
preferences.getString('nama');
```

#### Contoh
```bash
import 'dart:async';

import 'package:flutter/material.dart';
import 'package:shared_preferences/shared_preferences.dart';

void main() => runApp(MyApp());

class MyApp extends StatefulWidget {
    @override
    _MyAppState createState() => new _MyAppState(appTitle: 'Shared Preference Demo');
}

class _MyAppState extends State<MyApp> {
    _MyAppState({ this.appTitle });
    
    String appTitle;
    String nama;
    
    Future<String> setPreference(String index, String value) async {
        SharedPreferences preferences = await SharedPreferences.getInstance();
        setState(() { preferences.setString('${index}', '${value}'); });
    }
    
    Future<String> getPreference(String index) async {
        SharedPreferences preferences = await SharedPreferences.getInstance();
        return preferences.getString(index);
    }
    
    initPreference() async {
        await setPreference('nama', 'maulana');
        nama = await getPreference('nama');
    }
    
    @override
    void initState() {
        super.initState();
        initPreference();
    }
    
    @override
    Widget build(BuildContext context) {
        return MaterialApp(
            title: appTitle,
            home: Scaffold(
                appBar: AppBar(
                    title: Text(appTitle),
                ),
                body: Center(
                    child: Text(nama),
                ),
            ),
        );
    }
}
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://www.byriza.com/flutter-41-menyimpan-data-dengan-shared-preferences-pada-flutter) tersebut.
