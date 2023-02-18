# PICK

<aside>
💡 Pick<T, K>  타입은 특정 타입(T) 에서 몇 개의 속성 (K)을 선택하여 타입을 정의한다

</aside>

[type-challenges/README.md at main · type-challenges/type-challenges](https://github.com/type-challenges/type-challenges/blob/main/questions/00004-easy-pick/README.md)

## 풀이과정

### 1. 실패

```tsx
interface Todo {
  title: string;
  description: string;
  completed: boolean;
}

type MyPick<T, K extends keyof T> = T[K];

type PickedTodo = MyPick<Todo, "title">;

const pickedTodo: PickedTodo = {
// title이라는 키와 타입을 가져오지 못했다. 
};
```

- PickedTodo 에서 **title 프로퍼티와 string type을** 가져오지 못하고  **title 프로퍼티의 타입인 string 만 가져왔다.**
    
    

### 원인?

```tsx
type MyPick<T, K extends keyof T> = T[K];
```

- `K extends keyof T` 부분에서 T 타입의 프로퍼티 목록은 잘 가져온것 같다.
    - 그러나 `T[K]` 부분에서 해당 프로퍼티의 타입만 불러온게 문제라고 생각했다.

## 해결

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

- `T[K]` 가 아닌, 새로운 객체 형태의 타입을 만들어 T의 프로퍼티들과 프로퍼티의 타입을 받을 수 있게해야한다.
    - `{ [key in K]: T[key] }`
        - key in K 로 T의 프로퍼티들을 나열하는게 포인트였던것 같다.
