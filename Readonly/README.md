# Readonly<T>

<aside>
π‘ Readonly<T> λ νμ(T)μ νλ‘νΌν°λ€μ λͺ¨λ readonly μνλ‘ λ³ννλ€.

</aside>

[](https://github.com/type-challenges/type-challenges/blob/main/questions/00007-easy-readonly/README.md)

## νμ΄κ³Όμ 

### ν΄κ²°

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

- `[key in keyof T]: T[key]` λ‘ Tμ νλ‘νΌν°λ€μ μ λΆ λμ΄ν λ€, readonly λ₯Ό λΆμ¬μ£Όμλ€.
