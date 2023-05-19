# Chainable Options<T>

<aside>
💡 **Chainable Options** 는 options(key, value) , get() 메서드를 가진 타입 객체로 
options(key,value) 를 통해 타입 인자를 확장하고, get() 메서드를 통해 최종 결과 타입에 액세스 할 수 있도록 하는 타입이다. 이를 설계해보자

</aside>

## 해결 과정

> 어려웠음
> 

```tsx
declare const config: Chainable;

type Chainable<T = {}> = {
  option: <K extends string, V>(
    key: K extends keyof T ? (V extends T[K] ? never : K) : K,
    value: V
  ) => Chainable<Omit<T, K> & Record<K, V>>;
  get: () => T;
};

const result: Result = config
  .option("foo", 123)
  .option("name", "type-challenges")
  .option("bar", { value: "Hello World" })
  .get();

// expect the type of result to be:
interface Result {
  foo: number;
  name: string;
  bar: {
    value: string;
  };
}
```

- 메서드를 가진 타입객체를 만드는 법을 이번에 새롭게 알게 되었다.
    - 우선 반환할 T 라는 타입객체를 생성하며, 기본값 `{}`을 지정한다
    - options()
        - 첫 인자는 프로퍼티 이름(key), 두번째 인자는 해당 프로퍼티의 타입(V)을 반환하도록 한다
        - `key: K extends keyof T ? (V extends T[K] ? never : K) : K`
            - 중복된 프로퍼티 명/프로퍼티 타입으로 option()메소드를 사용할 경우 같은 타입이라면 never를 반환하는 예외처리가 되어있다.
        - `Chainable<Omit<T, K> & Record<K, V>>;`
            - 재귀로 Chainable을 호출하는데, 처음엔 기본값 `{}` 이었던 T 타입 객체에 Record<K,V>를 할당하여 T타입에 프로퍼티를 담도록 하였다.
            - Omit<T, K>의 경우 중복된 프로퍼티명이지만, 다른 프로퍼티 타입으로 T 객체 타입에 할당하려 했을때 기존 프로퍼티를 제거하고 다시 할당하기 위함이다.
    - get() 에서는 완성된 T 타입을 반환한다.