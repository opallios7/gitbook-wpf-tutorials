# Grid Panel (그리드 패널)

### Introduction (소개)

![](/assets/v2_gridlayout.png)
 
그리드는 행과 열의 구조를 가지는 표형식의 자식 컨트롤을 정렬시키는 레이아웃 패널이다. HTML table과 기능상 유사하지만 좀더 유연하다. 셀은 여러개의 컨트롤을 가질수 있고, 여러개의 셀에 걸치거나 겹칠수 있다.

컨트롤 크기조정은 앵커(anchor)를 정의하는 수평, 수직정렬 프로퍼티에 의해 정의된다. 앵커와 그리드 라인간의 거리는 컨트롤의 여백에 의해 지정된다.

### Define Rows and Columns (행과 열 정의)

그리드는 기본적으로 하나의 열과 행을 가진다. 추가적으로 열과 행을 생성하려면 RowDefinition 항목을 RowDefinitions 컬랙션에 ColumnDefinition 항목은 ColumnDefinitions 컬랙션에 추가해야 한다. 다음의 예제는 3개의 열과 2개의 행을 가지는 그리드를 보여준다.

사이즈는 절대적 논리 단위의 합계를 백분율(퍼센트) 또는 자동으로 지정할 수 있다. 

<b>고정</b> 논리단의 크기를 고정으로 지정함 (1/96 inch)

<b>자동</b> 포함된 컨트롤에 필요한 공간을 차지함

<b>별 (*)</b> 모든 자동 및 고정크기의 열을 채운 뒤 가능한 공간을 차지하며, 사용가능한 공간을 차지함(모든 자동과 고정된 크기 컬럼을 채운 뒤에 작동함), 모든 별크기의 열에 비례하여 나눈다. 그래서  3*/5*는 30*/50*와 같다. 만약 그리드 크기가 내용에 따라 계산되는 경우 별 크기조정은 동작하지 않는다는 것을 기억해야 한다.

``` 
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto" />
        <RowDefinition Height="Auto" />
        <RowDefinition Height="*" />
        <RowDefinition Height="28" />
    </Grid.RowDefinitions>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="Auto" />
        <ColumnDefinition Width="200" />
    </Grid.ColumnDefinitions>
</Grid>
``` 
 
### How to add controls to the grid (컨트롤을 그리드에 추가하는 방법)

컨트롤을 그리드 레이아웃 패널에 추가하기 위해서는 보통 그리드의 시작과 종료 태그사이에 선언한다. 열과 행정의는 어떤 자식컨트롤의 정의보다 우선한다는 것을 명심해야 한다.

그리드 레이아웃 패널은 두개의 부착된 프로퍼티인 Grid.Column과 Grid.Row로 컨트롤의 위치를 정의한다.
```
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto" />
        <RowDefinition Height="Auto" />
        <RowDefinition Height="*" />
        <RowDefinition Height="28" />
    </Grid.RowDefinitions>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="Auto" />
        <ColumnDefinition Width="200" />
    </Grid.ColumnDefinitions>
    <Label Grid.Row="0" Grid.Column="0" Content="Name:"/>
    <Label Grid.Row="1" Grid.Column="0" Content="E-Mail:"/>
    <Label Grid.Row="2" Grid.Column="0" Content="Comment:"/>
    <TextBox Grid.Column="1" Grid.Row="0" Margin="3" />
    <TextBox Grid.Column="1" Grid.Row="1" Margin="3" />
    <TextBox Grid.Column="1" Grid.Row="2" Margin="3" />
    <Button Grid.Column="1" Grid.Row="3" HorizontalAlignment="Right" 
            MinWidth="80" Margin="3" Content="Send"  />
</Grid>
```
 
### Resizable columns or rows (행과 열 크기 조정)

![](/assets/v2_gridsplitter.png)
 
