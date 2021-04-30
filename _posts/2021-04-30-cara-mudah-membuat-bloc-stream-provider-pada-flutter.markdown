---
layout: post
title: Cara Mudah Membuat BLoC Stream Provider Pada Flutter
github: https://medium.com/flutter-community/flutter-bloc-with-streams-6ed8d0a63bb8
image: https://miro.medium.com/max/700/1*RQH7ykFD3EEMn6NuAmO4_g.png
language: dart | flutter
---

Memastikan possible untuk memisahkan business login dari ui dengan memanfaatkan fungsionalitas Stream untuk mengelola dan menyebarkan perubahan.

### 1. Install
`pubspec.yaml`
```bash
dependencies:
  rxdart: 0.18.1
  provider: 1.4.0
```
kemudian jalankan
```bash
flutter pub get
```

### 2. Membuat BLoC Stream Provider
#### Contoh
susunan directory
```bash
❏ lib
    ❏ page
        ❏ profile_form_page.dart
        ❏ profile_page.dart
    ❏ model
        ❏ profile.dart
    ❏ bloc
        ❏ profile_bloc.dart
    ❏ main.dart
```

`lib/main.dart`
```bash
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'package:my_app/page/profile_form_page.dart';
import 'package:my_app/bloc/profile_bloc.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
    final appTitle = 'BLoC Stream Demo';
    
    @override
    Widget build(BuildContext context) {
        return MaterialApp(
            title: appTitle,
            theme: ThemeData(
                primarySwatch: Colors.blue,
            ),
            home: StatefulProvider<ProfileBloc>(
                valueBuilder: (context) => ProfileBloc(),
                onDispose: (context, bloc) => bloc.dispose(),
                child: ProfileFormPage(appTitle: appTitle),
            ),
        );
    }
}
```

`lib/bloc/profile_bloc.dart`
```bash
import 'package:rxdart/rxdart.dart';
import 'package:my_app/model/profile.dart';

class ProfileBloc {
    final BehaviorSubject _profileSubject = BehaviorSubject<Profile>(seedValue: Profile());
    
    Stream<Profile> get profileStream => _profileSubject.controller.stream;
    
    void updateWith({ String name, String email, String phone }) {
        Profile value = _profileSubject.value.copyWith(name: name, email: email, phone: phone);
        _profileSubject.add(value);
    }
    
    void dispose() {
        _profileSubject.close();
    }
}
```

`lib/model/profile.dart`
```bash
class Profile {
    final String name;
    final String email;
    final String phone;
    
    Profile({ this.name, this.email, this.phone });
    
    Profile copyWith({ String name, String email, String phone }) {
        return Profile(
            name: name ?? this.name,
            email: email ?? this.email,
            phone: phone ?? this.phone,
        );
    }
}
```

`lib/page/profile_form_page.dart`
```bash
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'package:my_app/page/profile_page.dart';
import 'package:my_app/bloc/profile_bloc.dart';
import 'package:my_app/model/profile.dart';

class ProfileFormPage extends StatefulWidget {
    ProfileFormPage({ this.appTitle });
    
    String appTitle;
    
    @override
    _ProfileFormPageState createState() => new _ProfileFormPageState(appTitle: appTitle);
}

class _ProfileFormPageState extends State<ProfileFormPage> {
    _ProfileFormPageState({ this.appTitle });
    
    String appTitle;
    final _formKey = GlobalKey<FormState>();
    
    @override
    Widget build(BuildContext context) {
        final profileBloc = Provider.of<ProfileBloc>(context);
        
        return Scaffold(
            appBar: AppBar(
                title: Text(appTitle),
            ),
            body: Form(
                key: _formKey,
                child: StreamBuilder(
                    stream: profileBloc.profileStream,
                    initialData: Profile(),
                    builder: (context, snapshot) {
                        return Container(
                            margin: EdgeInsets.all(20.0),
                            child: ListView(
                                children: [
                                    TextFormField(
                                        validator: (value) {
                                            if (value == null || value.isEmpty) return 'Name must filled';
                                            return null;
                                        },
                                        keyboardType: TextInputType.text,
                                        decoration: InputDecoration(
                                            hintText: 'Barry allen',
                                            labelText: 'Name',
                                            icon: Icon(Icons.verified_user),
                                        ),
                                        onChanged: (text) => profileBloc.updateWith(name: text),
                                    ),
                                    TextFormField(
                                        validator: (value) {
                                            if (value.contains('@') && value.contains('.')) return null;
                                            return "Not valid email";
                                        },
                                        keyboardType: TextInputType.emailAddress,
                                        decoration: InputDecoration(
                                            hintText: 'hero@example.com',
                                            labelText: 'Email',
                                            errorText: snapshot.error,
                                            icon: Icon(Icons.email),
                                        ),
                                        onChanged: (text) => profileBloc.updateWith(email: text),
                                    ),
                                    TextFormField(
                                        validator: (value) {
                                            if (value == null || value.isEmpty) return 'Phone must filled';
                                            return null;
                                        },
                                        keyboardType: TextInputType.number,
                                        decoration: InputDecoration(
                                            hintText: 'Enter your phone',
                                            labelText: 'Phone',
                                            errorText: snapshot.error,
                                            icon: Icon(Icons.contact_phone),
                                        ),
                                        onChanged: (text) => profileBloc.updateWith(phone: text),
                                    ),
                                    SizedBox(height: 10.0),
                                    RaisedButton(
                                        child: Text('submit'),
                                        color: Colors.blue,
                                        onPressed: () {
                                            final FormState form = _formKey.currentState;
                                            if (form.validate()) {
                                                // form.save();
                                                Navigator.push(
                                                    context,
                                                    MaterialPageRoute(builder: (context) => ProfilePage(appTitle: appTitle, profile: snapshot.data)),
                                                );
                                                form.reset();
                                            }
                                        }
                                    ),
                                ]
                            ),
                        );
                    }
                ),
            ),
        );
    }
}
```

`lib/page/profile_page.dart`
```bash
import 'package:flutter/material.dart';
import 'package:my_app/model/profile.dart';

class ProfilePage extends StatelessWidget {
    ProfilePage({ this.appTitle, this.profile });
    
    String appTitle;
    Profile profile;
    
    @override
    Widget build(BuildContext context) {
        return Scaffold(
            appBar: AppBar(
                title: Text(appTitle),
            ),
            body: ListView(
                shrinkWrap: true,
                padding: EdgeInsets.all(10.0),
                children: [
                    _information('Name', profile.name),
                    _information('Email', profile.email),
                    _information('Phone', profile.phone),
                ],
            ),
        );
    }
    
    Expanded _information(String title, String value) {
        return Expanded(
            child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                    Container(
                        padding: EdgeInsets.only(bottom: 8),
                        child: Text(
                            title,
                            style: TextStyle(
                                fontSize: 12.0,
                                fontWeight: FontWeight.bold,
                            ),
                        ),
                    ),
                    Text(
                        value,
                        style: TextStyle(
                            fontSize: 14.0,
                        ),
                    ),
                    Padding(
                        padding: EdgeInsets.all(1.0),
                        child: new Divider(),
                    ),
                ],
            ),
        );
    }
}
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://medium.com/flutter-community/flutter-bloc-with-streams-6ed8d0a63bb8) tersebut.
