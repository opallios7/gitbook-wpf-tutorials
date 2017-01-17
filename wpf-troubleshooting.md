# WPF Troubleshooting (WPF 문제해결)

During my time as a consultant I noticed, that there were typical traps in WPF, where developers can loose a lot of time. So I decided to make a hitlist of the most common mistakes and solutions how to resolve them. I hope this helps.

내가 컨설턴트였던 동안에 WPF에는 개발자들이 많은 시간을 소모할 수 있는 전형적인 문제가 있었다. 그래서 가장 일반적인 실수를 해결하는 방법에 대한 목록을 만들기로 결심했다. 나는 이것이 도움이 되길 희망한다.

### Layout

+ <b> Scrollbar is not active or visible </b>
+ <b> 스크롤바는 활성화 또는 보여지지 않는다.</b>
    + If your control is within a vertical stackpanel, it gives the control infinite height to layout. Consider replacing the stackpanel by a dockpanel.
    + 만약 컨트롤이 수직 패널안에 있다면, 무한 높이의 컨트롤을 레이아웃에게 제공한다. 스택 패널을 도킹패널로 바꾸는 것을 고려해라.
    
+ <b> I Created a data template and set HorizontalAlignment to Stretch but the item is not stretched </b>
+ <b> 데이터 템플릿을 생성하고 HorizontalAlignment를 Stretch로 설정했지만 항목이 늘어나지 않는다.</b>
    + Set the HorizontalContentAlignment on the list to Stretch.
    + 리스트의 HorizontalContentAlignment를 Stretch로 설정하라.
    
    
