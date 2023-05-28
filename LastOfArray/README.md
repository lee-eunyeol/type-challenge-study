# LastOfArray

<aside>
💡 Last<T> 는 T타입 배열의 가장 마지막 요소를 반환한다

</aside>

## 풀이

### 해결

```tsx
type arr1 = ['a', 'b', 'c']
type arr2 = [3, 2, 1]
type arr3 = [1]
type arr4 = []

type Last<T extends ArrayLike<any>> =T extends [...infer Rest , infer L] ? L : never
type tail1 = Last<arr1> // expected to be 'c'
type tail2 = Last<arr2> // expected to be 1
type tail3 = Last<arr3> // expected to be 'c'
type tail4 = Last<arr4> // expected to be 1
```

- infer를 통해서 가장 마지막 요소를 가져오도록 하였다.