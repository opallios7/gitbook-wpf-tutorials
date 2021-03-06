# Dependency Properties (종속적 프로퍼티)

### Introduction (소개)

WPF로 응용프로그램을 개발을 막 시작하면 머지않아 종속적 프로퍼티를 발견할 것이다. 그것은 .NET 프로퍼티와 매우 비슷하게 보이지만 숨어있는 개념은 매우 복잡하고 강력하다.

가장 큰 차이점은 일반 .NET 프로퍼티는 클래스내의 비공개 맴버로부터 직접 읽는 반면, 종속적 프로퍼티는 DependencyObject로부터 상속된 GetValue()메소드가 호출될때 동적으로 해석한다. 

종속적 프로퍼티의 값을 입력할 때 object필드에 저장되지 않고, DependendyObject의 기본 클래스에서 제공되는 키와 값의 Dictionar안에 저장된다. 접근하기 위한 키는 프로퍼티의 이름이고, 값은 입력하고 싶은 값이다.

종속적 프로퍼티의 장점음 다음과 같다.

+ <b>Reduced memory footprint (절약된 메모리 공간)</b>

일반적으로 UI 컨트롤의 90% 이상이 초기값에 머물러 있을때 각 프로퍼티에 대해 필드를 저장하는 것은 엄청난 손실이 발생한다. Dependency properties는 인스턴스에서 오직 수정된 프로퍼티만을 저장하는 것으로 문제를 해결했다. 기본값은 dependency 속성안에 한번 저장된다.

+ <b>Value inheritance (값 상속)</b>

종속적 프로퍼티에 접근할때 값은 값 확인전략에 의해 확인된다. 로컬값이 설정되지 않은 경우, 종속적 프로퍼티는 값을 찾을때까지 logical tree를 상향 탐색한다. 최상우 요소에 FontSize를 설정하면 재정의한 값을 제외하고 모든 textblock에 적용한다.  

+ <b>Change notification (변경 알림)</b>

종속적 프로퍼티는 변경 알림 메커니즘을 가지고 있다. 프로퍼티 메타데이터에 콜백을 등록함으로써 프로퍼티 값이 변경되었다는 알림을 받습니다. 또한, 데이터바인딩에도 사용된다. 

### Value resolution strategy (값 접근 정책)

항상 종속적 프로퍼티에 접근하면 내부적으로 위에서부터 아래의 방향으로 우선 값을 해석한다. 로컬값이 있는지 , 사용자 지정 스타일 트리거가 활성화되어 있는지 확인하고 값을 찾을때까지 계속 반복한다. 마지막으로 기본값은 항상 사용할 수 있다.

![](/assets/valueresolution.jpg)

### The magic behind it (숨은 마법같은 기능)

각각의 WPF컨트롤은 static DependencyProperty 클래스에 종속적 프로퍼티 설정을 등록한다. 그것들은 각각 키(타입마다 유일해야 함), 콜백과 기본값이 포함된 메타데이터로 구성된다.

종속적 프로퍼티를 사용하기 원하는 모든 타입들은 반드시 DependencyObject로부터 파생되어야 한다. 기본클래스는 종속적 프로퍼티의 로컬 값을 포함하는 키,값의 딕셔너리를 정의한다. 접근키는 종속적 프로퍼티에서 정의되어진 키이다.

.NET 프로퍼티로 감싸져있는 종속적 프로퍼티에 접근하려면 내부적으로 GetValue(DependencyProperty)를 호출한다. 이 메소드는 다음에 설명하고 있는 값 접근 정책에 의해 값을 해석한다. 로컬값이 있으면 딕셔너리로부터 직접 그 값을 읽는다. 만약 설정된 값이 없다면 logical tree와 상속되어진 값을 찾는다. 그래도 값을 찾지 못했다면 프로퍼티 메타데이터에 정의되어진 기본값을 가져온다. 이 접근순서는 아주 단순하지만 주 개념을 보여주고 있다.

![](/assets/depprop.png)


### How to create a DependencyProperty (종속적 프로퍼티를 만드는 방법)

