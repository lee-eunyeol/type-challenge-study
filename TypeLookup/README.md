# TypeLookup

<aside>
💡 Sometimes, you may want to look up a type in a union by its attributes.

In this challenge, we would like to get the corresponding type by searching for the common `type` field in the union `Cat | Dog`. In other words, we will expect to get `Dog` for `LookUp<Dog | Cat, 'dog'>` and `Cat` for `LookUp<Dog | Cat, 'cat'>` in the following example.

</aside>

## 풀이 과정

### 실패

```tsx
interface Cat {
  type: "cat";
  breeds: "Abyssinian" | "Shorthair" | "Curl" | "Bengal";
}

interface Dog {
  type: "dog";
  breeds: "Hound" | "Brittany" | "Bulldog" | "Boxer";
  color: "brown" | "white" | "black";
}

type LookUp<
  T extends { type: string },
  U extends T["type"]
> = T["type"] extends U ? T : never;

type MyDogType = LookUp<Cat | Dog, "dog">; // expected to be `Dog`
```

- `T extends { type: string }`
    - T 라는 유니온 타입 안에서 타입 좁히기를 위해 `{ type: string}` 을 extends 하도록 했다.
- `U extends T["type"]`
    - U는 T타입의 type을 extends하여 좁힐 타입을 쉽게 구분할 수 있도록 했다.

- `문제점`
    - `T["type"] extends U ? T : never`
        - 만약 U가 “dog”일때, `Cat | Dog` 에서 type : “dog”인 Dog 타입만 좁혀 추론해야 한다 생각해 위와 같이 작성했지만 결과는 never 타입을 반환하였다.
            - T[”type”] 은 “cat” | “dog” 를 추론하는데, 이는 “dog”에 포함되지 않기 때문이다

## 해결

```tsx
interface Cat {
  type: "cat";
  breeds: "Abyssinian" | "Shorthair" | "Curl" | "Bengal";
}

interface Dog {
  type: "dog";
  breeds: "Hound" | "Brittany" | "Bulldog" | "Boxer";
  color: "brown" | "white" | "black";
}

type LookUp<T extends { type: string }, U extends T["type"]> = T extends {
  type: U;
}
  ? T
  : never;

type MyDogType = LookUp<Cat | Dog, "dog">; // expected to be `Dog`
```

- 유니온 타입은 조건에 대해 각각 추론되므로 `T extends { type : U }` 를 통해 type : “dog” 를 가진 타입만 T에서 좁힐 수 있게 하였다.

### Recoomend 된 풀이법

```tsx
type LookUp<U, T extends string> = {
  [K in T]: U extends { type: T } ? U : never
}[T]
```