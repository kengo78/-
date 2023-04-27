# typescriptについて

## Promise, await, asyncについて
### Promise
非同期処理を簡単に行うためのもの

### await
非同期処理が終わるまで待つもの

### async
その関数が非同期処理か、普通の関数か区別するためのもの

以上を用いることで、以下を簡単に記述することができる
1. 非同期の処理を簡単に記述できる(コールバックから地獄の解放
2. 複数の非同期処理を同時(並列)に走らせる

### 残余引数/可変長引数 (rest parameter)
通常の関数は引数の数が決まっています。JavaScriptでは引数の数に決まりがない関数も作れます。引数の個数が決まっていない引数のことを可変長引数といい、特にJavascriptでは、可変長引数のことを残余引数という。
```Javascript
function func(...params) {
  console.log(params);
}
func(1, 2, 3);
```
