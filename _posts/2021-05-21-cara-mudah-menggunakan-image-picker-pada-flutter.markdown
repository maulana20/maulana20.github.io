---
layout: post
title: Cara Mudah Menggunakan Image Picker Pada Flutter
github: https://github.com/bizz84/image-picker-demo-flutter
image: https://miro.medium.com/max/700/1*fSvEkoeX5peLZ2toiXS8zQ.png
language: dart | flutter
---

Memastikan possible untuk mengambil gambar dari kamera maupun galeri lalu kita dapat menampilkannya di widget image.

### 1. Install
pubspec.yaml
```bash
dependencies:
  image_picker: ^0.6.1+4
```
kemudian jalankan
```bash
flutter pub get
```

### 2. Menjalankan Image Picker
#### Contoh
susunan directory
```bash
❏ lib
    ❏ main.dart
    ❏ image_picker_channel.dart
```

`lib/main.dart`
```bash
import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';

import 'dart:io';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return MaterialApp(
            title: 'Flutter Demo',
            theme: ThemeData(
                primarySwatch: Colors.blue,
            ),
            home: MyHomePage(title: 'Image Picker Demo'),
        );
    }
}

class MyHomePage extends StatefulWidget {
    MyHomePage({ Key key, this.title }) : super(key: key);
    
    final String title;
    
    @override
    _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
    File _imageFile;
    
    Future<void> captureImage(ImageSource imageSource) async {
        try {
            final imageFile = await ImagePicker.pickImage(source: imageSource);
            setState( () => _imageFile = imageFile );
        } catch (e) {
            print(e);
        }
    }
    
    @override
    Widget build(BuildContext context) {
        return Scaffold(
            appBar: AppBar(
                title: Text(widget.title),
            ),
            body: Column(
                children: [
                    Expanded(
                        child: Center(
                            child: _imageFile == null ? Text(
                                'Take an image to start',
                                style: TextStyle(
                                    fontSize: 18.0
                                ),
                            ) : Image.file(_imageFile),
                        ),
                    ),
                    _buildButtons(),
                ],
            ),
        );
    }
    
    Widget _buildButtons() {
        return ConstrainedBox(
            constraints: BoxConstraints.expand(height: 80.0),
            child: Row(
                crossAxisAlignment: CrossAxisAlignment.stretch,
                mainAxisAlignment: MainAxisAlignment.spaceAround,
                children: <Widget>[
                    _buildActionButton( key: Key('retake'), text: 'Photos', onPressed: () => captureImage(ImageSource.gallery) ),
                    _buildActionButton( key: Key('upload'), text: 'Camera', onPressed: () => captureImage(ImageSource.camera) ),
                ],
            ),
        );
    }
    
    Widget _buildActionButton({ Key key, String text, Function onPressed }) {
        return Expanded(
            child: FlatButton(
                key: key,
                child: Text(
                    text,
                    style: TextStyle(
                        fontSize: 20.0
                    )
                ),
                shape: RoundedRectangleBorder(),
                color: Colors.blueAccent,
                textColor: Colors.white,
                onPressed: onPressed,
            ),
        );
    }
}
```

`lib/image_picker_channel.dart`
```bash
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';

import 'dart:async';
import 'dart:io';

enum ImageSource {
    photos,
    camera
}

String _stringImageSource(ImageSource imageSource) {
    switch (imageSource) {
        case ImageSource.photos:
            return 'photos';
        case ImageSource.camera:
            return 'camera';
    }
    
    return null;
}

class ImagePickerChannel implements ImagePicker {
    static const platform = MethodChannel('com.musevisions.flutter/imagePicker');
    
    Future<File> pickImage({ ImageSource imageSource }) async {
        final stringImageSource = _stringImageSource(imageSource);
        final result = await platform.invokeMethod('pickImage', stringImageSource);
        
        if (result is String) {
            return File(result);
        } else if (result is FlutterError) {
            throw result;
        }
        
        return null;
    }
}

abstract class ImagePicker {
    Future<File> pickImage({ImageSource imageSource});
}
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://github.com/bizz84/image-picker-demo-flutter) tersebut.
