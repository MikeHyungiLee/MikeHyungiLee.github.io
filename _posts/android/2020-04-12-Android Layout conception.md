---
layout: post
title:  Layout 종류와 개념
categories: Android
comments: true
---

### Linear 레이아웃의 개념과 Orientation<br>

<strong>'LinearLayout'이란?</strong><br>

LinearLayout은 포함된 자식 뷰를 '선형'으로 배치시키는 레이아웃이다. 선형으로 배치하기 때문에, '가로 혹은 '세로'방향 등 두가지 방법으로 배치할 수 있다.<br>
LinearLayout의 Orientation 속성값은 'none', 'horizontal', 'vertical'로 선택할 수 있다.<br>

<strong><font color="Red">LinearLayout의 속성</font></strong><br>
① gravity, layout_gravity속성에 대해서 이해해보자.<br>

<table>
  <tr>
    <td>속성</td>
    <td>설명</td>
  </tr>
  <tr>
    <td>gravity</td>
    <td>객체가 자신의 경계 내에서 X축과 Y축의 내용을 배치하는 방법을 지정한다. 설정한 값은 단일 행이나 열 내의 모든 자식 뷰의 가로 및 세로 정렬에 영향을 준다.</td>
  </tr>
  <tr>
    <td>layout_gravity</td>
    <td>View 자신의 위치를 부모 뷰를 기준으로 정렬하는 속성이다. 구성 요소를 셀 그룹에 배치하는 방법을 지정한다. 기본값은 'LEFT | BASELINE'이다.</td>
  </tr>
</table>
<br>
→ 'Margin'과 'Padding', 이 두가지 요소는 비슷하면서도 서로 달라 자칫 헷갈리기 쉬우니 여기서 개념을 확실히 잡아 두는 것이 중요하다.<br>
'배치기준(center, left, right)'이 먼저 적용이 되고, 그 적용된 기준선에 대해 'margin값'이 적용된다는 것을 알 수 있다.<br>

<strong>Margin과 Padding</strong><br>

<table>
  <tr>
    <td>속성</td>
    <td>설명</td>
  </tr>
  <tr>
    <td>layout_margin(외부 여백)</td>
    <td>뷰의 왼쪽, 위쪽, 오른쪽 및 아래쪽에 추가 공간을 지정한다.</td>
  </tr>
  <tr>
    <td>padding(내부 여백)</td>
    <td>왼쪽, 위쪽, 오른쪽 및 아래쪽 가장자리의 padding을 픽셀 단위로 설정한다. padding은 view의 가장자리와 view의 내용 사이의 간격을 지정한다.</td>
  </tr>
</table>
<br>
'Padding'속성은 Marginㄹ과 달리 View 자기 자신의 영역이 움직이는 것이 아니다. 대신 View가 Drawing하는 내부 컨텐츠가 View 기준선으로부터의 여백을 결정한다.<br>
※'Margin'은 View의 기준선에 여백을 설정하여, <strong>View의 영역 자체를 옮기는 것이고,</strong>Padding은 View의 기준선은 그대로 있지만 <strong>그려야 할 내부 컨텐츠의 영역에 여백을 주는 것</strong>이다.<br>

<strong><font color="Blue">weight 속성</font></strong><br>
'weight'속성은 ViewGroup 전체 크기에서 View가 갖는 크기의 비중을 설정하는 속성이다.<br>
기존에 알지 못했던 'weightSum'속성에 대해서 알아보자.<br>
<strong><font color="Red">'weightSum'</font></strong>속성은 자신의 비중총합을 설정할 수 있는 속성이다. <br>
<strong>※ View가 비율로 지정될 쪽의 사이즈를 '0dp'로 지정해야한다.(안드로이드 개발자 레퍼런스)</strong><br>

