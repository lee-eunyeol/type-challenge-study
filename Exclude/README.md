# Exclude<T,U>

<aside>
π‘ Exclude<T,U>λ Uμ ν λΉν  μ μλ μ νμ Tμμ μ μΈν©λλ€.

</aside>

[type-challenges/README.md at main Β· type-challenges/type-challenges](https://github.com/type-challenges/type-challenges/blob/main/questions/00043-easy-exclude/README.md)

## ν΄κ²° κ³Όμ 

### ν΄κ²°

```tsx
type MyExclude<T, U> = T extends U ? never : T;

type Result = MyExclude<'a' | 'b' | 'c', 'a'>; // 'b' | 'c'
```

- μ κ³΅λ μ λμ¨νμ(`'a' | 'b' | 'c'`)μμ κ°κ° U(`βaβ`)μ ν λΉ κ°λ₯νμ§ νμΈ ν, λΆκ°λ₯ ν  κ²½μ°μλ§ ν΄λΉ νμμ λ°ν(`'b' | 'c'`)νλ€.
    
    > μ λμ¨ νμμ ν΄λΉ μ‘°κ±΄μ κ°κ° μ€ν μν¨λ€ ( a to a , b to a , c to a ) λ λΆλΆμ λͺμ¬νμ
    >
