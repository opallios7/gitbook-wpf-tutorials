# WPF Troubleshooting (WPF 문제해결)

내가 컨설턴트였던 동안에 WPF에는 개발자들이 많은 시간을 소모할 수 있는 전형적인 문제가 있었다. 그래서 가장 일반적인 실수를 해결하는 방법에 대한 목록을 만들기로 결심했다. 나는 이것이 도움이 되길 희망한다.

### Layout (레이아웃)

+ <b> 스크롤바는 활성화 또는 보여지지 않는다.</b>
    + 만약 컨트롤이 수직 패널안에 있다면, 무한 높이의 컨트롤을 레이아웃에게 제공한다. 스택 패널을 도킹패널로 바꾸는 것을 고려해라.
    
+ <b> 데이터 템플릿을 생성하고 HorizontalAlignment를 Stretch로 설정했지만 항목이 늘어나지 않는다.</b>
    + 리스트의 HorizontalContentAlignment를 Stretch로 설정하라.

### DataBinding (데이터 바인딩)

+ <b> 값을 변경했는데 바인디이 변경된 값을 반영하지 않는다. </b>
    + 만약 바인딩 오류가 있다면 Visual Studio 출력창을 확인해라.
    + 당신의 데이터가 INotifyPropertyChanged를 제공하는가?
    + 데이터를 변경하지 않고 단지 PropertyChanged 이벤트를 발생하는 것만으로는 작동하지 않는다. 왜냐하면 바인딩은 옛날값과 새로운값이 다른지를 검사하기 때문이다.
    
### Performance (성능)

+ <b> 아이템 목록의 렌더링 하는데 너무 오래 걸린다. </b>
    + 목록이 가상화되지 않았다. 이말은 모든 아이템이 생성되어지더라도 보여지지 않는다. 이를 피하기 위해서는 다음을 확인하기 바란다.
        + ScrollViewer.CanContentScroll은 반드시 False로 설정되어 있어야 한다.
        + 그루핑은 비활성화 되어 있어야 한다.
        + 아이템 패널을 가상화를 제공하지 않는 것으로 바꿔야 한다.
    + 아주 복잡한 데이터 템플릿을 사용하고 있다.
    
+ <b> 애니메이션은 CPU 부하가 높다. </b>
    + WPF는 하드웨어 가속을 사용할 수 없고, 소프트웨어 렌더링을 한다. 다음과 같은 이유 때문이다.
        + 윈도우에 AllowTransparancy를 True로 설정했다.
        + 빠른 픽셀 쉐이더(Effects) 대신에 기존의 BitmapEffect를 사용하고 있다.
        + 그래픽 아답타 또는 드라이버가 DirectX를 지원하지 않는다.
        
### Custom Controls (커스텀 컨트롤)

+ <b> 커스텀 컨트롤을 만들었는데 템플릿이 보이지 않는다. </b>
    + DefaultStyleKeyProperty의 메타데이터를 재정의 했고 그것으로 설정되어 있는지 확인하라.
    + 템플릿이 스타일로 둘러싸여져 있고 둘다 맞는 TargetType을 가지고 있는지 확인하라.
    + 기본 스타일이 포함된 리소스 딕셔너리가 로드되었는지 확인하라.
    
+ <b> 나의 컨트롤 템플릿에 {TemplateBinding}를 사용하는데 작동이 안된다. </b>
    + 대부분의 경우 {TemplateBinding Property}을 {Binding Property RelativeSource={RelativeSource TemplatedParent}}로 바꿔야 한다.
    + 오직 컨트롤 템플릿의 내용안에 TemlateBinding을 사용할 수 있다. 그외 다른 어느곳에서도 실행이 안된다.
    + 트리거내 부모 프로퍼티에 접근하고 싶다면, Relative Source Self를 사용하여 일반 바인딩을 해야 한다.
    + TemplateBinding은 오직 템플릿의 VisualTree안에서만 동작한다. LogicalTree에만 있는 아이템에서는 사용할 수 없다. Freezable 또는 양방향 바인딩을 할 수 없다.

    
