---
layout: post
title: Cara Mudah Menampilkan Tab Tetap Pada Flutter
github: https://medium.com/@diegoveloper/flutter-persistent-tab-bars-a26220d322bc
image: https://miro.medium.com/max/2880/1*Xwnl2ZrORcIUh92SfeEHjw.png
language: dart | flutter
---

Memastikan possible untuk menampilkan data tetap pada tab di dalam aplikasi.

### 2. Menjalankan Tab Persistent
#### Contoh
susunan directory
```bash
❏ lib
    ❏ main.dart
    ❏ persistent.dart
    ❏ non_persistent.dart
```

`lib/main.dart`
```bash
import 'package:flutter/material.dart';
import 'package:my_app/non_persistent.dart';
import 'package:my_app/persistent.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return MaterialApp(
            title: 'Persistent Tab Demo',
            theme: ThemeData(
            primarySwatch: Colors.blue,
            fontFamily: "Arial",
            textTheme: TextTheme(
                button: TextStyle(color: Colors.white, fontSize: 18.0),
                title: TextStyle(color: Colors.red))),
            home: MyHomePage(),
        );
    }
}

class MyHomePage extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return DefaultTabController(
            length: 2,
            child: Scaffold(
                appBar: AppBar(
                    bottom: TabBar(
                        isScrollable: true,
                        tabs: [
                            Tab(icon: Icon(Icons.directions_car), text: "Non persistent", ),
                            Tab(icon: Icon(Icons.directions_transit), text: "Persistent", ),
                        ],
                    ),
                    title: Text('Persistent Tab Demo'),
                ),
                body: TabBarView(
                    children: <Widget>[
                        NonPersistent(),
                        Persistent(),
                    ],
                ),
            ),
        );
    }
}
```

`lib/non_persistent.dart`
```bash
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

import 'dart:async';
import 'dart:convert';

class NonPersistent extends StatefulWidget {
    @override
    _NonPersistentState createState() => _NonPersistentState();
}

class _NonPersistentState extends State<NonPersistent> {
    var list = List();
    
    _loadList() async {
        final response = await http.get(Uri.parse("https://jsonplaceholder.typicode.com/posts/"));
        if (response.statusCode == 200) {
            await Future.delayed(const Duration(seconds: 1));
            if (mounted) setState( () => list = json.decode(response.body) as List );
        } else {
            throw Exception('Failed to load posts');
        }
    }
    
    @override
    void initState() {
        super.initState();
        _loadList();
    }
    
    @override
    Widget build(BuildContext context) {
        return Column(
            children: <Widget>[
                Expanded(
                    child: ListView.builder(
                        itemCount: list.length,
                        itemBuilder: (BuildContext context, int index) {
                            final data = list[index];
                            return ListTile(
                                contentPadding: EdgeInsets.all(10.0),
                                title: Text(data['title']),
                                subtitle: Text(
                                    data['body'],
                                    maxLines: 2,
                                    overflow: TextOverflow.ellipsis,
                                ),
                            );
                        },
                    ),
                ),
            ],
        );
    }
}
```

`lib/persistent.dart`
```bash
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

import 'dart:async';
import 'dart:convert';

class Persistent extends StatefulWidget {
    @override
    _PersistentState createState() => _PersistentState();
}

class _PersistentState extends State<Persistent> with AutomaticKeepAliveClientMixin<Persistent> {
    var list = List();
    
    _loadList() async {
        final response = await http.get(Uri.parse("https://jsonplaceholder.typicode.com/photos/"));
        if (response.statusCode == 200) {
            await Future.delayed(const Duration(seconds: 1));
            if (mounted) setState( () => list = json.decode(response.body) as List );
        } else {
            throw Exception('Failed to load posts');
        }
    }
    
    @override
    void initState() {
        super.initState();
        _loadList();
    }
    
    @override
    Widget build(BuildContext context) {
        super.build(context);
        return Column(
            children: <Widget>[
                Expanded(
                    child: ListView.builder(
                        itemCount: list.length,
                        itemBuilder: (BuildContext context, int index) {
                            final data = list[index];
                            return ListTile(
                                contentPadding: EdgeInsets.all(10.0),
                                title: Text(data['title']),
                                trailing: Image.network(
                                    data['thumbnailUrl'],
                                    height: 20.0,
                                    width: 20.0,
                                ),
                            );
                        },
                    ),
                ),
            ],
        );
    }
    
    @override
    bool get wantKeepAlive => true;
}
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://medium.com/@diegoveloper/flutter-persistent-tab-bars-a26220d322bc) tersebut.
