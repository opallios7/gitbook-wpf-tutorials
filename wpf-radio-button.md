# Radio Button

![](/assets/radiobuttons.jpg)

### Intruduction (소개)

라디오 버튼은 프로그래밍이 가능한 여러개의 스테이션 버튼을 가지는 오래된 아날로그 라디오의 이름을 가지고 있다. 하나를 선택할 때, 이전에 선택된 것이 해제된다. 그래서 한번에 하나만 선택할 수 있다.

라디오 버튼의 동작은 같다. 소수의 옵션중에서 하나를 선택한다. 옵션이 길어지면 콤보박스나 리스트박스를 사용하는게 좋다.

라디오 버튼끼리 그룹핑하기를 정의하려면 그룹이름을 같도록 설정해야 한다.

하나의 옵션을 미리 선택되어진것으로 하려면 IsChecked 프로퍼티를 True로 설정한다.

```
<StackPanel>
  <RadioButton GroupName="OS" Content="Window XP" IsChecked= "True" />
  <RadioButton GroupName="OS" Content="Window Vista" />
  <RadioButton GroupName="OS" Content="Window 7" />
  <RadioButton GroupName="Office" Content="Microsoft Office 2007" IsChecked="True" />
  <RadioButton GroupName="Office" Content="Microsoft Office 2003" />
  <RadioButton GroupName="Office" Content="Open Office" />
</StackPanel>
```

### How to DataBind Radio Buttons in WPF (WPF에서 라디오버튼을 데이터바인딩 하는 방법)

라디오버튼은 데이터바인딩에 대한 알려진 이슈가 있다. IsChecked 프로퍼티를 부울값으로 바인딩하고 라디오버튼을 확인하면 값이 True입니다. 그러나 다른 라디오버튼을 확인해보면 여전히 True로 되어있습니다.  

그 이유는 컨트롤이 내부적으로 종속적 프로퍼티에서 ClearValue()를 호출하기 때문에 선택하지 않는 동안 바인딩이 손실되는 이유이다.

```
<Window.Resources>
  <EnumMatchToBooleanConverter x:Key="enumConverter" />
</Window.Resources>

<RadioButton Content="Option 1" GroupName="Options1" IsChecked="{Binding Path=CurrentOption, Mode=TwoWay, Converter={StaticResource enumConverter}, CnverterParameter=Opation1}" />
<RadioButton Content="Option 2" GroupName="Option2" IsChecked="{Binding Path=CurrentOption, Mode=TwoWay, Converter={StaticResource enumConverter}, ConverterParameter=Option2}" />
<RadioButton Content="Option 3" GroupName="Option3" IsChecked="{Binding Path=CurrentOption, Mode=TwoWay, Converter={StaticResource enumConverter}, ConverterParameter=Option3}" />
```

```
public class EnumMatchToBooleanConverter : IValueConverter
{
  public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
  {
    if(value == null || parameter == null)
      return false;

    string checkValue = value.ToString();
    string targetValue = parameter.ToString();
    return checkValue.Equals(targetValue, StringComparison.InvariantCultureIgnoreCase);
  }

  public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
  {
    if(value == null || parameter == null)
      return null;

      bool useValue = (bool)value;
      string targetValue = parameter.ToString();
      if(useValue)
        return Enum.Parse(targetType, targetValue);

        return null;
  }
}
```
