---
layout: post
title: Cara Mudah Membuat Navigation Drawer Pada Flutter
github: https://medium.com/@kashifmin/flutter-setting-up-a-navigation-drawer-with-multiple-fragments-widgets-1914fda3c8a8
image: https://miro.medium.com/max/540/1*EsZiL8weIycbTDMo2m49MA.png
language: dart | flutter
---

### 1. Membuat Drawer
#### Contoh
susunan directory
```bash
❏ lib
    ❏ pages
        ❏ home_page.dart
    ❏ fragments
        ❏ first_fragment.dart
        ❏ second_fragment.dart
        ❏ third_fragment.dart
    ❏ main.dart
```

`lib/main.dart`
```bash
import 'package:flutter/material.dart';
import 'package:my_app/pages/home_page.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return MaterialApp(
            title: 'NavigationDrawer Demo',
            theme: ThemeData(
                primarySwatch: Colors.blue,
            ),
            home: HomePage(),
        );
    }
}
```

`lib/pages/home_page.dart`
```bash
import 'package:flutter/material.dart';
import 'package:my_app/fragments/first_fragment.dart';
import 'package:my_app/fragments/second_fragment.dart';
import 'package:my_app/fragments/third_fragment.dart';

class DrawerItem {
    String title;
    IconData icon;
    DrawerItem(this.title, this.icon);
}

class HomePage extends StatefulWidget {
    final drawerItems = [
        new DrawerItem("Fragment 1", Icons.rss_feed),
        new DrawerItem("Fragment 2", Icons.local_pizza),
        new DrawerItem("Fragment 3", Icons.info)
    ];
    
    @override
    _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
    int _selectedDrawerIndex = 0;
    
    _getDrawerItemWidget(int pos) {
        switch (pos) {
            case 0:
                return new FirstFragment();
            case 1:
                return new SecondFragment();
            case 2:
                return new ThirdFragment();
            default:
                return new Text("Error");
        }
    }
    
    _onSelectItem(int index) {
        setState(() => _selectedDrawerIndex = index);
        Navigator.of(context).pop(); // close the drawer
    }
    
    @override
    Widget build(BuildContext context) {
        var drawerOptions = <Widget>[];
        
        for (var i = 0; i < widget.drawerItems.length; i++) {
            var d = widget.drawerItems[i];
            drawerOptions.add(
                new ListTile(
                    leading: new Icon(d.icon),
                    title: new Text(d.title),
                    selected: i == _selectedDrawerIndex,
                    onTap: () => _onSelectItem(i),
                )
            );
        }
        
        return new Scaffold(
            appBar: new AppBar(
                title: new Text(widget.drawerItems[_selectedDrawerIndex].title),
            ),
            drawer: new Drawer(
                child: new Column(
                    children: <Widget>[
                        new UserAccountsDrawerHeader(
                            accountName: new Text("John Doe"),
                            accountEmail: null
                        ),
                        new Column(children: drawerOptions)
                    ],
                ),
            ),
            body: _getDrawerItemWidget(_selectedDrawerIndex),
        );
    }
}
```

`lib/fragments/first_fragment.dart` seterusnya sama hingga fragment ke 3
```bash
import 'package:flutter/material.dart';

class FirstFragment extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return new Center(
            child: new Text("Hello Fragment 1"),
        );
    }
}
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://medium.com/@kashifmin/flutter-setting-up-a-navigation-drawer-with-multiple-fragments-widgets-1914fda3c8a8) tersebut.
