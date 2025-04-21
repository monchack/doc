# アンラップ

## nil じゃない時だけアクセス

```Swift
let result = someOptional?.property
```

## nil じゃない時だけアクセス

```Swift
if let unwrappedName = name {
    // nil じゃなかった
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
