# Length of Tuple<T>

<aside>
๐ก Length of Tuple<T> ๋ ํํ์ ๊ธธ์ด๋ฅผ ๋ฆฌํดํ๋ค.

</aside>

[type-challenges/README.md at main ยท type-challenges/type-challenges](https://github.com/type-challenges/type-challenges/blob/main/questions/00018-easy-tuple-length/README.md)

## ํ์ด ๊ณผ์ 

### ํด๊ฒฐ

```tsx
type tesla = ['tesla', 'model 3', 'model X', 'model Y'];
type spaceX = ['FALCON 9', 'FALCON HEAVY', 'DRAGON', 'STARSHIP', 'HUMAN SPACEFLIGHT'];

type Length<T extends readonly unknown[]> = T['length'];
type teslaLength = Length<tesla>; // expected 4
type spaceXLength = Length<spaceX>; // expected 5
```

- ํํ์ ๋ถ๋ณ์ ๊ตฌ์กฐ๋ฅผ ์ง๋๊ธฐ ๋๋ฌธ์ ์ผ๋ฐ์ ์ผ๋ก `readonly` ๋ฅผ ๋ถ์ธ๋ค๊ณ  ํ๋ค
    - ๊ผญ ์๋ถ์ฌ๋ ์ด๋ฒ ๋ฌธ์  ํ์ด์ ํฐ ๋ฌธ์ ๋ ์๋ค๊ณ  ์๊ฐํ๋ค.