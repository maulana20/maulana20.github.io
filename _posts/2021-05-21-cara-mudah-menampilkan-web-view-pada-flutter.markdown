---
layout: post
title: Cara Mudah Menampilkan Web View Pada Flutter
github: https://github.com/eccosuprastyo/flutter/tree/master/webview
image: https://miro.medium.com/max/2880/1*Xwnl2ZrORcIUh92SfeEHjw.png
language: dart | flutter
---

Memastikan possible untuk menampilkan sebuah halaman website di dalam aplikasi.

### 1. Install
pubspec.yaml
```bash
dependencies:
  webview_flutter: ^0.3.3
```
kemudian jalankan
```bash
flutter pub get
```

### 2. Menjalankan Web View
`lib/main.dart`
```bash
import 'package:flutter/material.dart';
import 'package:webview_flutter/webview_flutter.dart';

import 'dart:async';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Web Views',
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
  String url = "https://gentle-river-19491.herokuapp.com";

  @override
  createState() => _MyHomePageState(this.url);
}

class _MyHomePageState extends State<MyHomePage> {
    _MyHomePageState(this._url);
  
    String _url;
    
    bool loading = true;
    WebViewController _controller;
    
    final Completer<WebViewController> _controllerCompleter = Completer<WebViewController>();
    
    Future<bool> _onWillPop(BuildContext context) async {
        if (await _controller.canGoBack()) {
            _controller.goBack();
            return Future.value(false);
        } else {
            return Future.value(true);
        }
    }
    
    Future<bool> startSplashScreen() async {
        var duration = const Duration(seconds: 3);
        
        await Timer(
            duration,
            () => setState(() => loading = false ),
        );
        
        return false;
    }
    
    @override
    void initState() {
        super.initState();
        startSplashScreen();
    }
    
    @override
    Widget build(BuildContext context) {
        return WillPopScope(
            onWillPop: () => _onWillPop(context), 
            child: Scaffold(
                body: loading == true ? Center(
                    child: Text(
                        'APP LOGO',
                        style: TextStyle(
                            fontSize: 30,
                            fontWeight: FontWeight.bold,
                        ),
                    ),
                ) : SafeArea(
                    child: WebView(
                        key: UniqueKey(),
                        javascriptMode: JavascriptMode.unrestricted,
                        initialUrl: _url,
                        onWebViewCreated: (WebViewController webViewController) {
                            _controllerCompleter.complete(webViewController);
                        },
                    ),
                ),
            ),
        );
    }
}
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://github.com/eccosuprastyo/flutter/tree/master/webview) tersebut.
