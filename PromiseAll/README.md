# PromiseAll

<aside>
💡 PromiseAll은 배열로 구성된 PromiseLike 객체들을  Resolve 된 배열타입들로 반환한다.

</aside>

## 풀이

```tsx
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise<string>((resolve, reject) => {
  setTimeout(resolve, 100, 'foo');
});

declare function PromiseAll<T extends unknown[]>(values: readonly [...T]): Promise<{
  [K in keyof T]: T[K] extends PromiseLike<infer R> ? R : T[K]
}>

// expected to be `Promise<[number, 42, string]>`
const p = PromiseAll([promise1, promise2, promise3] as const)
```

> 이전 declare const 처럼 함수 타입형태로 정의하는 방법을 잘 몰라서 많이 헤맸던것 같다.
>