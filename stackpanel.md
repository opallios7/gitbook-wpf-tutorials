# StackPanel

![](/assets/stackpanel.jpg)

### Introduction (소개)

WPF 스택페널은 심플하고 유용한 레이아웃 페널이다. 방향을 기준으로 자식 엘리먼트들을 아래 또는 옆으로 겹친다. 리스트 종류를 생성할 때 매우 유용하다. 콤보박스, 리스트박스, 메유와 같은 모든 WPF 아이템 컨트롤들은 내부 레이아웃 패널에 스택패널을 사용한다.

```
<StackPanel>
    <TextBlock Margin="10" FontSize="20">How do you like your coffee?</TextBlock>
    <Button Margin="10">Black</Button>
    <Button Margin="10">With milk</Button>
    <Button Margin="10">Latte machiato</Button>
    <Button Margin="10">Chappuchino</Button>
</StackPanel>
```

### Stack Items horizontally (수평적 스택 아이템)

수평 스택의 가장 좋은 예제는 다이얼로드의 "OK"와 "Cansel"버튼이다. 사용자가 폰트 크기를 바꾸거나 언어를 전환하면 텍스트의 크기가 바뀔수 있으므로 고정된 버튼은 피해야 한다. 스택 패널은 두개의 버튼을 원하는 크기에 따라 정렬한다. 공간이 더 필요하면 자동으로 가져온다. 너무 크거나 너무 작은 버튼으로 다시는 엉망이 되지 마다.

![](/assets/stackpanel2.jpg)

```
<StackPanel Margin="8" Orientation="Horizontal">            
   <Button MinWidth="93">OK</Button>
   <Button MinWidth="93" Margin="10,0,0,0">Cancel</Button>
</StackPanel>
```