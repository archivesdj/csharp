# 프로그램 구조

## 개요

C# 프로그래밍 언어의 기본적인 구조는 일반적으로 다음과 같습니다:

1. **네임스페이스 (Namespace):** 네임스페이스는 관련된 클래스, 인터페이스, 구조체, 델리게이트 등을 그룹화하는 데 사용됩니다. 예를 들어, `System`은 많은 기본 클래스 및 유틸리티를 포함하는 네임스페이스입니다.

    ```csharp
    using System;

    namespace MyNamespace
    {
        // 클래스, 인터페이스, 등을 선언
    }
    ```

2. **클래스 (Class):** C#에서 코드의 주된 구조는 클래스입니다. 클래스는 데이터와 해당 데이터를 조작하는 메서드를 포함합니다.

    ```csharp
    namespace MyNamespace
    {
        class MyClass
        {
            // 멤버 변수 (필드)
            private int myField;

            // 생성자
            public MyClass(int initialValue)
            {
                myField = initialValue;
            }

            // 메서드
            public void MyMethod()
            {
                Console.WriteLine("MyMethod called with value: " + myField);
            }
        }
    }
    ```

3. **메서드 (Method):** 클래스 내부에 선언된 함수를 메서드라고 부릅니다. 메서드는 특정 작업을 수행하거나 값을 반환할 수 있습니다.

4. **속성 (Property):** 클래스의 필드에 대한 접근자(getter, setter)를 캡슐화한 것으로, 프로퍼티를 통해 값을 읽거나 쓸 수 있습니다.

    ```csharp
    class MyClass
    {
        private int myField;

        // 프로퍼티
        public int MyProperty
        {
            get { return myField; }
            set { myField = value; }
        }
    }
    ```

5. **이벤트 (Event):** 클래스에서 발생하는 특정 상황에 대한 통지 메커니즘으로, 다른 부분에서 해당 이벤트에 대한 리스너(이벤트 핸들러)를 등록할 수 있습니다.

    ```csharp
    class MyEventClass
    {
        // 이벤트 선언
        public event EventHandler MyEvent;

        // 이벤트를 발생시키는 메서드
        public void RaiseEvent()
        {
            // 이벤트 호출
            MyEvent?.Invoke(this, EventArgs.Empty);
        }
    }
    ```

6. **구조체 (Struct):** 클래스와 유사하지만 값 형식을 나타내며, 스택에 할당되어 힙에 할당되는 클래스보다 경량입니다.

    ```csharp
    public struct Point
    {
        public int X;
        public int Y;
    }
    ```

7. **인터페이스 (Interface):** 메서드, 속성, 이벤트 등의 시그니처를 정의하여 다른 클래스에서 구현할 수 있도록 하는 추상화 메커니즘입니다.

    ```csharp
    public interface IDrawable
    {
        void Draw();
    }
    ```

8. **Main 메서드:** C# 프로그램은 실행 시 Main 메서드에서 시작됩니다. Main 메서드는 프로그램의 진입점으로 동작하며, 필요한 작업을 수행하고 다른 메서드 및 클래스를 호출할 수 있습니다.

    ```csharp
    class Program
    {
        static void Main()
        {
            // 프로그램 시작
            MyClass myObject = new MyClass(42);
            myObject.MyMethod();
        }
    }
    ```

이러한 기본적인 구조를 사용하여 C#에서 강력하고 모듈화된 코드를 작성할 수 있습니다. 클래스, 메서드, 속성 등을 조합하여 프로그램을 구성하고, 네임스페이스를 사용하여 코드를 조직화하여 유지보수성을 향상시킬 수 있습니다.

## Main 메서드

`Main` 메서드는 C# 프로그램의 시작점을 나타내는 특별한 메서드입니다. C# 응용 프로그램이 실행될 때 시스템은 `Main` 메서드를 찾아 실행하게 됩니다. `Main` 메서드는 일반적으로 `Program` 클래스 또는 해당 프로그램의 진입 클래스에 속해 있습니다.

