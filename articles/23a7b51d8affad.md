---
title: "ReadonlyMapを活用する"
emoji: "🔖"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ['asobi']
published: false
---

# ReadonlyMapなんて便利なものがあったのか！！

- ObjectをReadonlyにできれば、バグも減るはず！

# `Map`の使い方について

へえぇ。今までこういう「キーバリュー型」をJSで書くときはObject一択と思ってたけど、Mapなんてあったのか‥‥

https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Map

公式の使い方をみてみる

```typescript
let contacts = new Map()
contacts.set('Jessie', {phone: "213-555-1234", address: "123 N 1st Ave"})
contacts.has('Jessie') // true
contacts.get('Hilary') // undefined
contacts.set('Hilary', {phone: "617-555-4321", address: "321 S 2nd St"})
contacts.get('Jessie') // {phone: "213-555-1234", address: "123 N 1st Ave"}
contacts.delete('Raymond') // false
contacts.delete('Jessie') // true
console.log(contacts.size) // 1
```

「お堅いObject」って感じかな？

ただ注意しないといけないのは、Mapを初期化するときにObjectのノリで書いてしまうと、クエリができなくなってしまうらしい

```typescript
// 公式の例
let wrongMap = new Map()
wrongMap['bla'] = 'blaa'
wrongMap['bla2'] = 'blaaa2'

wrongMap.has('bla')    // false
wrongMap.delete('bla') // false
console.log(wrongMap)  // Map { bla: 'blaa', bla2: 'blaaa2' }
```

データで初期化をするときは

- setメソッドを使うか
- コンストラクターの引数に初期データを渡す

の二択みたい

今回は後者を使います
この時もちょっと癖があって、「キー名,バリュー名」を一要素とした「二次元配列」を使って初期化する

```typescript
// 渡すデータは[[key1, value1], [key2, value2], ....]の形
const me = new Map([['name', 'dialbird'], ['age', '24'], ['gender', 'male']])
```

# ReadonlyMapに変換しよう

Mapを作れば、あとはそれをそれ用の方に設定するだけ！

# 作り方

```typescript
const readonlyMe: ReadonlyMap<string, string> = me
```

# 終わりに
いかがでしたでしょうか？

自分も今回初めて知った書き方ですが、`「varよりconst使おうぜ！」`的なノリで、`「Objectより、ReadonlyMap使おうぜ！」`的な文化を作っていこうと思いました！
