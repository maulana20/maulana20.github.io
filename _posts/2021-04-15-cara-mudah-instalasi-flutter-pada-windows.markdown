---
layout: post
title: Cara Mudah Instalasi Flutter Pada Windows
github: https://flutter.dev/docs/get-started/install/windows
image: https://flutter.dev/images/flutter-logo-sharing.png
language: dart | flutter
---

## Getting Started

### Basic Install

#### Donwload :
- Download [Flutter SDK](https://flutter.dev/docs/get-started/install/windows)
- Download [Android Studio](https://developer.android.com/studio) : for need SDK Management (i use API 28 => Android 9.0) or adjust for your needed

#### Setup :
Update [path](https://www.architectryan.com/2018/03/17/add-to-the-path-on-windows-10/) in system variable add path `D:\flutter\bin`, after setup check run :
- `$ flutter --version`
- `$ flutter doctor` for checking issue

#### Create :
- With command
```bash
$ flutter create my_app
$ cd my_app
$ flutter pub get
$ flutter run
```
note :
- if you want to run with android studio, please run [emulator](https://developer.android.com/studio/run/emulator?hl=id#:~:text=Klik%20File%20%3E%20Settings%20%3E%20Tools%20%3E,View%20%3E%20Tool%20Windows%20%3E%20Emulator.)
- if you want to run with your android device, please enable [mode debugging](https://www.nesabamedia.com/apa-itu-usb-debugging/#:~:text=B.-,Mengaktifkan%20USB%20Debugging,%E2%80%9D%20saat%20mengaktifkannya%2C%20pilih%20OK.) in your device

checking device `$ flutter devices`, in sample :
```bash
$ flutter devices
2 connected devices:

Nexus 5 XXXX (mobile)             • 0418029825235987 • android-arm64 • Android 9 (API 28)
Android SDK built for x86 (mobile) • emulator-5554    • android-x86   • Android 8.1.0 (API 27) (emulator)
```

additional : create flutter with [plugin](https://medium.com/@syakirarif/cara-install-flutter-di-android-studio-c33c461bc690)

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://flutter.dev/docs/get-started/install/windows) tersebut.
