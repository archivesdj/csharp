# 상속

상속(Inheritance)은 객체 지향 프로그래밍(OOP)에서 사용되는 중요한 개념으로, 기존의 클래스에서 정의된 특성(속성과 메서드)을 새로운 클래스에서 다시 사용하거나 확장하는 것을 의미합니다. 이를 통해 코드의 재사용성을 높이고, 프로그램의 유지보수성과 확장성을 개선할 수 있습니다.

### 상속의 주요 특징:

1. **기본 클래스(Base Class)와 파생 클래스(Derived Class):**
   - 상속에서 기본 클래스는 부모 클래스 또는 상위 클래스로 불리며, 파생 클래스는 자식 클래스 또는 하위 클래스로 불립니다. 기본 클래스에서 정의된 특성들은 파생 클래스에서 상속됩니다.

   ```csharp
   // 기본 클래스 (부모 클래스)
   public class Animal
   {
       public void Eat()
       {
           Console.WriteLine("Eating...");
       }
   }

   // 파생 클래스 (자식 클래스)
   public class Dog : Animal
   {
       public void Bark()
       {
           Console.WriteLine("Barking...");
       }
   }
   ```

2. **재사용성과 확장성:**
   - 기본 클래스에서 정의된 속성과 메서드를 파생 클래스에서 재사용할 수 있습니다. 이로 인해 코드의 재사용성이 증가하며, 새로운 기능을 추가하거나 기존 기능을 수정하여 확장할 수 있습니다.

3. **메서드 오버라이딩(Method Overriding):**
   - 파생 클래스에서 기본 클래스에 이미 존재하는 메서드를 다시 정의하는 것을 메서드 오버라이딩이라고 합니다. 이를 통해 파생 클래스는 특정 메서드의 동작을 재정의할 수 있습니다.

   ```csharp
   public class Cat : Animal
   {
       public override void Eat()
       {
           Console.WriteLine("Cat is eating...");
       }
   }
   ```

4. **다중 상속(Multiple Inheritance) 불가:**
   - C#에서는 하나의 클래스가 여러 개의 클래스로부터 동시에 상속받는 다중 상속을 지원하지 않습니다. 하지만 인터페이스를 통한 다중 상속을 지원합니다.

### 상속의 사용 예제:

```csharp
// 기본 클래스
public class Vehicle
{
    public string Brand { get; set; }
    public int Year { get; set; }

    public void Start()
    {
        Console.WriteLine("Vehicle started...");
    }
}

// 파생 클래스
public class Car : Vehicle
{
    public int NumDoors { get; set; }

    public void Accelerate()
    {
        Console.WriteLine("Car is accelerating...");
    }
}

class Program
{
    static void Main()
    {
        // 파생 클래스의 인스턴스 생성
        Car myCar = new Car();
        myCar.Brand = "Toyota";
        myCar.Year = 2022;
        myCar.NumDoors = 4;

        // 기본 클래스의 메서드 호출
        myCar.Start();

        // 파생 클래스의 메서드 호출
        myCar.Accelerate();
    }
}
```

상속은 객체 지향 프로그래밍에서 코드의 재사용성과 가독성을 높이는 중요한 도구로 사용됩니다. 코드를 더 추상화하고 유연하게 만들어 새로운 기능을 쉽게 추가하거나 수정할 수 있도록 도와줍니다.

## 사용 시 유의사항

상속을 사용할 때는 몇 가지 주의사항을 고려해야 합니다. 이러한 유의사항을 알고 적절하게 상속을 활용하면 코드의 구조를 더욱 확장 가능하고 유지보수가 용이한 형태로 설계할 수 있습니다.

1. **"is-a" 관계를 확인:**
   - 상속은 "is-a" 관계를 나타내야 합니다. 즉, 파생 클래스는 기본 클래스의 일종이어야 합니다. 만약 "is-a" 관계가 성립되지 않는다면 상속보다는 다른 방법을 고려해야 합니다.

   ```csharp
   // 좋은 예: Dog은 Animal의 일종이다.
   public class Dog : Animal

   // 나쁜 예: Car은 Engine의 일종이 아니다.
   public class Car : Engine
   ```

2. **클래스 계층 구조 설계:**
   - 클래스의 계층 구조를 잘 설계해야 합니다. 너무 깊거나 복잡한 계층 구조는 이해하기 어렵고 유지보수가 어렵게 만들 수 있습니다. 필요한 경우에만 상속을 사용하고, 인터페이스를 활용하여 유연한 설계를 고려해야 합니다.

3. **가상 메서드의 적절한 활용:**
   - 가상 메서드를 사용할 때에는 적절하게 사용해야 합니다. 부모 클래스에서 기본 동작을 제공하고, 필요한 경우 파생 클래스에서 가상 메서드를 오버라이딩하여 특정 동작을 변경할 수 있습니다.

   ```csharp
   public class Animal
   {
       public virtual void Speak()
       {
           Console.WriteLine("Animal speaks");
       }
   }

   public class Dog : Animal
   {
       public override void Speak()
       {
           Console.WriteLine("Dog barks");
       }
   }
   ```

4. **상속의 한계를 고려:**
   - 클래스의 기능을 확장하기 위해 상속을 사용할 때, 어떤 기능을 추가하고 어떤 기능을 재정의해야 하는지 신중히 결정해야 합니다. 필요하지 않은 메서드를 오버라이딩하는 등 불필요한 코드를 생성하지 않도록 주의해야 합니다.

5. **다중 상속의 제한:**
   - C#에서는 클래스의 다중 상속을 지원하지 않습니다. 하나의 클래스가 여러 개의 클래스로부터 상속받지 못하게 하기 위해 `sealed` 키워드를 사용할 수 있습니다.

   ```csharp
   public sealed class FinalClass : BaseClass
   {
       // 클래스 내용
   }
   ```

6. **캡슐화와 응집도:**
   - 캡슐화를 적절히 활용하고, 클래스 내의 멤버 변수와 메서드가 어떤 기능을 수행하는지 명확하게 구분해야 합니다. 높은 응집도와 낮은 결합도를 유지하여 코드의 가독성과 유지보수성을 높일 수 있습니다.

상속을 적절히 사용하면 코드를 구조화하고 재사용성을 높일 수 있지만, 위의 주의사항을 고려하지 않으면 코드의 복잡성이 증가할 수 있습니다. 상황에 맞게 상속과 다른 객체 지향 기법들을 함께 사용하여 유연하고 확장 가능한 코드를 작성해야 합니다.