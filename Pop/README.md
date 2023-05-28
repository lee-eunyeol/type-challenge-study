# POP<T>

<aside>
💡 POP<T> 는 배열 타입의 T 타입에서 마지막 인자만 제거한 배열 타입을 반환한다.

</aside>

```tsx
type Pop<T extends ArrayLike<unknown>> = T extends [...infer A, infer B]
  ? A
  : undefined;

type arr1 = ["a", "b", "c", "d"];
type arr2 = [3, 2, 1];
type arr3 = [];
type re1 = Pop<arr1>; // expected to be ['a', 'b', 'c']
type re2 = Pop<arr2>; // expected to be [3, 2]
type re3 = Pop<arr3>; // expected to be undefined
```

- 이전 Last 풀이 처럼 전개연산자로 가장 마지막 배열타입의 값을 분리했다
- 기존 arr.pop() 의 경우 arr 이 빈 배열일때, undefined를 반환하므로 이와 같이 동작하도록 설계했다.