<strong><font color="Red">레이아웃 중첩(nested)</font></strong><br>
<strong>'LinearLayout의 중첩'</strong>이란? LinearLayout 안에 또 LinearLayout 등을 넣는 것을 의미한다. 이렇게 하는 이유는 LinearLayout은 '가운데 또는 세로', 즉 어느 한 방향의 배치 기준만 가질 수 있기 때문이다.<br>

<img src="/images/android/2020-04-12 nested layout.png" alt="blog capture" title="capture img" width="500">  <br>

<strong>'안드로이드의 지원 라이브러리(Support Library)'</strong>는 프레임워크에는 포함되지 않았지만, 많은 유용한 기능을 포함하고 있다. 안드로이드를 개발할때, 좀 더 편리하게 개발할 수 있도록 도와주는 라이브러리이다. 이런 라이브러리들이 프레임워크가 아닌 별도의 라이브러리가 된 가장 큰 이유는 '하위 호환성'때문이다. 하위 버전에서는 새로운 버전에서 생긴 UI요소들을 사용할 수 없기 때문이다.<br>

***

### RelativeLayout 레이아웃의 개념<br>

<strong>'RelativeLayout'이란?</strong><br>

'RelativeLayout'은 View를 '부모 뷰' 또는 '다른 View'와의 상대적인 위치 관계 기반으로 배치한다.<br>
<strong><font color="Red">RelativeLayout의 속성</font></strong>을 크게 보면 <strong>2가지</strong> 정도로 생각할 수 있는데, 하나는 <strong>부모 뷰를 기준으로 배치하는 것</strong>이고, <strong>다른 하나</strong>는 <strong>부모 뷰가 같은 형제 뷰를 기준으로 배치하는 것</strong>이다.<br>

<strong><font color="Red">※RelativeLayout을 사용할때의 주의점</font></strong><br>
① View객체를 화면이 아닌 [Component Tree]에 Drag&Drop해야한다. 그 이유는 '상대적인 배치' 기준인 'RelativeLayout'상태에서 화면으로 직접 끌어 옮기면 <strong><font color="Red">다른 뷰와의 관계, margin 값이 자동으로 생성되어 버리기 때문</font></strong>이다. 그렇기 때문에 RelativeLayout상태에서는 <strong>XML에 코드를 직접 View의 속성을 정의</strong>하거나, [Design]탬에서 [Component Tree]에 버튼을 추가한 후 속성을 변경하여 배치하는 것이 좋다.<br>

RelativeLayout에서 View의 배치는 <strong>'edge'</strong>를 기준으로 이루어지므로, 'edge'에 대한 이해가 선행된다면 전체적인 이해 또한 보다 수월해진다.<br>
View에서의 'edge'는 일종의 '기준선'을 의미한다.<br>

<strong>※기준선 구조 그림</strong><br>
<img src="/images/android/2020-04-12 Relativelayout alignment.png" alt="blog capture" title="capture img" width="500"><br>

### <strong>RTL(Right To Left) 지원</strong><br>
앞서서 부모 뷰를 기준으로 하여 상대적으로 뷰들을 배치하는 방법에 대해서 배워보았다. 그런데 'alignParentStart'와 'alignParentEnd'속성은 무엇인가?<br>
'alignParentStart'와 'alignParentLeft'는 똑같은 동작을 하는데, 사실 두 속성의 차이는 'RTL(Right To Left)보기 지원'과 관련이 있다.<br>

우선<strong><font color="Red">'RTL'</font></strong>이란 무엇일까요? 이는 <strong>화면을 보는 방식</strong>을 의미한다. 사실 국가마다 조금씩 차이가 있지만, 한국의 경우에는 일반적으로 <strong>LTR(Left To Right)방식</strong>을 사용한다. 즉 <strong>왼쪽에서 오른쪽으로 화면을 본다는 의미</strong>이다. <strong>RTL(Right To Left)</strong>은 거꾸로 <strong>오른쪽에서 왼쪽으로 보는 방식</strong>이다.<br>

