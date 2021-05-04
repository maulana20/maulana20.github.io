---
layout: post
title: Cara Mudah Menggunakan Push Notification Firebase Pada Flutter
github: https://www.freecodecamp.org/news/how-to-add-push-notifications-to-flutter-app/
image: https://cdn-media-2.freecodecamp.org/w1280/5fd0362ce6787e098393c56a.jpg
language: dart | flutter
---

Memastikan possible untuk mengirim atau menerima pesan notifikasi pada aplikasi kita.

Pada kali ini kita akan daftarkan dahulu aplikasi untuk bisa akses pada [firebase cloud messanging](https://console.firebase.google.com/). contoh aplikasi yang di demo kan adalah com.example.my_app

### 1. Firebase Configuration
Untuk mengaktifkan service firebase pada aplikasi, kita perlu menambahkan plugin google ke dalam file `gradle` [sumber](https://alfach.com/2020/05/19/push-notification-di-flutter-untuk-android-menggunakan-firebase-cloud-messaging-fcm/)

`android/build.gradle`
```bash
dependencies {
    // Add this line
    classpath 'com.google.gms:google-services:4.3.2'
```
`android/app/build.gradle`
```bash
apply plugin: 'com.google.gms.google-services'

dependencies {
    // Add this line
    implementation 'com.google.firebase:firebase-messaging:20.1.0'
```
`android/app/src/main/AndroidManifest.xml`
```bash
<intent-filter>
    <action android:name="FLUTTER_NOTIFICATION_CLICK" />
    <category android:name="android.intent.category.DEFAULT" />
</intent-filter>
```
`android/app/src/main/kotlin/com/example/my_app/Application.kt` [issue](https://github.com/FirebaseExtended/flutterfire/issues/1684#issuecomment-568352433)
```bash
package com.example.my_app

import io.flutter.app.FlutterApplication;
import io.flutter.plugin.common.PluginRegistry;
import io.flutter.plugin.common.PluginRegistry.PluginRegistrantCallback;
import io.flutter.plugins.GeneratedPluginRegistrant;
import io.flutter.plugins.firebasemessaging.FlutterFirebaseMessagingService;

class Application : FlutterApplication(), PluginRegistrantCallback {
    override fun onCreate() {
        super.onCreate()
        FlutterFirebaseMessagingService.setPluginRegistrant(this)
    }

    override fun registerWith(registry: PluginRegistry?) {
        registry?.registrarFor("io.flutter.plugins.firebasemessaging.FirebaseMessagingPlugin");
    }
}
```
`android/app/src/main/AndroidManifest.xml`
```bash
<application
    // Add this line    
    android:name=".Application"
```
kemudian jalankan
```bash
flutter packages get
```

### 2. Install
pubspec.yaml
```bash
dependencies:
  firebase_messaging: ^7.0.3
```
kemudian jalankan
```bash
flutter pub get
```
#### Contoh
`lib/main.dart`
```bash
import 'package:flutter/material.dart';
import 'package:firebase_messaging/firebase_messaging.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
    final appTitle = 'Push Notification Demo';
    
    @override
    Widget build(BuildContext context) {
        return MaterialApp(
            title: appTitle,
            theme: ThemeData(
                primarySwatch: Colors.blue,
            ),
            home: HomePage(appTitle: appTitle),
        );
    }
}

class Notification {
    final String title;
    final String body;
    
    Notification({ @required this.title, @required this.body });
}

class HomePage extends StatefulWidget {
    HomePage({ this.appTitle });
    
    String appTitle;
    
    @override
    _HomePageState createState() => _HomePageState(appTitle: appTitle);
}

class _HomePageState extends State<HomePage> {
    _HomePageState({ this.appTitle });
    
    String appTitle;
    String information = "information";
    
    List<Notification> notifications = [];
    ValueNotifier<int> notificationCounterValueNotifer = ValueNotifier(0);
    
    FirebaseMessaging _firebaseMessaging = FirebaseMessaging();
    
    @override
    void initState() {
        _firebaseMessaging.getToken().then((String token) {
            print("Push Messaging token: $token");
        });
        
        _firebaseMessaging.subscribeToTopic("general");
        
        _firebaseMessaging.configure(
            onMessage: (Map<String, dynamic> message) async {
                print("onMessage: $message");
                setState(() {
                    notifications.add(
                        Notification(
                            title: message["notification"]["title"],
                            body: message["notification"]["body"],
                        ),
                    );
                    
                    notificationCounterValueNotifer.value++;
                    notificationCounterValueNotifer.notifyListeners(); 
                });
            },
            onLaunch: (Map<String, dynamic> message) async {
                print("onLaunch: $message");
            },
            onResume: (Map<String, dynamic> message) async {
                print("onResume: $message");
            },
        );
        
        super.initState();
    }
    
    @override
    Widget build(BuildContext context) {
        return Scaffold(
            appBar: AppBar(
                title: Text(appTitle),
                actions: <Widget>[
                    Stack(
                        children: <Widget>[
                            IconButton(
                                icon: Icon(Icons.notifications),
                                onPressed: () {
                                    Navigator.push(
                                        context,
                                        MaterialPageRoute(builder: (context) => NotificationsPage(notifications: notifications)),
                                    );
                                    notificationCounterValueNotifer.value = 0;
                                },
                            ),
                            ValueListenableBuilder(
                                builder: (BuildContext context, int counter, Widget child) {
                                    return counter != 0 ? Positioned(
                                        right: 11,
                                        top: 11,
                                        child: new Container(
                                            padding: EdgeInsets.all(2.0),
                                            decoration: new BoxDecoration(
                                                color: Colors.red,
                                                borderRadius: BorderRadius.circular(6.0),
                                            ),
                                            constraints: BoxConstraints(
                                                minWidth: 14,
                                                minHeight: 14,
                                            ),
                                            child: Text(
                                                counter.toString(),
                                                style: TextStyle(
                                                    color: Colors.white,
                                                    fontSize: 8,
                                                ),
                                                textAlign: TextAlign.center,
                                            ),
                                        ),
                                    ) : new Container();
                                },
                                valueListenable: notificationCounterValueNotifer,
                            ),
                        ],
                    ),
                ],
            ),
            body: Center(
                child: Column(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: <Widget>[
                        Container(
                            padding: EdgeInsets.only(bottom: 8),
                            child: Text(
                                'Firebase Push Notification',
                                style: TextStyle(
                                    fontSize: 16.0,
                                    fontWeight: FontWeight.bold,
                                ),
                            ),
                        ),
                    ],
                ),
            ),
        );
    }
}

class NotificationsPage extends StatelessWidget {
    NotificationsPage({ @required this.notifications });
    
    List<Notification> notifications;
    
    @override
    Widget build(BuildContext context) {
        return Scaffold(
            appBar: AppBar(
                title: Text('Notification List'),
            ),
            body: notifications != null ? ListView(
                children: notifications.map(buildNotification).toList(),
            ) : Container(),
        );
    }
    
    Widget buildNotification(Notification notification) {
        return ListTile(
            title: Text(notification.title),
            subtitle: Text(notification.body),
        );
    }
}
```

### Catatan
pada dokumentasi firebase flutter, kita diminta untuk menambahkan file `Application.java` pada lokasi `MainActivity.java` berada, namun untuk flutter terbaru menggunakan kotlin pada `MainActivity.kt`,  jadi kita akan buat kotlin `Application.kt` pada lokasi `MainActivity.kt` berada.

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://www.freecodecamp.org/news/how-to-add-push-notifications-to-flutter-app/) tersebut.
