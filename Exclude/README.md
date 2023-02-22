# Exclude<T,U>

<aside>
💡 Exclude<T,U>는 U에 할당할 수 있는 유형을 T에서 제외합니다.

</aside>

[type-challenges/README.md at main · type-challenges/type-challenges](https://github.com/type-challenges/type-challenges/blob/main/questions/00043-easy-exclude/README.md)

## 해결 과정

### 해결

```tsx
type MyExclude<T, U> = T extends U ? never : T;

type Result = MyExclude<'a' | 'b' | 'c', 'a'>; // 'b' | 'c'
```

- 제공된 유니온타입(`'a' | 'b' | 'c'`)에서 각각 U(`’a’`)에 할당 가능한지 확인 후, 불가능 할 경우에만 해당 타입을 반환(`'b' | 'c'`)한다.
    
    > 유니온 타입은 해당 조건을 각각 실행 시킨다 ( a to a , b to a , c to a ) 는 부분을 명시하자
    >