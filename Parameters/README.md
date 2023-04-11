# Parameters<T>

<aside>
💡 Parameters<T>는 T 함수 타입의 인자를 반환한다.

</aside>

## 해결 과정

## 해결

```tsx
const foo = (arg1: string, arg2: number): void => {};

type MyParameters<T extends (...args: any[]) => any> = T extends (
  ...any: infer Parameters
) => any
  ? Parameters
  : [];

type FunctionParamsType = MyParameters<typeof foo>; // [arg1: string, arg2: number]

const a = () => 1;
type test1 = MyParameters<typeof a>;
```

- 인자가 없을 경우 args는 빈 배열형태로 반환하도록 처리하였다.