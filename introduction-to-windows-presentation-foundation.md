# Introduction to Windows Presentation Foundation (WPF 소개)

## Overview (개요)

Windows Presentation Foundation은 풍부한 사용자 경험을 담는 어플리케이션을 생성하는 Microsofts의 차세대 UI 프레임워크이다.

WPF는 단일 프레임워크에서 어플리케이션 UI, 2D그래픽, 3D그래픽, 문서, 멀티미디어를 결합한다. 이 벡터기반 렌더링 엔진은 그래픽 카드의 하드웨어 엑셀레이터를 사용한다. 이것은 UI를 빠르고, 스케일러블하고, 해상도에 독립적으로 만든다.

다음의 그림은 WPF의 새로운 특징의 개요를 보여준다.

![WPF Main Features](/assets/wpfMainFeatures.png)

## Separation of Appearance and Behavior (외관표현과 작업실행을 구분)

WPF는 작업실행과 사용자인터페이스의 외관표현을 구분한다. 외관표현은 일반적으로 XAML안에 기술하고, 작업실행은 C#이나 Visual Basic과 같은 관리되는 프로그램 언어에서 실행한다. 두개는 데이터바인딩, 이벤트, 커맨드로 묶여져 있다. 외관표현과 작업실행의 구분은 다음과 같은 이점을 가져다 준다.

+ 외관표현과 작업실행은 느슨하게 묶인다.
+ 디자이너와 개발자가 모델을 구분해서 작업할 수 있다.
+ 그래픽 디자인 툴은 코드를 분석하는 대신에 단순히 XML문서로 작업할 수 있다.

## Rich composition (풍부한 구성요소)

WPF 컨트롤들은 자유롭게 구성할 수 있다. 다른 컨텐트처럼 컨트롤의 거의 어떤 종류도 정의할 수 있다. 이 자유도는 디자이너에게는 끔찍한 이야기지만, 그것을 적절하게 사용한다면 매우 강력한 기능이 된다. 이미지버튼을 생성하기 위해 버튼에 이미지를 넣는거나 비디오 파일 선택을 위해 콤보박스에 비디오 목록을 넣는다.

![Play Sound Button](/assets/playsound_button.png)

```
<Button>
    <StackPanel Orientation="Horizontal">
        <Image Source="speaker.png" Stretch="Uniform"/>
        <TextBlock Text="Play Sound" />
    </StackPanel>
</Button>
```

## Highly customizable

외관표현과 작업실행을 엄격하게 구분한 이유는 컨트롤의 겉모습을 쉽게 할 수 있게 하기 위함이다. 스타일의 개념은 거의 HTML의 CSS처럼 사용하도록 허용한다. 템플릿은 컨트롤의 전체 외관표현을 바꾸도록 허용한다.

다음의 그림은 기본 WPF버튼과 변형된 버튼을 보여준다.

![Introduction Buttons](/assets/introduction_buttons.png)

## Resolution independence

WPF의 모든 치수는 논리 단위이다 - 픽셀이 아니다. 논리 단위는 1/96인치이다. 만약 스크린의 해상도가 커져도 사용자 인터페이스가 같은 크기로 유지한다. WPF는 벡터 기반의 렌더링 엔진에 기반을 두고 있기 때문에 스케일러블한 사용자 인터페이스로 빌드되는 것이 엄청나게 쉽게 된다.

![WPF Scaling](/assets/wpf_scaling.png)


 

