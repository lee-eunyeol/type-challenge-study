# TupleToObject<T>

<aside>
π‘ TupleToObject<T>λ ννμ λͺ¨λ  μμλ€μ κΈ°λ°μΌλ‘ Object ννλ‘ λ³ννλ€.

</aside>

[type-challenges/README.md at main Β· type-challenges/type-challenges](https://github.com/type-challenges/type-challenges/blob/main/questions/00011-easy-tuple-to-object/README.md)

## ν΄κ²° κ³Όμ 

## μ±κ³΅??

```tsx
const tuple = ['tesla', 'model 3', 'model X', 'model Y'] as const

type TupleToObject<T extends readonly any[]> = {
  [key in T[number]]: key
}

type result = TupleToObject<typeof tuple> 
// expected { 'tesla': 'tesla', 'model 3': 'model 3', 'model X': 'model X', 'model Y': 'model Y'}
```

- μ λ΅μ΄κΈ΄νλ κ°μΈμ μΌλ‘ `T extends readonly any[]` λΆλΆμμ T νμμ μ§ν©μ any[]λ‘ νννλλ° anyλ₯Ό μ΄ κ²μ΄ μμ½λ€κ³  μκ°νλ€.
    - μ? Objectμ keyλ‘ ν λΉ λ  μ μλ νμμ string, number , symbolμ΄λ€.
    
    ```tsx
    const tuple = ['tesla', 'model 3', {no : true}] as const
    
    type TupleToObject<T extends readonly any[]> = {
      [key in T[number]]: key
    }
    
    type result = TupleToObject<typeof tuple> 
    // expected { 'tesla': 'tesla', 'model 3': 'model 3', 'model X': 'model X', 'model Y': 'model Y'}
    ```
    
    - λ§μ½ μμ κ°μ΄, tupleμ μμμ€ `{ no : true }` κ°μ κ°μ²΄ ννκ° μλ€λ©΄ μ΄λ₯Ό ν€λ‘ μ΄μ©ν  μ μκΈ° λλ¬Έμ νμ μ²΄νΉμ΄ μ μμνλμ§ μμμΌ νλλ°, `T extends readonly any[]` λ μ΄λ₯Ό λ¬΄μ¬ν ν΅κ³Όν  κ²μ΄λ€.
        - κ²°κ΅­ `any[]`λ₯Ό μ¬μ©ν¨μΌλ‘μ¨ ννμ λͺ¨λ  μμλ₯Ό Objectλ‘ λ³ννμ§ μλ μ λ€λ¦­ νμμ λ§λ κ²μ΄λ€.

### λ λμ λ΅

```tsx
const tuple = ['tesla', 'model 3', 'model X', 'model Y'] as const

type TupleToObject<T extends readonly PropertyKey[]> = {
  [key in T[number]]: key
}

type result = TupleToObject<typeof tuple> 
// expected { 'tesla': 'tesla', 'model 3': 'model 3', 'model X': 'model X', 'model Y': 'model Y'}
```

- PropertyKey νμμ objectμ ν€κ° λ  μ μλ string | number | symbol μ λμ¨ νμμ΄λ―λ‘ μ΄λ₯Ό νμ©νλ©΄ μ’ λ λμ κ²°κ³Όλ₯Ό λΌ μ μκ² λμλ€.
    - μκΉμ κ°μ λ¬Έμ μ κ²½μ° νμμλ¬λ₯Ό μ‘μλΌ μ μκ² λμλ€.
    
    ```tsx
    const tuple = ['tesla', 'model 3', {no : true}] as const
    
    type TupleToObject<T extends readonly PropertyKey[]> = {
      [key in T[number]]: key
    }
    
    type result = TupleToObject<typeof tuple>
    //Error Type '"tesla" | "model 3" | { readonly no: true; }' is not assignable to type 'PropertyKey'. 
    ```