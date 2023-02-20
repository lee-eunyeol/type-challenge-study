# TupleToObject<T>

<aside>
💡 TupleToObject<T>는 튜플의 모든 원소들을 기반으로 Object 형태로 변환한다.

</aside>

[type-challenges/README.md at main · type-challenges/type-challenges](https://github.com/type-challenges/type-challenges/blob/main/questions/00011-easy-tuple-to-object/README.md)

## 해결 과정

## 성공??

```tsx
const tuple = ['tesla', 'model 3', 'model X', 'model Y'] as const

type TupleToObject<T extends readonly any[]> = {
  [key in T[number]]: key
}

type result = TupleToObject<typeof tuple> 
// expected { 'tesla': 'tesla', 'model 3': 'model 3', 'model X': 'model X', 'model Y': 'model Y'}
```

- 정답이긴하나 개인적으로 `T extends readonly any[]` 부분에서 T 타입의 집합을 any[]로 표현했는데 any를 쓴 것이 아쉽다고 생각했다.
    - 왜? Object의 key로 할당 될 수 있는 타입은 string, number , symbol이다.
    
    ```tsx
    const tuple = ['tesla', 'model 3', {no : true}] as const
    
    type TupleToObject<T extends readonly any[]> = {
      [key in T[number]]: key
    }
    
    type result = TupleToObject<typeof tuple> 
    // expected { 'tesla': 'tesla', 'model 3': 'model 3', 'model X': 'model X', 'model Y': 'model Y'}
    ```
    
    - 만약 위와 같이, tuple의 원소중 `{ no : true }` 같은 객체 형태가 있다면 이를 키로 이용할 수 없기 때문에 타입 체킹이 정상수행되지 않아야 하는데, `T extends readonly any[]` 는 이를 무사히 통과할 것이다.
        - 결국 `any[]`를 사용함으로써 튜플의 모든 원소를 Object로 변환하지 않는 제네릭 타입을 만든것이다.

### 더 나은 답

```tsx
const tuple = ['tesla', 'model 3', 'model X', 'model Y'] as const

type TupleToObject<T extends readonly PropertyKey[]> = {
  [key in T[number]]: key
}

type result = TupleToObject<typeof tuple> 
// expected { 'tesla': 'tesla', 'model 3': 'model 3', 'model X': 'model X', 'model Y': 'model Y'}
```

- PropertyKey 타입은 object의 키가 될 수 있는 string | number | symbol 유니온 타입이므로 이를 활용하면 좀 더 나은 결과를 낼 수 있게 되었다.
    - 아까와 같은 문제의 경우 타입에러를 잡아낼 수 있게 되었다.
    
    ```tsx
    const tuple = ['tesla', 'model 3', {no : true}] as const
    
    type TupleToObject<T extends readonly PropertyKey[]> = {
      [key in T[number]]: key
    }
    
    type result = TupleToObject<typeof tuple>
    //Error Type '"tesla" | "model 3" | { readonly no: true; }' is not assignable to type 'PropertyKey'. 
    ```