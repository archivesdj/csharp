# 코딩 스타일

C#의 코딩 스타일은 주로 Microsoft에서 제공하는 [C# 코딩 규칙 및 스타일 가이드](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions)에 기반하여 형성됩니다. 이러한 규칙은 코드의 일관성과 가독성을 높이고, 팀원 간의 협업을 용이하게 만들기 위해 사용됩니다.

주요한 C# 코딩 스타일 가이드 포인트는 다음과 같습니다:

1. **들여쓰기와 중괄호:**
   - 들여쓰기에는 스페이스 4개를 사용하며, 중괄호는 다음 줄에 위치합니다.

   ```csharp
   if (condition)
   {
       // 코드 블록
   }
   ```

1. **빈 줄:**
   - 코드 블록 간에는 빈 줄을 사용하여 가독성을 높입니다.

   ```csharp
   public void Method1()
   {
       // 코드 블록 1
   }

   public void Method2()
   {
       // 코드 블록 2
   }
   ```

1. **네임스페이스:**
   - 네임스페이스 간에는 빈 줄을 사용하여 구분하고, 선언 순서는 표준 네임스페이스(예: `System`)가 먼저 오도록 합니다.

   ```csharp
   using System;

   using MyNamespace1;
   using MyNamespace2;
   ```

1. **코드 주석:**
   - 코드 주석은 필요한 경우에만 사용하고, 코드의 의도를 설명하는 주석보다는 명확한 코드 작성을 선호합니다.

   ```csharp
   // 좋은 예: 
   // Calculates the sum of two numbers.
   int Sum(int a, int b)
   {
       return a + b;
   }

   // 나쁜 예:
   // This method adds two numbers.
   int AddNumbers(int num1, int num2)
   {
       return num1 + num2;
   }
   ```

1. **LINQ 쿼리 표현식:**
   - LINQ 쿼리 표현식이 여러 줄에 걸쳐 있다면 각 줄의 마지막에 연산자나 키워드를 두고, 첫 번째 줄은 쿼리의 시작 지점에서 시작합니다.

   ```csharp
   var query = from customer in customers
               where customer.City == "New York"
               orderby customer.LastName
               select customer;
   ```

1. **속성(Property):**
   - 속성은 간단하면서도 계산이 필요하지 않은 경우에는 자동 구현 속성을 사용할 수 있습니다.

   ```csharp
   public class MyClass
   {
       // 자동 구현 속성
       public int MyProperty { get; set; }
   }
   ```

1. **리터럴 값과 상수:**
   - 리터럴 값은 대문자를 사용하며, 의미 있는 이름을 가진 상수를 선호합니다.

   ```csharp
   const int MAX_COUNT = 100;
   const string ConnectionString = "your_connection_string";
   ```

1. **메서드 매개변수 정렬:**
    - 메서드 매개변수가 많을 경우 각 매개변수를 새 줄에 하나씩 나열하고, 정렬하여 가독성을 높입니다.

    ```csharp
    public void MethodWithManyParameters(
        int parameter1,
        string parameter2,
        double parameter3,
        bool parameter4)
    {
        // 메서드 내용
    }
    ```

1. **예외 처리:**
    - 예외 처리 시에는 구체적인 예외 클래스보다는 더 일반적인 `Exception` 클래스를 사용하는 것이 좋습니다.

    ```csharp
    try
    {
        // 예외가 발생할 수 있는 코드
    }
    catch (Exception ex)
    {
        Console.WriteLine($"An error occurred: {ex.Message}");
    }
    ```

1. **네이밍 컨벤션:**
    - 프로젝트에 맞는 네이밍 컨벤션을 선택하되, 각 요소의 명명에 일관성을 유지합니다. 예를 들어, 클래스, 메서드, 변수 등에 대한 명명에 일관된 규칙을 적용합니다.

    ```csharp
    // 클래스 명명: Pascal 케이스
    public class MyClassName
    {
        // 메서드 명명: Pascal 케이스
        public void MyMethodName()
        {
            // 변수 명명: Camel 케이스
            int myVariableName = 42;
        }
    }
    ```

1. **널 조건부 연산자:**
    - 널 조건부 연산자(`?.`)를 사용하여 null 체크를 간결하게 할 수 있습니다.

    ```csharp
    int? length = text?.Length;
    ```

1. **패턴 매칭:**
    - C# 9.0부터 패턴 매칭을 사용할 수 있으며, 이를 활용하여 코드를 더 간결하게 작성할 수 있습니다.

    ```csharp
    switch (myObject)
    {
        case MyClass myClass when myClass.MyProperty > 0:
            // 처리
            break;
        case null:
            // 처리
            break;
        default:
            // 처리
            break;
    }
    ```

1. **파일 및 클래스 구조:**
    - 하나의 파일에는 하나의 클래스만을 선언하는 것을 권장하며, 클래스 파일의 구조는 일반적으로 다음과 같습니다.
  
    ```csharp
    using System;

    namespace MyNamespace
    {
        // using 문 다음에 네임스페이스 선언
        public class MyClass
        {
            // 정적 필드
            private static int myStaticField;

            // 필드
            private int myField;

            // 속성
            public int MyProperty { get; set; }

            // 생성자
            public MyClass()
            {
                // 생성자 내용
            }

            // 메서드
            public void MyMethod()
            {
                // 메서드 내용
            }

            // 정적 메서드
            public static void MyStaticMethod()
            {
                // 정적 메서드 내용
            }

            // 중첩 클래스, 구조체, 열거형
            private class NestedClass
            {
                // 중첩 클래스 내용
            }
        }
    }
    ```

