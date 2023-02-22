# Length of Tuple<T>

<aside>
💡 Length of Tuple<T> 는 튜플의 길이를 리턴한다.

</aside>

[type-challenges/README.md at main · type-challenges/type-challenges](https://github.com/type-challenges/type-challenges/blob/main/questions/00018-easy-tuple-length/README.md)

## 풀이 과정

### 해결

```tsx
type tesla = ['tesla', 'model 3', 'model X', 'model Y'];
type spaceX = ['FALCON 9', 'FALCON HEAVY', 'DRAGON', 'STARSHIP', 'HUMAN SPACEFLIGHT'];

type Length<T extends readonly unknown[]> = T['length'];
type teslaLength = Length<tesla>; // expected 4
type spaceXLength = Length<spaceX>; // expected 5
```

- 튜플은 불변의 구조를 지니기 때문에 일반적으로 `readonly` 를 붙인다고 한다
    - 꼭 안붙여도 이번 문제 풀이에 큰 문제는 없다고 생각한다.