### <strong>형제 뷰 기준 배치</strong><br>
이번에 배울 내용은 부모 뷰가 기준이 아닌 <strong>'형제 뷰를 기준으로 배치하는 방법'</strong>이다. 형제 뷰란, 같은 뷰를 공유하는 View들을 의미한다.<br>
<strong>형제 뷰의 기준선을 일치시키는 방법으로 지정하는 것</strong>이다.<br>
<strong>ex) layout_alignLeft = "@+id/button14"</strong>라는 명령은 <strong>"자기 자신의 왼쪽 기준선을 'button14'의 왼쪽 기준선과 일치시킨다."</strong><br>

<img src="/images/android/2020-04-13 RelativeLayout(2).png" alt="blog capture" title="capture img" width="700"><br>

위의 그림 이외에 <strong>'layout_alignBaseLine'</strong>이라는 속성이 있다. 이 속성은 다른 속성들과는 다르게  <strong>View의 테두리 기준선이 아닌 컨텐츠의 기준선을 맞춘다.</strong><br>

### LinearLayout과 RelativeLayout의 장단점 비교 <br>
<strong>RelativeLayout은</strong> LinearLayout에 비해 View의 중첩을 줄일 수 있는 장점이 있다. 앞서 LinearLayout을 배울때, View의 정렬 방향이 바뀌면서  LinearLayout 안에 또 다른 LinearLayout을 넣어야 했지만, <strong><font color="Red">'레이아웃의 중첩'은 UI 성능을 떨어뜨리는 주요 원인 중 하나가 된다.</font></strong>그런 면을 볼때 RelativeLayout의 장점을 활용해서 레이아웃을 만들어보는 것도 좋다.<br>

<strong><font color="Red">※RelativeLayout으로 레이아웃을 작성할때, 주의해야될 점</font></strong><br>
① <strong>'기준'으로 잡을 View를 찾아야 한다.</strong><br>
② 레이아웃 편집은 <strong>[Text]탭</strong>에서 타이핑하여 진행해야 한다. 그 이유는 <strong>RelativeLayout</strong>은 마우스로 글어 View를 배치할 경우 자동으로 'margin 및 관계'가 생성되어 오히려 편집이 어려워지기 때문이다.<br>

***

### ConstraintLayout 레이아웃의 개념<br>

<strong>'ConstraintLayout'이란?</strong><br>

ConstraintLayout은 <strong>RelativeLayout과 LinearLayout을 완전히 대체 가능한 <font color="Red">'ConstraintLayout'</font>에 대해 학습한다.</strong>'ConstraintLayout'은 '제약조건'을 기반으로 View를 배치하는 레이아웃으로, Android SDK에 기본적으로 포함된 것은 아니지만, Google에서 제공하는 'Support 라이브러리'로 제공되며 매우 강력하다.<br>
<strong>Google은 레이아웃을 작성할 때 ConstraintLayout을 사용할 것을 권장하고 있다.</strong><br>

<strong><font color="Red">Constraint 레이아웃과 제약</font></strong><br>
<strong>ConstraintLayout의 모든 View에는 적어도 하나씩의 '수평제약'과 '수직 제약'이 있다.</strong><br>

<img src="/images/android/2020-04-13 ConstraintLayout(1).png" alt="blog capture" title="capture img" width="400"><br>
다음과 같이 '수평','수직에 기준한 제약을 각 각 하나식 등록을 하게 되면, Button의 위치를 결정할 수 있게 된다.<br>

### 다른 뷰와의 제약 관계<br>
기존에 추가한 버튼에 새로 추가한 버튼을 '수평', '수직'Constraint관계로 엮어준다.<br>

<img src="/images/android/2020-04-13 ConstraintLayout(2).png" alt="blog capture" title="capture img" width="400"><br>

