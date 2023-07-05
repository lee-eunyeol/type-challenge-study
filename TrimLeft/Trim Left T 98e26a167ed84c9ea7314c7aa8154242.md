# Trim Left<T>

<aside>
💡 TrimLeft<T>는 문자열로 들어오는 T 타입에 대해 왼쪽의 공백을 모두 제거한 타입을 반환한다.

</aside>

## 풀이과정

## 해결

> 방법자체를 처음에 잘 몰랐다.
> 

```tsx
type Whitespace = '\n' | ' ' | '\t';
type TrimLeft<T> = T extends `${Whitespace}${infer U}` ? TrimLeft<U> : T;

type trimed = TrimLeft<'  Hello World  '> // expected to be 'Hello World  '
```

- `type Whitespace = '\n' | ' ' | '\t';`
    - Whitespace라는 공백 타입을 선언한다.
    
- `T extends `${Whitespace}${infer U}` ? TrimLeft<U> : T`
    
    > 여기서 백틱을 이용하여 타입을 extends 할수 있다는걸 전혀 몰랐다.
    > 
    - T 타입이 왼쪽에 공백을 가지고 있다면, WhiteSpace가 제거된 U 타입을 반환하도록 했다.