# Dialogs in WPF

### OK and Cancel Buttons in a Dialog (다이얼로그 내의 확인과 취소버튼)

여러개의 버튼이 있는 모달 다이얼로그가 있고, 사용자가 그중 일부를 누르면 자동으로 닫기를 원한다. 이럴려면 다이얼로그가 닫아지면서 false가 리턴되는 모든 버튼의 IsCancel 프로퍼티를 true로 설정한다. 버튼의 IsDefault 프로퍼티에 true로 설정하면 엔터키를 누를때 실행되어진다. 다이얼로그가 닫아지면 이것또한 false가 리턴된다.
true를 리턴하려면 DialogResult를 true로 하는 콜백함수를 등록해야 한다.

```
<Window xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com.winfx/2006/xaml">
  <StackPanel>
    <Button Content="Cancel" IsCancel="True" />
    <Button Click="OkClick" Content="Ok" IsDefault="true" />
  </StackPanel>
</Window>
```

```
private void OkClick(object sender, RoutedEventArgs e)
{
  this.DialogResult = true;
}
```
