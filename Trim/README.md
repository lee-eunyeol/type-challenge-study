# Trim<T>

<aside>
💡 Trim<T> 는 문자열 타입으로 들어오는 T 타입에서, 양쪽 공백을 모두 제거한 문자열 타입을 반환한다.

</aside>

## 풀이 과정

## 해결

```tsx
type Whitespace = "\n" | " " | "\t";
type Trim<T> = T extends `${Whitespace}${infer U}${Whitespace}` ? Trim<U> : T;

type trimmed = Trim<"  Hello World  ">; // expected to be 'Hello World'
```