# WPF PasswordBox Control (WPF 패스워드 박스 컨트롤)

PasswordBox 컨트롤은 암호를 입력하도록 설계된 특별한 텍스트박스의 유형이다. 입력된 문자들은 별표로 바뀐다. PasswordBox는 민감한 암호가 포함되어 있으므로 잘라내기, 복사, 실행취소, 다시실행등의 명령이 실행되지 않는다.

![](/assets/passwordbox.png)

```
<StackPanel>
  <Label Content="Password :" />
  <PasswordBox x:Name="passwordBox" Width="130" />
</StackPanel>
```

### Change the password character (암호문자 바꾸기)

다른문자로 별표문자를 바꾸려면 PasswordChar 프로퍼티를 원하는 문자로 설정한다.

```
<PasswordBox x:Name="passwordBox" PasswordChar="*" />
```

### Limit the length of the password (암호 길이 제한)

입력할 수 있는 암호문자의 길이를 제한하려면 MaxLength 프로퍼티를 허용범위의 글자수로 설정한다.

```
<PasswordBox x:Name="passwordBox" MaxLength="8" />
```

### Databind the Password Property of a WPF PasswordBox (Password 프로퍼티의 데이터 바인딩)

password 프로퍼티를 데이터 바인딩 하려고 할때 이것은 바인딩이 되지 않는것을 알게 된다. 이유는 password 프로퍼티는 종속적 프로퍼티에 의해 지원되지 않기 때문이다.

데이터바인딩된 암호는 보안상의 이유로 좋은 설계는 아니기에 피해야 한다. 그러나 가끔 보안이 필요하지 않는 경우 password 프로퍼티에 바인딩을 할 수 없다는 것이 매우 힘든상황이 된다. 이 특별한 경우 다음의 PasswordHelper를 이용하여 해결할 수 있다.

```
<StackPanel>
  <PasswordBox w:PasswordHelper.Attach="True" w:PasswordHelper.Password="{Binding Text, ElementName=plain, Mode=TwoWay}" Width="130" />
  <TextBlock Padding="10, 0" x:Name="plain" />
</StackPanel>
```

PasswordHelper는 PasswordHelper.Attach를 호출하여 패스워드 박스에 연결된다. 연결된 프로퍼티인 PasswordHelper.Password는 PasswordBox 컨트롤의 원래의 password 프로퍼티에 대하여 바인딩이 가능한 복사본을 제공한다.

```
public static class PasswordHelper
{
  public static readonly DependencyProperty PasswordProperty = DependencyProperty.RegisterAttached("Password", typeof(string), typeof(PasswordHelper), new FrameworkPropertyMetadata(string.Empty, OnPasswordPropertyChanged));

  public string readonly DependencyProperty AttachProperty = DependencyProperty.RegisterAttached("Attach", typeof(bool), typeof(PasswordHelper), new PropertyMetadata(false, Attach));

  public static readonly DependencyProperty IsUpdatingProperty = DependencyProperty.RegisterAttached("IsUpdating", typeof(bool), typeof(PasswordHelper));

  public static void SetAttach(DependencyObject dp, bool value)
  {
    dp.SetValue(AttachProperty, value);
  }

  public static bool GetAttach(DependencyObject dp)
  {
    return (bool)dp.GetValue(AttachProperty);
  }

  public static string GetPassword(DependencyObject dp)
  {
    return (string)dp.GetValue(PasswordProperty);
  }

  public static void SetPassword(DependencyObject dp, string value)
  {
    dp.SetValue(PasswordProperty, value);
  }

  private static bool GetIsUpdating(DependencyObject dp)
  {
    return (bool)dp.GetValue(IsUpdatingProperty);
  }

  private static void SetIsUpdating(DependencyObject dp, bool value)
  {
    dp.SetValue(IsUpdatingProperty, value);
  }

  private static void OnPasswordPropertyChanged(DependencyObject sender, DependencyPropertyChangedEventArgs e)
  {
    PasswordBox passwordBox = sender as PasswordBox;
    passwordBox.PasswordChanged -= PasswordChanged;

    if(!(bool)GetIsUpdating(passwordBox))
    {
      passwordBox.Password = (string) e.NewValue;
    }
    passwordBox.PasswordChanged += PasswordChanged;
  }

  private static void Attach(DependencyObject sender, DependencyPropertyChangedEventArgs e)
  {
    PasswordBox passwordBox = sender as PasswordBox;

    if(passwordBox == null)
      return;

    if((bool)e.OldValue)
    {
      passwordBox.PasswordChanged -= PasswordChanged;
    }

    if((bool)e.NewValue)
    {
      passwordBox.PasswordChanged += PasswordChanged;
    }
  }

  private static void PasswordChanged(object sender, RoutedEventArgs e)
  {
    PasswordBox passwordBox = sender as PasswordBox;
    SetIsUpdating(passwordBox, true);
    SetPassword(passwordBox, passwordBox.Password);
    SetIsUpdating(passwordBox, false);
  }
}
```

이 PasswordHelper에 대한 아이디어는 원래 여기에 게시되었다 :
  [http://blog.functionalfun.net/2008/06/wpf-passwordbox-and-data-binding.html](http://blog.functionalfun.net/2008/06/wpf-passwordbox-and-data-binding.html)
