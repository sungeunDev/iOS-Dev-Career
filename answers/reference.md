# 문서명

| 질문출처 | 작성자 |
| :------- | :----: |
| 룩핀     |  썽니  |

## Question

- strong, weak, unowned 키워드를 어떤 상황에서 사용하고, 차이는 무엇인가요?

## Simple Answer

- 보통은 ARC에 의해 힙 메모리에 대해선 생각하지 않아도 되지만 ARC에 영향을 줄 수 있는 애들이 있는데 아래 3가지. 
- 변수 선언할 때 사용하는 키워드  
  1.strong 
    - default. normal reference counting. 스트롱 포인터는 힙 안에 있는 걸 강제로 힙에 머물도록 함. 포인터가 더이상 그걸 가르키지 않을 때까지.  
    
  2.weak
    - weak 포인터가 있다는 말은 힙에 있는 것에 아무도 관심이 없다면, 힙에서 제거할 수 있다는 의미. 그리고 nil로 설정됨. 그래서 weak은 오직 옵셔널 타입의 참조 포인터에서만 적용.
    - 예. Outlet >> Why? 뷰 계층에선, ex. UILabel의 상위 뷰는 UILabel에 대해 strong 포인터를 갖고 있어서 outlet을 따로 strong에 넣어놓지 않아도 뷰 계층에 따라 알아서 힙에 보관이 됨. but, 더이상 UILabel이 뷰의 일부가 아니라면(상위 뷰가 UILabel을 제거한다면) outlet이 nil이 될것.

  3.unowned
    - 참조 횟수를 세지 말라(추적하지 말라)는 의미.
    - unowned가 있는데, 참조를 나중에 하고, 참조한 것이 힙 밖으로 버려지게 되면, 더이상 스트롱 포인터가 존재하지 않기 때문에 앱 크래쉬 남. 메모리 참조 에러.
    - 왜 필요할까?
      -객체들 간의 메모리 순환을 부수기 위해서. (weak을 쓸 수도 있음. weak을 더 자주 쓰기도)
- Vs. weak?
  - 옵셔널이냐 아니냐의 차이
