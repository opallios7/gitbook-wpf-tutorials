# Menus in WPF

### Menu (메뉴)

메뉴 컨트롤은 HeaderedItemsControl로부터 파생되었다. 아이템을 수평으로 쌓고, 보통 회색 배경으로 그려진다. 메뉴에 ItemsControl을 추가하는 유일한 프로퍼티는 IsMainMenu 프로퍼티이다. 사용자가 F10 또는 ALT를 누르면 메뉴로 포커스를 가져간다.

![](/assets/menu2.jpg)

```
<Menu IsMainMenu="True">
    <MenuItem Header="_File" />
    <MenuItem Header="_Edit" />
    <MenuItem Header="_View" />
    <MenuItem Header="_Window" />
    <MenuItem Header="_Help" />
</Menu>
```

### MenuItem (메뉴 항목)

메뉴항목은 HeaderedItemsControl이다. 헤더 프로퍼티의 내용은 메뉴의 캡션을 의미한다. 메뉴항목의 아이템들은 해당 메뉴의 하위메뉴들이다. 아이콘은 캡션의 왼쪽에 그려진다. 일반적으로 작은 이미지를 사용한다. 그러나 내용의 유형에 사용될 수 있다.

글자 앞에 밑줄을 추가하여 바로가기 키를 정의할 수 있다.

![](/assets/wpfmenu2.jpg)

```
<MenuItem Header="_Edit">
    <MenuItem Header="_Cut" Command="Cut">
        <MenuItem.Icon>
            <Image Source="Images/cut.png" />
        </MenuItem.Icon>
    </MenuItem>
    <MenuItem Header="_Copy" Command="Copy">
        <MenuItem.Icon>
            <Image Source="Images/copy.png" />
        </MenuItem.Icon>
    </MenuItem>
    <MenuItem Header="_Paste" Command="Paste">
        <MenuItem.Icon>
            <Image Source="Images/paste.png" />
        </MenuItem.Icon>
    </MenuItem>
</MenuItem>
```

### Checkable MenuItems (선택가능한 메뉴항목)

IsCheckable 프로퍼티를 True로 설정함으로써 선택가능한 메뉴 항목을 만들 수 있다. 선택 상태는 IsChecked 프로퍼티에 의해 확인 가능하다. 선택상태가 변경될 때 알림을 받기 위해서는 핸들러를 Check와 Unchecked 프로퍼티에 추가하여 받을 수 있다.

![](/assets/checkMenu.jpg)

```
<MenuItem Header="_Debug">
    <MenuItem Header="Enable Debugging" IsCheckable="True" />
</MenuItem>
```

### Separators (구분기호)

구분기호는 메뉴 항목을 그룹핑하기 위한 간단한 컨트롤리다. 이것은 수평선으로 그려진다. 또한 ToolBar나 StatusBar에서도 사용가능하다.

![](/assets/menuseparator.jpg)

```
<Menu>
    <MenuItem Header="_File">
        <MenuItem Header="_New..." />
        <Separator />
        <MenuItem Header="_Open..." />
        <Separator />
        <MenuItem Header="_Save" />
        <MenuItem Header="_Save As..." />
        <Separator />
        <MenuItem Header="_Exit" />
    </MenuItem>
</Menu>
```

### Callbacks (콜백)

Click 이벤트에 콜백을 추가하는 방법으로 모든 메뉴항목에 콜백을 등록할 수 있다.

```
<Menu>
    <MenuItem Header="_File">
        <MenuItem Header="_New..."  Click="New_Click"/>
    </MenuItem>
</Menu>
```

```
private void New_Click(object sender, RoutedEventArgs e)
{
    MessageBox.Show("You clicked 'New...'");
}
```

### How to bind MenuItems dynamically using MVVM (MVVM을 사용하여 동적으로 메유항목에 바인딩 하는 방법)

MVVM 패턴을 사용한다면 아마도 코드에 사용가능한 메뉴 명령을 동적으로 정의하고, 메뉴항목 컨트롤에 바인딩하기를 원할것이다. 다음은 그 방법에 대해 보여준다.

```
<Menu>
    <Menu.Resources>
        <Style x:Key="ThemeMenuItemStyle" TargetType="MenuItem">
           <Setter Property="Header" Value="{Binding Name}"></Setter>
           <Setter Property="Command" Value="{Binding ActivateCommand}"/>
           <Setter Property="IsChecked" Value="{Binding IsActive}" />
           <Setter Property="IsCheckable" Value="True"/>
        </Style>
    </Menu.Resources>
    <MenuItem Header="Themes" ItemsSource="{Binding Themes}"
              ItemContainerStyle="{StaticResource ThemeMenuItemStyle}"  />
</Menu>
```

### Keyboard Shortcuts (바로가기 키)

메뉴 항목에 바로가기 키를 추가하는 것은 사용하기를 원하는 단축키를 글자앞에 밑줄 "_"을 추가하여 사용한다. 이것은 자동으로 InputGestureText를 적절한 값으로 설정한다. 그러나 이 프로퍼티에 원하는 텍스트를 입력하여 추천된 텍스트를 재정의할 수 있다.
