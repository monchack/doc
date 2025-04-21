# アンラップ

## nil じゃない時だけアクセス

```Swift
let result = someOptional?.property
```

## nil じゃない時だけ処理を行う

```Swift
if let unwrappedName = name {
    // nil じゃなかった
}
```

### どれも nil じゃないことを一度に確認

```Swift
if let first = firstName, let last = lastName {
    // どっちも nil じゃない
} else　{
    // 少なくともどっちかは nil
}
```

## nil の時は処理をやめる

```Swift
guard let unwrappedName = name else {
    // nil だった
    return
}
```

## nil だった時の代替を指定

```Swift
let displayName = nickname ?? "ゲスト"
```
