# FirstOfArray<T>

<aside>
๐ก FirstOfArray<T> ๋ ๋ฐฐ์ด์ ์ฒซ๋ฒ์งธ ์์์ ํ์์ ๋ฐํํ๋ค.

</aside>

[type-challenges/README.md at main ยท type-challenges/type-challenges](https://github.com/type-challenges/type-challenges/blob/main/questions/00014-easy-first/README.md)

## ํด๊ฒฐ ๊ณผ์ 

## ํด๊ฒฐ

```tsx
type arr1 = ["a", "b", "c"];
type arr2 = [3, 2, 1];
type arr3 = [];

type First<T extends any[]> = T['length'] extends 0 ? never : T[0]

type head1 = First<arr1>; // expected to be 'a'
type head2 = First<arr2>; // expected to be 3
type head3 = First<arr3>;
```

- ๋น arr๋ฅผ ๋ฐ์์๋ (`[]` ) undefined ํ์์ ๋ฐํํ์ง ์๊ณ , never๋ฅผ ๋ฐํํ  ์ ์๋๋ก ์์ธ์ฒ๋ฆฌ๋ฅผ ํด์ฃผ์๋ค.