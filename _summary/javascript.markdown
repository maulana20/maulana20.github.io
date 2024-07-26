1. array
```bash
array.findIndex(value => value.id === id)
array.splice(index, 1) // remove
array.concat(array)
[...array, object] // include
```
​
2. object
```bash
{ ...object, name: "change name" }
{ ...object, [prop]: value }
const { name } = object
```
​
3. filter
```bash
item.startsWith("group-")
item.includes("group-")
item.indexOf("group-")
```
​
#### umum
```bash
int + "" // string
```

#### folder alias
webpack.config.js
```
module.exports = options => ({
  ...
  resolve: {
    ...
    alias: {
      "@ot-components": path.resolve(__dirname, "../src/components/")
    }
```
.eslintrc
```
{
  "rules": {
    ...
    "settings": {
      "import/resolver": {
        "eslint-import-resolver-custom-alias": {
          "alias": {
            "@ot-components": "../src/components"
          }
        }
      }
    }
```
jsconfig.json
```
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@ot-components/*": ["./src/components/*"]
    }
  },
  "exclude": ["node_modules", "build", "coverage", "dist", "lib"]
}
```
