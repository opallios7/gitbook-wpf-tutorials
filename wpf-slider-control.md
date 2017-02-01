# WPF Slider Control (슬라이더 컨트롤)

### How to Make a Slider Snap to Integer Values (슬라이더 스냅을 정수값으로 사용하는 방법)

슬라이더의 최소, 최대값을 설정하고 값을 선택하면 결과는 표시자(Thumb)의 픽셀 위치에 따라 결정된다. 값은 일반적으로 자릿수가 많은 고정밀 값이다. 정수값만 허용하려면 IsSnapToTickEnabled 프로퍼티를 True로 설정해야 한다.

```
<Slider Minimum="0" Maximum="20" IsSnapToTickEnabled="True" TickFrequncy="2" />
```
