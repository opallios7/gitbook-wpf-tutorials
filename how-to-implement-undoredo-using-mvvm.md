# How to implement undo/redo using MVVM (MVVM을 사용한 실행취소/다시실행 구현 방법)

### Introduction (소개)

많은 사용자가 요구하는 기능 중 하나는 불필요한 실행취소/다시실행의 통합이다. 즉, 어플리케이션은 사용자가 - 한번에 하나씩 -  수정한 내용을 어플리케이션의 시작으로 되돌리고 결국 다시 적용하기보다는 다시 사용할 수 있음을 의미한다. 사용자가 명확하지 않은 명령어를 생각없이 사용할 수 있기때문에 유용성이 매우 높다. 왜냐하면 명확하지 않은 명령을 잘못사용하면 취소가 가능하기 때문이다. 현재 실행취소/다시실행은 모든 최신 데이터 편집 어플리케이션에 거의 표준이 되었다.

![](/assets/undoredo.png)

### The MVVM-Pattern (MVVM 패턴)

WPF의 강력한 데이터바인딩 기능으로 대부분의 어플리케이션은 인기있는 MVVM(Model-View-ViewModel) 패턴을 사용하고 있다. 이 패턴의 개념은 기본적으로 특정 뷰에 대한 모든 데이터와 명령어를 종합하고 바인딩 할 수 있는 프로퍼티로 뷰에 제공하는 클래스를 정의한다. 프로퍼티의 변경은 INotifyPropertyChanged 인터페이스의 이벤트에 의해 통지된다.

### A concept of implementing undo/redo (실행취소/다시실행 구현의 개념)

실행취소/다시실행을 구현하는 전통적인 접근방식은 오직 명령을 통해서만 모델을 변경할 수 있도록 하는 것이고, 모든 명령은 반전(invertible)이 가능해야 한다. 사용자가 작업을 실행하는 것보다 어플리케이션이 명령을 생성하여 실행하고, 실행취소 스택에 반대된 명령을 입력한다. 사용자가 실행취소를 클릭하면 어플리케이션은 실행취소 스택에서 가장 위(inverse)의 명령을 실행하고, 그것은 다시 반전하고(원래 명령을 얻기 위함)  다시실행 스택에 입력한다. 그것이 전부다.

#### Scenario 1: Executing an action (액선 실행)
![](/assets/undoredo1.png)

#### Scenario 2: Undoing an action (액션 실행취소)
![](/assets/undoredo2.png)

### Adoption for WPF (WPF가 채택한 것)

INotifyPropertyChanged 인터페이스를 구현하고 Notify(string propertyName)이라는 private 메소드를 제공하는 기본클래스로 시작한다.

```
public class NotifyableObject : INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;

    protected void Notify(string propertyName)
    {
        if (PropertyChanged != null)
        {
            PropertyChanged(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}
```
그런 다음 뷰에 직접 바인딩 된 모든 모델 객체 또는 뷰 모델이 상속해야 하는 기본클래스인 TrackableObject를 생성한다.

```
public class TrackableObject : NotifyableObject
{
    private readonly List<ITrackable> _trackableItems = new List<ITrackable>();

    public bool HasChanges
    {
        get { return _trackableItems.Any(i => i.HasChanges); }
    }

    public IModificationTracker ModificationTracker { get; set; }

    protected TrackableValue<T> RegisterTrackableValue<T>(string propertyName,
           T defaultValue = default(T))
    {
        var property = new TrackableValue<T>(propertyName, Modify, Notify, defaultValue);
        _trackableItems.Add(property);
        return property;
    }

    protected TrackableCollection<T> RegisterTrackableCollection<T>()
    {
        var collection = new TrackableCollection<T>(Modify);
        _trackableItems.Add(collection);
        return collection;
    }

    private void Modify(Action doAction, Action undoAction, Action notification)
    {
        var modification = new Modification(doAction, undoAction, notification);
        modification.Execute();
        ModificationTracker.TrackModification(modification);
    }
}
```

프로퍼티 값을 변경할 때 수정사항의 생성을 단순화하기 위해 우리는 각각의 프로퍼티에 TrackableValue라 불리는 제네릭 래퍼를 생성한다.