종속적 프로퍼티를 만드는 방법은 당신이 정의한 타입에 static 종속적 프로퍼티 타입의 필드를 추가하고, 종속적 프로퍼티 인스턴스를 생성한 DependencyProperty.Register()를 호출한다. 종속적 프로퍼티의 이름은 반드시 항상 ~Property로 끝나야 한다. 이것이 WPF의 이름정의 규칙이다.

.NET 프로퍼티처럼 접근가능하게 만들기 위해서는 프로퍼티를 추가로 감싸줘야 한다. 이 Wrapper는 단지 DependencyObject와 DependencyProperty의 메소드를 사용하여 내부적으로 값을 가져오거나 설정하는 것만 한다.

<b>중요: 이 프로퍼티에 어떠한 로직도 추가하면 안된다. 이유는 오직 코드에서 프로퍼티를 설정할때만 호출되기 때문이다. XAML에서 프로퍼티를 설정하려면 SetValue()메소드가 직접 호출되어야 한다.</b>

Visual Studio를 사용한다면, 당신은 propdp를 입력하고 탭을 누번누르면 종속적 프로퍼티를 생성할 수 있다.

``` 
// Dependency Property
public static readonly DependencyProperty CurrentTimeProperty = 
     DependencyProperty.Register( "CurrentTime", typeof(DateTime),
     typeof(MyClockControl), new FrameworkPropertyMetadata(DateTime.Now));
 
// .NET Property wrapper
public DateTime CurrentTime
{
    get { return (DateTime)GetValue(CurrentTimeProperty); }
    set { SetValue(CurrentTimeProperty, value); }
}
``` 
 
각각의 종속적 프로퍼티는 변경알림, 제한값, 검증등을 위한 콜백을 제공한다. 이 콜백들은 종속적 프로퍼티에 등록되어진다.

``` 
new FrameworkPropertyMetadata( DateTime.Now, 
                       OnCurrentTimePropertyChanged, 
                       OnCoerceCurrentTimeProperty ),
                       OnValidateCurrentTimeProperty );
``` 
 
### Value Changed Callback (값 변경 콜백)

변경알림 콜백은 TimeProperty의 값이 변경될때 항상 호출되는 고정메소드이다. 새로운 값은 EventArgs를 통해 
전달되며, 값이 변경되어질 객체는 source를 통해 전달된다.
``` 
private static void OnCurrentTimePropertyChanged(DependencyObject source, 
        DependencyPropertyChangedEventArgs e)
{
    MyClockControl control = source as MyClockControl;
    DateTime time = (DateTime)e.NewValue;
    // Put some update logic here...
}
``` 
 
### Coerce Value Callback (제한값 콜백)

지정 콜백은 예외를 던지지 않고 값의 범위를 벗어나지 않도록 조정할 수 있다. 좋은 예로는 최소값 미만이나 최대한 초과의 값을 설정하는 진행바가 있다. 이 경우 허용된 경계안으로 값을 강제할 수 있다. 다음의 예제는 시간이 지나가지 않도록 제한하는 코드이다.
``` 
private static object OnCoerceTimeProperty( DependencyObject sender, object data )
{
    if ((DateTime)data > DateTime.Now )
    {
        data = DateTime.Now;
    }
    return data;
}
``` 
 
### Validation Callback (검증 콜백)

검증콜백은 값이 유효한지 검사한다. 만약 false가 리턴된다면 ArgumentException이 예외로 던져질 것이다. 다음의 예는 data가 DateTime의 인스턴스인지를 요구하는 코드이다.
``` 
private static bool OnValidateTimeProperty(object data)
{
    return data is DateTime;
}
```
 
### Readonly DependencyProperties (읽기전용 의존적 프로퍼티)

몇몇의 WPF컨트롤의 종속적 프로퍼티는 읽기전용이다. 그것들은 IsMouseOver프로퍼티와 같이 컨트롤의 상태를 보고하는데 자주 사용되곤한다. 이 값을 위해 setter를 제공하는 것은 말이 되지 않는다.

아마도 "왜 그냥 일반적인 .NET프로퍼티를 사용하면 안되지?"라고 자문을 할 것이다. 한가지 중요한 이유는 일반적인 .NET 프로퍼티는 trigger를 설정할 수가 없다.

