# PerMutation<T>

<aside>
💡 PerMutation<T>는 T 유니온 타입의 각각 요소들을 순서를 번갈아가며 리스트형태의 유니온타입으로 반환한다.

</aside>

## 풀이과정

## 실패

> 유니온타입을 분리하여 원하는 형태로 번갈아 가며 리스트형태로 만드는 방법을 구상하지 못했다..
> 

## 풀이

참조 : [hhttps://github.com/type-challenges/type-challenges/issues/614ttps://github.com/type-challenges/type-challenges/issues/614](https://github.com/type-challenges/type-challenges/issues/614)

```graphql
type Permutation<T, K=T> =
    [T] extends [never]
      ? []
      : K extends K
        ? [K, ...Permutation<Exclude<T, K>>]
        : never

type perm = Permutation<'A' | 'B' | 'C'>; // ['A', 'B', 'C'] | ['A', 'C', 'B'] | ['B', 'A', 'C'] | ['B', 'C', 'A'] | ['C', 'A', 'B'] | ['C', 'B', 'A']
```