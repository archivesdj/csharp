# 병렬 프로그래밍 예제

병렬 프로그래밍은 CPU-intensive한 작업을 효율적으로 처리하기 위해 사용됩니다. 주로 다수의 CPU 코어를 활용하여 여러 작업을 동시에 실행함으로써 전체 성능을 향상시키는 데 활용됩니다. 아래는 C#에서 병렬 프로그래밍을 사용하는 몇 가지 예제입니다.

1. **Parallel.ForEach를 사용한 반복 작업:**
   - 배열의 각 요소를 병렬로 처리하는 예제입니다.

```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        int[] numbers = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

        Parallel.ForEach(numbers, number =>
        {
            Console.WriteLine($"Processed {number} on thread {Task.CurrentId}");
        });
    }
}
```

2. **PLINQ를 사용한 병렬 LINQ 쿼리:**
   - LINQ 쿼리를 사용하여 데이터를 병렬로 처리하는 예제입니다.

```csharp
using System;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        int[] numbers = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

        var parallelQuery = from number in numbers.AsParallel()
                            where number % 2 == 0
                            select number;

        parallelQuery.ForAll(number =>
        {
            Console.WriteLine($"Processed {number} on thread {Task.CurrentId}");
        });
    }
}
```

3. **Parallel.Invoke를 사용한 병렬 메서드 호출:**
   - 여러 메서드를 병렬로 호출하는 예제입니다.

```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        Parallel.Invoke(
            () => ProcessData("Task 1"),
            () => ProcessData("Task 2"),
            () => ProcessData("Task 3")
        );
    }

    static void ProcessData(string taskName)
    {
        Console.WriteLine($"Processing data in {taskName} on thread {Task.CurrentId}");
    }
}
```

이러한 예제들은 병렬 프로그래밍을 사용하여 여러 작업을 동시에 실행하여 전체 성능을 향상시키는 방법을 보여줍니다. 병렬 처리는 데이터를 분할하고 각 부분을 독립적으로 처리함으로써 다중 CPU 코어에서 동시에 실행될 수 있게 합니다.