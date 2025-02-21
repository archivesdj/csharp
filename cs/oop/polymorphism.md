# 다형성

다형성(Polymorphism)은 객체 지향 프로그래밍(OOP)의 중요한 특성 중 하나로, 동일한 인터페이스나 메서드를 여러 형태로 구현할 수 있는 능력을 의미합니다. 다형성은 코드의 재사용성을 증가시키고, 프로그램을 더 유연하고 확장 가능하게 만듭니다.

### 다형성의 주요 개념:

1. **메서드 오버로딩(Method Overloading):**
   - 동일한 클래스 내에서 메서드의 이름은 같지만 매개변수의 형식, 개수, 순서 등이 다르게 정의되는 것을 메서드 오버로딩이라고 합니다.

   ```csharp
   public class Calculator
   {
       public int Add(int a, int b)
       {
           return a + b;
       }

       public double Add(double a, double b)
       {
           return a + b;
       }
   }
   ```

2. **메서드 오버라이딩(Method Overriding):**
   - 파생 클래스에서 기본 클래스에 이미 존재하는 메서드를 다시 정의하는 것을 메서드 오버라이딩이라고 합니다. 이를 통해 파생 클래스는 특정 메서드의 동작을 재정의할 수 있습니다.

   ```csharp
   public class Animal
   {
       public virtual void MakeSound()
       {
           Console.WriteLine("Animal makes a sound");
       }
   }

   public class Dog : Animal
   {
       public override void MakeSound()
       {
           Console.WriteLine("Dog barks");
       }
   }
   ```

3. **인터페이스 다형성(Interface Polymorphism):**
   - 인터페이스를 통해 다형성을 구현할 수 있습니다. 여러 클래스가 동일한 인터페이스를 구현하면, 해당 인터페이스를 사용하는 코드는 각 클래스의 인스턴스를 동일한 방식으로 다룰 수 있습니다.

   ```csharp
   public interface IShape
   {
       void Draw();
   }

   public class Circle : IShape
   {
       public void Draw()
       {
           Console.WriteLine("Drawing a circle");
       }
   }

   public class Square : IShape
   {
       public void Draw()
       {
           Console.WriteLine("Drawing a square");
       }
   }
   ```

4. **다형성을 활용한 코드:**
   - 메서드나 인터페이스를 통해 다양한 형태의 객체를 동일한 코드로 다룰 수 있습니다.

   ```csharp
   public class Program
   {
       static void DrawShape(IShape shape)
       {
           shape.Draw();
       }

       static void Main()
       {
           IShape circle = new Circle();
           IShape square = new Square();

           DrawShape(circle);  // Drawing a circle
           DrawShape(square);  // Drawing a square
       }
   }
   ```

다형성은 코드의 유연성을 증가시키며, 코드의 일관성을 유지하는 데 도움이 됩니다. 상속과 함께 사용되어 기본 클래스 타입으로 여러 파생 클래스의 인스턴스를 다룰 수 있게 하며, 인터페이스를 통해 동일한 인터페이스를 구현하는 여러 클래스의 객체를 통일된 방식으로 처리할 수 있습니다.

## 사용 시 유의사항

다형성을 사용할 때에는 몇 가지 주의사항이 있습니다. 이를 고려하여 적절하게 다형성을 활용하는 것이 중요합니다.

1. **메서드 오버라이딩 시 `base` 키워드 사용:**
   - 메서드 오버라이딩을 할 때에는 `base` 키워드를 사용하여 기본 클래스의 메서드를 호출할 수 있습니다. 이를 통해 기본 클래스의 기능을 유지하면서 추가적인 동작을 구현할 수 있습니다.

   ```csharp
   public class Animal
   {
       public virtual void MakeSound()
       {
           Console.WriteLine("Animal makes a sound");
       }
   }

   public class Dog : Animal
   {
       public override void MakeSound()
       {
           base.MakeSound();  // 기본 클래스의 메서드 호출
           Console.WriteLine("Dog barks");
       }
   }
   ```

2. **다운캐스팅 시 `as` 또는 `is` 사용:**
   - 다형성을 사용할 때, 부모 클래스 타입으로 선언된 변수를 자식 클래스 타입으로 다운캐스팅할 때 `as` 또는 `is` 연산자를 사용하는 것이 안전합니다. 명시적인 캐스팅 연산자(`(자식클래스)부모클래스`)보다 안전하게 다운캐스팅할 수 있습니다.

   ```csharp
   Animal animal = new Dog();
   
   // 안전한 다운캐스팅
   Dog dog = animal as Dog;
   if (dog != null)
   {
       dog.MakeSound();
   }
   ```

3. **`virtual` 및 `override` 키워드 사용 주의:**
   - `virtual` 키워드는 메서드가 오버라이딩될 수 있음을 나타내고, `override` 키워드는 해당 메서드가 기본 클래스에서 정의된 것을 오버라이딩함을 나타냅니다. 주의해서 사용해야 하며, 필요한 경우에만 사용해야 합니다.

4. **인터페이스 다형성에서 명시적 구현 주의:**
   - 인터페이스 다형성을 사용할 때에는 클래스에서 인터페이스 메서드를 명시적으로 구현할 경우, 해당 메서드를 명시적으로 호출할 때에는 해당 인터페이스 타입으로 캐스팅하여 사용해야 합니다.

   ```csharp
   public interface IDrawable
   {
       void Draw();
   }

   public class Circle : IDrawable
   {
       // 명시적 구현
       void IDrawable.Draw()
       {
           Console.WriteLine("Drawing a circle");
       }
   }

   class Program
   {
       static void Main()
       {
           Circle circle = new Circle();
           // 명시적 구현된 메서드 호출
           ((IDrawable)circle).Draw();
       }
   }
   ```

5. **`sealed` 키워드 사용:**
   - 특정 클래스를 상속 불가능하도록 하려면 `sealed` 키워드를 사용할 수 있습니다. 이는 특정 클래스의 다형성을 제한하고, 불필요한 클래스의 확장을 방지할 수 있습니다.

   ```csharp
   public sealed class SealedClass
   {
       // 클래스 내용
   }
   ```

다형성을 사용할 때는 이러한 주의사항을 고려하여 안전하게 코드를 작성해야 합니다. 특히 타입 캐스팅이나 메서드 오버라이딩 등에서 발생할 수 있는 예외 상황에 대비하여 프로그래밍하는 것이 중요합니다.