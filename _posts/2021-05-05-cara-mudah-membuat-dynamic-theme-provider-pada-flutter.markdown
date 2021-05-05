---
layout: post
title: Cara Mudah Membuat Dynamic Theme Provider Pada Flutter
github: https://betterprogramming.pub/how-to-create-a-dynamic-theme-in-flutter-using-provider-e6ad1f023899
image: https://miro.medium.com/max/700/1*kqoy7vrgWAwjAsdLtiQ50w.png
language: dart | flutter
---

Memastikan possible untuk mengubah thema aplikasi kita sesuai keinginan pengguna dengan memanfaatkan `ChangeNotifierProvider` pada provider flutter.

### 1. Install
pubspec.yaml
```bash
dependencies:
  provider: ^4.0.1
  day_night_switch: ^0.0.2+1
```
kemudian jalankan
```bash
flutter pub get
```

### 2. Membuat Dynamic Theme Provider
#### Contoh
susunan directory
```bash
❏ lib
    ❏ page
        ❏ settings_page.dart
    ❏ util
        ❏ theme_notifier.dart
    ❏ values
        ❏ theme.dart
    ❏ main.dart
```

`lib/main.dart`
```bash
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'package:my_app/values/theme.dart';
import 'package:my_app/util/theme_notifier.dart';
import 'package:my_app/page/settings_page.dart';

void main() => runApp(
    ChangeNotifierProvider<ThemeNotifier>(
        create: (_) => ThemeNotifier(darkTheme),
        child: MyApp(),
    ),
);

class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        final themeNotifier = Provider.of<ThemeNotifier>(context);
        
        return MaterialApp(
            title: 'Chitr',
            theme: themeNotifier.getTheme(),
            home: SettingsPage(),
        );
    }
}
```

`lib/values/theme.dart`
```bash
import 'package:flutter/material.dart';

final darkTheme = ThemeData(
    primarySwatch: Colors.grey,
    primaryColor: Colors.black,
    brightness: Brightness.dark,
    backgroundColor: const Color(0xFF212121),
    accentColor: Colors.white,
    accentIconTheme: IconThemeData(color: Colors.black),
    dividerColor: Colors.black12,
);

final lightTheme = ThemeData(
    primarySwatch: Colors.grey,
    primaryColor: Colors.white,
    brightness: Brightness.light,
    backgroundColor: const Color(0xFFE5E5E5),
    accentColor: Colors.black,
    accentIconTheme: IconThemeData(color: Colors.white),
    dividerColor: Colors.white54,
);
```

`lib/util/theme_notifier.dart`
```bash
import 'package:flutter/material.dart';

class ThemeNotifier with ChangeNotifier {
    ThemeNotifier(this._themeData);
    
    ThemeData _themeData;
    
    getTheme() => _themeData;
    
    setTheme(ThemeData themeData) async {
        _themeData = themeData;
        notifyListeners();
    }
}
```

`lib/page/settings_page.dart`
```bash
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'package:day_night_switch/day_night_switch.dart';
import 'package:my_app/values/theme.dart';
import 'package:my_app/util/theme_notifier.dart';

class SettingsPage extends StatefulWidget {
    @override
    _SettingsPageState createState() => _SettingsPageState();
}

class _SettingsPageState extends State<SettingsPage> {
    var _darkTheme = true;
    
    @override
    Widget build(BuildContext context) {
        final themeNotifier = Provider.of<ThemeNotifier>(context);
        _darkTheme = (themeNotifier.getTheme() == darkTheme);
        
        return Scaffold(
            appBar: AppBar(
                title: Text('Settings'),
            ),
            body: ListView(
                children: <Widget>[
                    ListTile(
                        title: Text('Dark Theme'),
                        contentPadding: const EdgeInsets.only(left: 16.0),
                        trailing: Transform.scale(
                            scale: 0.4,
                            child: DayNightSwitch(
                                value: _darkTheme,
                                onChanged: (val) {
                                    setState(() => _darkTheme = val );
                                    onThemeChanged(val, themeNotifier);
                                },
                            ),
                        ),
                    ),
                ],
            ),
        );
    }

    void onThemeChanged(bool value, ThemeNotifier themeNotifier) async {
        (value) ? themeNotifier.setTheme(darkTheme) : themeNotifier.setTheme(lightTheme);
    }
}
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://betterprogramming.pub/how-to-create-a-dynamic-theme-in-flutter-using-provider-e6ad1f023899) tersebut.
