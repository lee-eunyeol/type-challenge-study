# ReturnType<T>

<aside>
💡 ReturnType은 해당 함수의 실행 값(return type)을 반환한다

</aside>

## 해결 과정

```tsx
const fn = (v: boolean) => {
  if (v) return 1;
  else return 2;
};

type MyReturnType<T extends (...args: any) => any> = T extends (
  ...args: any[]
) => infer ReturnType
  ? ReturnType
  : never;

type a = MyReturnType<typeof fn>; // should be "1 | 2"
```

> 딱히 어려운 부분은 없었다.
>