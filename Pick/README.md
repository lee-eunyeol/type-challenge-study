# PICK<T, K>

<aside>
π‘ Pick<T, K>  νμμ νΉμ  νμ(T) μμ λͺ κ°μ μμ± (K)μ μ ννμ¬ νμμ μ μνλ€

</aside>

[type-challenges/README.md at main Β· type-challenges/type-challenges](https://github.com/type-challenges/type-challenges/blob/main/questions/00004-easy-pick/README.md)

## νμ΄κ³Όμ 

### 1. μ€ν¨

```tsx
interface Todo {
  title: string;
  description: string;
  completed: boolean;
}

type MyPick<T, K extends keyof T> = T[K];

type PickedTodo = MyPick<Todo, "title">;

const pickedTodo: PickedTodo = {
// titleμ΄λΌλ ν€μ νμμ κ°μ Έμ€μ§ λͺ»νλ€. 
};
```

- PickedTodo μμ **title νλ‘νΌν°μ string typeμ** κ°μ Έμ€μ§ λͺ»νκ³   **title νλ‘νΌν°μ νμμΈ string λ§ κ°μ Έμλ€.**
    


### μμΈ?

```tsx
type MyPick<T, K extends keyof T> = T[K];
```

- `K extends keyof T` λΆλΆμμ T νμμ νλ‘νΌν° λͺ©λ‘μ μ κ°μ Έμ¨κ² κ°λ€.
    - κ·Έλ¬λ `T[K]` λΆλΆμμ ν΄λΉ νλ‘νΌν°μ νμλ§ λΆλ¬μ¨κ² λ¬Έμ λΌκ³  μκ°νλ€.

## ν΄κ²°

```tsx
interface Todo {
  title: string;
  description: string;
  completed: boolean;
}

type MyPick<T, K extends keyof T> = { [key in K]: T[key] };

type PickedTodo = MyPick<Todo, "title">;

const pickedTodo: PickedTodo = {
  title: "good",
};
```

```tsx
type MyPick<T, K extends keyof T> = { [key in K]: T[key] };
```

- `T[K]` κ° μλ, μλ‘μ΄ κ°μ²΄ ννμ νμμ λ§λ€μ΄ Tμ νλ‘νΌν°λ€κ³Ό νλ‘νΌν°μ νμμ λ°μ μ μκ²ν΄μΌνλ€.
    - `{ [key in K]: T[key] }`
        - key in K λ‘ Tμ νλ‘νΌν°λ€μ λμ΄νλκ² ν¬μΈνΈμλκ² κ°λ€.
