# WPF ListBox Control

![](/assets/listbox1.png)

### Introduction (소개)

The ListBox control displays a list of items. The user can select one or multiple items depending on the selection mode. The typical usage of a listbox in WPF is to bind its items to a list of business objects and display them by applying a data template.

리스트박스 컨트롤은 아이템의 목록을 보여준다. 사용자는 선택모드에 따라서 아이템을 하나 또는 여러개 선택할 수 있다. WPF 리스트박스의 일반적인 사용법은 아이템을 비즈니스 객체의 목록에 바인딩하고 데이터 템플릿이 적용하여 보여준다.

```
<ListBox Margin="20">
  <ListBoxItem>New York</ListBoxItem>
  <ListBoxItem>Los Angles</ListBoxItem>
  <ListBoxItem>Paris</ListBoxItem>
  <ListBoxItem>Zurich</ListBoxItem>
</ListBox>
```

### How to define a Trigger for IsSelected in the DataTemplate (데이터 템플릿에 IsSelected 트리거를 정의하는 방법)

If you want to change the appearance of a ListBoxItem when it is selected, you have to bind the isSelected property of the ListBoxItem. But this is a bit tricky, you have to use a relative source with FindAcestor to navigate up the visual tree until you reach the ListBoxItem.

리스트박스가 선택되었을때 ListBoxItem의 모습이 바뀌기를 바란다면, ListBoxItem의 IsSelected 프로퍼티를 바인딩해야 한다. 하지만 약간 까다롭다. ListBoxItem을 찾을때까지 Visual Truee를 탐색하는 FindAncestor가 있는 관계 소스를 사용해야 하기 때문이다.

```
<DataTemplate x:Key="myDataTemplate">
  <Border x:Name="border" Height="50">
    <TextBlock Text="Binding Text" />
  </Border>
  <DataTemplate.Triggers>
    <DataTrigger Binding="{Binding RelativeSouce={RelativeSource  
      Mode=FindAncestor, AncestorType={x:Type ListBoxItem}}, Path=IsSelected}" Value="True">
      <Settre TargetName="border" Property="Height" Value="100" />
    </DataTrigger>
  </DataTemplate.Triggers>
</DataTemplate>
```

More articles about ListBox

+ [Appli a DataTemplate]()
+ [Strech an item]()
+ [Selected item Background]()
+ [Layout of items]()