<strong>ConstraintLayout의 강력한 기능인 <font color="Red">'Bias'</font></strong>에 대해서 알아보자.<br>
이 <strong>'Bias'기능은 수평 또는 수직 방향으로 제약을 2개 추가하게 되면 더는 제약을 지킬 수 없는 상태가 된다. 이 경우 Constraint는 매우 유용한 기능인 'Bias'를 사용할 수 있다.</strong><br>
<img src="/images/android/2020-04-13 ConstraintLayout(3).png" alt="blog capture" title="capture img" width="600"><br>

위의 캡쳐를 보면, 아래에 위치한 버튼은 좌측 제약은 좌측 상단에 위치한 버튼과 연결되어 있고, 우측제약은 부모 뷰와 연결이 되어 있는 것을 알 수 있다. 이 경우는 현재 크기로는 양쪽 제약을 모두 지킬 수 없는 상태이다.<br>
이렇게 <strong>서로 동시에 성립할 수 없는 제약 상태가 되면, </strong> ConstraintLayout은 각 제약을 마치 '서로 당기는 힘'처럼 사용한다. <br>
아래 위치한 버튼의 좌측 제약과 우측 제약이 같은 힘으로 버튼을 당긴다고 생각해보자.<br>
이때 'Bias(선호도)'는 '퍼센테이지'로 표현된다. 기본값은 '50'으로 양쪽 제약 가운데에 배치되지만, 그 값을 변경함으로써 뷰의 위치를 퍼센테이지로 결정하게 된다. 즉 제약의 margin을 지키는 범위 내에서 자유롭게 배치할 수 있다.<br>

<img src="/images/android/2020-04-13 ConstraintLayout(4).png" alt="blog capture" title="capture img" width="600"><br>

위의 캡쳐는 'Bias(선호도)'를 '20'으로 조정한 결과이다. 버튼의 위치가 제약을 지키는 범위 내에서 20% 지점에 위치한 것을 확인할 수 있다. <br>

수평 제약에 대한 Bias 설정을 해봤으니, 수직 제약도 추가하여 수직제약에 대한 Bias도 확인해보자.<br>

### Aspect Ratio<br>
'ConstraintLayout'의 크기의 기준은 <strong>'wrap_content, match_constraint, fixed_size'</strong>등의 3가지 경우가 있다.<br>

여기서 'match_constraint'로 'layout_width'나 'layout_height'의 속성 중 하나를 지정하게 되면, View의 크기 비율을 지정할 수 있다. <strong>'aspectRatio(종횡비, 가로와 세로의 비율)'</strong> 속성이 그것이다.<br>

### Circle 제약<br>
<strong>layout_constraintCircle</strong>속성은 특정 뷰를 기준으로 View를 원형으로 배치되도록 하는 기능이다.<br>

<table>
  <tr>
    <td width="400">
      <img src="/images/android/2020-04-13 Circle Constraint.png" alt="blog capture" title="capture img" width="300"><br>
    </td>
    <td width="400">
      <img src="/images/android/2020-04-13 Circle constraint(1).png" alt="blog capture" title="capture img" width="300"><br>
    </td>
    <td width="400">
      이 Circle 제약에서는 하단에 위치한 버튼 위에 TextView를 위치시키고, 이 TextView의 위치는 타켓이 되는 뷰의 중점을 기준으로 '각도'와 '떨어진 거리'를 각각 'circleAngle'과 'circleRadius'값들로 설정한다.<br>
      이는 화면의 해상도가 바뀌어도 정확한 'angle' 방향에 위치하게 되는 강력한 기능이다.<br>

      ① layout_constraintCircle <br>
      ② layout_constraintCircleAngle <br>
      ③ layout_constraintCircleRadius <br>

    </td>
  </tr>
</table>
<br>

### 가이드라인(Guideline)<br>
<strong>'Guideline'은 뷰를 더 쉽게 배치할 수 있도록 '기준선'을 추가하는 것이다.</strong>'수직'과 '수평'의 두 가지 종류가 있는데, 우선 'vertical guideline'에 대해서 살펴보자.<br>

