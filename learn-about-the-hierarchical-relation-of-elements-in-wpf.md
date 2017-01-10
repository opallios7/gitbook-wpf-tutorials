# WPF요소의 계층관계에 대해서 배우자!

## 1. Logical and Visual Tree

![logical and visual tree](/assets/trees.jpg)


### 개요

WPF 사용자 인터페이스의 요소들은 계층적으로 관계를 갖는다. 이 관계를 논리적 구조(LogicalTree)라고 부른다. 요소 하나의 템플릿은 다수의 시각화 요소를 갖는다. 이 구조를 시각적 구조(VisualTree)라고 부른다. 이 두가지 구조에 차이가 있는데, 몇몇은 논리적 요소만 필요로하고, 그외에는 모든 요소가 필요로하기 때문이다.

```
<Window>
    <Grid>
        <Label Content="Label" />
        <Button Content="Button" />
    </Grid>
</Window>
```

### 왜 두개의 다른 종류의 트리가 필요할까?

WPF 컨트롤은 보기보다 여러개의 원시적인 컨트롤로 구성되어있다. 예를 들어보자. 버튼의 경우border(외곽선), rectangle(사각형), content presenter(내용을 표시하는 부분)으로 구성되어있다. 이 컨트롤들은 버튼의 visual children이다.
WPF가 버튼을 만들때 그 요소들은 모습이 없지만, visual tree를 통해 반복되고 visual children을 만든다.또한, 이 계층적 관계는 hit-testing(요소를 선택했다고 인식하는것), 레이아웃, 기타등등을 수행하는데 사용되곤 한다.
그러나 종종 컨트롤 템플릿을 부분적으로 변경하거나 접근할 필요가 없을때가 있기에 모든것을 Visual tree와 연관지어서는 안된다. 이는 Logical tree가 더 적합하기 때문이다.

### The Logical Tree
logical tree는 사용자 인터페이스 요소 사이의 관계를 가지며, 다음과 같은 역활를 한다.
+ 의존 속성값의 상속
+ 동적 리소스 참조
+ 바인딩을 위한 요소이름의 탐색
+ 라우트된 이벤트 포워딩

### The Visual Tree
visual tree는 각 요소의 시각적 요소(visual elements)들을 포함한 모든 논리 요소를 가지며, 다음과 같은 역활을 한다.
+ 시각적 요소 표현
+ 요소 투명도 처리
+ 레이아웃 및 RenderTransforms 처리
+ 활성화 속성 처리
+ 요소 선택여부 처리
+ 관련요소 탐색(FindAncestor)

### Programmatically Find an Ancestor in the Visual Tree (Visual Tree에서 상위를 찾는 프로그래밍 방법)

만약 사용자 인터페이스의 자식요소이고 부모요소로부터 데이터 접근을 원하는데 얼마나 많은 단계를 올라가야 할지 모른다면, 요청된 타입의 요소를 찾을때까지 tree를 상위탐색하는 가장 좋은 해결방법이다.
helper는 정확하게 이것을 수행한다. 거의 동일한 코드를 사용하여 logical tree를 탐색할 수 있다. 

```
public static class VisualTreeHelperExtensions
{
    public static T FindAncestor<T>(DependencyObject dependencyObject)
        where T : class
    {
        DependencyObject target = dependencyObject;
        do
        {
            target = VisualTreeHelper.GetParent(target);
        }
        while (target != null && !(target is T));
        return target as T;
    }
}
```

다음과 같은 예제는 어떻게 사용하는지를 보여준다. this에서 시작하여 Grid유형의 요소를 찾을때까지 visual tree를 상위 탐색한다. 만약 tree의 최상위요소에 다다르면 null을 반환한다.

```
var grid = VisualTreeHelperExtensions.FindAncestor<Grid>(this);
```