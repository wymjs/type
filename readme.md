@wymjs/type
===

> 通用高級類型(我慢慢補~)

## 安裝

```shell
$ pnpm i -D @wymjs/type
```

## 使用

```typescript
import {
  UnionIntersection,
  // ...
} from '@wymjs/type'

// 取 union 交集
// 'a' | 'b'
type UnionAb = UnionIntersection<
  'a' | 'b' | 'c',
  'a' | 'b'
>

// 將 union 轉換成 tuple
// ['a', 'b']
type AbTuple = UnionToTuple<'a' | 'b'>

// 將嵌套物件的 key 取出來
// 'a.b' | 'c'
type DictUnion = RecursiveKeyOf<{
  a: {
    b: string
  }
  c: number
}, '.' /* 二參可選，預設就是 .，此為連接符號 */>

// 將物件的前綴移除
// { name: string; password: string }
type PublicDict = IgnoreKeyPrefix<{
  name: string
  _password: string
}, '_' /* 二參是要砍掉的前綴 */>

// 嵌套物件的 Partial
// { a?: { b?: string }; c?: string }
type PartialObj = DeepPartial<{
  a: {
    b: string
  }
  c: string
}>

// 原生 Pick 增強版，可以將 key 更名以及轉成可選
// {
//    a: string
//    b?: string
//    c2: string
//    d2?: string
// }
type NewObj = BetterPick<
  {
    a: string
    b: string
    c: string
    d: string
  },
  | 'a'      // 就是將 a 取出來
  | '?b'     // 將 b 轉成可選
  | 'c->c2'  // 將 c 更名為 c2 (-> 為更名符號)
  | '?d->d2' // 將 d 更名為 d2 並轉成可選
>

// 首字串變大寫
// 'Apple'
type Apple = FirstUppercase<'apple'>
```
