# TableView cell Height
| 질문출처 | 작성자 |
| :--- | :---: |
| 룩핀 | 썽니 |

## Question
- UITableView를 구성할때 셀의 컨텐츠에 따라 높이를 설정하고싶다면 어떻게 해야하나요?

## Simple Answer
1. 각 IndexPath 별로 셀 내 컨텐츠의 높이를 계산하여 `tableView:heightForRowAtIndexPath:` 메서드로 셀의 높이를 지정
2. `AutomaticDimension`을 통해 셀 높이가 유동적으로 선언한 후, `tableView:estimatedHeightForRowAtIndexPath:` 메서드 혹은 직접 지정을 통해 테이블 뷰의 프로퍼티인 `estimatedRowHieght`를 설정 
  > ㅁ 필수 조건:  
  > - 컨텐츠의 오토레이아웃을 설정
  > - heightForRowAtIndexPath 함수를 오버라이딩 해서는 안됨  

  > ㅁ 주의: 테이블을 reload 할 때 estimatedRowHeihgt에 따라 스크롤 position이 정해지기 때문에 추정치를 너무 작게 잡으면 테이블을 reload 했을 때 이상한 곳에 스크롤 되는 경우가 발생함.

#### - Sample Code
``` swift
var myTableView = UITableView()

// Answer 1)
func tableView(_ tableView: UITableView, heightForRowAtIndexPath indexPath: IndexPath) -> CGFloat {
  return 500
}

// Answer 2)
// AutomaticDimension
myTableView.rowHeight = UITableViewAutomaticDimension

// 직접 대입
myTableView.estimatedRowHeight = 500

// 메서드 사용
func tableView(_ tableView: UITableView, estimatedHeightForRowAt indexPath: IndexPath) -> CGFloat {
  return 500
}
```

## Details
> 공식 문서와 함께 살펴보기 (SFTD, Straight From the Docs)

### [1. Working with Self-Sizing Table View Cells](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/AutolayoutPG/WorkingwithSelf-SizingTableViewCells.html)

![image](/images/self-sizing-tableview-cells-1.png)
- 오토 레이아웃을 사용하여 셀의 높이를 정의 할 수 있으나 이 방식이 셀 높이를 설정하는 default 값은 아닙니다. 일반적으로 셀의 높이는 tableView delegate의 `tableView : heightForRowAtIndexPath :` 를 사용합니다.
- 따라서 셀의 self-sizing을 가능하게 하려면 테이블뷰의 `rowHeight` 프로퍼티를 `UITableViewAutomaticDimension`으로 설정해야합니다. 또한 `estimatedRowHeight` 프로퍼티에도 값을 할당해야합니다. 이 두 속성이 설정되면 시스템은 행의 실제 높이를 계산하는데 오토레이아웃을 사용합니다.

![image](/images/self-sizing-tableview-cells-2.png)
- 그런 다음 셀의 content view 내에 셀의 컨텐츠를 배치하세요. 셀의 높이를 정의하기 위해서는, content view의 top edge와 bottom edge 사이의 제약조건들을 끊기지 않도록 설정해야 합니다. 즉, 셀의 컨텐츠 뷰에 오토레이아웃을 제대로 설정하세요.
- 뷰에 본래의 컨텐츠 높이가있는 경우 시스템은 해당 값을 사용합니다. 그렇지 않은 view 또는 content view 자체에 적절한 높이 제약 조건을 추가해야합니다.

![image](/images/self-sizing-tableview-cells-4.png)
- 또한 예상되는 행 높이(estimated row height)를 가능한 한 정확하도록 만드십시오. 시스템은 추정값을 기반으로 스크롤 막대 높이와 같은 항목을 계산합니다. 예상치가 정확할수록 사용자 경험이 원활 해집니다.

### [2. UITableViewAutomaticDimension](https://developer.apple.com/documentation/uikit/uitableviewautomaticdimension?language=objc)
   
![image](/images/automaticDimension.png)
 - 지정된 dimension의 기본 값을 나타내는 상수.

### [3. EstimatedRowHeight](https://developer.apple.com/documentation/uikit/uitableview/1614925-estimatedrowheight)
  
![image](/images/estimatedRowHeight.png)
- 행 높이를 음수가 아닌 값으로 제공하면 테이블 뷰를 로드하는 성능이 향상 될 수 있습니다.
- 테이블에 가변적인 높이의 행이 있을 경우 높이를 계산하는데 다소 시간이 걸릴 수 있음. 
- 기본값은 `automaticDimension`입니다. 즉, 테이블 뷰는 사용자를 대신하여 사용할 것으로 예상되는 높이를 선택합니다. 값을 0으로 설정하면 테이블 뷰가 각 셀의 실제 높이를 요청하게하는 예상 높이가 비활성화됩니다. 테이블에서 자체 크기 조정 셀을 사용하는 경우이 속성의 값은 0이 아니어야합니다.
- 추정값을 사용할 때, 테이블 뷰는 스크롤 뷰에서 상속된 `contentOffset` 및 `contentSize` 프로퍼티를 능동적으로 관리합니다. 해당 속성을 직접 읽거나 수정하지 마십시오. 

### [4. UITableViewAutomaticDimension](https://developer.apple.com/documentation/uikit/uitableviewdelegate/1614926-tableview)

![image](/images/tableView_estimatedHeightForRowAt.png)
- 행이 있어야 하는 높이를 추정하는 음수가 아닌 float 값. 추정치가 없을 경우 `automaticDimension`을 반환.


## Links
- [SFTD 관련 참고](https://itnext.io/uicollectionview-uicvdatasource-uicvdelegateflowlayout-straight-from-the-docs-8201a3f12bf5)
