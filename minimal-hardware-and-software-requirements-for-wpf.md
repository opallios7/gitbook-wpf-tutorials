# Minimal Hardware and Software Requirements for WPF (WPF를 위한 최소 하드웨어와 소프트웨어 요구사양)

### Software Requirements (소프트웨어 요구사항)

당신의 머신에서 WPF를 동작하려면 다음의 소프트웨어 최신버전이 있어야 한다.

+ Windows XP 서비스 팩 2 이상
+ .NET Framework 3.0 이상

### Hardware Requirements (하드웨어 요구사항)

WPF를 위한 최소한의 하드웨어 요구사항은 없다. 모든 요구사항은 어플리케이션에서 사용되는 복잡함과 효과로부터 온다.

그래픽 카드가 Direct X 9이상을 지원하면 하드웨어 가속을 할수 있는 장점이 있다. 공급업체가 WDDM 드라이버를 지원하는 그래픽아답터를 추천한다.

Window XP이하에서는 하드웨어 렌더링의 일부 효과를 낼수 없다. 예를 들어 AllowTransparency 윈도우를 True로 설정하거나 BitmapEffects를 사용하는 것을 말한다.

### How to specify minimal hardware requirements (하드웨어 최소요구사항 명시하는 법)

고객에게 좋은 경험을 제공할 수 있도록 최소한의 하드웨어 요구사항을 지정하는 심플한 방법은 Microsoft의 Premium Ready 라벨이다. 장비는 최소한 다음과 같은 요구사항을 가진다.

+ > 800MHz Prozessor
+ 512 MBytes RAM
+ A DirectX 9가 실행가능한 그래픽 아답터

