# 리플렉션 및 특성

Reflection과 Attribute는 C#에서 메타프로그래밍을 지원하는 기능입니다.

1. **Reflection (리플렉션):**
   - Reflection은 실행 중에 코드를 검사하고 조사하는 기능을 의미합니다. 즉, 프로그램이 실행 중일 때 해당 프로그램의 형식(Type)이나 객체 등의 정보를 가져오거나 수정할 수 있는 기능을 제공합니다.

   - Reflection을 사용하면 어셈블리, 형식, 메서드, 속성, 필드 등을 동적으로 검사하고 조작할 수 있습니다.

   - 예를 들어, 특정 형식의 모든 메서드를 가져오거나, 메서드의 매개변수 형식을 확인하거나, 동적으로 인스턴스를 생성하는 등의 작업을 할 수 있습니다.

   - Reflection은 일반적으로 디버깅, 플러그인 시스템, 코드 분석 도구 등에서 활용됩니다.

2. **Attribute (어트리뷰트):**
   - Attribute는 코드에 부가적인 정보를 제공하는 역할을 합니다. 코드에 메타데이터를 추가하여 컴파일러나 런타임에 특정한 동작이나 정보를 전달할 수 있습니다.

   - C#에서는 `[AttributeName]` 형태로 사용되며, 주로 클래스, 메서드, 속성 등에 적용됩니다.

   - Attribute를 사용하면 코드에 대한 정보를 확장하고, 외부 라이브러리나 프레임워크에서 추가적인 작업을 수행할 수 있습니다.

   - 예를 들어, `[Serializable]` 어트리뷰트를 클래스에 적용하면 해당 클래스의 객체가 직렬화될 수 있도록 하는 등의 기능을 부여할 수 있습니다.

아래는 Reflection과 Attribute를 함께 사용하는 간단한 예제입니다:

```csharp
using System;

[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method)]
public class CustomAttribute : Attribute
{
    public string Description { get; }

    public CustomAttribute(string description)
    {
        Description = description;
    }
}

[Custom("This is a sample class.")]
class SampleClass
{
    [Custom("This is a sample method.")]
    public void SampleMethod()
    {
        Console.WriteLine("Sample Method Executed.");
    }
}

class Program
{
    static void Main()
    {
        Type type = typeof(SampleClass);

        // 클래스에 적용된 어트리뷰트 읽기
        var classAttributes = type.GetCustomAttributes(typeof(CustomAttribute), true);
        foreach (CustomAttribute attribute in classAttributes)
        {
            Console.WriteLine($"Class Attribute: {attribute.Description}");
        }

        // 메서드에 적용된 어트리뷰트 읽기
        var methodInfo = type.GetMethod("SampleMethod");
        var methodAttributes = methodInfo.GetCustomAttributes(typeof(CustomAttribute), true);
        foreach (CustomAttribute attribute in methodAttributes)
        {
            Console.WriteLine($"Method Attribute: {attribute.Description}");
        }
    }
}
```

이 예제에서는 `CustomAttribute`라는 사용자 정의 어트리뷰트를 정의하고, 이를 클래스와 메서드에 적용하여 Reflection을 사용해 어트리뷰트의 정보를 읽어오는 방법을 보여줍니다.