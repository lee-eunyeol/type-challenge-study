# IF<C, T, F>

<aside>
💡 IF<C, T, F>는  C(condition)이 truthy 면 T 그렇지 않으면 F 타입을 반환한다.

</aside>

## 해결과정

```tsx
type If<C extends boolean, T, F> = C extends true ? T : F

type A = If<true, "a", "b">; // expected to be 'a'
type B = If<false, "a", "b">; // expected to be 'b'
```

- 입력 받는 Condition Type이 boolean을 extends 하는지 체크 후, C의 조건(true 여부)에따라 T , F 를 반환하였다.