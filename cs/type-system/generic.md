# 제네릭

제네릭 타입(Generic Type)은 C#에서 도입된 강력한 기능 중 하나로, 타입을 일반화하여 재사용성을 높이고 형식 안전성을 확보하는 데 사용됩니다. 제네릭은 클래스, 인터페이스, 메서드 등 여러 컴포넌트에 적용될 수 있습니다.

### 제네릭 클래스:

제네릭 클래스는 타입 매개변수를 사용하여 클래스를 일반화합니다.

```csharp
public class Box<T>
{
    private T value;

    public void Set(T newValue)
    {
        value = newValue;
    }

    public T Get()
    {
        return value;
    }
}
```

위의 예제에서 `Box<T>` 클래스는 어떤 타입(`T`)의 값을 담을 수 있는 상자를 나타냅니다.

### 제네릭 메서드:

제네릭 메서드는 메서드 레벨에서 타입 매개변수를 사용하여 메서드를 일반화합니다.

```csharp
public T Max<T>(T a, T b) where T : IComparable<T>
{
    return a.CompareTo(b) > 0 ? a : b;
}
```

위의 예제에서 `Max` 메서드는 어떤 타입(`T`)에 대해서라도 두 값 중 큰 값을 반환합니다.

### 제네릭 인터페이스:

제네릭 인터페이스는 인터페이스를 일반화하여 여러 타입에서 구현될 수 있도록 합니다.

```csharp
public interface IRepository<T>
{
    void Add(T item);
    T GetById(int id);
    IEnumerable<T> GetAll();
}
```

위의 예제에서 `IRepository<T>`는 어떤 타입(`T`)에 대한 데이터 저장소 인터페이스를 정의합니다.

### 제네릭 제약 조건:

제네릭 타입에 대한 제약 조건을 지정하여 특정 인터페이스를 구현하도록 하거나, 특정 클래스로부터 상속받도록 할 수 있습니다.

```csharp
public class GenericList<T> where T : IComparable<T>
{
    // ...
}
```

위의 예제에서 `T`는 `IComparable<T>` 인터페이스를 구현한 타입만 허용됩니다.

### 형식 안전성과 재사용성:

제네릭을 사용하면 코드의 형식 안전성을 보장할 수 있습니다. 또한, 같은 기능을 하는 코드를 여러 타입에 대해 중복해서 작성하지 않고도 재사용할 수 있게 됩니다. 이는 코드의 유지보수성을 높이고 중복을 줄이는 데 도움이 됩니다.

```csharp
Box<int> intBox = new Box<int>();
intBox.Set(42);
int value = intBox.Get();

Box<string> stringBox = new Box<string>();
stringBox.Set("Hello, Generics!");
string stringValue = stringBox.Get();
```

위의 예제에서 `Box<T>` 클래스를 `int`와 `string`에 대해 재사용하고 있습니다.

제네릭은 타입에 대한 일반화된 솔루션을 제공하여 코드의 품질과 유지보수성을 향상시킵니다. 이는 컬렉션, LINQ, 데이터 구조, 디자인 패턴 등 다양한 상황에서 활용됩니다.

## 사용 시 유의사항

제네릭을 사용할 때 몇 가지 주의사항이 있습니다. 이러한 주의사항을 고려하여 적절하게 제네릭을 활용하면 코드의 안전성과 유연성을 높일 수 있습니다.

1. **제약 조건 사용:**
   - 제네릭 타입에 제약 조건을 사용하여 특정 인터페이스를 구현하도록 하거나, 특정 클래스로부터 상속받도록 할 수 있습니다. 이는 코드 안정성을 높이고 예상치 못한 타입의 사용을 방지하는 데 도움이 됩니다.

     ```csharp
     public class MyGenericClass<T> where T : SomeInterface
     {
         // ...
     }
     ```

2. **제네릭과 상속 구조:**
   - 제네릭 클래스나 메서드를 설계할 때 상속 구조를 고려해야 합니다. 제네릭을 사용하는 클래스를 상속받는 경우, 기반 클래스나 인터페이스에 대한 타입 매개변수를 정의할 수 있습니다.

     ```csharp
     public class MyBaseClass<T>
     {
         // ...
     }

     public class MyDerivedClass : MyBaseClass<int>
     {
         // ...
     }
     ```

3. **성능 고려:**
   - 제네릭은 형식 안전성을 제공하지만, 가끔씩 성능 오버헤드가 발생할 수 있습니다. 대부분의 경우에는 이를 무시해도 되지만, 성능이 중요한 부분에서는 이를 고려해야 합니다.

4. **박싱과 언박싱 주의:**
   - 제네릭을 사용할 때 박싱(Boxing)과 언박싱(Unboxing)에 주의해야 합니다. 값 형식을 제네릭으로 다루다가 참조 형식으로 변환될 경우 성능 저하가 발생할 수 있습니다.

     ```csharp
     List<object> myList = new List<object>();
     myList.Add(42); // int가 박싱됨
     int value = (int)myList[0]; // 박싱된 값이 언박싱됨
     ```

5. **비교 및 동등성 비교:**
   - 제네릭을 사용하여 객체의 비교나 동등성 비교를 할 때에는 `EqualityComparer<T>.Default`나 `IEquatable<T>` 인터페이스를 사용하여 적절한 방식으로 비교해야 합니다.

     ```csharp
     List<string> strings = new List<string> { "apple", "banana", "cherry" };
     string searchTerm = "banana";
     bool contains = strings.Contains(searchTerm, StringComparer.OrdinalIgnoreCase);
     ```

6. **Null 체크:**
   - 제네릭을 사용하는 메서드나 클래스에서는 null 값에 대한 적절한 처리를 해주어야 합니다. 특히, 제네릭 타입 매개변수로부터 null이 허용되는 경우에는 그에 대한 대응을 고려해야 합니다.

     ```csharp
     public class MyGenericClass<T>
     {
         public void DoSomething(T value)
         {
             if (value != null)
             {
                 // ...
             }
         }
     }
     ```

7. **가독성과 명확성:**
   - 제네릭 코드를 작성할 때에는 가독성과 명확성을 유지하는 것이 중요합니다. 제네릭 타입이나 메서드의 목적이 명확하게 전달되도록 작성해야 합니다.

     ```csharp
     // 좋은 예
     public class Cache<TKey, TValue> { /* ... */ }

     // 나쁜 예 (의도를 알기 어려움)
     public class C<T1, T2> { /* ... */ }
     ```

이러한 주의사항을 고려하여 제네릭을 사용하면 코드의 안전성과 재사용성을 향상시킬 수 있습니다.