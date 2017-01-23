# User Experience Design Process (사용자 경험기반 설계 프로세스)

### User Experience becomes a Key Success Factor (사용자 경험은 중요한 성공요인이다.)

과거에 우리는 주로 사용자의 기능 요구사항을 충족하는 제품을 만드는데 주력했다. 사용자 경험은 종종 개발 프로세스의 후순위로 밀려났다. 그러나 오늘날 고객은 기능중심의 제품이상을 요구하고 있다. 올바른 기능을 제공하는 것은 여전히 좋은 제품의 필수조건이지만 뭔가 특별한 것으로 바꾸려면 좋은 사용자 경험이 필요하다.

풍부한 사용자 경험의 제공은 운이 아니다. 계획, 설계 및 제품 개발에 통합되어야 한다. 풍부한 사용자 경험을 디자인하는 것은 약간의 그래픽과 그라디언트를 반사도에 의한 사용자 인터페이스를 만드는 것이 아니라 훨씬 더 광범위한 개념이다. 그것은 사용자과 소프트웨어간의 감성적인 연결을 생성하며 사용자의 기분을 좋게하고, 소프트웨어의 사용을 유지하게 한다.

### New Tools for Designers

Microsft는 개발팀에게 Visual Studio가 제공할 수 있는 것보다 훨씬 많은 그래픽 도구 지원이 필요한 풍부한 사용자 환경을 만들수 있는 힘을 주었다. 그래서 그들은 디자이너를 위한 새로운 툴들을 만들기로 결정했다.

![](/assets/expression_suite.png)

이 툴들은 Microsoft Expression이라 불리고, 다음의 4개의 제품으로 구성되었다.

+ <b>Expression Blend</b>는 WPF와 Silverlight의 사용자 인터페이스를 만들기위해 탄생했다. 이것은 디자이너와 개발자 사이의 다리역활을 한다. Visual Studio 솔루션 파일을 오픈한다.
+ <b>Expression Design</b>은 벡터그래픽을 생성, 편집하는 Adobe Illustrator의 가벼운 버전이다.
+ <b>Expression Media</b>는 비디오 파일을 인코딩, 자르기, 병합하기등과 실버라이트 스프리밍을 위한 최적화등을 한다.
+ <b>Expression Web</b>은 마이크로소프트의 차세대 HTML, Javascript 편집기이다. 이것은 FrontPage를 대체한다.

강력한 패키지들이다. 다음의 그림은 Visual Studio 솔루션의 일부분인 WPF프로젝트에 Adobe Illustrator 그래픽 디자이너에 의핸 생성된 벡터이미지를 통합하는 작업과정의 샘플을 보여준다.

![](/assets/collaboration_WorkOnTheSameSolution.png)

### Development Workflow of a WPF Project (WPF 프로젝트 개발작업공정)

풍부한 사용자 경험기반 WPF응용프로그램 개발은 유즈케이스 목록을 정의하는 요구분석가와 소프트웨어 구현하는 개발자 이상으로 훨씬 많은 기술을 필요로 한다. 당신은 사용자가 정말로 필요로 하는것이 무엇인지를 찾아야 한다. 이것은 사용자 중심 접근방식에 따라 실행되어질 수 있다.

![](/assets/workflow.jpg)

#### 1. Elicit Requirements (요구사항 유도)

어떤 종류의 소프트웨어 프로젝트와 마찬가지로, 개발 목표를 알고 집중하는 것이 중요하다. 관계자들, 사용자들과 대화를 하여 정말 필요로하는 것이 무엇인지 찾아야한다. 이러한 요구들은 기능으로 구체화하고, 유즈케이스(추상) 또는 사용자 시나리오(설명)로 표현해야 한다. 위험, 중요성별로 작업의 우선순위를 정하고 반복적으로 작업하라. 이 작업은 요구사항 엔지니어의 역활에 따라 작업된다.

#### 2. Create and Validate UI Prototype (UI 프로토타입 생성 및 검증)

사용자 인터페이스 프로토타입을 만든는 것은 사용자와 엔지니어간에 아이디어를 공유하여 상호 작용 디자인에 대한 공통된 이해를 만드는 중요한 단계이다. 이 작업은 보통 상호작용 디자이너에 의해 작업된다. 다지인 세부 사항에 대한 초기 논의를 막기 위해 사용자 인터페스를 대략적으로 스케치하는 것은 도움이 된다. 이 작업을 하는 다수의 기술과 도구가 다음과 같이 있다.

