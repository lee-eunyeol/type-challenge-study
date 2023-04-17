# Omit<T, K>

<aside>
💡 Omit<T,K>는 T 객체타입에서 K라는 프로퍼티를 삭제한 객체 타입을 반환한다.

</aside>

## 해결 과정

### 실패

```tsx
interface Todo {
  title: string;
  description: string;
  completed: boolean;
}

type MyOmit<T, K extends keyof T> = { [U in keyof T]: T[U] };

type TodoPreview = MyOmit<Todo, "description" | "title">;

const todo: TodoPreview = {
  completed: false,
};
```

- `U in keyof T` 부분에서 K 프로퍼티를 제거해야 하는데 방법을 몰랐다.

## 해결

```tsx
interface Todo {
  title: string;
  description: string;
  completed: boolean;
}

type MyOmit<T, K extends keyof T> = {
  [U in keyof T as U extends K ? never : U]: T[U];
};

type TodoPreview = MyOmit<Todo, "description" | "title">;

const todo: TodoPreview = {
  completed: false,
};
```

- `U in keyof T as U` 부분에서 `U in keyof T` 를 다시 as U 를 통해 extends 조건문을 만들 수 있다는 것을 처음 알았다
    - 이를 type predicate라 한다
        
        > In the context of the code you provided, **`T as U`**
         is a type predicate that tells TypeScript that **`T`**has the same type as **`U`**. This is useful in situations where TypeScript cannot infer the type automatically, such as when dealing with generic types or complex expressions.
        > 
        - 이전에 타입가드를 설계 할때 봤었는데 이와 같이 T 를 U 로 assertion 한다는 의미이다.
        
        ```tsx
        function isString(val: any): val is string {
          return typeof val === 'string';
        }
        ```
        
        - 타입 가드에서도 val 이 string 타입임을 강제로 명시해서 타입스크립트가 타입을 추론하는데 도움을 줄 수 있다.