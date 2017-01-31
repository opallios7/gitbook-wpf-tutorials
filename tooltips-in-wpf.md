# ToolTips in WPF (WPF 툴팁)

![](/assets/tooltip.png)

```
<Button Content="Submit">
  <Button.ToolTip>
    <ToolTip>
      <StackPanel>
        <TextBlock FontWeight="Bold">Submit Request</TextBlock>
        <TextBlock>Submits the request to the server.</TextBlock>
      </StackPanel>
    </ToolTip>
  </Button.ToolTip>
</Button>
```

### How to show ToolTips on disabled controls (비활성화 컨트롤에서 툴팁을 보여주는 방법)

IsEnabled가 False로하여 컨트롤을 비활성화하면 툴팁은 더이상 보이지 않는다. 만약 툴팁을 항상 보이게 하고 싶다면 ToolTipService.ShowOnDisabled 프로퍼티를 True로 설정해야 한다.

```
<Button IsEnabled="False"
            ToolTip="Saves the current document"
            ToolTipService.ShowOnDisabled="True"
            Content="Save">
</Button>
```

### How to change the show duration of a ToolTip (툴팁 지속 시간을 바꾸는 방법)

정적 클래스인 ToolTipService는 툴팁의 지속시간을 수정할 수 있다.

```
<Button ToolTip="Saves the current document"
            ToolTipService.ShowDuration="20"
            Content="Save">
</Button>
```
