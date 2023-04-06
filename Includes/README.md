# Includes<T,K>

<aside>
💡 Includes<T, K> 는 Array.Includes 함수를 모방하는 타입시스템을 구현한다.

</aside>

## 풀이과정

### 실패1

```tsx
type Includes<T extends any[], K> = K extends keyof T
  ? true
  : false;

type isPillarMen = Includes<["Kars", "Esidisi", "Wamuu", "Santana"], "Dio">; // expected to be `false`

type test2 = Includes<["a", "b", "c"], "c">;
type test3 = Includes<["a", "b", "c"], "d">;
type test4 = Includes<["a", "b", "c"], 1>;
```

- T 타입 배열의 key 목록(인덱스) 과 K 타입을 비교하려 해서 무조건 false 가 되었다.
    - 값 목록을 비교하도록 해주어야한다.

### 실패2

```tsx
type Includes<T extends any[], K> = T extends [
  infer A,
  ...infer B
]
  ? K extends A
    ? true
    : Includes<B, K>
  : false;

type isPillarMen = Includes<["Kars", "Esidisi", "Wamuu", "Santana"], "Dio">; // expected to be `false`

type test1 = Includes<["a", "b", "c"], "a" | "A">; // boolean (실패)
type test2 = Includes<["a", "b", "c"], "c">; //통과
type test3 = Includes<["a", "b", "c"], "d">;
type test4 = Includes<["a", "b", "c"], 1>;
```

- infer를 통해 T 배열타입의 값을 참조할 수 있도록 한 후, 나머지 B 들을 다시 재귀호출하였다.

<aside>
💡 그러나. test1과 같이 union된 key 타입의 결과로 false 타입을 반환하지 않고 boolean을 반환하여 실패했다

</aside>

- `K extends A` 부분에서의 문제라 생각했다.
    - 실행시 K의 union 요소별로 “a” 에서는 true, “A” 에서는 false라 판단하여 결과적으로 boolean 타입을 반환한것.
        - 따라서 이 부분을 보완할 타입을 설계해야 했다.

## 해결?

```tsx
type Includes<T extends readonly any[], U> = (
  T extends (infer ListTypes)[] ? (U extends ListTypes ? true : false) : false
) extends true
  ? true
  : false;

type isPillarMen = Includes<["Kars", "Esidisi", "Wamuu", "Santana"], "Dio">; // expected to be `false`
type test1 = Includes<["a", "b", "c"], "b">; // true
type test2 = Includes<["a", "b", "c"], "c">; // true
type test3 = Includes<["a", "b", "c"], "b" | "c">; // true
type test4 = Includes<["a", "b", "c"], "a">; // true
type test5 = Includes<["a", "b", "c"], 1>; //false
type test6 = Includes<["a", "b", "c"], "d">; // false
type test7 = Includes<["a", "b", "c"], "a" | "d">; // false
type test8 = Includes<[{ a: "a" }, "b", "c"], { a: "a" }>; // true
type test9 = Includes<[[1]], 1 | 2>; // false
type test10 = Includes<[1 | 2], 1>; // false
```

- T의 리스트 타입 전체를 유니온으로 받아 온 후(infer ListTypes) 해당 타입과 U를 비교하여 하나라도 포함되지 않는 요소가 있다면 false를 반환하도록 하였다.

> git 에서 다른사람들이 올린 해결법은 test3과 같은 예시에서 false를 반환하였는데, 나는 Includes 를 implement하는데 있어서 Pick 유틸리티 타입처럼 `“b” | “c”` 와 같은 요소도 true로 반환 할 줄 아는 타입을 설계해야 한다 생각해서 위처럼 만들었다
>