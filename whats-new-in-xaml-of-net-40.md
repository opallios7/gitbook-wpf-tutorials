# What's new in XAML of .NET 4.0 (.NET 4.0의 XAML에는 새로운게 뭐가 있을까?)

마이크로 소프트의 .NET 4.0은 향상된 XAML의 버전을 가져왔다. 이 글은 그들이 만든 향상된 언어를 보여준다.

### Easy Object References with {x:Reference} (쉬운 객체 참조 {x:Reference})

만약 오늘 객체참조를 만들고 싶다면 데이터 바인딩을 실행하여 ElementName을 이용하여 소스를 선언하는 것이 필요하다. XAML 2009에는 새로운 {x:Reference} 태그 확을 사용할 수 있다.

```
<!-- XAML 2006 -->
<Label Target="{Binding ElementName=firstName}">FirstName</Label>
<TextBox x:Name="firstName" />
 
<!-- XAML 2009 -->
<Label Target="{x:Reference firstName}">FirstName</Label>
<TextBox x:Name="firstName" />
```

### Built-in Types (기본 내장된 유형)

오늘 스트링 또는 더블과 같은 유형의 단순한 객체를 리소스 사전에 추가한다면 필요한 clr-namespaces를 XML namespaces에 매핑해야 한다. XAML 2009에는 XAML언어에 포함된 많은 심플한 유형이 있다. 

```
<!-- XAML 2006 -->
<sys:String xmlns:sys="clr-namespace:System;assembly=mscorlib >Test</sys:String>
 
<!-- XAML 2009 -->
<x:String>Test</x:String>
```

XAML언어에 포함된 유형은 다음과 같다:
+ <x:Object/>
+ <x:Boolean/>
+ <x:Char/>
+ <x:String/>
+ <x:Decimal/>
+ <x:Single/>
+ <x:Double/>
+ <x:Int16/>
+ <x:Int32/>
+ <x:Int64/>
+ <x:TimeSpan/>
+ <x:Uri/>
+ <x:Byte/>
+ <x:Array/>
+ <x:List/>
+ <x:Dictionary/>

### Generics in XAML with x:TypeArguments (XAML의 제네릭 x:TypeArguments)

만약 XAML에서 ObservableCollection<Employee>를 사용하고 싶다면, XAML에서 선언할 수 없기에  ObservableCollection에서 파생되는 형식을 만들어야 한다. XAML 2009는 x:TypeArgements 속성을 제네릭의 유형으로 정의하여 사용할 수 있다.

```
<!-- XAML 2006 -->
class EmployeeCollection : ObservableCollection<Employee>
{
}
 
<l:EmployeeCollection>
    <l:Employee FirstName="John" Name="Doe" />
    <l:Employee FirstName="Tim" Name="Smith" />
</lEmployeeCollection>
 
<!-- XAML 2009 -->
<ObservableCollection x:TypeArguments="Employee">
    <l:Employee FirstName="John" Name="Doe" />
    <l:Employee FirstName="Tim" Name="Smith" />
</ObservableCollection />
```

### Support for Arbitrary Dictionary Keys (임의적인 사전 키 제공)

XAML 2006은 명시적인 x:Key값은 모두 문자열로 처리되었습니다. XAML 2009는 엘리먼트문법에 키를 작성하여 당신이 원하는 그 어떤 유형의 키를 정의할 수 있다.

```
<!-- XAML 2006 -->
<StreamGeometry x:Key="CheckGeometry">M 0 0 L 12 8 l 9 12 z</StreamGeometry>
 
<!-- XAML 2009 -->
<StreamGeometry>M 0 0 L 12 8 l 9 12 z
    <x:Key><x:Double>10.0</x:Double></x:Key>
</StreamGeometry>
```

### Use of Non-Default Constructors with x:Arguments (x:Arguments를 이용한 기본값이 없는 생성자 사용)

XAML 2006객채는 그것을 사용하기 위해 반드시 공개용 기본 생성자가 있어야 한다. XAML 2009는 x:Arguments 문법을 사용하여 생성자 인수를 전달할 수 있다.

```
<!-- XAML 2006 -->
<DateTime>00:00:00.0000100</DateTime>
 
<!-- XAML 2009 -->
<DateTime>
    <x:Arguments>
        <x:Int64>100</x:Int64>
    </x:Arguments>
</DateTime>
```

### Use of Static Factory Methods with x:FactoryMethod (정적 팩토리 메소드 x:FactoryMethod 사용)

공개 생성자가 없지만 정적 팩토리 메소드가 있는 형식이 있는 경우 XAML 2006의 코드에서 해당 유형을 만들어야 한다. XAML 2009는 x:FactoryMethod라는 x:Arguement속성을 사용하여 인수값을 전달할 수 있다.

```
<!-- XAML 2006 -->
Guid id = Guid.NewGuid();
 
<!-- XAML 2009 -->
<Guid x:FactoryMethod="Guid.NewGuid" />
```