```
public class TrackableValue<T> : ITrackable
{
    private readonly string _propertyName;
    private readonly Action<Action, Action, Action> _modifyCallback;
    private readonly Action<string> _notifyAction;
    private T _value;

    public TrackableValue(string propertyName,
               Action<Action, Action, Action> modifyCallback,
               Action<string> notifyAction, T defaultValue)
    {
        _propertyName = propertyName;
        _modifyCallback = modifyCallback;
        _notifyAction = notifyAction;
        _value = defaultValue;
    }

    public bool HasChanges
    {
        get { return _originalValue.Equals(_value); }
    }

    public T Value
    {
        get { return _value; }
        set
        {
            var oldValue = _value;
            _modifyCallback(() => _value = value,
                            () => _value = oldValue,
                            () => _notifyAction(_propertyName));
        }
    }
}
```

컬랙션에서 항목의 추가/제거를 추적하기 위해 해아 하는 것과 동일한 작업이다.

```
public class TrackableCollection<T> : IList<T>, ITrackable
{
    private readonly Action<Action, Action, Action> _modifyCallback;
    private readonly List<T> _list = new List<T>();
    private readonly List<T> _originalList = new List<T>();

    public TrackableCollection(Action<Action, Action, Action> modifyCallback)
    {
        _modifyCallback = modifyCallback;
    }

    public event EventHandler<EventArgs<T>> ItemAdded;
    public event EventHandler<EventArgs<T>> ItemRemoved;
    public event EventHandler CollectionChanged;

    public bool HasChanges
    {
        get
        {
            if( _list.Count == _originalList.Count)
            {
                return _list.Where((item, index) =>
                       !item.Equals(_originalList[index])).Any();
            }
            return true;
        }
    }

    public void AcceptChanges()
    {
        _originalList.Clear();
        _originalList.AddRange(_list);
    }

    public IEnumerator<T> GetEnumerator()
    {
        return _list.GetEnumerator();    
    }

    IEnumerator IEnumerable.GetEnumerator()
    {
        return GetEnumerator();
    }

    public void Add(T item)
    {
        _modifyCallback(() =>
        {
            _list.Add(item);
            ItemAdded.Notify(this, new EventArgs<T>(item));
        },
        () =>
        {
            _list.Remove(item);
            ItemRemoved.Notify(this, new EventArgs<T>(item));
        },
        OnCollectionModified);
    }

    public void Clear()
    {
        var items = new T[_list.Count];
        _list.CopyTo(items);
        _modifyCallback(() =>
        {
            _list.ForEach(i => ItemRemoved.Notify(this, new EventArgs<T>(i)));
            _list.Clear();
        },
        () =>
        {
            _list.AddRange(items);
            _list.ForEach(i => ItemAdded.Notify(this, new EventArgs<T>(i)));
        },
        OnCollectionModified);
    }

    public bool Contains(T item)
    {
        return _list.Contains(item);
    }

    public void CopyTo(T[] array, int arrayIndex)
    {
        _list.CopyTo(array, arrayIndex);
    }

    public bool Remove(T item)
    {
        var result = _list.Contains(item);
        _modifyCallback(() =>
        {
            _list.Remove(item);
            ItemRemoved.Notify(this, new EventArgs<T>(item));
        },
        () =>
        {
            _list.Add(item);
            ItemAdded.Notify(this, new EventArgs<T>(item));
        },
        OnCollectionModified);
        return result;
    }

    public int Count
    {
        get { return _list.Count; }
    }

    public bool IsReadOnly
    {
        get { return false; }
    }

    public int IndexOf(T item)
    {
        return _list.IndexOf(item);
    }

    public void Insert(int index, T item)
    {
        _modifyCallback(() =>
        {
            _list.Insert(index, item);
            ItemAdded.Notify(this, new EventArgs<T>(item));
        },
        () =>
        {
            _list.Remove(item);
            ItemRemoved.Notify(this, new EventArgs<T>(item));
        },
        OnCollectionModified);
    }

    public void RemoveAt(int index)
    {
        var item = _list[index];
        _modifyCallback(() =>
        {
            _list.Remove(item);
            ItemRemoved.Notify(this, new EventArgs<T>(item));
        },
        () =>
        {
            _list.Insert(index, item);
            ItemAdded.Notify(this, new EventArgs<T>(item));
        },
        OnCollectionModified);
    }

    public T this[int index]
    {
        get { return _list[index]; }
        set
        {
            var oldItem = _list[index];
            _modifyCallback(() =>
           {
               _list[index] = value;
               ItemAdded.Notify(this, new EventArgs<T>(value));
           },
           () =>
           {
               _list[index] = oldItem;
               ItemRemoved.Notify(this, new EventArgs<T>(oldItem));
           },
           OnCollectionModified);
        }
    }

    private void OnCollectionModified()
    {
        CollectionChanged.Notify(this, EventArgs.Empty);   
    }
}
```
