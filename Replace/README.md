# Replace<S, From, To>

<aside>
💡 Replace<S, From, To>는 문자열 타입 S에서 From 문자열을 To 문자열로 변경하는 타입이다.

</aside>

## 풀이과정

## 해결

```jsx
type Replace<S extends string, From extends string, To extends string> = From extends '' 
? S  
: S extends `${infer Rest}${From}${infer Rest2}` 
? `${Rest}${To}${Rest2}` 
: S

type replaced = Replace<'types are fun!', 'fun', 'awesome'> // expected to be 'types are awesome!'
```

- From이  빈 문자열일 경우 S 문자열 타입을 그대로 반환하도록 예외처리하였다.