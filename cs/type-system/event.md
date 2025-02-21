# 이벤트

이벤트(Event)는 C#에서 특정 동작이나 상태 변화를 다른 클래스나 객체에 알리는 역할을 하는 델리게이트 기반의 기능입니다. 이벤트는 주로 특정한 조건이나 동작이 발생했을 때 다른 객체들에게 통지할 때 사용됩니다. 이벤트를 사용하면 객체들 간의 효과적인 통신 및 협력이 가능하며, 특히 UI 프로그래밍에서는 사용자 동작에 대한 응답을 처리하는 데 많이 활용됩니다.

### 이벤트의 기본 구성 요소:

1. **이벤트 발생자(Event Publisher):**
   - 이벤트를 발생시키는 클래스 또는 객체입니다. 이벤트 발생자는 델리게이트를 사용하여 이벤트를 정의하고, 해당 이벤트가 발생했을 때 등록된 리스너(이벤트 핸들러)에게 통지합니다.

   ```csharp
   public class EventPublisher
   {
       // 이벤트 정의
       public event EventHandler<MyEventArgs> MyEvent;

       // 이벤트를 발생시키는 메서드
       public void RaiseEvent()
       {
           // 이벤트 발생
           MyEvent?.Invoke(this, new MyEventArgs("Event occurred!"));
       }
   }
   ```

2. **이벤트 핸들러(Event Handler):**
   - 이벤트를 구독하고 해당 이벤트가 발생했을 때 실행될 메서드를 가지고 있는 클래스 또는 객체입니다. 이벤트 핸들러는 델리게이트로 표현되며, 이벤트 발생자의 이벤트에 등록되어 이벤트가 발생하면 실행됩니다.

   ```csharp
   public class EventHandler
   {
       // 이벤트 핸들러 메서드
       public void HandleEvent(object sender, MyEventArgs e)
       {
           Console.WriteLine($"Event handled: {e.Message}");
       }
   }
   ```

3. **이벤트 인자(Event Args):**
   - 이벤트가 발생했을 때 전달되는 정보를 포함하는 클래스입니다. 이벤트 인자 클래스는 `EventArgs` 클래스를 상속하여 구현됩니다.

   ```csharp
   public class MyEventArgs : EventArgs
   {
       public string Message { get; }

       public MyEventArgs(string message)
       {
           Message = message;
       }
   }
   ```

### 이벤트 사용 예제:

```csharp
class Program
{
    static void Main()
    {
        EventPublisher publisher = new EventPublisher();
        EventHandler handler = new EventHandler();

        // 이벤트 핸들러 등록
        publisher.MyEvent += handler.HandleEvent;

        // 이벤트 발생
        publisher.RaiseEvent();

        Console.ReadLine();
    }
}
```

### 주의사항:

1. **이벤트 발생자에서의 `Invoke` 호출:**
   - 이벤트를 발생시킬 때에는 델리게이트의 `Invoke` 메서드를 직접 호출하는 것이 아니라 `?.Invoke` 연산자를 사용하는 것이 안전합니다. 이는 이벤트에 등록된 핸들러가 없을 때 `null`을 반환하므로 예외를 방지할 수 있습니다.

   ```csharp
   MyEvent?.Invoke(this, new MyEventArgs("Event occurred!"));
   ```

2. **`EventHandler` 대신 `EventHandler<T>` 사용:**
   - 일반적으로 `EventHandler` 대신에 `EventHandler<T>`를 사용하는 것이 좋습니다. `EventHandler<T>`는 이벤트 인자를 제공하므로 더 유연한 이벤트 처리를 할 수 있습니다.

   ```csharp
   public class EventPublisher
   {
       public event EventHandler<MyEventArgs> MyEvent;

       public void RaiseEvent()
       {
           MyEvent?.Invoke(this, new MyEventArgs("Event occurred!"));
       }
   }
   ```

이벤트는 객체 간의 통신 및 협력을 쉽게 구현할 수 있도록 도와주며, 특히 UI 프로그래밍에서는 사용자의 동작에 대한 응답을 처리하는 데 주로 활용됩니다.