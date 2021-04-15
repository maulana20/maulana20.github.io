---
layout: post
title: Cara Mudah Menyimpan Data Dalam Aplikasi Pada Flutter
github: https://www.byriza.com/flutter-41-menyimpan-data-dengan-shared-preferences-pada-flutter
image: https://miro.medium.com/max/700/1*d7_x3XnsC6FJXNHNx_seQg.png
language: dart | flutter
---

### 1. Menambahkan Package Manager
```bash
import 'package:shared_preferences/shared_preferences.dart';
```

Jalankan
```bash
flutter pub get
```

### 2. Membuat Fungsi Pada Preference
```bash
    Future<String> setPreference(String index, String value) async {
        SharedPreferences preferences = await SharedPreferences.getInstance();
        setState(() { preferences.setString('${index}', '${value}'); });
    }
    
    Future<String> getPreference(String index) async {
        SharedPreferences preferences = await SharedPreferences.getInstance();
        return preferences.getString(index);
    }
```

#### Contoh 
simpan nama dengan `setState(() { setPreference('nama', 'maulana'); });`, lalu panggil nama dengan `final nama = await getPreference('nama');`

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://www.byriza.com/flutter-41-menyimpan-data-dengan-shared-preferences-pada-flutter) tersebut.
