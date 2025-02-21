# 제네릭과 특성

C#에서 Generic 형식에 Attribute를 적용하는 방법은 일반적인 형식에 Attribute를 적용하는 방법과 유사합니다. Generic 클래스 또는 메서드에 Attribute를 적용하려면 제네릭 형식에 대한 Attribute를 만들고 사용해야 합니다. 아래는 Generic 클래스에 Attribute를 적용하는 예제 코드입니다:

```csharp
using System;

// Generic 클래스에 적용할 Attribute 정의
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method)]
public class MyGenericAttribute : Attribute
{
    public string Description { get; }

    public MyGenericAttribute(string description)
    {
        Description = description;
    }
}

// Generic 클래스 정의
[MyGeneric("This is a generic class.")]
public class GenericClass<T>
{
    // Generic 메서드에 적용할 Attribute 정의
    [MyGeneric("This is a generic method.")]
    public void GenericMethod<U>(U value)
    {
        Console.WriteLine($"Generic Method Executed with value: {value}");
    }
}

class Program
{
    static void Main()
    {
        // Generic 클래스의 Attribute 읽기
        Type genericType = typeof(GenericClass<>);
        object[] classAttributes = genericType.GetCustomAttributes(typeof(MyGenericAttribute), true);
        foreach (MyGenericAttribute attribute in classAttributes)
        {
            Console.WriteLine($"Class Attribute: {attribute.Description}");
        }

        // Generic 메서드의 Attribute 읽기
        Type genericMethodType = typeof(GenericClass<>).GetMethod("GenericMethod");
        object[] methodAttributes = genericMethodType.GetCustomAttributes(typeof(MyGenericAttribute), true);
        foreach (MyGenericAttribute attribute in methodAttributes)
        {
            Console.WriteLine($"Method Attribute: {attribute.Description}");
        }
    }
}
```

이 예제에서는 `MyGenericAttribute`라는 사용자 정의 Attribute를 정의하고, `GenericClass<T>` 클래스에 적용했습니다. 또한 `GenericMethod<U>` 메서드에도 동일한 Attribute를 적용했습니다. 이후 `Reflection`을 사용하여 Generic 클래스와 메서드에서 Attribute를 읽어오는 방법을 보여줍니다.

주의: 제네릭 형식의 일부 구성원에 대해 Attribute를 적용할 때는 해당 구성원이 어떤 형식에 대해 정확히 사용될지 명시적으로 지정해야 합니다. 위의 예제에서는 `typeof(GenericClass<>)`와 `typeof(GenericClass<>).GetMethod("GenericMethod")`와 같이 `<>`를 사용하여 일반적인 제네릭 형식을 나타내었습니다.