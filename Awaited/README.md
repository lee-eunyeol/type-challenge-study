# Awaited<T>

<aside>
💡 Awaited<T> 는 만약 T가 Promise로  래핑 되어 있다면, 래핑된 T안의 타입을 반환한다.

</aside>

## 해결 과정

### 초기 풀이

```tsx
type ExampleType = Promise<string>;
type ExampleType2 = string;

type MyAwaited<T> = T extends PromiseLike<infer U> ? U : T;

type Result = MyAwaited<ExampleType>; // string
type Result2 = MyAwaited<ExampleType>;
```

- Typescript `infer` 는 조건부 타입에서 사용할 수 있는 키워드로 타입 추론을 가능하게 해준다.
    - 따라서 T가 PromiseLike<infer U> 타입 형태에 할당될 수 있는 집합이면,  Promise 안의 래핑된 타입을 U 라는 타입 파라미터로 지정하여 다시 해당 타입을 반환할 수 있게 하였다.

> 보완 필요?..(재귀적 호출)
> 

### 실 구현체

```tsx
/**
 * Recursively unwraps the "awaited type" of a type. Non-promise "thenables" should resolve to `never`. This emulates the behavior of `await`.
 */
type Awaited<T> =
    T extends null | undefined ? T : // special case for `null | undefined` when not in `--strictNullChecks` mode
        T extends object & { then(onfulfilled: infer F, ...args: infer _): any } ? // `await` only unwraps object types with a callable `then`. Non-object types are not unwrapped
            F extends ((value: infer V, ...args: infer _) => any) ? // if the argument to `then` is callable, extracts the first argument
                Awaited<V> : // recursively unwrap the value
                never : // the argument to `then` was not callable
        T; // non-object or non-thenable
```