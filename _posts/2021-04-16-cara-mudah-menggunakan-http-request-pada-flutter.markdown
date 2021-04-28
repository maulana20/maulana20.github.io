---
layout: post
title: Cara Mudah Menggunakan Http Request Pada Flutter
github: https://medium.com/swlh/how-to-make-http-requests-in-flutter-d12e98ee1cef
image: https://miro.medium.com/max/700/1*YcF4X4FFw-p59uFTiS8gQQ.png
language: dart | flutter
---

### 1. Install
`pubspec.yaml`
```bash
dependencies:
  http: any
```
kemudian jalankan
```bash
flutter pub get
```

### 2. Fungsi Pada Http
```bash
import 'package:http/http.dart' as http;

Map<String, String> headers = {'Content-Type': 'application/json'};
http.Response response = await http.get('https://jsonplaceholder.typicode.com/posts', headers: headers);

Map<String, dynamic> result = json.decode(response.body);
```

#### Contoh
susunan directory
```bash
❏ lib
    ❏ page
        ❏ post_page.dart
        ❏ post_detail_page.dart
    ❏ model
        ❏ post.dart
    ❏ main.dart
```

`lib/main.dart`
```bash
import 'package:flutter/material.dart';
import 'package:my_app/page/post_page.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
    final appTitle = 'Http Demo';
    
    @override
    Widget build(BuildContext context) {
        return MaterialApp(
            title: appTitle,
            theme: ThemeData(
                primarySwatch: Colors.blue,
            ),
            home: PostPage(appTitle: appTitle),
        );
    }
}
```

`lib/model/post.dart`
```bash
class Post extends Object {
    int userId;
    int id;
    String title;
    String body;
    
    Post({ this.userId, this.id, this.title, this.body });
    
    factory Post.fromJson(Map<String, dynamic> json) {
        return Post(
            userId: json['userId'],
            id: json['id'],
            title: json['title'],
            body: json['body'],
        );
    }
}
```

`lib/page/post_page.dart`
```bash
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'package:my_app/model/post.dart';
import 'package:my_app/page/post_detail_page.dart';

import 'dart:async';
import 'dart:convert';

class PostPage extends StatefulWidget {
    PostPage({ this.appTitle });
    
    String appTitle;
    
    @override
    _PostPageState createState() => new _PostPageState(appTitle: appTitle);
}

class _PostPageState extends State<PostPage> {
    _PostPageState({ this.appTitle });
    
    String appTitle;
    List<Post> posts;
    
    void getList() async {
        Map<String, String> headers = {'Content-Type': 'application/json'};
        http.Response response = await http.get('https://jsonplaceholder.typicode.com/posts', headers: headers);
        
        final result = json.decode(response.body);
        
        setState(() { posts = result.map<Post>((json) => Post.fromJson(json)).toList(); });
    }
    
    void initState() {
        super.initState();
        getList();
    }
    
    @override
    Widget build(BuildContext context) {
        return Scaffold(
            appBar: AppBar(
                title: Text(appTitle),
            ),
            body: Container(
                margin: EdgeInsets.all(10.0),
                child: ListView.builder(
                    itemCount: posts == null ? 0 : posts.length,
                    itemBuilder: (BuildContext context, int index) {
                        return Container(
                            child: Card(
                                child: Column(
                                    mainAxisSize: MainAxisSize.min, children: <Widget>[
                                        ListTile(
                                            title: Text(
                                                posts[index].title,
                                                maxLines: 2,
                                            ),
                                            subtitle: Text(
                                                posts[index].body,
                                                textAlign: TextAlign.justify,
                                                maxLines: 2,
                                            ),
                                        ),
                                        ButtonTheme.bar(
                                            child: ButtonBar(
                                                children: <Widget>[
                                                    FlatButton(
                                                        child: const Text('LIHAT DETAIL'),
                                                        onPressed: () {
                                                            Navigator.push(
                                                                context,
                                                                MaterialPageRoute(builder: (context) => PostDetailPage(post: posts[index])),
                                                            );
                                                        },
                                                    ),
                                                ],
                                            ),
                                        ),
                                    ],
                                ),
                            ),
                        );
                    }
                ),
            ),
        );
    }
}
```

`lib/page/post_detail_page.dart`
```bash
import 'package:flutter/material.dart';
import 'package:my_app/model/post.dart';

class PostDetailPage extends StatelessWidget {
    PostDetailPage({ this.post });
    
    final Post post;
    
    @override
    Widget build(BuildContext context) {
        final appTitle = 'Post Detail ${post.id}';
        return Scaffold(
            appBar: AppBar(
                title: Text(appTitle),
            ),
            body: ListView(
                shrinkWrap: true,
                padding: EdgeInsets.all(10.0),
                children: <Widget>[
                    TextFormField(
                        enabled: false,
                        initialValue: '${post.userId}',
                        decoration: InputDecoration(
                            labelText: 'User ID',
                            contentPadding: EdgeInsets.all(10.0),
                        ),
                    ),
                    TextFormField(
                        enabled: false,
                        initialValue: post.title,
                        keyboardType: TextInputType.multiline,
                        maxLines: 3,
                        decoration: InputDecoration(
                            labelText: 'Title',
                            contentPadding: EdgeInsets.all(10.0),
                        ),
                    ),
                    TextFormField(
                        enabled: false,
                        initialValue: post.body,
                        maxLines: 8,
                        decoration: InputDecoration(
                            labelText: 'Body',
                            contentPadding: EdgeInsets.all(10.0),
                        ),
                    ),
                ],
            ),
        );
    }
}
```

note : Apabila terjadi gagal request di karenakan not allow pada domain http <span style="color:red;">Bad state: Insecure HTTP is not allowed by platform</span>, maka tambahkan pada `android/app/src/main/AndroidManifest.xml`
```bash
<application
        android:name="io.flutter.app.FlutterApplication"
        android:label="receipt"
        android:usesCleartextTraffic="true" <!-- This Line -->
        android:icon="@mipmap/ic_launcher">
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://medium.com/swlh/how-to-make-http-requests-in-flutter-d12e98ee1cef) tersebut.
