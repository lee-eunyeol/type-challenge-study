# Readonly<T>

<aside>
💡 READONLY<T> 는 타입(T)의 프로퍼티들을 모두 readonly 상태로 변환한다.

</aside>

[](https://github.com/type-challenges/type-challenges/blob/main/questions/00007-easy-readonly/README.md)

## 풀이과정

### 해결

```tsx
interface Todo {
  title: string;
  description: string;
}

type MyReadonly<T> = {
  readonly [key in keyof T]: T[key];
};

const todo: MyReadonly<Todo> = {
  title: "Hey",
  description: "foobar",
};

todo.title = "Hello"; // Error: cannot reassign a readonly property
todo.description = "barFoo"; // Error: cannot reassign a readonly property
```

- `[key in keyof T]: T[key]` 로 T의 프로퍼티들을 전부 나열한 뒤, readonly 를 붙여주었다.