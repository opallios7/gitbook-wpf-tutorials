# Instroduction to WPF Layout (WPF 레이아웃 소개)

### Why layout is so important (레이아웃이 왜 중요한가?)

컨트롤의 레이아웃은 응용프로그램의 유용함에 있어 중요하다. 고정된 픽셀 좌표기반으로 정렬된 컨트롤들은 제한된 환경에서 작동한다. 그러나 다른 화면 해상도 또는 다른 폰트 크기에 사용하길 원하는 즉시 안 될것이다. WPF는 일반적인 위험을 피하는 것을 도와줄 풍부한 세트가 있는 레이아웃 패널을 제공한다.

WPF에서 제공하는 가장 인기있는 5가지 레이아웃은 다음과 같다.

+ Grid Panel
+ Stack Panel
+ Dock Panel
+ Wrap Panel
+ Canvas Panel

### Best Practices (최선의 선택)

+ 고정된 위치를 피하라 - 패널내에 엘리먼트들간의 간격을 결합하여 정렬하는 프로퍼티를 사용한다.
+ 고정된 크기를 피하라 - 가능하면 엘리먼트들의 Width와 Height를 자동으로 설정한다.
+ 캔바스 패널을 레이아웃 엘리먼트에 악용하지 마라. 벡터 그래픽을 위해서만 사용해라.
+ 스택 패널을 다이얼로그의 레이아웃 버튼에 사용하라
+ 그리드 패널을 고정된 데이터 입력 폼에 사용하라. 라벨을 위한 Auto Size 컬럼과 텍스트박스를 위한 Star Size를 생성하라.
+ 데이타 템플릿의 그리드 패널이 있는 ItemControl을 동적 키-값 목록 레이아웃에 사용하라. SharedSize 특성은 라벨 폭을 동기화하는데 사용하라.

### Vertical and Horizontal Alignment (가로, 세로 정렬)

수평과 수직 정렬 프로퍼티는 패널의 하나 또는 다양한 면에 컨트롤을 붙이는데 사용한다. 다음의 그림은 서로 다른 조합으로 크기조정이 어떻게 되는지를 보여준다.

![](/assets/v2_alignment.png)

### Margin and Padding (마진 및 패딩)

마진과 패딩 프로퍼티는 컨트롤 내의 주변 일부 공간을 예약하여 사용할 수 있다.

+ 마진은 컨트롤 주변의 여분공간이다.
+ 패딩은 컨트롤 내부속 여분공간이다.
+ 컨트롤 바깥쪽 패딩은 컨트롤 안쪽의 마진이다.

![](/assets/padding_margin.png)

### Height and Width (높이와 넓이)

그다지 추천하는 방법은 아니지만 모든 컨트롤들은 하나의 엘리먼트에 고정된 크기를 제공하는 높이와 넓이 프로퍼티를 제공한다. 더 좋은 방법은 수용가능한 범위를 정의한 MinHeight, MaxHeight, MinWidth, MaxWidth 프로퍼티들을 사용하는 것이다.
너비 또는 높이를 자동으로 설정하면 컨트롤의 크기가 내용의 크기로 조정됩니다.

### Overflow Handling (오버플로우 핸들링)

#### Clipping (클리핑)

레이아웃 패널은 패널의 경계선을 넘어서는 자식 엘리먼트의 부분을 자른다. 이 동작은 ClipToBounds 프로퍼티를 true 또는 false 설정에 의해 제어할 수 있다.

![](/assets/cliptobounds.PNG)

#### Scrolling (스크롤)

내용이 너무커서 보여줄수 있는 크기에 다 보여지지 않는다면 ScrollViewer로 감싸 스크롤로 보여줄 수 있다. ScrollViewer는 두개의 스크롤 바를 보여줄 영역을 선택해서 사용한다.

스크롤바의 가시성은 수평, 수직 ScrollbarVisiblility 프로퍼티에 의해 제어할 수 있다.

```
<ScrollViewer>
    <StackPanel>
        <Button Content="First Item" />
        <Button Content="Second Item" />
        <Button Content="Third Item" />
    </StackPanel>
</ScrollViewer>
```
 
### Related Articles (관련 정보)

[MSDN - The Layout System](http://msdn.microsoft.com/en-us/library/ms745058.aspx)