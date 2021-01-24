---
layout: post
title: Cara Mudah Push Notifikasi Dengan Laravel Firebase
github: https://www.itsolutionstuff.com/post/laravel-firebase-push-notification-tutorialexample.html
image: data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkGBxMQEBASEhIVEhAVEBUQEBIQEBsVEhIZGBoWFxUSExYYHyggGBoxHhUTIzEhJik3Li4uFx8zODMvOigtLisBCgoKDQ0NGBAQFzclHx43Nzg3Nzc3NTY1Nys3KzcrNjYtNzI3Ly0rKy4rNDUtLSs1LS0tLTcrKy0rLS0tNS0tLf/AABEIAKABOwMBIgACEQEDEQH/xAAcAAACAwADAQAAAAAAAAAAAAAABAMFBgECBwj/xABHEAABAwEDBwcIBwgCAgMAAAABAAIDEQQSIQUTFTFRU9EiQVKRkpOxBhcyMzRhcXIUFnOBobLBByNCVGKCg7ND4eLwJGOU/8QAGwEBAAIDAQEAAAAAAAAAAAAAAAUGAQMEAgf/xAAwEQEAAQICBgkDBQAAAAAAAAAAAQIDBBEyNFFScbEFEhMVITFykaEUQcEGM1Nhgf/aAAwDAQACEQMRAD8Ar7LlGTNx8oeg3+Buwe5SaSl6Q7DeCQs3oM+RvgFKga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8EaSl6Q7DeCVQga0lL0h2G8FrMmTtfDG50UbnXRVxibU0wqcPcsStdkj1Efw/UoMVZnchnyN8ApLy09h/Z/K6KJ2fjxjY70Xc7QVN5u5t/H2XIMleReWt83c2/j7Lkebubfx9lyDJXkXlrfN3Nv4+y5Hm7m38fZcgyV5F5a3zdzb+PsuR5u5t/H2XIMleReWt83c2/j7Lkebubfx9lyDJXkXlrfN3Nv4+y5Hm7m38fZcgyV5F5a3zdzb+PsuR5u5t/H2XIMleReWt83c2/j7Lkebubfx9lyDJXkXlrfN3Nv4+y5Hm7m38fZcgyV5F5a3zdzb+PsuR5u5t/H2XIMleReWt83c2/j7Lkebubfx9lyDJXkXlrfN3Nv4+y5Hm7m38fZcgyV5F5a3zdzb+PsuR5u5t/H2XIMleReWt83c2/j7Lkebubfx9lyDJXkXlrfN3Nv4+y5Hm7m38fZcgyV5F5a3zdzb+PsuR5u5t/H2XIMleReWt83c2/j7Lkebubfx9lyDJXlzVa3zeTb+PsuXSfyBnaxzhLG4hpIaA4VpzVKDLVXKia6qkCDla7JHqI/h+pWRWuyR6iP4fqUG3yV7PB9jH+UJpK5K9ng+xj/KE0ssBCEIBCEIBCEIBCEIBCEIBCEIBCEIBCEIBCEIBCEIBCEIOkszWCrnBo1VJouwKXt1nLwKUBBJBNQRhSoI/9KQlya/EhwLjQAtFKcxcfur1oLSSdrTQuANL2J5tqI52u9FwOFcDXDV+ijnsoLKCgIDQ0kdEggH3YJN2TXlxfebeJJIobtTXwqEFooxM0uLbwvDW2uPUq6y5Ocx7KmrQS51PRwpcHXeOpSS5PeS6jwGkudTHG9zH3e9BYrrfFbtcaVp7tVVWaMd0gMDSlat9LkM/p5Q6lHHk17mmtGVPo81Kg058MEFsyVriQDUg0d7l2caAn3VUUEVwNApgKOPOTtrzri2QX20Bo4EOaTqqNvu1j70C+SMo59rjdu0dTXWtdSbn9B/ynwKrclWG6a3bjWudRtSSXYtvVIHJpWnxVlP6D/lPgUHhUBwHwCnalLOeSPgE01YZSLXZI9RH8P1KyK12SPUR/D9Sg3WSonfR4MP+CP8AKE1mnbPBMZGaPo1nwHqI+b+kJu4Ng6kFZmnbPBGads8FZ3BsHUi4Ng6kFZmnbPBGads8FZ3BsHUi4Ng6kFZmnbPBGads8FZ3BsHUi4Ng6kFZmnbPBGads8FZ3BsHUi4Ng6kFZmnbPBGads8FZ3BsHUi4Ng6kFZmnbPBGads8FZ3BsHUi4Ng6kFZmnbPBGads8FZ3BsHUi4Ng6kFZmnbPBGads8FZ3BsHUi4Ng6kFZmnbPBGads8FZ3BsHUi4Ng6kFZmnbPBGads8FZ3BsHUi4Ng6kFZmnbPBGads8FZ3BsHUi4Ng6kFZmnbPBGads8FZ3BsHUi4Ng6kFZmnbPBGads8FZ3BsHUi4Ng6kFZmnbPBGadsT8z2sFSOemA6z8KVUhaKah1IKzNO2eCM07Z4JwKuyrl2z2UtE0oY52IbQudTbRoNB70Euads8EZp2zwU9mtDJWNexwexwq1zTUFSoE807Yo7RE64/D+F3gVYKO0eg/wCR3gUHztZvRb8Am2JSy+i35Qm2IJFrskeoj+H6lZFa7JHqI/h+pQem5G9ms/2Ef5QnFXZHn/8Aj2fA+oj2dEe9N/SBsP4cUEyFD9IGw/hxR9IGw/hxQTIUP0gbD+HFH0gbD+HFBMq3L+VxZIs4Wl/KDboNNfPVOfSBsP4cVmP2gS1swwPpjZt+K924ia4iXPirlVuxXXT5xEl/OCzcO7wcEecFn8u7vBwWBQpD6a3sVTvjGb3xDfecFn8u7vBwR5wW/wAu7vBwWBQn01vYd8Yze+Ib7zgs3Du8HBHnBZ/Lu7wcFgUJ9Nb2HfGM3viG+84LP5d3eDgtNkXKP0mBkwbdDr3JJqRRxbr+5eNr1XyH9gg/yf7HrRiLNFFOcQk+isffxF+abk5xls/uF7ijFIWPLcEtLkgJJYLtCHAyMzkdWkVFW4iqeEg11FPiuNYHOKMUgMtwXzHnOWH5uha4VdeDKNJFHcpzQSNRIqmLVbGRsdI53IaxzzdF40bi4gDE/cgnxRioPpsedEN8Z4x54M/iuAht/wCFSApc4No6/vKDtijFcF4HOOtGcG0c/Ps1oOcUYqGK1scXgOBLHXH+40a6nU9vWuG22MuLQ8Ei9WmoXaBwJ1A8oYHFBPijFcGQY4jDXjq58dijhtbHhxa4G68xu5qOBukY+8EIOrLMA5zqA12jHHXjs1YLmCz3L1KYnGgoBsAClzg2jXTXz7PxCgmt0bDRzsc2+WgBcbsZaHkADGhc3DXig75o7QszlXySdNNNLfiN8wuYJYC8x5sgloN4chwDgRz1WnltLGi85zWtvBpJIABcQGj4kkD713vjaNmv8PxHWgqchZGNmZIy80h075WhrLrWB1KMaK6hT8U1bbBnW3S97Ma1ikdG7nwq3GmOpONeDqIPwK7IM3ZsnvjtIAzz2N1vfbnObi064na8eKt7R6D/AJHeBQT+8k/t8EWg8h/yO8Cg+drL6LflCbYlLL6LflCbYgkWuyR6iP4fqVkVrskeoj+H6lB6XkaMfRrPgPUR839ITeabsHUlsjezWf7CP8oTiDpmm7B1IzTdg6l3Qg6ZpuwdSM03YOpd0IOmabsHUsv+0FgFmFAByxqC1ayv7Q/Zh84Wy1p0uXHatc4TyebJ/INmbLaYY3irHOo4VpXAmlfuSCtfJb2yz/OfAqUr0ZUnDRE3qIn7zHNa2y1WCKSSM2RxLHlhIfgaGlRylDpGwfyb+3/5LU2izRl7iWRklxJJst4/eef4qP6LF0Iv/wAf/ShZqxG++j02uisozw/j/igsVpsEsjIxZHAveGAl+AqaVPKVJl6zNitM0bBRjXUaK1pUA0r9631ns0Ye0hkYN4UIst0/c7m+Kw/lT7ZaPnH5QuzBzc60xXVmr36ht4SLVE4e31fH8Sql6r5D+wQf5P8AY9eVL1XyG9gg/wAn+x634vQjijegtZq9M84LM8jIixgke/OBoa90TrgeMwLOWUoeTRoeOcO1GhIPdnkbAHRuvPqwtNAQGuIeXuLhTG9W6fcEWjLk0L332ska20mAiJt11BZjaS/lvpXU2nHBuPyjjc20uuSXYGSPJLKXxGXteGE4E1jd1j30jlsLyeSUTpJXmSSsjy8hpa3W9shFQ2pxbQEnAE01pGfyL5dY5G0zUjBnIhyXPZJHfaGBobhJzU/j136iwn8p2RFwkjeLokcaAGlxrnXMDi6jHfHmwDiGHZdaIWyZt9XPkZcdRjgYw8vJvkClI3EfdqxoHY5DZ9IFovyZ0OBHL5F0MMebuai3lOdtqdfMqyyeQ1mjzQF4tja1l03brgGQRkuAaBUizsJPvPuo0fKG5A6aSMlpnlhibGAXOuFwYDU+k4sI5sXAe9Ry+VTCDmmOfi268j92+9dLSH6qFjg4GvOEBZvI+Fkb4y+SQPdA95kLXFxhkbLU8mnKeC52GJcaUwouPIWARtjEkgYGXQBcGOZjgLvR1lsdT73FWkuXWtjY+441MocKtq3Mlwk1nlei6lNaif5SRgsFx5vBhJwowPLxV+PJpcNScMRigXtPkbA90rg57RIWEsbTNtuBgYGtpRo5JqBrrj6LaSHyThLgSSWh7n3C1hbynRPIPJxxiGvafdSWw5dvwCR0bg+7CbjS3lZ66GFprgKnnxwUU3lMAOTE4uzgho5zQBJS85mvUGgm9qqKIFcm+R4ibOx0l5rzFddcGcGaeZGBxIoRWlQRQkuOF6gktnkbDIyRucezOXhI5gYHOvGQ67uFM4aU1UA1VB5s3lK50rmmOorciDaAvIEBJcS6jR+/GH9OvGi5tHlU0VDIySMbxc0tpiHEFpIcQRSgP3hB2d5IQFxdV1cTgG4OLnPzg5Pp1dr9wRZ/JGFkcjGufR8M0BNRW7KImlxJGLgIm0J96k+sjcAInuJLwyhaL1zOXzi7k4xO168PfSa2eUEcTo23XOvsa/k05IcHXLwrhW44VNB8aGgQt8loQ2RoJF98ch5LPSjmfaGupdoTefQ11gBKzeREDhTOSAgktc24HDCrcbuLg8RyXjiXRMqTShcn8pGMswtBY+hc9pjFM4CwPc4XTjWjHGlKjnoKkNZOyqJ3vaGObdvXXOpR4a98biKEkYsOvmIQL5L8nYrM8PiJbQFpaA2j2mlGuNKmlBTFXKEIF2MBe+oB9Hm9y5tUYzb8B6Dub3Fcxem/+3wXNq9W/wCR3gUHzdZfRb8oTbEpZfRb8oTbEEi12SPUR/D9Ssitdkj1Efw/UoPTcjezWf7CP8oTiTyN7NZ/sI/yhOIBCEIBCEIBZX9ofsw+cLVLK/tD9mHzhbLWnS5cdqtzhPJ5srXyW9ss/wA58CqpWvkt7ZZ/nPgVKXNCVKwv79vjHNtrTHPfddc67eNP3gGHNhVTxh9xocXl1XVuygH3VPOus5bed6qt4643E/eV0qz/AOrunKJXmm1FNWeZiIOvD1msa5gR94515/5U+2Wj5x+UL0Gz2b0XARUwNQwg/dVefeVPtlo+cflC6cLpyiOndXp4/iVUvVfIb2CD/J/sevKl6r5DewQf5P8AY9bsXoRxcHQWs1emecF7f5TRBpMMX0g33Xhg0YRycutDWojLdtPdSrVmyxZnl4Yy89xDZWxxXi/BwJNBygLj9eOrDlCr4yVDj+7biSThtDgQNgo9+Aw5R2rh+R4DWsTTV141/uw+HLfydXKdhiVHLYrocs2d/LfGGO1C8y86js0HVIGHrWVoThjzGksOU7M+zhzGB0QkbG2NsQPKddLLrdX8bTXmqa0INHm5LhBac0yrXmVpLa3XFpYXCuo3XOb8DRdocnxMaGtYA2+H0/qFLpx2BrQNgAHMgrY/KKyuzbcRnHAsDo6HlZtzZKHHHOxnbia0oaRx5asbyKMvH1OEIN1oMOBI1N/fw4c1dWBpZjJMHJ/dN5NLtBqoGgD3j93HgegNi4hyPAwUbE0YU1V6GGP2UQ+DG7EFfLlCzPhinEd6OOZkTBdAERe5jL104Cl4GmsUIwNQp2WqzuaX5rESs5JhAkMjqOY4Cmsh4NeaprShTbMlwtYYxG24XteW01ubduk/C4ymwNA5lyzJkQYYxGAwuDiBtFLprrqLrabLopqQVVh8oIHtiJZmw5sd68wgMLhE5jK0oQM9HjhQke+k9kynZZnPDWtLhES+9GK3MC9pwqMXCoPOTroU3oez3DHmWZssMZZdF26WtYW02XWMH9oUzbDGHPcGC88EOO0GlcOatBXbQV1IKcZbsj7zLlTRt6Mw8o381daW7SHwnHDV0TTnTFjvPF1t6l6QGMA1F03X11EcnE4CmvBP2jIsL61ZQksJLcDyCwj/AFsFddGgVwC7OyPAf+JuoAUqKXaXXCmpwut5WvAYoEYcqwuZNLHDUNdFiGNBkLw0Aj4B9DX3qG3ZfszQ15jvPzL3wtdGA5wY2SSja4gERPNdWA2ituzJkLWuYI2hrgGuaNRA1ffjr+GxdJMjwOIJiaaNuCowAuuZSnyve2uxxHOgqrBlWKRubfZg27I4MhazOUuPkjdJdugAVY7VU4jnNFoGRNGpoHwFOeviSUq/JUJ1xN9IuOGskuca7QS95I57xTbGBoAGoakHZCEIIYvTf/b4Lm1erf8AI7wK4i9N/wDb4Lm1erf8jvAoPm6y+i35Qm2JSy+i35Qm2IJFrskeoj+H6lZFa7JHqI/h+pQem5G9ms/2Ef5QnEnkb2az/YR/lCcQCEIQCEIQCyv7Q/Zh84WqWV/aH7MPnC2WtOly47VrnCeTzZTWS0uie2Rho5pq00r+ChQpafFRIqmmYmPs0P1ytW1nd/8AaPrlatrO7/7WeQtfY29jq7wxX8ktD9crTtj7v/tUlrtLpXukeavcak0p1BQoXqmimnyhqu4m9djKuqZgL1XyG9gg/wAn+x68qXqvkN7BB/k/2PWjF6EcUp0FrNXpnnC+Qq02GTUHYXHCl8ihNDzDVyfxXdsMtSb2F40BedVXUOAwwLcPdXFRy2H0JJ1meXB1RUOvUvEV1gg0Gy52feomWOWrXFwqCK4nEVfyakbHDH3ILJCQZZ5cKvwwBo419LHmxJHPghtnmqKvBFW15RqaDHmp93PVA+hJOhlP8QGNfSNBswpzaqc+vBd7JC9p5T7wpQ41xo3EYbb/AFj7gaQhCAQhCAQhCAQhCAQhCCGL03/2+C5tXq3/ACO8CuIvTf8A2+C5tXq3/I7wKD5usvot+UJtiUsvot+UJtiCRa7JHqI/h+pWRWuyR6iP4fqUHpuRvZrP9hH+UJxJ5G9ms/2Ef5QnEAhCEAhCEAlMpZPZaGXJBVtaptCMTETGUs99T7N0UfU+zdFaFC9dera19ha3I9oZ76n2boo+p9m6K0KE69W07C1uR7Qz31Ps3RR9T7N0VoUJ16tp2Frcj2hnvqfZuim4MhtjaGskkYwamtkIaK4mgB2kq2QsTVM+cvVNuimc6aYhW6KO+l713FGijvpe9dxVkhYe1boo76XvXcUaKO+l713FWSEFboo76XvXcUaKO+l713FWSEFboo76XvXcUaKO+l713FWSEFboo76XvXcUaKO+l713FWSEFboo76XvXcUaKO+l713FWSEFboo76XvXcUaKO+l713FWSEFboo76XvXcUaKO+l713FWSEFboo76XvXcUaKO+l713FWSEENms9wUqXHnLjUn4krm1erf8jvAqVRWr1b/kd4FB83WX0W/KE2xKWX0W/KE2xBItdkj1Efw/UrIrXZI9RH8P1KD03I3s1n+wj/KE4qnJGUYRZ7ODNGDmY/8Akb0R705pKHfR943igaQldJQ76PvG8UaSh30feN4oGkJXSUO+j7xvFGkod9H3jeKBpCV0lDvo+8bxRpKHfR943igaQldJQ76PvG8UaSh30feN4oGkJXSUO+j7xvFGkod9H3jeKBpCV0lDvo+8bxRpKHfR943igaQldJQ76PvG8UaSh30feN4oGkJXSUO+j7xvFGkod9H3jeKBpCV0lDvo+8bxRpKHfR943igaQldJQ76PvG8UaSh30feN4oGkJXSUO+j7xvFGkod9H3jeKBpCV0lDvo+8bxRpKHfR943igaQldJQ76PvG8UaSh30feN4oGkJXSUO+j7xvFGkod9H3jeKBpCV0lDvo+8bxRpKHfR943igaQldJQ76PvG8UaSh30feN4oGlFavVv+R3gVFpKHfR943iorVlKG4/99H6Dv8AkbsPvQfPFl9FvyhNsSVmkF1uI1DnTTJW9IdYQTrXZI9RH8P1Kx2db0h1hbDJDxmI8R6O33lB/9k=
language: php | Laravel
---

