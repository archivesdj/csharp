# 비동기 프로그래밍

C#에서 asynchronous programming은 비동기 프로그래밍 모델을 지원하는 기능을 제공합니다. 비동기 프로그래밍은 주로 I/O 작업, 웹 요청, 데이터베이스 쿼리 등과 같이 시간이 소요되는 작업을 효율적으로 처리하기 위해 사용됩니다. Asynchronous programming은 기본적으로 `async` 및 `await` 키워드를 사용하여 구현됩니다.

아래는 C#에서 asynchronous programming을 사용하는 기본 개념과 예제 코드입니다:

1. **`async` 및 `await` 키워드:**
   - `async` 키워드는 비동기 메서드를 선언할 때 사용되며, `await` 키워드는 비동기적으로 실행되는 작업이 완료될 때까지 기다릴 때 사용됩니다.

   ```csharp
   using System;
   using System.Threading.Tasks;

   class Program
   {
       static async Task Main()
       {
           await DoAsyncWork();
           Console.WriteLine("Main method completed.");
       }

       static async Task DoAsyncWork()
       {
           Console.WriteLine("Start of asynchronous method.");
           await Task.Delay(2000); // 비동기적인 작업 시뮬레이션
           Console.WriteLine("End of asynchronous method.");
       }
   }
   ```

2. **`Task` 클래스:**
   - `Task` 클래스는 비동기적인 작업을 나타내는데 사용됩니다. `Task.Delay`와 같은 메서드는 일정 시간 동안 작업을 지연시키는 등의 기능을 제공합니다.

   ```csharp
   using System;
   using System.Threading.Tasks;

   class Program
   {
       static async Task Main()
       {
           Task<int> result = DoAsyncWork();
           Console.WriteLine("Main method continuing.");

           int finalResult = await result;
           Console.WriteLine($"Result from asynchronous method: {finalResult}");
       }

       static async Task<int> DoAsyncWork()
       {
           Console.WriteLine("Start of asynchronous method.");
           await Task.Delay(2000); // 비동기적인 작업 시뮬레이션
           Console.WriteLine("End of asynchronous method.");

           return 42;
       }
   }
   ```

3. **Exception Handling:**
   - 비동기 메서드에서 발생한 예외는 `await`를 사용하여 처리할 수 있습니다.

   ```csharp
   using System;
   using System.Threading.Tasks;

   class Program
   {
       static async Task Main()
       {
           try
           {
               await DoAsyncWorkWithError();
           }
           catch (Exception ex)
           {
               Console.WriteLine($"Exception caught: {ex.Message}");
           }
       }

       static async Task DoAsyncWorkWithError()
       {
           Console.WriteLine("Start of asynchronous method with error.");
           await Task.Delay(2000); // 비동기적인 작업 시뮬레이션
           throw new Exception("Something went wrong!");
       }
   }
   ```

이러한 예제에서는 비동기 메서드를 선언하고, `await`를 사용하여 비동기적으로 작업이 완료될 때까지 기다리는 방법 등을 보여줍니다. Async 및 await의 사용은 주로 비동기 I/O 작업, 웹 요청, 데이터베이스 쿼리 등과 같이 시간이 소요되는 작업을 효과적으로 처리하기 위해 채택됩니다.