### Main 메서드 특징

`Main` 메서드의 특징은 다음과 같습니다:

1. **시작점 역할:** C# 응용 프로그램은 `Main` 메서드에서 시작됩니다. 프로그램 실행 시 처음으로 호출되는 메서드입니다.

2. **시그니처:** `Main` 메서드는 특정한 시그니처를 가져야 합니다. 보통 다음과 같은 형태를 가집니다:

    ```csharp
    static void Main()
    {
        // 프로그램 시작
    }
    ```

    또는 명령행 인수를 처리해야 할 경우 다음과 같이 `string[] args` 매개변수를 사용할 수도 있습니다:

    ```csharp
    static void Main(string[] args)
    {
        // 프로그램 시작
    }
    ```

3. **`static` 키워드:** `Main` 메서드는 정적(static) 메서드여야 합니다. 이는 프로그램이 인스턴스를 생성하지 않고도 진입점으로 사용될 수 있음을 의미합니다.

4. **반환 타입:** `Main` 메서드는 보통 `void`를 반환하며, 프로그램이 종료되면 바로 시스템에 제어를 반환합니다. 반환 타입이 `int`일 경우, 해당 값은 운영 체제에 전달되며 종료 코드(exit code)로 사용될 수 있습니다.

    ```csharp
    static int Main()
    {
        // 프로그램 시작
        return 0; // 종료 코드 0
    }
    ```

    반환 타입이 `int`인 경우, 일반적으로 0은 성공적인 종료를 나타내고, 다른 값은 오류를 나타냅니다.

예시:

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Hello, World!");
    }
}
```

위 예시에서 `Main` 메서드는 간단한 "Hello, World!" 메시지를 콘솔에 출력하는 간단한 프로그램을 시작합니다.

## 최상위 문

C# 9.0부터 도입된 Top-level statements는 C# 프로그램에서 진입점 (`Main` 메서드)을 명시적으로 작성하지 않아도 되게 하는 기능입니다. 기존의 클래스와 메서드 구조 없이 간결하게 코드를 작성할 수 있도록 도와줍니다.

바로 위에서 예시로 보여준 일반적인 C# 프로그램의 구조인데, Top-level statements를 사용하면 클래스와 `Main` 메서드를 작성하지 않고도 코드를 간결하게 만들 수 있습니다.

```csharp
using System;

Console.WriteLine("Hello, World!");
```

여기에서 `using` 문과 `Console.WriteLine`이 프로그램의 진입점에 직접 위치하고 있습니다. 컴파일러는 이 코드를 기반으로 자동으로 클래스와 `Main` 메서드를 생성하게 됩니다.

### 최상위 문 사용 시 이점

Top-level statements를 사용하는 이점은 다음과 같습니다:

1. **간결성:** 클래스와 메서드를 명시적으로 작성하지 않아도 되므로 코드가 간결해집니다.

2. **초기 설정 단순화:** 작은 프로그램 또는 스크립트 형태의 코드에서 초기 설정이 단순화됩니다.

3. **급한 테스트:** 간단한 기능을 빠르게 테스트하거나 간단한 스크립트를 작성할 때 편리합니다.

### 최상위 문 사용 시 주의 사항

Top-level statements를 사용할 때에는 몇 가지 주의 사항이 있습니다:

- Top-level statements는 C# 9.0 이상에서 지원됩니다.
- 한 파일에 하나의 Top-level statement만 사용하는 것이 좋습니다.
- 프로덕션 레벨의 큰 프로젝트에서는 전통적인 클래스 및 메서드 구조를 사용하는 것이 바람직합니다.

Top-level statements를 사용하면 간단한 작업을 더 편리하게 수행할 수 있으며, 특히 스크립팅이나 간단한 프로그램에서 매우 유용합니다.
