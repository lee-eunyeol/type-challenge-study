# TupletoUnion<T>

<aside>
💡 **TupletoUnion<T> 는 튜플타입인 T의 값들을 유니온 타입으로 가져온다.**

</aside>

## 해결과정

### 해결

```tsx
type Arr = ['1', '2', '3']

type TupleToUnion<T extends any[]> = T extends (infer A)[] ? A : never
type Test = TupleToUnion<Arr> // expected to be '1' | '2' | '3'
```

> 크게 어렵진 않았다.
> 

### 다른 풀이

```tsx
type Arr = ['1', '2', '3']

type TupleToUnion<T extends any[]> = T[number]
type Test = TupleToUnion<Arr> // expected to be '1' | '2' | '3'
```

- `T[number]` 로 값 타입들에 접근하는 방식이다.