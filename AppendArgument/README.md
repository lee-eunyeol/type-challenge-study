# Append Argument<F,A>

<aside>
💡 **Append Argument<F,A> 는 Function 타입인 F의 인자에 A타입 Argument를 추가하여 반환한 Function 타입이다.**

</aside>

## 풀이과정

## 성공

```jsx
type Fn = (a: number, b: string) => number

type AppendArgument<F extends  (...args : any) => any , A> = 
	F extends (...args : infer ARGS) => infer R 
? () => (...args: [...ARGS, A]) => R
: never

type Result = AppendArgument<Fn, boolean>
```

- `F extends  (...args : any) => any`
    - F 타입을 Function타입으로만 받도록 지정하였다.
    - 
- `F extends (...args : infer ARGS) => infer R`
    - F 타입의 인자타입(Args) 들을 infer로 가져왔다.

- `() => (...args: [...ARGS, A]) => R`
    - 새 Function타입을 반환하되, ARGS 에 A타입을 추가한 파라미터를 완성하여 반환하였다.