### 1. Menambahkan File Credential
Di sini kita akan menambahkan env firebase bedasarkan donwload apps berupa credential json yang kita daftarkan dari firebase console
```html
FIREBASE_CREDENTIALS=firebase-credential-demo.json
```

### 2. Membuat Firebase Notification
Pada langkah ini kita akan menambahkan request permission, mengambil token, dan menampilkan notifikasi pada browser.

Buat file pada public\js\firebase.js dan masukan script di bawah ini.
```bash
var firebaseConfig = {
	apiKey: "xxx",
	authDomain: "firebase-demo.firebaseapp.com",
	projectId: "firebase-demo",
	storageBucket: "firebase-demo.appspot.com",
	messagingSenderId: "12345",
	appId: "1:12345:web:12345abc",
	measurementId: "G-N8EHJ1Y15R"
};
  
firebase.initializeApp(firebaseConfig);
const messaging = firebase.messaging();
messaging.requestPermission().then(function () {
	return messaging.getToken({ vapidKey: '*public-key' })
}).then(function(token) {
	console.log(token);
	$.ajaxSetup({ headers: { 'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content') } });
	$.ajax({
		url: 'api/firebase/register',
		type: 'POST',
		data: { token: token },
		dataType: 'JSON',
		success: function (response) {
			console.log('Token has storing.');
		},
		error: function (err) {
			console.log('Token Error: ' + err);
		},
	});
}).catch(function (err) {
	console.log('Token Error'+ err);
});
  
messaging.onMessage(function(payload) {
	const noteTitle = payload.notification.title;
	const noteOptions = {
		body: payload.notification.body,
		icon: payload.notification.icon,
	};
	new Notification(noteTitle, noteOptions);
});
```