<strong>'Component Tree'</strong>에서 ConstraintLayout을 우클릭하고, [Helpers] - [Add ~ Guideline]<br>

가이드라인의 상단부에 타입을 바꿀 수 있는 버튼이 있는데, 이를 클릭하면 <strong>'begin, end, percent'</strong>순으로 전환됨을 확인할 수 있다.<br>

이 가이드 라인은 <strong><font color="Red">특히 '퍼센트(비율)'로 배치할 때 매우 유용하다.</font></strong><br>
예를 들어 특정 버튼이 상단으로부터 '80%', 크기는 '10%', 좌측에서 '30%' 떨어진 곳에 위치한다면, 화면의 사이즈가 바뀌어도 걔속 비율상 같은 '크기'와 같은 '위치'로 존재하게 된다. 단 constraintGuidePercent 속성을 입력할때는 'constraintGuideBegin', 'constraintGuideEnd'등 다른 속성은 반드시 지워야 한다. <br>

### 체인(Chain)<br>
'ConstraintLayout'에서 'Chain'은 <strong><font color="Red">가로축 또는 세로축을 기준으로 여러 개의 View를 그룹처럼 관리하게 해 주는데,</font></strong>별도로 속성이 존재하는 것이 아니라 '2개의 뷰가 서로를 참조'하고 있으면 Chain으로 묶인다.<br>
이렇게 '상호 제약'이 걸린 상태가 바로 '체인(Chain)'이다. 여러 개의 View가 체인으로 연결되어 있을 때 그 첫 번째 View를 가르켜 <strong><font color="Red">'Chain Head'</font></strong>라고 부른다.<br>

이 'Chain Head'를 담당하는 View에는 Chain 스타일을 지정할 수 있는데, 이 Chain Head를 담당하는 뷰에서 지정 가능한 스타일은 아래와 같다.<br>

<table>
  <tr>
    <td>스타일</td>
    <td>설명</td>
  </tr>
  <tr>
    <td>CHAIN_SPREAD</td>
    <td>각 View들이 동일한 간격으로 펼쳐지게 한다.</td>
  </tr>
  <tr>
    <td>CHAIN_SPREAD_INSIDE</td>
    <td>CHAIN SPREAD처럼 펼쳐지지만 View의 양끝은 펼치지 않는다. 즉 여백을 두지 않는다.</td>
  </tr>
  <tr>
    <td>CHAIN_PACKED</td>
    <td>View 사이에 여백을 두어 펼치지 않고 딱 붙게 한다. CHAIN_PACKED상태에서는 Bias로 'PACKED'된 뷰의 위치를 조정할 수 있다.</td>
  </tr>
  <tr>
    <td>WEIGHTED CHAIN</td>
    <td>체인으로 묶인 View의 일부가 'match_constraint'인 경우 '비율'로서 크기를 지정할 수 있다.</td>
  </tr>
</table>

<img src="/images/android/2020-04-13 ConstraintLayout chain.png" alt="blog capture" title="capture img" width="600"><br>

<strong>※ ConstraintLayout으로 레이아웃 작성하</strong><br>
① 제약의 중심이 될 가이드라인을 생성하기.<br>
② 레이아웃상에 각 View를 위치시키고, 필요에 따라 각 가이드라인에 제약조건을 걸어 각 View요소를 위치시킨다.<br>

<img src="/images/android/2020-04-13 ConstraintLayout guideline layout.png" alt="blog capture" title="capture img" width="300"><br>


### 전체적인 학습내용을 복습한다.<br>