1. **`var` 키워드 사용:**
    - `var` 키워드는 컴파일러가 변수의 형식을 추론하도록 하는데, 사용 시에는 코드의 가독성을 향상시키기 위해 명시적인 형식 선언을 선호할 수 있습니다.

    ```csharp
    // 좋은 예: 명시적인 형식 선언
    List<string> names = new List<string>();

    // 나쁜 예: var 사용
    var names = new List<string>();
    ```

1. **멤버 순서:**
    - 클래스의 멤버 순서는 일반적으로 필드, 생성자, 속성, 메서드, 이벤트 등으로 정렬됩니다. 관련된 멤버끼리 묶어 놓는 것이 가독성을 높일 수 있습니다.

    ```csharp
    public class MyClass
    {
        // 필드

        // 생성자

        // 속성

        // 메서드

        // 이벤트
    }
    ```

1. **가급적 불필요한 형변환 피하기:**
    - 필요한 경우가 아니라면 불필요한 형변환은 피해야 합니다. 런타임 오버헤드를 줄이고 가독성을 높이기 위함입니다.

    ```csharp
    // 좋은 예: 필요한 경우에만 형변환
    if (myObject is MyClass myClass)
    {
        // myClass를 사용
    }

    // 나쁜 예: 불필요한 형변환
    MyClass myClass = (MyClass)myObject;
    ```

1. **대문자 약어 사용:**
    - 대문자 약어는 대문자로 유지되어야 합니다.

    ```csharp
    // 좋은 예: HTTP, URL
    string httpUrl;

    // 나쁜 예: http, url
    string httpurl;
    ```

2. **열거형(Enum) 형식:**
    - 열거형의 값은 대문자로 작성하며, 각 단어는 언더스코어로 구분합니다.

    ```csharp
    public enum DaysOfWeek
    {
        SUNDAY,
        MONDAY,
        TUESDAY,
        // ...
    }
    ```

1. **예외 메시지:**
    - 예외 메시지는 간결하고 명확해야 합니다. 사용자에게 유용하고 이해하기 쉬운 메시지를 제공하는 것이 좋습니다.

    ```csharp
    // 좋은 예: 파일을 찾을 수 없습니다.
    throw new FileNotFoundException("File not found.");

    // 나쁜 예: System.IO.FileNotFoundException: 파일을 찾을 수 없습니다.
    throw new FileNotFoundException("System.IO.FileNotFoundException: File not found.");
    ```

1. **리턴문과 브라켓:**
    - 메서드나 속성의 본문이 한 줄이라도, 명시적으로 중괄호 `{}`를 사용하는 것이 좋습니다.

    ```csharp
    // 좋은 예: 한 줄에 중괄호 사용
    public int GetCount() { return count; }

    // 나쁜 예: 중괄호 없이 사용
    public int GetCount() 
        => count;
    ```

1. **`foreach` 사용:**
    - 배열이나 컬렉션을 순회할 때는 `foreach`를 사용하는 것이 가독성이 좋습니다.

    ```csharp
    // 좋은 예
    foreach (var item in items)
    {
        // 처리
    }

    // 나쁜 예
    for (int i = 0; i < items.Length; i++)
    {
        var item = items[i];
        // 처리
    }
    ```

1. **문자열 합치기:**
    - 문자열을 합칠 때는 `StringBuilder`를 사용하거나, `string.Concat` 또는 문자열 보간(interpolation)을 사용하는 것이 좋습니다.

    ```csharp
    // 좋은 예
    string result = string.Concat(str1, str2, str3);

    // 나쁜 예
    string result = str1 + str2 + str3;
    ```
    
1. **속성 초기화:**
    - 속성 초기화 시에는 생성자보다는 객체 이니셜라이저를 사용하는 것이 가독성이 높습니다.

    ```csharp
    // 좋은 예
    MyClass myObject = new MyClass
    {
        Property1 = value1,
        Property2 = value2
    };

    // 나쁜 예
    MyClass myObject = new MyClass();
    myObject.Property1 = value1;
    myObject.Property2 = value2;
    ```

1. **`async` 및 `await`:**
    - `async` 및 `await`를 사용할 때 메서드 이름에 "Async"를 붙이는 것이 관례입니다.

    ```csharp
    // 좋은 예
    public async Task<int> CalculateAsync()
    {
        // 비동기 처리
    }

    // 나쁜 예
    public async Task<int> Calculate()
    {
        // 비동기 처리
    }
    ```

1. **구문 삼항 연산자:**
    - 간단한 조건식에는 구문 삼항 연산자를 사용하여 코드를 간결하게 유지할 수 있습니다.

    ```csharp
    // 좋은 예
    int result = (condition) ? trueValue : falseValue;

    // 나쁜 예
    int result;
    if (condition)
    {
        result = trueValue;
    }
    else
    {
        result = falseValue;
    }
    ```

이러한 규칙들은 코드의 일관성과 가독성을 높이기 위한 것이며, 프로젝트 팀이나 개발자 간에 합의된 스타일을 사용하는 것이 중요합니다. C# 코딩 스타일은 일관성 있게 유지하면서도 팀의 필요와 특성에 따라 적절히 조정될 수 있어야 합니다.