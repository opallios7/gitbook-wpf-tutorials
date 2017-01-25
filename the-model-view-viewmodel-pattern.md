# The Model-View-ViewModel Pattern

### How the MVVM pattern became convenient (MVVM 패턴이 어떻게 편리해졌는가?)

WPF는 매우 강력한 데이터 바인딩 기능을 가지고 있어, 프로퍼티간의 단방향 또는 양방향 동기화가 쉽다. 두개의 WPF 엘리먼트를 직접 바인딩 할 수 있지만, 일반적인 데이터바인딩은 일종의 데이터를 뷰에 연결하는 것이다. 이것은 DataContext 프로퍼티를 사용하여 실행한다. DataContext 프로퍼티는 상속된 것으로 표시되기 때문에 뷰의  루트 엘리먼트에 설정할 수 있고, 값은 뷰의 모든 하위 엘리먼트에 상속된다.

DataContext 프로퍼티를 데이터소스로 사용하는 한가지 중요한 제한사항은 그것 하나뿐이지만 실생활 프로젝트에서는 보통 뷰마다 데이터 객체를 하나이상 가지고 있다. 그러면 뭘 할 수 있을까? 가장 확실한 접근방법은 모든 데이터 객체를 하나의 단일 객체로 합하여 합쳐진 데이터를 프로퍼티로 노출하고 DataContext에 바인딩 되어지도록 하는 것이다. 이 객체를 뷰 모델이라 부른다.

### Separation of logic and presentation (로직과 프리젠테이션의 분리)

MVVM 패턴은 지금까지 데이터를 뷰에 바인드하는 편리한 방법일 뿐이다. 그러나 사용자의 행동은 어떤가? 어떻게 다뤄야 하는가? WinForm에서 알려진 전통적인 접근방법은 뷰의 코드비하인드 파일에 구현된 이벤트 핸들러를 등록하는 것이다. 그렇게 하면 다음과 같은 몇가지 단점이 있다.

  + 코드비하인트에 이벤트 핸들러가 있는 것은 뷰를 mock away할 수 없기때문에 테스트에 않좋다.
  + 뷰의 디자인을 변경하면 모든 엘리먼트가 다른 이벤트 핸들러를 가지고 있기 때문에 코드 변경을 자주 요구할 수 있다.
  + 로직은 뷰에 강하게 연결되어 있어 다른 뷰에서 해당 로직을 재사용하기가 어렵다.

그래서 아이디어는 WPF의 다른 기능, 즉 커맨드을 사용하여 모든 프리젠테이션 로직를 뷰모델로 이동하는 것이다. 커맨드은 데이터 처럼 연결될 수 있고 버튼, 토글버튼, 메뉴아이템, 체크박스, 입력바인딩과 같은 많은 엘리먼트에 지원된다. 목표는 뷰의 코드비하인드에 어떠한 로직의 코드라인도 가지지 않는 것이다. 이로 인해 다음과 같은 장점이 있다.

  + 뷰모델은 표준 단위 테스트(UI 테스트 대신)를 사용하여 쉽게 테스트를 할 수 있다.
  + 인터페이스가 동일하게 유지하기 때문에 뷰모델의 변경 없이 뷰를 다시 디자인 할 수 있다.
  + 뷰모델은 특별한 경우(일반적으로 추천하지 않음)에 재사용이 가능하다.

### what's the different between MVVM, MVP and MVC? (MVVM, MVP, MVC 무엇이 다른가?)

MVP, MPC, MVVM 패턴의 차이에 대해 항상 혼란스럽다. 그래서 그것을 좀더 명확하게 정의하고 구별하려고 한다.

### MVC : Model-View-Vontroller

MVC패턴은 모든 사용자의 입력을 받아오는 하나의 컨트롤러로 구성된다. 입력의 종류에 따라 다른 뷰를 보여주거나 모델의 데이터를 수정한다. 모델과 뷰는 컨트롤러에 의해 생성된다. 뷰는 오직 모델말 알고 있지만, 모델은 다른 객체에 대해서 모른다. 이 패턴은 주로 오래된 MFC에서 사용되었고 지금은 ASP.NET MVC에서 사용된다.

![](/assets/pattern_mvc.png)

### MVP : Model-View-Presenter

MVP 패턴에서 뷰는 사용자 입력을 가져와서 프리젠터에서 전달한다. 프리젠터는 사용자 액션의 유형에 따라 뷰 또는 모델을 수정한다. 뷰와 프리젠터는 밀접하게 결합되어있다. 이 둘사이는 양방향 일대일 관계이다. 모델은 프리젠터에 대해 모른다. 뷰 자체는 수동적이다. 다시말해 프리젠터는 데이터를 뷰로 푸쉬하기 때문에 프리젠터 패턴이라 불리기 때문이다. 이 패턴은 종종 WinForm이나 초기 WPF 어플리케이션에서 보여지곤 했다.

![](/assets/pattern_mvp.png)

### MVVM : Model-View-ViewModel

모델-뷰-뷰모델은 일반적으로 WPF 패턴이다. 이것은 뷰로 구성되어 모든 사용자의 입력을 받아 일반적으로 커맨드를 사용하여 뷰모델로 전달한다. 뷰는 데이터바인딩을 사용하여 뷰모델에서 데이터를 활발히 가져온다. 모델은 뷰모델에 대해 모른다.

![](/assets/pattern_mvvm.png)

### Some MVVM Frameworks
다음은 MVVM 프레임워크와 관련된 URL이니 사용해보고 비교해보면 도움이 될것이다.

+ [PRISM (Microsoft)](http://compositewpf.codeplex.com/)
+ [MVVM Light (Laurent Bugnion)](http://mvvmlight.codeplex.com/)
+ [WPF Application Framework](http://waf.codeplex.com/)
+ [Cinch](http://cinch.codeplex.com/)
+ [Caliburn Micro](http://caliburn.codeplex.com/)
+ [Core MVVM](http://coremvvm.codeplex.com/)
+ [Onyx](http://wpfonyx.codeplex.com/)
+ [MVVM Foundation](http://mvvmfoundation.codeplex.com/)
+ [How to build your own MVVM Framework](https://channel9.msdn.com/events/mix)
