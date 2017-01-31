# WPF Expander Control (WPF Expander 컨트롤)

### Introduction (소개)

![](/assets/expander_example.png)

Expander 컨트롤은 그룹박스와 비슷하지만 내용을 축소 또는 확장하는 부가적인 기능이 있다. HeaderedContentControl에서 파생하여 헤더내용을 설정하는 Header 프로퍼티와 확장 가능한 내용을 위한 Content 프로퍼티를 가지고 있다.

Expander를 확장 또는 축소 상태를 가져오거나 설정하는 IsExpanded 프로퍼티가 있다.

축소상태의 Expander는 오직 헤더에 필요한 공간만 차지하고, 확장상태에서는 헤더와 내용을 포함한 크기의 공간을 차지한다.

```
<Expander Header="More Options">
  <StackPanel Margin="10, 4, 0, 0">
    <CheckBox Margin="4" Content="Option 1" />
    <CheckBox Margin="4" Content="Option 2" />
    <CheckBox Margin="4" Content="Option 3" />
  </StackPanel>
</Expander>
```
