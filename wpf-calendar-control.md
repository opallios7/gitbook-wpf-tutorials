# WPF Calendar Control

[![](/assets/download_calendar_sample.png)](http://www.wpftutorial.net/uploads/Calendar.zip)

### Introduction (소개)

WPF 4.0부터 Microsoft는 다음과 같은 완벽한 기능의 달력 컨트롤을 제공한다.  
+ 표시되는 날짜 설정
+ 다중 선택 모드
+ 통제 날짜
+ 다양한 달력 모드

### Set the displayed date (표시되는 날짜 설정)

달력은 현재 날짜를 기본으로 표시한다. 그러나 DisplayDate 프로퍼티를 설정함으로써 표시할 다른 날짜를 명시할 수 있다.

```
<Calendar DisplayDate="01.01.2016" />
```

### Multiple Selection modes (다중 선택 모드)

달력컨트롤은 다중선택모드를 제공한다. SelectionMode 프로퍼티를 SingleDateSingleRange, MultipleRanges, Node중 하나로 설정할 수 있다.

![](/assets/calendar1.png)
```
<Calendar SelectionMode="MultipleRange" />
```

### Blackout dates (통제 날짜)

달력 컨트롤은 선택에 유효하지 않은 통제날짜 기능을 제공한다. BlackoutDates 프로퍼티를 하나 또는 여러 CalendarDateRange로 설정하여 여러 범위를 정의할 수 있다.

![](/assets/calendar2.png)

```
<Calendar SelectionMode="{Binding SelectedItem, ElementName=selectionmode}" >
  <Calendar.BlackoutDates>
    <CalendarDateRange Start="01/01/2016" End="01/06/2016" />
    <CalendarDateRange Start="05/01/2016" End="05/03/2016" />
  </Calendar.BlackoutDates>
</Calendar>
```

### Calendar modes (다양한 달력 모드)

달력은 날짜 범위를 표시하는 3가지 모드(년, 월, 10년)를 지원한다. DisplayMode 프로퍼티를 설정하여 모드를 제어할 수 있다.

![](/assets/calendar3.png)

```
<Calendar DisplayMode="Year" />
```
