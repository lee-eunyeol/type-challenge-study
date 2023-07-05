# Capitalize<T>

<aside>
💡 Capitalize<T> 는 문자열로 들어오는 타입인 T 에서 첫글자만 대문자로 변환하여 반환한다.

</aside>

## 해결과정

## 해결

```tsx
type MyCapitalize<T extends string> = T extends `${infer First}${infer Rest}`
  ? `${Uppercase<First>}${Rest}`
  : T;
type capitalized = MyCapitalize<"hello world">; // expected to be 'Hello world'
```

- 첫문자를 추론 후 Uppercase<T> 라는 유틸리티 타입을 통해 대문자로 변경하였다.