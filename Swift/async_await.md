# async, await

## さいしょの async

```Swift
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
- async の付いた関数は、async な関数か、Task { } の中でしか呼べない
- async の付いた関数は、呼び出し時 await をつけないと呼べない
<br>

## 非同期に処理する

```Swift
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
A → X → B → Y になる
<br>
<br>
<br>

### 非同期に処理する2

```Swift
func fetchA() async -> String {
    try? await Task.sleep(nanoseconds: 1_000_000_000)
    return "A"
}

func fetchB() async -> String {
    try? await Task.sleep(nanoseconds: 1_000_000_000)
    return "B"
}

func runInParallel() async {
    print("Start")

    // async let で並行に開始
    async let resultA = fetchA()
    async let resultB = fetchB()

    // 両方の結果を同時に待つ（並行に待機）
    let (a, b) = await (resultA, resultB)

    print("Results: \(a), \(b)")
}
```
<br>
<br>

## UIの更新
UIKit（iOS）や AppKit（macOS）の内部はスレッドセーフ（＝複数スレッドから同時アクセスしても壊れない）に設計されていない。
@MainActor を使うことで「この関数はメインスレッドで実行せよ」と明示することができる。

### 関数の中
```Swift
func fetchUserData() async {
    let user = await loadUserFromNetwork()

    await MainActor.run {
        self.label.text = user.name
    }
}
```
### 関数自体を指定
```Swift
@MainActor
func updateLabel() {
    label.text = "Hello" // ✅ メインスレッドで安全に実行される
}
```
<br>

## タスクのキャンセル
```Swift
func cancellableTask() async {
    for i in 1...10 {
        if Task.isCancelled {
            print("キャンセルされました")
            return
        }
        print("処理中 \(i)")
        try? await Task.sleep(nanoseconds: 300_000_000)
    }
}
```
Task.cancel() を呼んでキャンセルする。
