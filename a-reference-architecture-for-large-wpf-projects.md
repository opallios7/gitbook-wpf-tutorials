# A reference architecture for large WPF projects (대규모 WPF 프로젝트를 위한 참고 아키택쳐)

### Introduction (소개)
적절한 아키택쳐를 선택하는 것은 소프트웨어 프로젝트의 성공을 위해 매우 중요하다. 최고의 개념을 가질 수 있다. 아키택쳐가 작동되지 않는다면 사용자는 어플리케이션이 로딩하는 동안 안좋은 경험을 가질 것이다. 또한 강건성, 유지보수성, 테스트 가능성과 같은 측면은 매우 중요합니다.

WPF는 강력한 바인딩 프레임워크를 제공한다. MVVM 패턴을 사용한 장점을 활용하고 종속적으로 주입된 뷰를 분리시킨다면 굉장히 확장가능한 아키택쳐를 구축할 수 있다.

다음은 주요 구성요소와 패턴이다.

+ WPF 데이터바인딩
+ 모델-뷰-뷰모델 패턴
+ 종속적 컨테이너 (예, Unity)
+ System.Windows.Interactivity 라이브러리 작업

### How it works (어떻게 작동할까?)
기본 아이디어는 뷰를 구축하는 종속적 컨테이너를 가지는 것이다. 뷰는 DataContext에 바인딩 된 뷰모델이 삽입되어 있다. 뷰모델은 생성자에 의해 주입된 서비스에서 얻은 뷰에 대한 명령과 데이터를 집중적으로 제공한다. 서비스는 컨테이너 안에 싱글톤으로 존재한다.

아키택쳐를 사용하는 것은 백그라운드에서 서비스로 부터 오는 공통 데이터에 대해 마술처럼 상호작용하는 느슨하게 결합된 뷰를 구축할 수 있다. 서로 의존성을 가져야 하기 때문에 뷰를 재배치 하거나 대체가 아주 간단하다.

아키택쳐의 장점은 다음과 같다.

+ 데이터 바인딩 덕분에 UI 엘리먼트들을 간단하게 대체할 수 있다.
+ 뷰는 느슨하게 결합되어 빠르게 구성된다.
+ 뷰모델은 기존 단위 테스트로 테스트 할 수 있다.
+ 각 서비스는 단일 목적을 가진다. 개발이 쉽고, 아키택쳐를 확장 가능하게 만든다.

![](/assets/refarchitecture.png)

### Initializing the container and build up the main window (컨테이너를 초기화하고 매인 윈도우를 구축)
```
public class App : Application
{
  protected override void OnStartup(StartupEventArgs e)
  {
    IUnitContainer container = new UnitContainer();
    container.RegisterType<ICustomerService, CustomerService>();
    container.RegisterType<IShoppingCartService, ShoppingCartService>();

    MainWindow mainWindow = container.Resolve<MainWindow>();
    mainWindow.Show();
  }
}
```

### Injecting the viewmodel to the view (뷰모델을 뷰에 삽입)
프로퍼티에 [종속적] 특성을 추가하면, 종속적 컨테이너가 뷰를 생성한 후 명시된 유형을 확인하고 삽입한다. 삽입된 뷰 모델은 뷰의 데이터 컨텍스트로 직접 설정된다. 뷰 자신은 별 다른 로직이 없다.

```
public class MainWindow : Window
{
  [Dependency]
  public MainWindowViewModel ViewModel
  {
    set { DataContext = value;}
  }

  public MainWindow()
  {
    InitializeComponent();
  }
}
```

### Implementing the viewmodel (뷰모델 구현)
```
public class MainWindowViewModel
{
  private ICustomerService _customerService;

  public MainWindowViewModel(ICustomerService customerService)
  {
    _customerService = customerService;
    Customers = new ListCollectionView(customerService.Customers);
  }

  public ICollectionView Customers { get; private set;}
}
```

### Binding the data to the view (데이터를 뷰에 바인딩)
```
<Window x:Class="WpfTutorial.MainWindow"
              xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
              xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
  <ListBox ItemsSource="{Binding Customers}" />
</Window>
```
