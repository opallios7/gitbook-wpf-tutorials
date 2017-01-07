# WPF요소의 계층관계에 대해서 배우자!

## 1. Logical and Visual Tree (논리와 시각화 트리)

![논리 및 시각화 트리](/assets/trees.jpg)


### 개요

WPF 사용자 인터페이스의 요소들은 계층적으로 관계를 갖는다. 이 관계를 논리적 구조(LogicalTree)라고 부른다. 요소 하나의 템플릿은 다수의 시각화 요소를 갖는다. 이 구조를 시각화 구조(VisualTree)라고 부른다. 이 두가지 구조에 차이가 있는데, 몇몇은 논리적 요소만 필요로하고, 그외에는 모든 요소가 필요로하기 때문이다.

```
<Window>
    <Grid>
        <Label Content="Label" />
        <Button Content="Button" />
    </Grid>
</Window>
```

### 왜 두개의 다른 종류의 트리가 필요할까?

WPF 컨트롤은 보기보다 여러개의 원시적인 컨트롤로 구성되어있다. 예를 들어보자. 버튼의 경우border(외곽선), rectangle(사각형), content presenter(내용을 표시하는 부분)으로 구성되어있다. 이 컨트롤들은 버튼의 시각화 자식들이다.

WPF가 버튼을 만들때 그 요소들은 모습이 없지만, visual tree를 통해 반복되고 visual children을 만든다.또한, 이 계층적 관계는 hit-testing(요소를 선택했다고 인식하는것), 레이아웃, 기타등등을 수행하는데 사용되곤 한다.

But sometimes you are not interested in the borders and rectangles of a controls' template. Particulary because the template can be replaced, and so you should not relate on the visual tree structure! Because of that you want a more robust tree that only contains the "real" controls - and not all the template parts. And that is the eligibility for the logical tree.
그러나 가끔은 컨트롤 템플릿의 외곽선이나 사각형에 관심이 없을때가 있다. 따라서, 템플릿을 부분적으로 바꿀수 있기에 Visual Tree 구조와 관련되어서는 안된다. 템플릿 부분 전부가 아닌 "실제" 컨트롤을 포함하는 보다 더 완벽한 tree를 원하기 때문에 그것이 Logical tree가 적격이다.

### The Logical Tree
The logical tree describes the relations between elements of the user interface. The logical tree is responsible for:

+ Inherit DependencyProperty values
+ Resolving DynamicResources references
+ Looking up element names for bindings
+ Forwaring RoutedEvents

### The Visual Tree

The visual tree contains all logical elements including all visual elements of the template of each element. The visual tree is responsible for:
+ Rendering visual elements
+ Propagate element opacity
+ Propagate Layout- and RenderTransforms
+ Propagate the IsEnabled property.
+ Do Hit-Testing
+ RelativeSource (FindAncestor)

### Programmatically Find an Ancestor in the Visual Tree

If you are a child element of a user interface and you want to access data from a parent element, but you don't know how many levels up that elemens is, it's the best solution to navigate up the tree until it finds an element of the requested type.

This helper does excactly this. You can use almost the same code to navigate through the logical tree.

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

The following example shows how to use the helper. It starts at this and navigates up the visual tree until it finds an element of type Grid. If the helper reaches the root element of the tree, it returns null.

```
var grid = VisualTreeHelperExtensions.FindAncestor<Grid>(this);
```