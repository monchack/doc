# プログラミングに関するメモ

# SWift

## async, await

### さいしょの async

```
func test() aynsc {
    await subtest()
}

func test2() {
    Task {
        await subtest()
    }
}

```
- async をつける関数か、Task {} の中で await が使える
 - というか、async の付いた関数は、async な関数か、　Task { } の中でしか呼べない
- test() は、

