# 비동기 vs 병렬 프로그래밍 비교

비동기 프로그래밍과 병렬 프로그래밍은 C#에서 모두 성능 최적화와 효율성을 위해 사용되지만, 그 목적과 접근 방식이 다릅니다.

## 비동기 프로그래밍 (Asynchronous Programming)

- 정의: 비동기 프로그래밍은 작업을 호출한 스레드가 해당 작업의 완료를 기다리지 않고 다른 작업을 수행할 수 있도록 하는 방식입니다. 주로 I/O 작업(파일 읽기/쓰기, 네트워크 요청 등)처럼 시간이 오래 걸리는 작업에서 유용합니다.
- C#에서의 구현: `async`와 `await` 키워드를 사용하며, `Task` 또는 `Task<T>` 클래스를 기반으로 동작합니다.
- 특징:
  - 단일 스레드 혹은 최소한의 스레드로 효율적으로 작업을 처리.
  - 작업이 완료될 때까지 스레드를 블록(block)하지 않음.
  - 주로 UI 응답성 유지나 I/O-bound 작업 처리에 사용.
- 예제:
- 
```csharp
public async Task<int> GetDataAsync()
{
    HttpClient client = new HttpClient();
    string result = await client.GetStringAsync("https://example.com");
    return result.Length;
}
```

## 병렬 프로그래밍 (Parallel Programming)

- 정의: 병렬 프로그래밍은 여러 작업을 동시에 실행하기 위해 다중 스레드나 다중 코어를 활용하는 방식입니다. 주로 CPU 집약적인 작업(계산, 데이터 처리 등)에 적합합니다.
- C#에서의 구현: `Parallel` 클래스, `PLINQ(Parallel LINQ)`, 또는 `Task Parallel Library (TPL)`를 사용합니다.
- 특징:
  - 다중 스레드를 활용해 작업을 병렬로 분할 실행.
  - CPU-bound 작업에 최적화됨.
  - 스레드 관리와 동기화가 필요할 수 있어 복잡도가 증가할 수 있음.
- 예제:

```csharp
public void ProcessDataInParallel(int[] data)
{
    Parallel.For(0, data.Length, i =>
    {
        data[i] = data[i] * 2; // CPU 집약적 작업
    });
}
```

## 언제 무엇을 사용할까?

- 비동기 프로그래밍:
  - 외부 리소스(예: API 호출, 데이터베이스 쿼리)와의 상호작용이 많을 때.
  - UI 애플리케이션에서 사용자 경험을 개선하고 싶을 때(예: 버튼 클릭 후 응답 대기).
- 병렬 프로그래밍:
  - 대량의 데이터를 처리하거나 복잡한 계산(예: 이미지 처리, 수학 연산)을 할 때.
  - 하드웨어(멀티코어 CPU)를 최대한 활용해야 할 때.
 
## 혼합 사용 가능성

C#에서는 비동기와 병렬을 함께 사용할 수도 있습니다. 예를 들어, 여러 비동기 작업을 병렬로 실행하려면 `Task.WhenAll`을 활용할 수 있습니다:

```csharp
public async Task ProcessMultipleAsync()
{
    var tasks = new List<Task<int>>
    {
        GetDataAsync(),
        GetDataAsync()
    };
    int[] results = await Task.WhenAll(tasks);
    Console.WriteLine(results.Sum());
}
```

이 경우 비동기 작업을 병렬로 실행하며, 모든 작업이 완료될 때까지 기다립니다.

## 결론

- 비동기 프로그래밍은 "대기"를 효율적으로 관리하며 스레드 낭비를 줄이는 데 초점.
- 병렬 프로그래밍은 "동시 실행"으로 작업 속도를 높이는 데 초점.
