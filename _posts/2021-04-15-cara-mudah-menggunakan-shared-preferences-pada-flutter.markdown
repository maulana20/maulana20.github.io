---
layout: post
title: Cara Mudah Menggunakan Shared Preferences Pada Flutter
github: https://www.byriza.com/flutter-41-menyimpan-data-dengan-shared-preferences-pada-flutter
image: https://miro.medium.com/max/700/1*d7_x3XnsC6FJXNHNx_seQg.png
language: dart | flutter
---

### 1. Install
`pubspec.yaml`
```bash
dependencies:
  shared_preferences: ^0.5.2+2
```
kemudian jalankan
```bash
flutter pub get
```

### 2. Fungsi Pada Preferences
```bash
import 'package:shared_preferences/shared_preferences.dart';

SharedPreferences preferences = await SharedPreferences.getInstance();

preferences.setString('test', 'String yang disimpan');
preferences.getString('test');
```

#### Contoh
`lib/main.dart`
```bash
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
    String test;
    
    initPreference() async {
        SharedPreferences preferences = await SharedPreferences.getInstance();
        await preferences.setString('test', 'String yang disimpan');
        setState(() { test = preferences.getString('test'); });
    }
    
    void initState() {
        super.initState();
        initPreference();
    }
    
    @override
    Widget build(BuildContext context) {
        return MaterialApp(
            title: 'NavigationDrawer Demo',
            theme: ThemeData(
                primarySwatch: Colors.blue,
            ),
            home: Scaffold(
                appBar: AppBar(
                    title: Text(appTitle),
                ),
                body: Center(
                    child: Text(test),
                ),
            ),
        );
    }
}
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://www.byriza.com/flutter-41-menyimpan-data-dengan-shared-preferences-pada-flutter) tersebut.
