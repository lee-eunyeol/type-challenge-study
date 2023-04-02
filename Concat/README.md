# Concat<A,B>

<aside>
💡 Concat<A, B> 는 Array.concat 함수를 모방하는 타입시스템을 구현한다.

</aside>

## 풀이과정

## 해결

```tsx
type Concat<A extends any[], B extends any[]> = [...A, ...B];

type Result = Concat<[1], [2]>; // expected to be [1, 2]
```

- any[] 를 extends하여 A, B 모두 모든유형의 배열 형태를 받을 수 있도록한다
- 순서대로 해당 타입의 전개연산자를 통해 새 배열 타입을 반환한다