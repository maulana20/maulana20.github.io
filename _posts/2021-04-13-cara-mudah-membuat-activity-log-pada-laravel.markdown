---
layout: post
title: Cara Mudah Membuat Activity Log Pada Laravel
github: https://spatie.be/docs/laravel-activitylog/v3/installation-and-setup
image: https://www.tutsmake.com/wp-content/uploads/2020/11/Laravel-8-User-Activity-Log.jpg
language: php | Laravel
---

### 1. Menambahkan Depedency
Di sini kita perlu menginstall depedency dengan menjalankan perintah.
```bash
$ composer require spatie/laravel-activitylog
$ php artisan vendor:publish --provider="Spatie\Activitylog\ActivitylogServiceProvider" --tag="migrations"
$ php artisan migrate
$ php artisan vendor:publish --provider="Spatie\Activitylog\ActivitylogServiceProvider" --tag="config"
```

### 2. Menambahkan LogsActivity Pada Model
```bash
use Spatie\Activitylog\Traits\LogsActivity;
use Spatie\Activitylog\Models\Activity;

class Announcement extends Model
{
    use HasFactory, LogsActivity;
    
    protected static $recordEvents = ['created', 'updated'];
    
    protected static $ignoreChangedAttributes = ['updated_at'];
    
    protected static $logFillable = true;
    
    protected static $logOnlyDirty = true;
    
    public static $logName = 'announcement';
    
    public function getDescriptionForEvent(string $eventName): string
    {
        if ($eventName == "created") {
            return Auth::user()->name . " created for announcement";
        } elseif ($eventName == "updated") {
            return Auth::user()->name . " updated for announcement";
        }
        
        return "You have {$eventName} announcement";
    }
    
    public function tapActivity(Activity $activity)
    {
        if (!empty(request()->note)) {
            $activity->properties = $activity->properties->merge([
                'note' => request()->note,
            ]);
        }
    }
}
```
note : pada `getDescriptionForEvent` merupakan custom pada description berdasarkan event nya, `tapActivity` merupakan kebutuhan jika ada tambahan pada properties.

### 2. Menampilkan Activity Pada Controller
```bash
use Spatie\Activitylog\Models\Activity;

    public function edit(Announcement $announcement)
    {
        $activities = Activity::forSubject($announcement)->get();
        
        //
    }
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://spatie.be/docs/laravel-activitylog/v3/installation-and-setup) tersebut.
