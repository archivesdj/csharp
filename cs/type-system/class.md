# 클래스

C#에서 클래스는 객체 지향 프로그래밍의 기본 구성 요소 중 하나로, 데이터와 해당 데이터를 처리하는 메서드를 포함하는 사용자 정의 데이터 형식을 정의하는데 사용됩니다. 클래스는 특정 형식의 객체를 생성하는 템플릿으로, 이를 통해 코드를 모듈화하고 재사용성을 높일 수 있습니다.

## 기본 구조

클래스를 정의하는 기본 구조는 다음과 같습니다:

```csharp
// 클래스 정의
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
```

위 코드에서 `MyClass`는 클래스의 이름이며, 이 클래스는 `myField`라는 멤버 변수와 `MyMethod`라는 메서드를 포함하고 있습니다. 클래스는 다음과 같은 요소로 구성됩니다:

1. **멤버 변수 (필드):** 클래스 내부에 선언된 변수로, 클래스의 상태를 나타냅니다. 멤버 변수는 클래스의 인스턴스마다 별도의 메모리 공간에 할당되며, 일반적으로 `private`, `public` 등의 접근 제한자로 접근을 제어할 수 있습니다.

2. **생성자(Constructor):** 클래스의 인스턴스를 초기화하는 특별한 메서드입니다. 클래스의 이름과 동일하며, 객체가 생성될 때 자동으로 호출됩니다.

3. **메서드(Method):** 특정 작업을 수행하는 함수로, 클래스의 행동을 정의합니다. 메서드는 클래스의 인스턴스 또는 클래스 자체에 속할 수 있습니다.

4. **속성(Property):** 클래스의 필드에 대한 접근자(getter, setter)를 캡슐화한 것으로, 프로퍼티를 통해 값을 읽거나 쓸 수 있습니다.

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

5. **인스턴스 및 정적 멤버:** 클래스는 인스턴스 멤버와 정적 멤버를 가질 수 있습니다. 인스턴스 멤버는 클래스의 각 인스턴스에 속하며, 정적 멤버는 클래스 자체에 속합니다.

    ```csharp
    class MyClass
    {
        // 인스턴스 멤버
        private int instanceField;

        // 정적 멤버
        private static int staticField;

        // ...
    }
    ```

클래스는 객체 지향 프로그래밍의 핵심 개념 중 하나로, 코드의 모듈화와 재사용성을 높이는데 사용됩니다. 객체를 생성하여 클래스의 인스턴스를 만들고, 이를 통해 클래스에 정의된 멤버에 접근하고 메서드를 호출할 수 있습니다.

## 상속

클래스 상속은 객체 지향 프로그래밍에서 중요한 개념 중 하나로, 한 클래스가 다른 클래스의 속성과 동작을 물려받아 확장하는 것을 의미합니다. 이를 통해 코드의 재사용성이 증가하고, 계층 구조를 통해 일반적인 특성을 가진 클래스를 정의하여 특정 클래스의 새로운 버전을 만들 수 있습니다.

C#에서 클래스 상속은 다음과 같은 형태를 가집니다:

```csharp
class BaseClass
{
    // 기본 클래스의 멤버
}

class DerivedClass : BaseClass
{
    // 파생 클래스의 멤버
}
```

위 코드에서 `DerivedClass`는 `BaseClass`로부터 상속을 받고 있습니다. 이로 인해 `DerivedClass`는 `BaseClass`의 모든 멤버(필드, 메서드, 속성 등)를 상속받게 됩니다.

클래스 상속의 주요 특징과 개념은 다음과 같습니다:

1. **기본 클래스(Base Class):** 상속을 제공하는 클래스를 기본 클래스 또는 부모 클래스라고 합니다. `BaseClass`는 상속을 통해 기능을 제공하고 확장될 수 있는 기반 역할을 합니다.

    ```csharp
    class BaseClass
    {
        public void BaseMethod()
        {
            Console.WriteLine("BaseClass method called");
        }
    }
    ```

2. **파생 클래스(Derived Class):** 상속을 받는 클래스를 파생 클래스 또는 자식 클래스라고 합니다. `DerivedClass`는 기본 클래스로부터 멤버를 상속받고, 필요에 따라 새로운 멤버를 추가하거나 기존 멤버를 재정의할 수 있습니다.

    ```csharp
    class DerivedClass : BaseClass
    {
        public void DerivedMethod()
        {
            Console.WriteLine("DerivedClass method called");
        }
    }
    ```

