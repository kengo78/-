## Go言語についての学んだこと

- ファイルの整形
```go
go fmt "ソースファイル名"
```

- Goファイルのコンパイル
```go
go build -o "実行ファイル名" "ソースファイル名"
```

- コンパイルと実行を同時に行う
```go
go run "ソースファイル名"
```

- 型宣言
```go
//int型からMyIntegerを宣言
type MyInteger int

//MyInterger型の変数をを作成
var i MyInteger = 123

//int型と同様に演算ん可能
i += 1

pmt.Println(i)
//出力 124

//構造体の宣言
type mystruct struct {
    a int 
    b int
}
```
Go言語のソースファイルは「パッケージ」という単位で、グルーピングされて、各パッケージには、1つ以上のソースファイルが所属する。  
ソースファイルは、同一パッケージに所属している別のソースファイル内で、宣言された定数、型、変数、関数といった識別子にアクセスすることができる。  
関数ないで定義したローカルな変数については、同一パッケージ内でも参照ができない。

ソースファイルは必ずいずれかのパッケージに所属する必要がある。その際の宣言方法は以下の通り。
```go
package "パッケージ名"
```
パッケージ名は、すべて小文字かつ1単語で構成されることが推奨されている。

変数の宣言の際に、先頭を大文字にすることで、パッケージ外で、宣言された変数にアクセスできるようになる。

- importしたパッケージに任意の名前をつける
```go
import "任意の名前" "packageのpath"
```
- 未使用のimport
これは、コンパイル時にエラーが起きてしまうので、ブランク識別子を用いて
```go
import _ "package path"
```

- 独自パッケージを使用する際の注意点
ディレクトリの最上位パスをフルパスで環境変数「GOPATH」に登録する必要がある。

- for文
```go
package main

import "fmt"

func main() {
    for i := 0;i < 5;i++ {
        fmt.Println(i)
    }
    //出力は1,2,3,4,5と一行ずつ出力される。
}
/*
func main(){
    i := 0
    for i< 5 {
        fmt.Println(i)
        i ++ 
    }
}
*/
```
- range式を使用する場合
```go
package main 
import "fmt"

func main(){
    //配列の宣言と初期化
    arr := [...] int {0,1,2,3,4}

    //for 文
    for i:= range arr {
        fmt.Println(i)
    }
}
```

- switch文
```go
package main

import "fmt"

func main() {
    //ループ
    for i:= 0; i< 5; i++ {
        switch i {
            case 0:
                fmt.Println("0")
            case 1,2:
                fmt.Println("1または2")
            default:
                fmt.Println("その他")
        }
    }
}
/*出力は、
0
1または2
1または2
その他
その他
*/
```
## ポインタ
