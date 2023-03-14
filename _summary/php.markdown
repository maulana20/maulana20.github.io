1. array
menggunakan map
```bash
array_map(function($item) {
    return $item["name"];
}, $array);
```
filter berdasarkan left char
```bash
array_values(array_filter($array, function($item) {
    return str_starts_with($item["name"], "group-"); // php 8
}));
```
menambahkan index value
```bash
array_walk($array, function(&$value, $key) {
    $value["test"] = true;
});
```
declare variable pada array
```bash
[, $array01, $array02] = [array];
​```

#### umum
```bash
sprintf('id in ("%s") and category in ("%s")', $ids, $categories);
$name = $_GET['name'] ?? $_POST['name'] ?? 'nobody'; // if > elseif > else
```

#### konfigurasi manual
sample default value dan ubah type data
```bash
private const SETTINGS_SCHEMA = [
    "color-scheme" => [ "name" => "color_scheme", "type" => "intval", "default" => 1 ],
];
foreach (static::SETTINGS_SCHEMA as $schema) {
    $data[$schema["name"]] = $schema["default"];
}
foreach ($result as $value) {
    $name = $value->name;
    if (array_key_exists($name, static::SETTINGS_SCHEMA)) {
        $schema = static::SETTINGS_SCHEMA[$name];
        $data[$schema["name"]] = $schema["type"]($value->value);
    }
}
​```
sample function konfigurasi array
```bash
function config(): array
{
    return [ 'foo' => 'bar' ];
}

class Configuration
{
    private $configuration = [];
    
    public function __construct(array $configuration)
    {}
    
    public function get(string $key): ?string
    {
        return $this->configuration[$key] ?? null;
    }
}
```
​
sample function init
```bash
public function __construct(User $user)
{
    $this->user = $user;
    $this->auth = new UserAuth($user);
}
```
