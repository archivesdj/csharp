# 비동기 프로그래밍 예제

다음은 C#에서 비동기 프로그래밍을 사용하는 간단한 예제들입니다. 이 예제들은 주로 네트워크 통신, 파일 I/O, 데이터베이스 액세스 등의 I/O-bound 작업을 다룹니다.

1. **웹 요청 비동기 처리:**
   - 웹에서 데이터를 비동기적으로 가져오는 예제입니다. `HttpClient` 클래스를 사용하여 웹 서버에 GET 요청을 보냅니다.

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        await GetDataAsync();
    }

    static async Task GetDataAsync()
    {
        using (HttpClient client = new HttpClient())
        {
            string result = await client.GetStringAsync("https://jsonplaceholder.typicode.com/todos/1");
            Console.WriteLine(result);
        }
    }
}
```

2. **파일 읽기 비동기 처리:**
   - 파일을 비동기적으로 읽어오는 예제입니다. `StreamReader`를 사용하여 파일의 내용을 읽어옵니다.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        await ReadFileAsync("example.txt");
    }

    static async Task ReadFileAsync(string filePath)
    {
        using (StreamReader reader = new StreamReader(filePath))
        {
            string content = await reader.ReadToEndAsync();
            Console.WriteLine(content);
        }
    }
}
```

3. **비동기 데이터베이스 액세스:**
   - Entity Framework를 사용하여 데이터베이스에서 데이터를 비동기적으로 가져오는 예제입니다.

```csharp
using System;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.EntityFrameworkCore;

class Program
{
    static async Task Main()
    {
        await GetUserDataAsync();
    }

    static async Task GetUserDataAsync()
    {
        using (var dbContext = new MyDbContext())
        {
            var users = await dbContext.Users.ToListAsync();
            foreach (var user in users)
            {
                Console.WriteLine($"ID: {user.Id}, Name: {user.Name}");
            }
        }
    }
}

public class MyDbContext : DbContext
{
    public DbSet<User> Users { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseSqlServer("your_connection_string");
    }
}

public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```

이러한 예제들은 비동기 프로그래밍을 사용하여 I/O-bound 작업을 효율적으로 처리하는 방법을 보여줍니다. 이를 통해 응용 프로그램이 블로킹되지 않고 다른 작업을 수행할 수 있습니다.