WPF는 GridSplitter라 불리는 컨트롤을 제공한다. 이 컨트롤은 다른 컨트롤과 마찬가지로 그리드의 셀에 추가된다. 당신이 이 컨트롤을 드래그하면 그리드 라인 근처에 있는 것들의 넓이와 높이를 변경한다.
```
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="*"/>
        <ColumnDefinition Width="Auto"/>
        <ColumnDefinition Width="*"/>
    </Grid.ColumnDefinitions>
    <Label Content="Left" Grid.Column="0" />
    <GridSplitter HorizontalAlignment="Right" 
                  VerticalAlignment="Stretch" 
                  Grid.Column="1" ResizeBehavior="PreviousAndNext"
                  Width="5" Background="#FFBCBCBC"/>
    <Label Content="Right" Grid.Column="2" />
</Grid>
```
 
그리드 스플리터를 배치하는 가장 좋은 방법은 자신의 자동크기조정 컬럼 안에 배치하는 것이다. 이 방법을 사용하면 인접한 셀이 겹치는 것을 예방한다. 그리드 스플리터가 이전와 다음 셀의 크기를 변경하려면 ResizeBehavior와 PreviousAndNext를 설정해야 한다. 

스플리터는 일반적으로 폭과 높이사이의 비율에 따라 크기 방향을 인식하지만 원한다면 수동으로 크기방향을 행 또는 열로 설정할 수 있다.

```
<GridSplitter ResizeDirection="Columns"/>
```

### How to share the width of a column over multiple grids (여러 그리드에 컬럼의 폭을 공유하는 방법)

그리드 레이아웃의 공유 크기조정 기능을 사용하면 여러 그리드에 크기조정을 동기화 할수 있다. 이 기능은 데이타 템플릿 내에서 레이아웃 패널로 그리드를 사용하면 여러 컬럼 리스트뷰를 구현하려는 경우 매우 유용하다.

부모 엘리먼트에 연결된 Grid.IsSharedSizeScope를 true로 설정하여 컬럼 폭의 범위를 정의하여 공유한다.

두개의 ColumnDefinition의 폭을 동기화하려면 SharedSizeGroup을 같은 이름으로 설정한다.
``` 
<ItemsControl Grid.IsSharedSizeScope="True" >
  <ItemsControl.ItemTemplate> 
    <DataTemplate>
      <Grid>
        <Grid.ColumnDefinitions>
          <ColumnDefinition SharedSizeGroup="FirstColumn" Width="Auto"/>
          <ColumnDefinition Width="*"/>
        </Grid.ColumnDefinitions>
        <TextBlock Text="{Binding Path=Key}" TextWrapping="Wrap"/>
        <TextBlock Text="{Binding Path=Value}" Grid.Column="1" TextWrapping="Wrap"/>
      </Grid>
    </DataTemplate>
  </ItemsControl.ItemTemplate>
</ItemsControl>
``` 
 
### Useful Hints (유용한 힌트)

크기 조정공유에 참여하는 열과 행은 별 크기조정을 고려하지 않는다. 크기조정공유 시나리오는 별크기조정은 자동으로 처리된다. 공유된 크기조정 컬럼내의 텍스트블럭에 대한 TextWrapping이 작동하지 않으므로 마지막 컬럼을 공유크기조정에서 제외할 수 있다. 이것은 종종 문제를 해결하는데 도움이 된다.

### Using GridLenghts from code (코드에서 GridLength 사용)

코드에서 열 또는 행을 추가하고 싶다면 GridLength 클래스를 다른 형식의 크기로 정의하여 사용할 수 있다.

<b>sized</b>	GridLength.Auto

<b>Star sized</b>	new GridLength(1,GridUnitType.Star)

<b>Fixed size</b>	new GridLength(100,GridUnitType.Pixel)

```
Grid grid = new Grid();
 
ColumnDefinition col1 = new ColumnDefinition();
col1.Width = GridLength.Auto;
ColumnDefinition col2 = new ColumnDefinition();
col2.Width = new GridLength(1,GridUnitType.Star);
 
grid.ColumnDefinitions.Add(col1);
grid.ColumnDefinitions.Add(col2);
```
 
### More on this topic (추가내용)

[크기조정이 가능한 컬럼 생성방법](http://www.wpftutorial.net/GridSplitter.html)