# Frame & Bounds
| 질문출처 | 작성자 |
| :--- | :---: |
| 룩핀 | 썽니 |

## Question
- Frame 과 Bounds 의 차이는 무엇인가요?

## Simple Answer
- 둘 다 UIView의 instance property로 View의 위치와 크기를 나타내는데 쓰임
- View의 위치를 표현하는데 차이가 있는데, Frame은 상위 뷰의 좌표시스템에 의해 종속되고 Bounds는 자신만의 좌표시스템을 이용함.

## Sample Images

- Frame, Bounds 표현
![image](/images/sample-frame-bounds-1.png)

- View의 bounds를 (10, 10)으로 변경했을 때
![image](/images/sample-frame-bounds-2.png)

## Details
> 공식 문서와 함께 살펴보기 (SFTD, Straight From the Docs)

### [1. Frame](https://developer.apple.com/documentation/uikit/uiview/1622621-frame)

![image](/images/frame.png)

### [2. Bounds](https://developer.apple.com/documentation/uikit/uiview/1622580-bounds)

![image](/images/bounds.png)

##### ㅁ Frame, Bounds 공통점
- 뷰의 위치와 사이즈를 나타내는 사각형입니다.
- 사각형의 좌표는 항상 점으로 지정됩니다.
- 프레임 사각형을 변경하면 `draw(_ :)` 메서드를 호출하지 않고도 뷰가 자동으로 다시 표시됩니다. 프레임 사각형이 변경 될 때 UIKit에서 `draw(_ :)` 메서드를 호출하게하려면 contentMode 속성을 UIView.ContentMode.redraw로 설정합니다.
- 이 속성에 대한 변경 사항은 애니메이션으로 표시 할 수 있습니다.

##### ㅁ 차이점
- Frame은 superView의 좌표계에서, Bound는 그 자신의 좌표계로 나타냅니다.
- Frame에만 해당: transform 속성에 비정상 변환이 포함 된 경우 frame 속성의 값은 정의되지 않으므로 수정하면 안됩니다. 이 경우 center 속성을 사용하여 뷰의 위치를 ​​변경하고 bounds 속성을 사용하여 크기를 조정하십시오.

## Links
- [제드님 블로그 Frame과 Bounds의 차이](https://zeddios.tistory.com/203)
