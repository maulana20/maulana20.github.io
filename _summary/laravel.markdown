1. collection
#### sample collection function
```bash
collect($files)
    ->reject(fn (string $file) => in_array($file, $tasks))
    ->each(fn ($file) => Storage::disk('public')->delete($file))
```
menggunakan operations (max, avg, sum)
```bash
collect->avg('age')
```
​
#### sample collection model eloquent
sample manipulasi data
```bash
$product->where('name', '=', 'xxx')->firstOrFail() // findOrFail
$product->updateOrCreate($data)
$product = Product::firstOrNew(['name' => 'xxx'])
if ($product->exists) $product->fill($data)->save()
```
sample kondisi menggunakan where
```bash
$query->whereRaw('TIMESTAMPDIFF(DAY, created_at, updated_at) > ?', 30)
$query->whereRaw("CONCAT(first_name, last_name) = $fullName")->get()
$query->where('preferences->dining->meal', 'salad')
$query->whereJsonContains('options->languages', ['en', 'de'])
$query->whereJsonLength('options->languages', '>', 1)
```
​sample kondisi menggunakan when
```bash
$query->when(true, fn ($query, $search) {
    $query->whereHas('comments', fn ($query) use ($search) {
        $query->where('comments.body', 'LIKE', '%' . $search . '%');
    });
});
```
umum
```bash
$query->latest('updated_at')->get() // latest, oldest
$query->increment() // +1
$query->explain()->dd() // detail dd
$query->touch() // update timestamps
$query->orderBy('published_date', 'asc')
```

3. attribute
sample ubah pada attribute value
```bash
use Illuminate\Database\Eloquent\Casts\Attribute;

// set only once and never updated again
protected function email(): Attribute
{
    return Attribute::make(
        set: fn ($value, $attributes) => $attributes['email'] ?? $value,
    );
}

protected function title(): Attribute
{
    return new Attribute(
        get: fn ($value) => strtoupper($value),
        set: fn ($value) => strtolower($value),
    );
}

protected function createdAtFormatted(): Attribute // get format date
{
    return Attribute::make(
        get: fn ($value, $attributes) => $attributes['created_at']->format('H:i d, M Y'),
    );
}
```
sample ubah pada attribute menggunakan cast
```bash
// example store json retrieve db used array
protected $casts = [ 'images' => 'array' ];
```
[custom](https://github.com/LaravelDaily/laravel-tips/blob/master/db-models-and-eloquent.md#custom-casts)
​
