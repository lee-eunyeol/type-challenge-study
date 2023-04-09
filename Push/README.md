# Push<T,V>

<aside>
💡 Push<T,V>는 Array와 유사하게 T 배열 타입의 가장 뒤에 V 타입을 추가한다.

</aside>

## 해결과정

## 해결

```tsx
type Push<T extends unknown[], U> = [...T, U];

type Result = Push<[1, 2], "3">; // [1, 2, '3']
```

> 딱히 설명할게 없다.
>