# ARC
| 질문출처 | 작성자 |
| :--- | :---: |
| 룩핀 | 썽니 |

## Question
- ARC(Automatic Reference Counting)는 어느 시점에 작동하나요?

## Simple Answer
- 컴파일 할 때 작동합니다.

## Details
1. 왜 메모리를 관리해야 할까? 
> 메모리가 과부하되면 워닝단계에서는 백그라운드에서 돌아가는 앱들 중 가장 사용하지 않은 최초의 앱들이 종료되고, 그 이상 넘어가면 실행시키는 앱이 종료되기 때문.

2. iOS의 메모리 관리 방법?
> 하나의 객체가 생성되어 메모리에 올라가게 되면, 그 객체를 참조하는 횟수를 표시하는 [참조 횟수 계산 방식](https://ko.wikipedia.org/wiki/%EC%B0%B8%EC%A1%B0_%ED%9A%9F%EC%88%98_%EA%B3%84%EC%82%B0_%EB%B0%A9%EC%8B%9D). 
> class는 Reference type으로 heap에 저장된 후 ARC에 의해 자동으로 관리됨

3. ARC 란?
> Auto Reference Counting. 객체의 참조 카운팅이 0이 될 경우, 더이상 사용되지 않는 메모리로 인식하고 메모리에서 자동(Auto)으로 해제시켜 주는 메모리 관리 방법.

4. ARC 이전에는?
> MRC (Manual Reference Counting). 수동으로 retain 해서 참조를 넣고, release로 참조를 해제하며 수동으로 카운팅 관리.

> ㅁ MRC를 이용할때의 문제점?
  > * 앱의 비정상 종료 원인 중 많은 부분이 메모리 문제. 메모리 관리는 애플의 앱 승인 거부(Rejection)의 대다수 원인 중 하나. 
  > * 많은 개발자들이 수동적인 (retain/release) 메모리 관리로 힘들어함.
  > *  retain/release 로 코드 복잡도가 증가.  
> -> 매우 불편하다는 의견을 수렴. WWDC 2011, iOS 5 부터 ARC를 쓸 수 있게 되었다.

5. Java의 가비지 컬렉터(Garbage Collector, GC)와의 차이점
> - GC는 프로그램 실행중(Runtime)에 메모리를 검사하여 앱 퍼포먼스에 악영향을 준다.  
> - ARC는 컴파일단에서 처리 되어 개발자가 직접 코딩하던 메모리 retain/release를 컴파일러가 자동으로 코드에 삽입시키므로, 동작시에는 MRC와 동일하여 성능 저하를 유발하지 않는다.  
> - 또한 가비지 컬렉터는 불규칙적인 사이클로 체크하고, 카운팅이 0인 모든 프로퍼티를 휩쓸어 없애는 반면 ARC는 카운팅이 0이 되는 순간에 해당 인스턴스를 메모리에서 제거한다.

6. ARC로 인해 발생할 수 있는 문제?
> - 강한 순환 참조로 인해 메모리 leak이 생길 수 있음  
> - 이 문제를 방지하기 위해서 weak / unowned를 사용.   
>   - 둘의 차이는 weak - optional이냐, unowned 값이 있냐의 차이.
>   - weak, unowned는 약한 참조로, 카운팅 횟수를 증가시키지 않고, 참조하는 객체가 해제되면 자동으로 해제된다.  
>   - 자세한 내용은 [Reference](Reference.md) 참고

## Links
- [Swift Language Guide - ARC](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html)
- [Apple ARC & Strong Reference Cycle 번역](https://rhammer.tistory.com/139?category=553762)
- [Yongjai님 깃헙](https://github.com/Yongjai/TIL/blob/master/iOS/Objective-C/MemoryManagement.md/)
- [chunghyup님 블로그](http://chunghyup.tistory.com/2?category=674481)
  
