# WPF TextBox

### How to enable spell checking (맞춤법 검사 활성화 방법)

![](/assets/spellcheck.png)

TextBox와 RichTextBox는 즉시 사용할 수 있는 맞춤법 검사 기능을 제공한다. 영어, 스페인어, 독일어, 프랑스어등이 가능하다. SpellCheck.IsEnabled 프로퍼티를 true로 설정하여 활성화 할 수 있다.
```
<TextBox SpellCheck.IsEnabled="True" Language="en-US" />
```

### How to validate input (입력 유효성 검사 방법)

정규식을 사용하면 사용자의 입력을 쉽게 제한하고 유효성을 검사할 수 있다. 다음 코드는 어떻게 사용하는지를 보여준다.

```
protected override void OnTextInput(TextCompositionEventArgs e)
{
  string fullText = Text.Remove(SelectionStart, SelectionLength) + e.Text;
  if(_regex != null && !_regex.IsMatch(fullText))
  {
    e.Handled = true;
  }
  else
  {
    base.OnTextInput(e);
  }
}
```
