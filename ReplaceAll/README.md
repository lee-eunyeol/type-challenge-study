# ReplaceAll<S, From, To>

<aside>
💡 ReplaceAll<S, From, To> 는 S 문자열 타입에서 From문자열을 포함하고 있다면 모두 To 문자열로 변경하는 타입이다

</aside>

## 풀이과정

## 해결

```tsx
type ReplaceAll<S extends string, From extends string, To extends string> = From extends '' 
? S
: S extends `${infer Rest}${From}${infer Rest2}`
? `${Rest}${ReplaceAll<`${To}${Rest2}`,From,To>}`
: S
type replaced = ReplaceAll<'t y p e s', ' ', ''> // expected to be 'types'
```

- 기존 Replate에서 재귀를 돌렸다.