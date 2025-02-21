# 구조체

`struct`는 C#에서 값 형식(Value Type) 중 하나로 사용되는 키워드입니다. 구조체(Struct)를 정의할 때 사용되며, 클래스와 유사하지만 몇 가지 중요한 차이점이 있습니다. 아래에서 `struct`의 특징과 사용법에 대해 상세히 설명하겠습니다.

## 특징 및 사용법

### 구조체 (Struct)의 특징:

1. **값 형식 (Value Type):** 구조체는 값 형식으로 선언되며, 인스턴스는 스택 메모리에 저장됩니다. 이는 힙 메모리에 저장되는 클래스와는 대조적입니다.

2. **스택에 할당:** 구조체의 인스턴스는 스택에 할당되므로 힙에 할당되는 클래스보다 메모리 사용이 더 경제적입니다.

3. **기본 생성자:** 구조체는 생성자를 선언하지 않아도 기본 생성자가 자동으로 생성되어 모든 멤버를 기본값으로 초기화합니다.

4. **상속 불가능:** 구조체는 클래스와 달리 상속을 지원하지 않습니다. 즉, 다른 클래스나 구조체에서 상속받을 수 없습니다.

5. **값 복사:** 구조체의 변수는 값이 직접 복사되므로 하나의 구조체를 수정해도 다른 구조체에 영향을 미치지 않습니다.

6. **메서드 선언 가능:** 구조체 내에서 메서드를 선언하고 정의할 수 있습니다.

### 구조체의 선언과 사용:

```csharp
// 구조체 선언
public struct Point
{
    public int X;
    public int Y;

    // 생성자
    public Point(int x, int y)
    {
        X = x;
        Y = y;
    }

    // 메서드
    public void Display()
    {
        Console.WriteLine($"X: {X}, Y: {Y}");
    }
}

class Program
{
    static void Main()
    {
        // 구조체 인스턴스 생성
        Point point1 = new Point(10, 20);
        Point point2 = point1; // 값이 복사됨

        // 값 변경
        point1.X = 30;

        // 값이 서로 독립적
        point1.Display(); // 출력: X: 30, Y: 20
        point2.Display(); // 출력: X: 10, Y: 20
    }
}
```

구조체를 사용할 때는 주로 간단한 데이터 구조를 표현하고자 할 때나 값 복사가 필요한 경우에 활용됩니다. 그러나 데이터 크기가 크고 변경 빈도가 높은 경우에는 클래스를 사용하는 것이 일반적으로 더 효율적입니다.

## 사용시 주의사항

구조체를 사용할 때에는 몇 가지 주의사항과 규칙을 고려해야 합니다. 아래는 구조체 사용시 주의할 점들입니다:

1. **복사 비용:** 구조체는 값 형식이므로 인스턴스를 다른 변수에 할당하거나 메서드에 전달할 때마다 값이 복사됩니다. 만약 구조체가 큰 데이터나 여러 멤버를 가지고 있고, 빈번하게 복사되는 경우 성능 이슈가 발생할 수 있습니다.

2. **가변성(Volatility):** 구조체는 값 형식이기 때문에 메서드 내에서 인스턴스의 멤버를 수정할 경우 호출된 메서드에서의 변경은 원본에 영향을 미치지 않습니다. 이는 예상치 못한 동작을 초래할 수 있으므로 주의가 필요합니다.

    ```csharp
    public struct Point
    {
        public int X;
        public int Y;
    }

    class Program
    {
        static void ModifyPoint(Point point)
        {
            point.X = 100;
            point.Y = 200;
        }

        static void Main()
        {
            Point original = new Point();
            ModifyPoint(original);
            Console.WriteLine($"X: {original.X}, Y: {original.Y}"); // 출력: X: 0, Y: 0
        }
    }
    ```

3. **초기화:** 구조체를 사용할 때는 반드시 초기화되어야 합니다. 기본 생성자가 자동으로 생성되지만, 모든 멤버에 대한 초기화가 보장되어야 합니다.

    ```csharp
    public struct Point
    {
        public int X;
        public int Y;
    }

    class Program
    {
        static void Main()
        {
            Point point; // 초기화되지 않음
            Console.WriteLine($"X: {point.X}, Y: {point.Y}"); // 컴파일 오류: 변수 'point'는 할당되지 않았습니다.
        }
    }
    ```

4. **Boxing과 Unboxing 피하기:** 구조체는 값 형식이므로 힙 메모리에 박싱(boxing) 및 언박싱(unboxing)이 발생하지 않도록 주의해야 합니다. 특히, 인터페이스와 함께 사용될 때 주의가 필요합니다.

    ```csharp
    interface IExample
    {
        void Display();
    }

    public struct Point : IExample
    {
        public int X;
        public int Y;

        public void Display()
        {
            Console.WriteLine($"X: {X}, Y: {Y}");
        }
    }

    class Program
    {
        static void Main()
        {
            Point point = new Point();
            IExample example = point; // 박싱 발생

            // ...

            Point newPoint = (Point)example; // 언박싱 발생
        }
    }
    ```

구조체를 적절히 활용하면 성능을 향상시킬 수 있지만, 사용 시에는 주의 깊게 설계하고 다루어야 합니다. 대부분의 경우, 간단한 데이터 구조를 표현하거나 값 복사를 피하기 위해 사용됩니다.