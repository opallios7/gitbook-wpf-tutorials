# ComboBox with Live Preview (실시간 미리보기의 콤보박스)

![](/assets/livepreview.jpg)

### The Live Preview Pattern

Microsoft Office 2007 이상의 사용한다면 "실시간 미리보기"라는 개념에 익숙할 것이다. 이것을 컬러, 폰트종류, 폰트크기와 같은 모든 선택종류를 위해서 사용하고 있다. 이 패턴의 기본 개념은 사용자가 선택하지 않으면 실제로 작동하지 않고, 객체가 어쩧게 보이는지를 즉각적으로 피드백을 주는 것이다. 그래서 콤보를 벗어나면 아무것도 변하지 않는다.

### How to use the LivePreviewComboBox Control (LivePreviewComboBox 사용법)

바인딩 할 수 있는 추가 종속적 프로퍼티인 LivePreviewItem을 제공하는 LivePreviewComboBox라 불리는 사용자 컨트롤에 이 기능을 캡슐화했다. 다음 코드는 이 기능을 사용하는 방법을 설명하고 있다.

```
<Window xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:l="clr-namespace:LivePreviewComboBox">

  <StackPanel>
    <TextBlock Text="Preview Value:" />
    <TextBlock Text="{Binding LivePreviewItem, ElementName=liveBox}" />
    <l:LivePreviewComboBox x:Name="liveBox" />
  </StackPanel>
</Window>
```
