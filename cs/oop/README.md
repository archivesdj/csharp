# 객체지향 프로그래밍

C#은 객체지향 프로그래밍(OOP, Object Oriented Programming) 언어로서, OOP의 핵심 개념과 원칙을 지원합니다. 객체지향 프로그래밍은 소프트웨어를 객체(object) 단위로 구성하고, 객체들 간의 상호 작용을 통해 프로그램을 구현하는 프로그래밍 패러다임 중 하나입니다.

### 객체지향 프로그래밍의 주요 특징:

1. **클래스와 객체:**
   - C#에서 클래스(class)는 객체를 정의하는 틀이며, 객체(object)는 클래스의 인스턴스입니다. 클래스는 속성(멤버 변수)과 메서드(함수)로 구성되며, 객체는 클래스에서 정의된 속성과 메서드를 사용할 수 있습니다.

   ```csharp
   // 클래스 정의
   public class Car
   {
       // 속성(멤버 변수)
       public string Model { get; set; }

       // 메서드(함수)
       public void StartEngine()
       {
           Console.WriteLine("Engine started!");
       }
   }

   // 객체 생성
   Car myCar = new Car();
   myCar.Model = "Toyota";
   myCar.StartEngine();
   ```

2. **캡슐화(Encapsulation):**
   - 캡슐화는 관련된 데이터와 메서드를 하나의 단위로 묶고, 외부에서의 직접적인 접근을 제한하는 개념입니다. C#에서는 클래스를 사용하여 캡슐화를 구현합니다.

3. **상속(Inheritance):**
   - 상속은 기존 클래스의 특성을 그대로 유지하면서 새로운 클래스를 만들 수 있는 개념입니다. 상속을 통해 코드의 재사용성을 높일 수 있습니다.

   ```csharp
   // 기존 클래스
   public class Animal
   {
       public void Eat()
       {
           Console.WriteLine("Eating...");
       }
   }

   // 새로운 클래스가 기존 클래스 상속
   public class Dog : Animal
   {
       public void Bark()
       {
           Console.WriteLine("Barking...");
       }
   }

   // 사용 예제
   Dog myDog = new Dog();
   myDog.Eat();   // 기존 클래스의 메서드 호출
   myDog.Bark();  // 새로운 클래스의 메서드 호출
   ```

4. **다형성(Polymorphism):**
   - 다형성은 하나의 인터페이스나 메서드가 여러 형태로 구현될 수 있음을 의미합니다. C#에서는 메서드 오버로딩, 인터페이스, 가상 메서드 등을 활용하여 다형성을 구현합니다.

   ```csharp
   public class Shape
   {
       public virtual void Draw()
       {
           Console.WriteLine("Drawing a shape");
       }
   }

   public class Circle : Shape
   {
       public override void Draw()
       {
           Console.WriteLine("Drawing a circle");
       }
   }

   // 사용 예제
   Shape shape = new Circle();  // 다형성 활용
   shape.Draw();  // Circle 클래스의 Draw 메서드가 호출됨
   ```

객체지향 프로그래밍은 코드의 재사용성, 유지보수성, 확장성을 높이는 등 여러 장점을 제공하며, C#은 이러한 개념을 효과적으로 지원하여 객체지향적인 소프트웨어 개발을 촉진합니다.