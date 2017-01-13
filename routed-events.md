# Routed Events

![Routed Events](/assets/routedevents.png)

라우팅 된 이벤트는 라우팅 전략에 따르는 Visual tree를 위 또는 아래로 탐색하는 이벤트이다. 라우팅 전략은 bubble, tunnel, direct가 있다. 당신은 이벤트가 발생되는 엘리먼트이거나 Button.Click="Button_Click" 문법과 같이 첨부된 이벤트를 사용하여 위 또는 아래의 다른 엘리먼트에 이벤트 핸들러를 연결할 수 있다.

라우팅된 이벤트는 일반적으로 쌍을 이룬다. 첫번째는 PreviewMouseDown이라 불리는 터널링 이벤트이고, 두번재는 MouseDown이라 불리는 버블링이다. 이벤트 핸들러에 접근하면 라우팅을 멈추지 않는다. e.Handled = true;라 설정할 때 라우팅을 멈춘다.

+ <b>터널링 이벤트</b>는 최상위 엘리먼트에서 발생되고 소스 엘리먼트에 접근하거나 터널링이 이벤트가 처리된 것으로 표시하여 멈출때까지 visual tree를 아래로 탐색한다. 이름 규칙은 Preview라 불리고 버블이벤트 응답전에 나타난다.

+ <b>버블링 이벤트</b>는 소스 엘리먼트에서 발생되고 최상위 엘리먼트에 접근하거나 버블링이 이벤트가 처리된 것으로 표시하여 멈출때까지 visual tree를 위로 탐색한다. 버블링 이벤트는 터널링 이벤트 후에 발생된다.

+ <b>다이렉트 이벤트</b>는 소스 엘리먼트에서 발생되고 반드시 소스 엘리먼트에서 처리되어야 한다. 이 행동은 일반 .NET 이벤트와 같다.

### How to Create a Custom Routed Event (라우팅된 이벤트를 만드는 방법)

``` 
// Register the routed event
public static readonly RoutedEvent SelectedEvent = 
    EventManager.RegisterRoutedEvent( "Selected", RoutingStrategy.Bubble, 
    typeof(RoutedEventHandler), typeof(MyCustomControl));
 
// .NET wrapper
public event RoutedEventHandler Selected
{
    add { AddHandler(SelectedEvent, value); } 
    remove { RemoveHandler(SelectedEvent, value); }
}
 
// Raise the routed event "selected"
RaiseEvent(new RoutedEventArgs(MyCustomControl.SelectedEvent));
``` 
 
 