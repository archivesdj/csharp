# 리플렉션

Reflection은 프로그램이 실행 중에 자기 자신의 형식(Type) 및 멤버 정보를 동적으로 검사하고 조작하는 프로세스를 나타냅니다. C#에서 Reflection은 `System.Reflection` 네임스페이스를 통해 제공됩니다.

Reflection을 사용하면 다음과 같은 작업을 수행할 수 있습니다:

1. **형식 정보 가져오기 (Type Information Retrieval):**
   - 실행 중에 현재 어셈블리에 포함된 형식(Type)의 정보를 가져올 수 있습니다. 이는 클래스, 인터페이스, 열거형 등의 형식에 대한 정보를 포함합니다.

2. **인스턴스 생성 및 메서드 호출 (Instance Creation and Method Invocation):**
   - Reflection을 사용하여 형식의 인스턴스를 동적으로 생성하고, 메서드를 호출할 수 있습니다.

3. **속성 및 필드 값 읽기 및 쓰기 (Property and Field Access):**
   - Reflection을 사용하여 형식의 속성과 필드의 값을 동적으로 읽거나 쓸 수 있습니다.

4. **어셈블리 및 모듈 정보 검색 (Assembly and Module Information Retrieval):**
   - Reflection을 사용하여 어셈블리와 모듈에 대한 정보를 가져올 수 있습니다.

5. **Attribute 읽기 (Attribute Reading):**
   - Reflection을 사용하여 형식, 멤버 또는 어셈블리에 적용된 Attribute를 읽을 수 있습니다.

6. **동적 코드 생성 (Dynamic Code Generation):**
   - Reflection.Emit 네임스페이스를 사용하여 실행 중에 새로운 형식을 동적으로 생성하고 컴파일할 수 있습니다.

아래는 Reflection을 사용하는 간단한 예제 코드입니다:

```csharp
using System;
using System.Reflection;

class Program
{
    static void Main()
    {
        // 형식 정보 가져오기
        Type type = typeof(SampleClass);

        // 속성 정보 가져오기
        PropertyInfo propertyInfo = type.GetProperty("SampleProperty");

        // 인스턴스 생성
        object instance = Activator.CreateInstance(type);

        // 속성 값 읽기
        object propertyValue = propertyInfo.GetValue(instance);

        // 메서드 정보 가져오기
        MethodInfo methodInfo = type.GetMethod("SampleMethod");

        // 메서드 호출
        methodInfo.Invoke(instance, null);
    }
}

class SampleClass
{
    public string SampleProperty { get; set; }

    public void SampleMethod()
    {
        Console.WriteLine("Sample Method Called.");
    }
}
```

이 예제에서는 Reflection을 사용하여 `SampleClass`의 형식 정보를 가져오고, 속성과 메서드의 정보를 확인하며, 인스턴스를 생성하고 속성 값을 읽어오고, 메서드를 동적으로 호출하는 등의 작업을 수행합니다.

## 리플렉션 주 활용처

Reflection은 주로 다음과 같은 상황에서 활용됩니다:

1. **플러그인 시스템 (Plugin Systems):**
   - Reflection을 사용하여 특정 인터페이스를 구현하는 플러그인을 동적으로 검색하고 로드할 수 있습니다. 이를 통해 애플리케이션의 확장성을 높일 수 있습니다.

   ```csharp
   // 예제: 인터페이스를 구현하는 플러그인 로드
   Type interfaceType = typeof(IPlugin);
   IEnumerable<Type> pluginTypes = Assembly.GetExecutingAssembly().GetTypes()
                                       .Where(t => interfaceType.IsAssignableFrom(t) && !t.IsInterface);

   foreach (Type pluginType in pluginTypes)
   {
       IPlugin plugin = (IPlugin)Activator.CreateInstance(pluginType);
       plugin.Execute();
   }
   ```

2. **속성 변경 및 메타데이터 처리:**
   - Reflection을 사용하여 속성(Attribute)을 읽어오거나 변경할 수 있습니다. 이를 통해 코드에 부가적인 메타데이터를 추가하고 동적으로 처리할 수 있습니다.

   ```csharp
   // 예제: 특정 Attribute를 가진 속성 찾기
   Type type = typeof(MyClass);
   PropertyInfo[] properties = type.GetProperties();

   foreach (PropertyInfo property in properties)
   {
       if (property.GetCustomAttribute(typeof(MyAttribute)) != null)
       {
           // 속성에 특정 Attribute가 있는 경우 처리
           // ...
       }
   }
   ```

3. **동적 코드 생성 (Dynamic Code Generation):**
   - Reflection.Emit을 사용하여 실행 중에 새로운 형식을 동적으로 생성하고 컴파일할 수 있습니다. 이를 통해 코드를 생성하거나 변경할 수 있습니다.

   ```csharp
   // 예제: 동적으로 메서드를 생성하여 실행
   AssemblyName assemblyName = new AssemblyName("DynamicAssembly");
   AssemblyBuilder assemblyBuilder = AssemblyBuilder.DefineDynamicAssembly(assemblyName, AssemblyBuilderAccess.Run);
   ModuleBuilder moduleBuilder = assemblyBuilder.DefineDynamicModule("DynamicModule");
   TypeBuilder typeBuilder = moduleBuilder.DefineType("DynamicType");

   MethodBuilder methodBuilder = typeBuilder.DefineMethod("DynamicMethod", MethodAttributes.Public | MethodAttributes.Static);
   ILGenerator ilGenerator = methodBuilder.GetILGenerator();
   ilGenerator.Emit(OpCodes.Ldstr, "Dynamic Method Executed");
   ilGenerator.Emit(OpCodes.Call, typeof(Console).GetMethod("WriteLine", new[] { typeof(string) }));
   ilGenerator.Emit(OpCodes.Ret);

   Type dynamicType = typeBuilder.CreateType();
   MethodInfo dynamicMethod = dynamicType.GetMethod("DynamicMethod");
   dynamicMethod.Invoke(null, null);
   ```

4. **단위 테스트 및 디버깅 (Unit Testing and Debugging):**
   - Reflection은 단위 테스트 프레임워크나 디버깅 도구에서 사용되어 특정 조건을 만족하는 테스트 메서드를 찾거나, 객체의 상태를 동적으로 검사하고 수정하는 데 활용될 수 있습니다.

   ```csharp
   // 예제: 특정 조건을 만족하는 테스트 메서드 찾기
   Type testClassType = typeof(TestClass);
   MethodInfo[] methods = testClassType.GetMethods();

   foreach (MethodInfo method in methods)
   {
       if (method.GetCustomAttributes(typeof(TestAttribute), true).Length > 0)
       {
           // 특정 Attribute를 가진 테스트 메서드 찾기
           // ...
       }
   }
   ```

이러한 예제들은 Reflection을 통해 프로그램의 동적인 특성을 활용할 수 있는 것을 보여줍니다. 그러나 Reflection은 성능 오버헤드가 있고, 컴파일 타임의 안전성을 잃을 수 있기 때문에 사용 시 주의가 필요합니다.