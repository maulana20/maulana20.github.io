---
layout: post
title: Cara Mudah Menampilkan Batas Awal Dan Akhir Pada Flutter
github: https://medium.com/@diegoveloper/flutter-lets-know-the-scrollcontroller-and-scrollnotification-652b2685a4ac
image: https://miro.medium.com/max/300/1*m9DhXoa7sgFFnSAz7_ig7A.png
language: dart | flutter
---

Memastikan possible untuk menampilkan batas awal dan akhir list dengan scrolling pada aplikasi.

### 1. Menjalankan Scroll Limit
`lib/main.dart`
```bash
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return MaterialApp(
            title: 'Scroll Limit reached',
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

class MyHomePage extends StatefulWidget {
    @override
    _MyHomePageState createState() => _MyHomePageState();
}
class _MyHomePageState extends State<MyHomePage> {
    ScrollController _controller;
    String message = "reach the top";
    
    _scrollListener() {
        if (_controller.offset >= _controller.position.maxScrollExtent && !_controller.position.outOfRange) {
            setState( () => message = "reach the bottom" );
        }
        if (_controller.offset <= _controller.position.minScrollExtent && !_controller.position.outOfRange) {
            setState( () => message = "reach the top" );
        }
    }
    
    @override
    void initState() {
        super.initState();
        _controller = ScrollController();
        _controller.addListener(_scrollListener);
    }
    
    @override
    void dispose() {
        super.dispose();
        _controller.removeListener(_scrollListener);
        _controller.dispose();
    }
    
    @override
    Widget build(BuildContext context) {
        return Scaffold(
            appBar: AppBar(
                title: Text("Scroll Limit reached"),
            ),
            body: Column(
                children: <Widget>[
                    Container(
                        height: 50.0,
                        color: Colors.green,
                        child: Center(
                            child: Text(message),
                        ),
                    ),
                    Expanded(
                        child: ListView.builder(
                            controller: _controller,
                            itemCount: 30,
                            itemBuilder: (context, index) {
                                return ListTile(title: Text("Index : $index"));
                            },
                        ),
                    ),
                ],
            ),
        );
    }
}
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://medium.com/@diegoveloper/flutter-lets-know-the-scrollcontroller-and-scrollnotification-652b2685a4ac) tersebut.
