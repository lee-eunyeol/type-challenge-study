# FirstOfArray<T>

<aside>
💡 FirstOfArray<T> 는 배열의 첫번째 원소의 타입을 반환한다.

</aside>

[type-challenges/README.md at main · type-challenges/type-challenges](https://github.com/type-challenges/type-challenges/blob/main/questions/00014-easy-first/README.md)

## 해결 과정

## 해결

```tsx
type arr1 = ["a", "b", "c"];
type arr2 = [3, 2, 1];
type arr3 = [];

type First<T extends any[]> = T['length'] extends 0 ? never : T[0]

type head1 = First<arr1>; // expected to be 'a'
type head2 = First<arr2>; // expected to be 3
type head3 = First<arr3>;
```

- 빈 arr를 받았을때 (`[]` ) undefined 타입을 반환하지 않고, never를 반환할 수 있도록 예외처리를 해주었다.