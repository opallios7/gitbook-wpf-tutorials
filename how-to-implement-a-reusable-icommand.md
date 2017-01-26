# How to implement a reusable ICommand (재사용 ICommand를 구현하는 방법 )

### Introduction (소개)
MVVM(model-view-viewmodel) 패턴을 사용하려면 뷰에 액션을 바인딩하는 가장 많이 사용하는 메커니즘 중의 하나인 커맨드를 사용하는 것이다. 커맨드를 제공하려면 ICommand 인터페이스를 구현해야 한다. 이것은 매우 간단하지만 반복 또 반복해야 한다. 매우 번거로운 작업이다.

패턴의 아이디어는 두개의 델리게이트를 가지는 보편적인 커맨드를 구축한다. 하나는 ICommand.Execute(object param)이 발동될때 호출되어지고, 다른 하나는 ICommand.CanExecute(object param)이 호출될때 커맨드의 상태를 평가하는 호출이다.

부가적으로 CanExecuteChanged 이벤트가 트리거하는 메소드가 필요하다. 이렇게 하면 UI 엘리먼트가 커맨드의 CanExecute()를 다시 평가하게 된다.

### Sample implementation (단순 구현)
```
public class DelegateCommand : ICommand
{
  private readonly Predicate<object> _canExcute;
  private readonly Action<object> _execute;

  public event EventHandler CanExecuteChanged;

  public DelegateCommand(Action<object> execute) : this(execute, null)
  {
  }

  public DelegateCommand(Action<object> execute, Predicate<object> canExecute)
  {
    _execute = execute;
    _canExcute = canExecute;
  }

  public override bool CanExecute(object parameter)
  {
    if (_canExecute == null)
    {
      return true;
    }

    return _canExecute(parameter)
  }

  public override void Execute(object parameter)
  {
    _execute(parameter);
  }

  public void RaiseCanExecuteChanged()
  {
    if(CanExecuteChanged != null)
    {
      CanExecuteChanged(this, EventArgs.Empty);
    }
  }
}
```