<strong><font color="Red">LinearLayout ?</font></strong>
1. 레이아웃은 ViewGroup의 실제 구현 클래스이며 자식 뷰를 어떻게 배치할지 결정한다. 자주 사용하는 레이아웃에는 LinearLayout, RelativeLayout, ConstraintLayout등이 있다.<br>
2. LinearLayout은 가로 또는 세로로 뷰를 순차적으로 배치한다.<br>
3. LinearLayout의 배치 기준은 gravity, layout_gravity 속성을 이용하여 변경이 가능하다.<br>
4. gravity 속성은 뷰 자신의 컨텐츠 또는 자식 뷰들의 배치 기준을 변경한다.<br>
5. layout_gravity 속성은 부모 뷰 안에서 뷰 자신의 배치 기준을 변경한다.<br>
6. Margin 속성은 뷰가 부모 뷰로부터 떨어진 여백을 설정한다.<br>
7. Padding 속성은 자신의 컨텐츠 또는 자식 뷰들이 떨어지는 영역을 설정한다.<br>
8. LinearLayout의 weight 속성을 사용하면, View의 크기를 비율로 설정할 수 있다.<br>
9. LinearLayout에서 여러 개의 뷰 중 한 개만 weight 속성을 설정하면, weight를 설정하지 않은 다른 뷰가 그려지고 남은 영역의 전부를 차지하게 된다. <br>
10. LinearLayout에서 정렬 기준(Orientation)이 다양한 UI를 만들려면 레이아웃을 중첩해서 사용해야 한다.<br>

***

<strong><font color="Red">RelativeLayout ?</font></strong>
11. RelativeLayout은 '부모 뷰'또는 '형제 뷰'와의 관계를 지정하여 View를 배치한다.<br>
12. RelativeLayout의 'align관련 속성은 자신의 기준선과 부모 뷰, 형제 뷰의 기준선을 맞추는 것이다.<br>
13. RTL(Right To Left)지원이란 국가마다 다른 '보기 방식의 지원'을 의미한다.<br>
14. RTL 지원을 적용하려면 left대신 start, right대신 end를 사용하는 것이 좋다.<br>
15. RelativeLayout을 사용하면 상대적인 관계지정이 되기 때문에 레이아웃 중첩을 줄일 수 있다.<br>

***

<strong><font color="Red">ConstraintLayout ?</font></strong>
16. ConstraintLayout은 레이아웃 편집창에서 사용하는 미리보기만을 위한 속성이 있다.<br>
17. ConstraintLayout은 뷰의 위치를 결정하기 위해 제약 조건을 사용한다.<br>
18. 각 뷰는 상/하/좌/우 제약을 의미하는 'constraintTop, constraintBottom, constraintLeft, constraintRight' 속성이 있다.<br>
19. <strong>수평 제약과 수직 제약 각각 1개 이상의 제약이 있어야 View의 위치를 결정<strong>할 수 있다.<br>
20. 각 뷰의 상/하/좌/우 제약을 다른 뷰 또는 부모 뷰의 면과 연결하면 제약이 지정된다.<br>
21. 제약조건은 마치 RelativeLayout의 관걔와 비슷하며, 제약 조건 이후 여백(margin)을 설정할 수 있다.<br>
22. 제약 조건이 수평/ 수직에 대하여 양방향으로 설정된 경우, 두 제약을 동시에 지킬 수 없는 상태가 되는데, 이때 ConstraintLayout은 선호도(Bias)값을 설정하여, 제약을 지키는 범위 내에서 뷰를 퍼센티지로 배치할 수 있다.<br>
23. Circle 제약은 뷰를 원형으로 배치할 수 있게 하는 강력한 기능이다.<br>
24. ConstraintLayout은 뷰를 쉽게 배치할 수 있도록 돕는 가이드라인을 제공한다. 가이드라인 역시 View로 취급되며, 방향과 여백으로 위치를 지정하거나 퍼센트로 위치를 지정할 수 있다.<br>
25. 뷰의 제약이 서로를 참조하고 있는 형태를 Chain이라고 한다. 이 Chain을 활용하면, 별도의 레이아웃 없이 View를 그룹화하여 관리할 수 있다.<br>
26. ConstraintLayout은 뷰의 중첩을 줄일 수 있어 UI 성능 향상에 유리하다.<br>
