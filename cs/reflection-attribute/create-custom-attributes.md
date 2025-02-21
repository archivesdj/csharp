# 사용자 지정 특성 만들기

C#에서 Custom Attribute를 만들기 위해서는 `Attribute` 클래스를 상속하고, 필요한 속성과 생성자를 정의해야 합니다. Custom Attribute를 만드는 과정은 다음과 같습니다:

1. **`Attribute` 클래스 상속:**
   - Custom Attribute를 만들기 위해서는 `Attribute` 클래스를 상속해야 합니다.

2. **생성자와 속성 정의:**
   - Custom Attribute에 필요한 속성을 정의하고, 생성자를 통해 초기화합니다.

3. **AttributeTargets 정의:**
   - 어떤 대상(클래스, 메서드, 속성 등)에 Attribute를 적용할 것인지를 `AttributeTargets` 열거형으로 지정합니다.

4. **유효성 검사 (선택 사항):**
   - 필요에 따라 Attribute가 특정 조건을 만족하는지 검사하는 코드를 추가할 수 있습니다.

아래는 Custom Attribute를 만드는 간단한 예제 코드입니다. 이 예제에서는 `AuthorAttribute`라는 Custom Attribute를 만들어 클래스에 적용하는 방법을 보여줍니다:

```csharp
using System;

[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, AllowMultiple = true)]
public class AuthorAttribute : Attribute
{
    public string AuthorName { get; }

    public string Date { get; }

    public AuthorAttribute(string authorName, string date)
    {
        AuthorName = authorName;
        Date = date;
    }
}

[Author("John Doe", "2022-01-01")]
[Author("Jane Smith", "2022-02-15")]
class SampleClass
{
    [Author("John Doe", "2022-01-15")]
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

        // 클래스에 적용된 AuthorAttribute 읽기
        var classAttributes = type.GetCustomAttributes(typeof(AuthorAttribute), true);
        foreach (AuthorAttribute attribute in classAttributes)
        {
            Console.WriteLine($"Class Author: {attribute.AuthorName}, Date: {attribute.Date}");
        }

        // 메서드에 적용된 AuthorAttribute 읽기
        var methodInfo = type.GetMethod("SampleMethod");
        var methodAttributes = methodInfo.GetCustomAttributes(typeof(AuthorAttribute), true);
        foreach (AuthorAttribute attribute in methodAttributes)
        {
            Console.WriteLine($"Method Author: {attribute.AuthorName}, Date: {attribute.Date}");
        }
    }
}
```

위 코드에서 `AuthorAttribute`는 `Attribute` 클래스를 상속하며, `AuthorName`과 `Date` 두 개의 속성을 가지고 있습니다. `AttributeUsage` 특성을 사용하여 어디에 적용할 수 있는지 정의하고, `AllowMultiple` 속성을 통해 여러 번 적용할 수 있도록 허용했습니다. 클래스와 메서드에 이 Attribute를 적용하고, Reflection을 사용하여 읽어오는 방법을 보여줍니다.