# Introduction to XAML (XAML 소개)

XAML은 Extensible Application Markup Language의 약자이다. XAML은 .NET객체등의 계층관계를 생성하고 초기화하는 XML에 기반한 심플한 언어이긴 하지만 원래 객체 tree의 어떤 종류도 생성하도록 사용할 수 있는 WPF를 위해 만들어졌다.

지금의 XAML은 WPF, Silverlight, WF의 워크플로어, XPS 표준 전자종이등 사용자 인터페이스를 생성하는데 사용한다.

WPF의 모든 클래스들은 파라메터가없는 생성자를 가지고 과다한 속성 사용을 합니다. XAML과 같은 XML 언어를 완벽하게 맞추기 위해 만들어졌다.

### Advantages of XAML (XAML의 장점)

XAML에서 실행할 수 있는 모든것은 코드로도 실행할 수 있다. 단지 객체를 생성하고 초기화하는 방법이 다르다. XAML없이 WPF를 사용할 수 있다. XAML로 선언하거나 코드로 작성하는 것은 당신의 맘에 달려있다. XAML로 UI를 선언하면 다음과 같은 장점이 있다.

+ XAML 코드는 짧고 읽기가 쉽다.
+ 코드와 로직을 구분한다.
+ Expression Blend와 같은 그래픽 디자인 툴은 XAML을 요구하낟.
+ XAML과 UI 로직을 구분한 것은 디자이너와 개발자의 역활을 깔끔하게 구분하도록 한다.

### XAML vs. Code

다음의 예제는 텍스트 블럭과 버튼이 있는 StackPanel을 생성하는데 C#코드와 비교하는 것이다.

``` 
<StackPanel>
    <TextBlock Margin="20">Welcome to the World of XAML</TextBlock>
    <Button Margin="10" HorizontalAlignment="Right">OK</Button>
</StackPanel>
```
 
C#으로 하면 다음과 같이 표현된다.

``` 
// Create the StackPanel
StackPanel stackPanel = new StackPanel();
this.Content = stackPanel;
 
// Create the TextBlock
TextBlock textBlock = new TextBlock();
textBlock.Margin = new Thickness(10);
textBlock.Text = "Welcome to the World of XAML";
stackPanel.Children.Add(textBlock);
 
// Create the Button
Button button = new Button();
button.Margin= new Thickness(20);
button.Content = "OK";
stackPanel.Children.Add(button);
``` 
 
보다시피 XAML은 아주 짧고 읽기가 쉽다. 이게 XAML 표현의 힘이다.

### Properties as Elements (요소 프로퍼티)

프로퍼티는 일반적으로 알다시피 <Button Content="OK" /> 과 같이 XML태그 안에 작성한다. 그런데 만약 이미지를 포함하거나 그리드 패널처럼 좀더 복잡한 객체를 만들고 싶다면 어떨까요? 그럴려면 속성요소문법을 사용할 수 있다. 이것은 자식요소를 가지는 것처럼 속성을 확장하는 것 허용한다.

``` 
<Button>
  <Button.Content>
     <Image Source="Images/OK.png" Width="50" Height="50" />
  </Button.Content>
</Button>
``` 
 
### Implicit Type conversion (암묵적인 타입 변환)

매우 강력한 WPF생성자는 암묵적으로 타입을 변환한다. 백그라운드에서 조용히 작업을 수행한다. BorderBrush를 선언할때 "Blue"라는 단어는 오직 문자열이다. 암묵적 BrushConverter는 그것을 System.Windows.Media.Brushes.Blue로 만들어준다. border thickness도 마찬가지로 Thickness객체로 암묵적인 변환을 한다. WPF는 클래스 내부에 상당히 많은 타입변환을 가지고 있다. 당신이 만든 클래스 또한 타입변환을 작성할 수 있다.

``` 
<Border BorderBrush="Blue" BorderThickness="0,10">
</Border>
```
 
### Markup Extensions (마크업 확장)

Markup Extension은 XAML에 속성값을 위한 역동적인 견본이다. 그것은 실행시 프로퍼티의 값을 해석한다. Markup Extension은 대괄호로 둘러싸여진다.(예: Background="{StaticResource NormalBackgroundBrush}") WPF는 약간의 내장형 Markup Extension을 가지고 있지만, Markup Extension을 파생하여 당신 스스로 작성할 수 있다. 내포된 Markup Extension은 다음과 같다.

+ Binding (바인딩) : 두 프로퍼티의 값을 하나로 연결
  
+ StaticResource (정적 리소스) : 리소스를 한번만 조회하여 참조함
  
+ DynamicResource (동적 리소스) : 리소스를 조회하여 자동으로 갱신함

+ TemplateBinding (템플릿 바인딩) : 컨트롤 템플릿의 프로퍼니와 컨트롤의 의존프로퍼티를 연결

+ x:Static : 고정 프로퍼티의 값을 해결함

+ x:Null : Return null

대괄호의 내용 중 첫번째 식별자는 확장자의 이름이다. 모든 preciding 식별자는 Property=value의 형태 매개변수로 이루어진다. 다음의 예제는 라벨의 내용을 텍스트박스의 텍스트와 연결되어지는것을 보여준다. 텍스트박스에 텍스트를 입력하면 텍스트 프로터피가 변경되고 바인딩 markup extension에 의해서 라벨의 내용을 자동으로 갱신한다.

``` 
<TextBox x:Name="textBox"/>
<Label Content="{Binding Text, ElementName=textBox}"/>
``` 
 
### Namespaces (네임스페이스)

모든 XAML 파일의 시작은 두개의 네임스페이스가 포함되어야 한다.
첫번째는 http://schemas.microsoft.com/winfx/2006/xaml/presentation이다. 이것은 System.Windows.Constrols에 있는 모든 WPF컨트롤 매핑 시켜준다.
두번째는 http://schemas.microsoft.com/winfx/2006/xaml이다. 이것은 XAML키워드를 정의하는  System.Windows.Markup을 매핑 시켜준다.
XML 네임스페이스오 CLR 네임스페이스의 매핑은 어셈블리 단계의 XmlnsDefinition 속성에 의해 실행된다. clr-namespace : prefix를 사용하여 XAML에 CLR namespace를 직접 포함시킬 수 있다.

``` 
<Window xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
</Window>
```
 
