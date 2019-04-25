# 문서명

| 질문출처 |   작성자   |
| :------- | :--------: |
| 룩핀 | 오원석 |

## Question

- Swift에서 Class와 Struct의 차이는 무엇인가요?

## Simple Answer

- Class는 reference type (참조 타입)이고, Struct는 value type (값 타입) 입니다

## Details

> Class의 인스턴스를 만들고 변수 값을 변경하면, 해당 인스턴스의 변수 값이 변경됩니다

* 샘플코드

~~~swift
class Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

var jack = Person(name: "Jack")
var emma = jack
emma.name = "emma"

print(jack.name)
print(emma.name)
~~~

~~~swift
*console log

emma
emma
~~~

> Struct의 인스턴스를 만들고 변수 값을 변경하면, 해당 인스턴스의 변수 값은 변하지 않습니다
> 단순히 값을 복사해서 사용하기 때문입니다

* 샘플코드

~~~swift
struct Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

var jack = Person(name: "Jack")
var emma = jack
emma.name = "emma"

print(jack.name)
print(emma.name)
~~~

~~~swift
*console log

jack
emma
~~~

## Links

- [richoh86의 깃헙](https://github.com/richoh86/OhWonSeok_iOS_School6)
