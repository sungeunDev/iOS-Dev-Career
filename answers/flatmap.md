# flatMap

| 질문출처 | 작성자 |
| :------- | :----: |
| 룩핀     |  썽니  |

## Question

- 4.1 버전 미만과 최신버전에서의 배열의 메소드인 FlatMap의 차이는 무엇인가요?

## Simple Answer

#### 4.1 버전 미만의 flatMap 기능

1. nil에 매핑되는 모든 것을 필터링

```swift
let possibleNumbers = ["1", "2", "three", "///4///", "5"]
let mapped: [Int?] = possibleNumbers.map { str in Int(str) }
// [1, 2, nil, nil, 5]

let flatMapped: [Int] = possibleNumbers.flatMap { str in Int(str) }
// [1, 2, 5]
```

2. 각 요소가 sequence 일 때 flat하게 만들어 줌

```swift
let numbers = [1, 2, 3, 4]

let mapped = numbers.map { Array(repeating: $0, count: $0) }
// [[1], [2, 2], [3, 3, 3], [4, 4, 4, 4]]

let flatMapped = numbers.flatMap { Array(repeating: $0, count: $0) }
// [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
```

#### 4.1 버전 이후 flatMap 기능

- 1번 `nil에 매핑되는 모든것을 필터링` 기능은 compactMap 메서드로 이전
- 2번 각 요소가 sequence 일 때 flat하게 만들어 주는 기능만 flatMap에 존재함
- 즉, Optional 변수가 반환될 수 있음.

#### 정리

```swift
Sequence.flatMap<S>(_: (Element) -> S) -> [S.Element]
    where S : Sequence
Optional.flatMap<U>(_: (Wrapped) -> U?) -> U?
Sequence.flatMap<U>(_: (Element) -> U?) -> [U]
```

- swift 4.1 버전 미만에서 `flatMap`의 정의가 위처럼 3가지가 있었는데, 마지막의 `Sequence.flatMap<U>(_: (Element) -> U?) -> [U]` 의 정의가 `compactMap`으로 이전되었음.

## Details

> 공식 문서와 함께 살펴보기

### [flatMap (Deprecated)](https://developer.apple.com/documentation/swift/sequence/2907182-flatmap)

- Returns an array containing the `non-nil results` of calling the given transformation with each element of this sequence.

### [flatMap](https://developer.apple.com/documentation/swift/sequence/2905332-flatmap)

- Returns an array containing the `concatenated results` of calling the given transformation with each element of this sequence.

### [compactMap](https://developer.apple.com/documentation/swift/sequence/2950916-compactmap)

- Returns an array containing `the non-nil results` of calling the given transformation with each element of this sequence.

## Links

- [swift-evolution: 0187-introduce-filtermap.md](https://github.com/apple/swift-evolution/blob/master/proposals/0187-introduce-filtermap.md)
- [Zedd님 블로그](https://zeddios.tistory.com/448)