3. **protected 접근 제한자:** 기본 클래스의 `protected` 멤버는 파생 클래스에서 접근할 수 있습니다. 이를 통해 기본 클래스의 일부 멤버를 파생 클래스에서만 사용하도록 할 수 있습니다.

    ```csharp
    class BaseClass
    {
        protected int protectedField;

        protected void ProtectedMethod()
        {
            // ...
        }
    }

    class DerivedClass : BaseClass
    {
        public void UseProtectedMember()
        {
            protectedField = 42;      // 접근 가능
            ProtectedMethod();        // 접근 가능
        }
    }
    ```

4. **메서드 오버라이딩(Method Overriding):** 파생 클래스에서 기본 클래스의 메서드를 재정의할 수 있습니다. 이를 통해 파생 클래스에서 특정 메서드의 동작을 변경할 수 있습니다.

    ```csharp
    class BaseClass
    {
        public virtual void VirtualMethod()
        {
            Console.WriteLine("BaseClass virtual method called");
        }
    }

    class DerivedClass : BaseClass
    {
        public override void VirtualMethod()
        {
            Console.WriteLine("DerivedClass virtual method called");
        }
    }
    ```

5. **다중 상속 불가능:** C#에서는 한 클래스가 여러 개의 클래스로부터 상속받는 다중 상속을 지원하지 않습니다. 하나의 클래스는 하나의 직접적인 부모 클래스만 가질 수 있습니다.

상속을 사용하면 코드의 재사용성을 높이고 계층 구조를 통해 프로그램의 설계를 더 유연하게 할 수 있습니다. 하지만 무분별한 상속 사용은 코드의 복잡성을 증가시키고 유지보수를 어렵게 할 수 있으므로 신중하게 사용해야 합니다.

## 추상 vs. 가상

`abstract`와 `virtual`은 모두 C#에서 다형성과 상속을 지원하기 위한 키워드로 사용되지만, 각각 다른 목적과 특징을 가지고 있습니다.

1. **abstract (추상):**
   - `abstract` 키워드는 추상 클래스와 추상 메서드를 정의하는 데 사용됩니다.
   - 추상 클래스는 인스턴스를 생성할 수 없으며, 상속을 통해 파생 클래스에서 구현되어야 합니다.
   - 추상 메서드는 선언만 되어 있고 본체가 없으며, 파생 클래스에서 반드시 구현되어야 합니다.
   - 추상 클래스 내에는 구현이 있는 메서드와 필드도 포함될 수 있습니다.
   - 다중 상속을 지원하지 않는 C#에서, 여러 추상 클래스로부터 상속받을 수 있습니다.

   ```csharp
   abstract class Shape
   {
       public abstract void Draw(); // 추상 메서드
   }

   class Circle : Shape
   {
       public override void Draw()
       {
           // 구현
       }
   }
   ```

2. **virtual (가상):**
   - `virtual` 키워드는 가상 메서드를 정의하는 데 사용됩니다.
   - 가상 메서드는 기본 구현을 가지고 있지만, 파생 클래스에서 필요에 따라 재정의(override)될 수 있습니다.
   - 가상 메서드는 인스턴스를 통해 호출될 때 실행 시간에 실제 객체의 형식에 따라 동적으로 결정됩니다.

   ```csharp
   class Animal
   {
       public virtual void Speak()
       {
           Console.WriteLine("Animal speaks");
       }
   }

   class Dog : Animal
   {
       public override void Speak()
       {
           Console.WriteLine("Dog barks");
       }
   }
   ```

   가상 메서드의 경우 기본 구현이 있지만, 필요에 따라 파생 클래스에서 재정의할 수 있습니다.

**요약:**
- `abstract`은 추상 클래스와 추상 메서드를 정의하는 데 사용되며, 인스턴스를 생성할 수 없고 반드시 파생 클래스에서 구현해야 합니다.
- `virtual`은 가상 메서드를 정의하는 데 사용되며, 기본 구현을 가지고 있고 파생 클래스에서 필요에 따라 재정의될 수 있습니다.
- 추상 클래스는 여러 개의 추상 메서드와 구현이 있는 메서드를 가질 수 있으며, 다중 상속을 지원합니다.
- 가상 메서드는 기본 구현을 가지고 있을 수 있으며, 동적 디스패치를 통해 실행 시간에 메서드가 결정됩니다.
