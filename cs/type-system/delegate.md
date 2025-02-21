# 델리게이트

델리게이트(Delegate)는 C#에서 메서드에 대한 형식 안전한 참조를 나타내는 개체입니다. 델리게이트를 사용하면 메서드를 다른 메서드로 전달하거나 메서드를 변수로 저장할 수 있으며, 이를 통해 이벤트 처리, 비동기 프로그래밍, 콜백 패턴 등 다양한 상황에서 유연한 코드를 작성할 수 있습니다.

### 델리게이트의 선언:

델리게이트를 선언하려면 델리게이트가 참조할 메서드의 시그니처와 일치하는 형식을 정의해야 합니다.

```csharp
// 델리게이트 선언
public delegate void MyDelegate(string message);

// 델리게이트 사용 예제
public class Example
{
    public void DisplayMessage(string message)
    {
        Console.WriteLine(message);
    }

    public static void ShowMessage(string message)
    {
        Console.WriteLine(message);
    }
}
```

### 델리게이트의 인스턴스화와 호출:

델리게이트를 인스턴스화하고 호출하는 방법은 다음과 같습니다.

```csharp
Example example = new Example();

// 인스턴스 메서드를 참조하는 델리게이트
MyDelegate delegateInstance1 = new MyDelegate(example.DisplayMessage);

// 정적 메서드를 참조하는 델리게이트
MyDelegate delegateInstance2 = new MyDelegate(Example.ShowMessage);

// 델리게이트 호출
delegateInstance1("Hello, World!"); // "Hello, World!" 출력
delegateInstance2("C# Delegates!");  // "C# Delegates!" 출력
```

### 다중 델리게이트 연결:

하나의 델리게이트 인스턴스에 여러 메서드를 연결하여 호출할 수 있습니다. 이를 다중 델리게이트 호출이라고 합니다.

```csharp
MyDelegate multiDelegate = delegateInstance1 + delegateInstance2;

// 델리게이트 호출 (모든 메서드가 호출됨)
multiDelegate("Multiple Delegates!"); // "Hello, World!" 출력, "C# Delegates!" 출력
```

### 이벤트에서 델리게이트 사용:

델리게이트는 이벤트 처리에도 널리 사용됩니다. [이벤트](./events)는 특별한 형태의 델리게이트로, 다른 클래스에서 이벤트를 발생시키고 해당 이벤트에 대한 리스너(델리게이트)를 등록할 수 있도록 해줍니다.

```csharp
public class Publisher
{
    // 이벤트 선언
    public event MyDelegate MyEvent;

    public void RaiseEvent(string message)
    {
        // 이벤트 발생
        MyEvent?.Invoke(message);
    }
}

public class Subscriber
{
    public void OnEventHandled(string message)
    {
        Console.WriteLine($"Event handled: {message}");
    }
}

// 사용 예제
Publisher publisher = new Publisher();
Subscriber subscriber = new Subscriber();

// 이벤트에 델리게이트 등록
publisher.MyEvent += subscriber.OnEventHandled;

// 이벤트 발생
publisher.RaiseEvent("Event Message"); // "Event handled: Event Message" 출력
```

델리게이트는 이벤트 처리, 비동기 프로그래밍, 콜백 패턴 등 다양한 상황에서 사용되며, C#에서 델리게이트를 통해 메서드를 참조하고 호출하는 것은 프로그램의 유연성과 모듈성을 높이는데 기여합니다.

## 사용 시 유의사항

델리게이트를 사용할 때 몇 가지 유의사항이 있습니다. 아래는 델리게이트 사용 시 고려해야 할 중요한 사항들입니다.

1. **Null 체크:**
   - 델리게이트를 호출하기 전에 항상 null 체크를 수행해야 합니다. 만약 델리게이트가 null인 상태에서 호출하려고 하면 `System.NullReferenceException`이 발생합니다.

   ```csharp
   MyDelegate myDelegate = /* ... */;
   if (myDelegate != null)
   {
       myDelegate();
   }
   ```

2. **Exception Handling:**
   - 델리게이트를 호출할 때 발생할 수 있는 예외를 적절히 처리해야 합니다. 델리게이트 내부의 코드에서 예외가 발생하면 해당 예외가 호출자로 전파됩니다.

   ```csharp
   try
   {
       myDelegate();
   }
   catch (Exception ex)
   {
       Console.WriteLine($"Exception caught: {ex.Message}");
   }
   ```

3. **Synchronous vs. Asynchronous 호출:**
   - 델리게이트는 동기적으로 호출될 수도 있고, 비동기적으로 호출될 수도 있습니다. 비동기적 호출을 다루려면 `BeginInvoke` 및 `EndInvoke`와 같은 메서드를 사용하거나, C# 5.0 이후의 버전에서는 `async` 및 `await`를 활용할 수 있습니다.

   ```csharp
   // 동기적 호출
   myDelegate();

   // 비동기적 호출
   IAsyncResult result = myDelegate.BeginInvoke(null, null);
   myDelegate.EndInvoke(result);
   ```

4. **Target 객체와 수명 관리:**
   - 델리게이트가 인스턴스 메서드를 참조하는 경우, 해당 메서드의 수명 주기에 따라 메모리 누수가 발생할 수 있습니다. 이를 방지하기 위해 델리게이트의 `Target` 속성을 사용하여 명시적으로 델리게이트가 참조하는 객체를 해제할 수 있습니다.

   ```csharp
   MyDelegate myDelegate = someObject.SomeMethod;

   // 델리게이트가 참조하는 객체의 수명이 종료되면
   myDelegate = null; // 명시적으로 델리게이트 해제
   ```

5. **성능 고려:**
   - 델리게이트 호출은 일반적으로 메서드 호출보다 느릴 수 있습니다. 델리게이트를 사용할 때 성능을 고려하여 최적화된 방식으로 구현하는 것이 중요합니다.

6. **대리자 체인과 순서:**
   - 델리게이트는 여러 메서드를 체인으로 연결하여 호출할 수 있습니다. 이 때, 체인된 델리게이트가 호출되는 순서를 주의해야 합니다.

   ```csharp
   MyDelegate delegate1 = /* ... */;
   MyDelegate delegate2 = /* ... */;

   MyDelegate combinedDelegate = delegate1 + delegate2;
   ```

   체인된 델리게이트에서 각 메서드의 반환값은 마지막으로 호출된 메서드의 반환값입니다.

델리게이트를 올바르게 사용하려면 이러한 유의사항을 고려하여 코드를 작성해야 합니다. 특히 예외 처리, null 체크, 메모리 관리, 성능 최적화 등에 주의를 기울이는 것이 중요합니다.