Lalu kita panggil pada home.
```script
<script src="{{ asset('js/firebase.js') }}" defer></script>
```

### 3. Membuat Controller Firebase 
Pada langkah ini kita akan membuat controller firebase untuk menyetor token dan membuat send notification. Untuk menyetor token di sini kita menggunakan cloud message yang sudah di sediakan, untuk lebih lanjut kalian bisa kunjungi tutorial di sini [kreait/laravel-firebase](https://github.com/kreait/laravel-firebase).

```html
php artisan make:controller FirebaseController
```

Kemudian tambahkan script di bawah ini.
```html
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Kreait\Firebase\Messaging\CloudMessage;
use Kreait\Firebase\Messaging\WebPushConfig;

class FirebaseController extends Controller
{
    public function register(Request $request)
    {
        $messaging = app('firebase.messaging');

        $topic = 'testing';

        $result = $messaging->subscribeToTopic($topic, $request->token);

        return response()->json(['status' => $result[$topic][$request->token] ?? 'OK']);
    }
    
    public function sendNotification(Request $request) {

        $messaging = app('firebase.messaging');

        $topic = 'testing';

        $message = CloudMessage::withTarget('topic', $topic);

        $config = WebPushConfig::fromArray([
            'notification' => [
                'title' => $request->title,
                'body' => $request->body,
                'icon' => asset('favicon.ico'),
            ],
            'fcm_options' => [
                'link' => url('/'),
            ],
        ]);

        $message = $message->withWebPushConfig($config);

        $messaging->send($message);
    }
}
```

Lalu tambahkan route pada api.
```html
Route::post('firebase/register', 'FirebaseController@register')->name('firebase.register');
Route::post('firebase/send-notification', 'FirebaseController@sendNotification')->name('firebase.send-notification');
```

### 4. Membuat Form
Pada langkah ini kita akan membuat form.blade.php untuk mengetes pada push notification.
```script
@extends('layouts.app')

@section('title', 'Form Push Notification')

@section('content')
<div class="card-body">
	@if (session('status'))
		<div class="alert alert-success" role="alert">
			{{ session('status') }}
		</div>
	@endif
	<form action="{{ route('firebase.send-notification') }}" method="POST">
		@csrf
		<div class="form-group">
			<label>Title</label>
			<input type="text" class="form-control" name="title">
		</div>
		<div class="form-group">
			<label>Body</label>
			<textarea class="form-control" name="body"></textarea>
		  </div>
		<button type="submit" class="btn btn-primary">Send</button>
	</form>
</div>
@endsection
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://www.itsolutionstuff.com/post/laravel-firebase-push-notification-tutorialexample.html) tersebut.
