# Unshift<T, U>

<aside>
💡 Push와 반대로 T 배열 타입에 U 타입을 제일 앞에 추가한다

</aside>

```tsx
type Unshift<T extends unknown[], U> = [U , ...T]

type Result = Unshift<[1, 2], 0> // [0, 1, 2,]
```