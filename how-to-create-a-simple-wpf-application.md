# How to create a simple WPF application (심플한 WPF 프로그램을 만들어보자)

## In Visual Studio 2008 (Visual Studio 2008 기준)

Visual Studio 2008을 실행하고 상단 메뉴에서 File > New > Project를 선택한다. 그리고, 프로젝트 종류를 WPF Application로 선택한다.

프로젝트를 위한 폴더를 선택하고 프로젝트 이름을 입력한다. 그리고 "OK"를 누른다.
![](/assets/hellowpf1.jpg)

Visual Studio는 프로젝트를 생성하고 프로젝트 솔루션에 Window1.xaml과 App.xaml파일들이 자동으로 추가된다. 이 구조는 Window1.designer.cs파일이 더이상 코드가 아니라는 것만 빼고는 윈폼과 매우 비슷하지만  Window1.xaml처럼 XAML에 선언되어 있다. 

![](/assets/hellowpf2.jpg)

WPF 디자이너에 있는 Window1.xaml파일을 열고 툴박스에서 버튼과 텍스트박스를 드래그한다.

![](/assets/hellowpf3.jpg)

버튼을 선택하고 속성창에 이벤트를 생성하는 화면으로 바꾼다(노란색 번개 아이콘을 클릭). "Click"이벤트를 더블클릭하면 사용자가 버튼을 클릭할 때 호출되는 메소드가 생성된다.

Note : 만약, 노랑색 번개 아이콘이 안보이면 Visual Studio Service Pack1을 설치해야 한다. 아니면 디자이너에서 버튼을 더블클릭하여 동일한 결과를 얻을 수 있다.

![](/assets/hellowpf4.jpg)

Visual Studio는 다음과 같이 버튼을 클릭할때 호출되는 code-behind에 메소드를 자동으로 생성한다.

``` 
private void button1_Click(object sender, RoutedEventArgs e)
{
    textBox1.Text = "Hello WPF!";
}
```
 
textbox는 WPF 디자이너에서 textBox1이라는 이름으로 자동생성된다. 위처럼 버튼을 클릭할 때 TextBox에 "Hello WPF"라고 보여지도록 코드를 입력하자! 그리고 [F5]를 눌러 어플리케이션을 실행해보자.

![](/assets/hellowpf5.jpg)

멋지지 않은가?