+ <b>Paper prototype</b>
사용자 인터페이스를 대략적으로 스케치를 하기 위해 종이와 연필을 사용한다. 도구와 인프라가 필요없다. 모든 사람들이 종이에 자신의 아이디어를 그릴 수 있다.

+ <b>Wireframes</b>
와이어프레임은 종종 페이지의 레이아웃을 스케치하는데 사용된다. 그것을 와이어프레임이라 부르는 이유는 단지 컨트롤과 이미지의 외곽선만을 그리기 때문이다. 파워포인트나 비지오와 같은 도구로 작업할 수 있다.

<b>Expression Blend 3- Sketch Flow</b> 스케치 플로우는 WPF에서 직접적으로 상호작용 프로토타입을 생성하는 새로운 멋진 기능이다. 통합된 "위글 스타일"을 사용하여 스케치 모양으로 만들 수 있다. 프로토타입은 통합된 피드백 메카니즘이 있는 독립실행형 플레이어에서 실행 할 수 있다. 

+ <b>Interactive Prototype</b> 가장 비싸고 실제같은 접근방식은 실제와 같은 응요프로그램으로 동작하지만 더미데이터로 동작하는 상호작용 프로토타입을 만드는 것이다.

실제 사용자에게 UI 프로토 타입을 테스트하는 것을 강력하게 추천한다. 이를 통해 초기 개발 과정에서 발생하는 디자인 문제를 찾아내도록 도와준다. 다음의 기술들은 UI 프로토타입을 평가하는 가장 인기있는 것들이다. 

+ <b>Walktrough</b>
워크트루는 일반적으로 와이어프레임이나 종이 프로토타입이 있는 프로젝트 초기에 작업한다. 사용자는 해결할 작업을 얻고 종이위에 터치에 의한 프로토타입을 제어한다. 테스트 리더는 상호작용 후 상태를 보여주는 새로운 종이를 제공한다.

+ <b>Usability Lab</b>
To do a usability lab, you need a computer with a screen capture software and a camera. The proband gets an task to do and the requirements and interaction engineer watch him doing this. They should not talk to him to find out where he gets stuck and why.
Usability Lab을 작동하려면 화면캡쳐 프로그램과 카메라가 있는 컴퓨터가 필요하다. 프로밴드(발상자)는 할 일을 얻고 요구사항과 상호작용 엔지니어는 그것이 작동하는 것을 지켜본다. 왜, 어디서 막혔는지 찾아낸 것을 그에게 말을 해서는 안된다.(???)

#### 3. Implement Business Logic and Raw User Interface (업무 로직과 원시 사용자 인터페이스 수행)

#### 4. Integrate Graphical Design (그래픽 디자인 통합)

#### 5. Test software (테스트 소프트웨어)

### Roles (역할)

풍부한 사용자 경험이 있는 현대의 사용자 인터페이스를 만드는 것은 당신의 개발팀에 추가적인 기술을 요구한다. 이 기술들은 개발팀의 사람들에게 분산 될 수 있는 역할로 설명된다.

+ <b>Developer</b>
개발자는 어플리케이션의 기능을 구현할 책임이 있다. 데이터 모델을 만들고, 업무 로직을 구현하며 모든것을 심플한 뷰로 만든다.

+ <b>Graphical Designer</b>
그래픽 디자이너는 그래픽적인 개념을 만들고 아이콘, 로고, 3D모델, 컬러표와 같은 그래픽 자산들을 생성할 책임이 있다. 만약 그래픽 디자이너가 Microsoft Expression 도구에 익숙하다면 스타일과 컨트롤 템플릿을 직접 만든다.

+ <b>Interaction Designer</b>
상호작용 디자이너는 내용과 사용자 인터페이스의 흐름에 대한 책임이 있다. 아이디어를 팀이나 고객과 공유하기 위해 와이어프레임이나 UI 스케치를 만든다. 워크쓰루나 스토리보드를 통해 작업의 검증을 해야 한다.

+ <b>Integrator</b>
통합자는 디자이너와 개발자 세계간의 예술가이다. 그래픽 디자이너의 자산을 가져와서 개발자의 원시 사용자 인터페이스에 통합한다. 이 역할은 희귀한 기술이 필요하기에 관련된 사람을 찾기는 아주 힘들다.

More Infos

[The New Iteration - Microsoft Paper about the Designer/Developer collaboration](http://windowsclient.net/wpf/white-papers/thenewiteration.aspx)
