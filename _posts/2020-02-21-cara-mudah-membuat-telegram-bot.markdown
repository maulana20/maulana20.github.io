---
layout: post
title: Cara Mudah Membuat Telegram Bot
github: https://gitlab.com/maulana20/telegram-bot
image: https://gitlab.com/maulana20/telegram-bot/-/raw/master/screen/telegram.png
category: python
---
Kita mungkin mengenal aplikasi chating Whatsapp, Line, dll, namun ada salah satu lagi chating yang tidak kalah menarik yaitu telegram. Sebelum kita lanjut kalian seharusnya sudah bisa menggunakan telegram.

Ok. Apa itu <b>bot telegram</b> ? Bot itu adalah mesin, layaknya mesin chatting pada telegram yang berinteraksi dengan manusia saat kita melakukan pengiriman pesan.

Lalu Bagaimana <b>cara menggunakan</b> ? Apakah bisa langsung jalan ? Mungkin untuk penggunaannya dilakukan secara bertahap diantaranya :
- Membuat <b>Telegram Bot</b>
- Konfigurasi <b>Telegram API</b> 

### 1. Membuat Telegram Bot
Untuk awal pembuatan bot lakukan pencarian @BotFather pada telegram. Apa itu <b>@BotFather</b> ? yaitu bot yang gunanya untuk menciptakan bot yang masih belum bisa di gunakan (botnya saja) atau dengan kata lain kamu buat botnya disana. lalu lakukan step pada sumber [link](https://www.petanikode.com/bot-telegram-tanpa-coding/) berikut untuk mendapatkan token dari bot kamu.

### 2. Konfigurasi Telegram API
Berikutnya setelah mendapatkan token pada bot yang telah kita buat lalu mulai lanjut dengan konfigurasi pada telegram apinya. Referensi untuk telegram api langkahnya pada sumber [link](https://core.telegram.org/bots/api) tersebut.

Menjalankan API dengan script, terlebih dahulu sudah menginstall phyton >= 3.6.0
```bash
Python 3.7.0
```
Jika sudah, hal berikutnya membuat <b>virtual environment</b> atau <b>virtualenv</b> apa itu ? yaitu sekumpulan tools untuk membuat lingkungan python virtual yang terisolasi (tertutup dan tidak bisa di akses dari luar).
```html
D:\web\telegram-bot>python -m venv D:\web\telegram-bot\venv
D:\web\telegram-bot>venv\Scripts\activate
(venv) D:\web\telegram-bot>pip list
Package    Version
---------- -------
pip        10.0.1
setuptools 39.0.1
```
apa itu <b>pip</b> ? yaitu manajemen paket pada python.

API pada telegram menggunakan metode HTTP POST GET maka kita akan mengambil paket requests untuk menjalankan HTTP URL untuk melakukan request dan response.
```bash
pip install requests==2.21.0
```

Kita akan membuat run.py untuk menjalankan bot api tsb. Ok kita buat class TelegramBot dengan menggunakan paket requests
```bash
import requests
import json

class TelegramBot:
	def __init__(self, url, token):
		self.request = requests.session()
		self.url = url + '/bot' + token
	
	def send(self, method, params):
		host_url = self.url + '/' + method
		response = self.request.get(host_url, data=params);
		res_json = json.loads(response.text)
		
		return res_json['result']

host = 'https://api.telegram.org'
token = 'xxx'

telegram = TelegramBot(host, token)
last_update = []
last_update = telegram.send('getUpdates', {})
```
jalankan dengan
```bash
py run.py
```
maka last_update menghasilkan data json hasil dari API Telegram, lakukan hingga bisa melakukan interaksi dengan bot seperti berikut.

<img src='https://gitlab.com/maulana20/telegram-bot/-/raw/master/screen/telegram.png' width='350' height='350'>&nbsp;&nbsp;&nbsp;<img src='https://gitlab.com/maulana20/telegram-bot/-/raw/master/screen/command.png' width='350' height='350'>

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://gitlab.com/maulana20/telegram-bot) tersebut
