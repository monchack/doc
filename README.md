# プログラミングに関するメモ

# SWift

## async, await

### さいしょの async

```
func fetchData() async {
    // 非同期処理
}

// ❌ 非 async コンテキストでは呼び出せない
func someFunction() {
    fetchData() // エラー
}

// ✅ async コンテキストなら呼び出せる
func someAsyncFunction() async {
    await fetchData()
}

// ✅ Task を使えば非 async 関数内からも呼び出せる
func someFunction() {
    Task {
        await fetchData()
    }
}

```
- async の付いた関数は、async な関数か、　Task { } の中でしか呼べない
- async の付いた関数は、呼び出し時 await をつけないと呼べない

### 非同期に処理する

```
func fetchData() async {
    // 非同期処理
}

func test()  {
    print("A")               
    Task {
        print("X")           
        await fetchData()    
        print("Y")           
    }
    print("B")               
}

```
は、fetchData での処理が重ければ
A →　X → B → Y になる
