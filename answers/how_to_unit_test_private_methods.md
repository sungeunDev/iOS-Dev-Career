# How to Unit Test Private Methods in Swift
| 질문출처 | 작성자 |
| :--- | :---: |
| 룩핀 | 썽니 |

## Question
- 커스텀뷰 클래스 내 Private Method를 테스트 할 수 있는 방법은 무엇이 있나요?

## Simple Answer
- 결론부터 말하면 `private`한 Access Control 때문에 Private Method를 직접적으로 테스트 할 수는 없다.
- 테스트의 목적은 구현(implementation) 이 아니라 사양(specification)을 테스트하는데 있다. 때문에 private method의 구현을 테스트할 수는 없어도 해당 메서드를 사용하는 public interface를 테스트하여 스펙이 제대로 갖춰져 있는지 확인하는 것으로 테스트 방법을 우회할 수 있다.

#### - Sample Code
``` swift
/* test model */
struct SampleViewModel {
  // Properties
  let account: Account

  // Public Interface
  var expiresAtAsString: String {
    let date = parse(date: account.expiresAt)
    let dateFormatter = DateFormatter()
    dateFormatter.dateFormat = "YYYY, MMMM"
    return dateFormatter.string(from: date)
  }

  // Private Interface
  private func parse(date dateAsString: String) -> Date {
    ...
  }
}

/* unit test */
class SampleTests: XCTestCase {
  func testExpiresAtAsString_20161226WithForwardSlashes() {
    let account = Account(expiresAt: "2016/12/25", subscription: .trial)
    let sampleViewModel = SampleViewModel(account: account)
    XCTAssertEqual(sampleViewModel.expiresAtAsString, "2016, December")
  }
}
```

## Links
- [How to Unit Test Private Methods in Swift](https://cocoacasts.com/how-to-unit-test-private-methods-in-swift/)