읽기전용 프로퍼티 생성은 보통 의존적인 프로퍼티의 생성과 비슷하다. DependencyProperty.Register()를 호출하는 대신에 DependencyProperty.RegisterReadonly()를 호출한다. 이것은 종속적 프로퍼티 키를 반환한다. 이 키는 당신의 클래스 필드에 private또는 protected static readonly로 저장되어진다. 키는 당신의 클래스에 있는 값을 설정하기위한 접근과 일반적인 종속적 프로퍼티처럼 사용하도록 한다.

두번째로 할일은 DependencyPropertyKey.DependencyProperty에 할당된 공개 종속적인 프로퍼티를 등록한다. 이 프로퍼티는 외부에서 접근할 수 있는 읽기전용 프로퍼티이다.

``` 
// Register the private key to set the value
private static readonly DependencyPropertyKey IsMouseOverPropertyKey = 
      DependencyProperty.RegisterReadOnly("IsMouseOver", 
      typeof(bool), typeof(MyClass), 
      new FrameworkPropertyMetadata(false));
 
// Register the public property to get the value
public static readonly DependencyProperty IsMouseoverProperty = 
      IsMouseOverPropertyKey.DependencyProperty;    
 
// .NET Property wrapper
public int IsMouseOver
{
   get { return (bool)GetValue(IsMouseoverProperty); }
   private set { SetValue(IsMouseOverPropertyKey, value); }
}
``` 
 
### Attached Properties (첨부 프로퍼티)

첨부 프로퍼티는 의존적 프로퍼티의 특별한 종류 중 하나이다. 값에 대해 어떤것도 모르는 객체에 값을 첨부하는 것을 허용한다.

이 개념을 위한 좋은 예제는 레이아웃 패널이다. 각각의 레이아웃 패널은 그것의 자식 요소를 정렬하는 다른 데이터가 필요하다. 캔바스는 Top과 Left, DocPanel은 Dock등이 필요하다. 당신 자신의 레이아웃 패널을 작성할 수 있기에 그안의 리스트는 무한하다. 그래서, 모든 WPF컨트롤 기반의 모든 프로퍼티를 가질수는 없다는 것을 알게 될 것이다.

이걸 해결하기 위한것이 첨부 프로퍼티이다. 특정 컨텍스트에서 다른 컨트롤의 데이터를 필요로하는 컨트롤에 의해 정의된다. 부모 레이아웃 패널에 의해 할당된 요소가 그 예이다.

첨부 프로퍼티의 값 설정은 첨부 프로퍼티를 제공하는 요소의 접두사를 XAML의 속성에 추가한다. 다음과 같이 버튼의 Canvas.Top과 Canvas.Left 프로퍼티의 설정은 캔바스 패널안에 할당되어 있다.

```
<Canvas>
    <Button Canvas.Top="20" Canvas.Left="20" Content="Click me!"/>
</Canvas>
```
 
```
public static readonly DependencyProperty TopProperty =
    DependencyProperty.RegisterAttached("Top", 
    typeof(double), typeof(Canvas),
    new FrameworkPropertyMetadata(0d,
        FrameworkPropertyMetadataOptions.Inherits));
 
public static void SetTop(UIElement element, double value)
{
    element.SetValue(TopProperty, value);
}
 
public static double GetTop(UIElement element)
{
    return (double)element.GetValue(TopProperty);
}
``` 
 
### Listen to dependency property changes (종속적 프로퍼티 변화 수신)

종속적 프로퍼티의 변화 수신을 원한다면 프로퍼티를 정의하는 타입의 하위클래스 생성, 프로퍼티 메타데이터를 재정의, PropertyChangedCallback 전달을 할 수 있다. 그러나 아주 쉬운 방법은 DependencyPropertyDescriptor를 만들고, AddValueChange() 호출에 의한 callback을 연결하는 것이다.

``` 
DependencyPropertyDescriptor textDescr = DependencyPropertyDescriptor.
    FromProperty(TextBox.TextProperty, typeof(TextBox));
 
if (textDescr!= null)
{
    textDescr.AddValueChanged(myTextBox, delegate
    {
        // Add your propery changed logic here...
    });
} 
``` 
 
### How to clear a local value (로컬 값 제거 방법)

null도 유효한 로컬 값이기 때문에 unset값을 의미하는 상수인 DependencyProperty.UnsetValue가 있다.

```
button1.ClearValue( Button.ContentProperty );
``` 


