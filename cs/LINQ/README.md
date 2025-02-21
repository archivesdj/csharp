# LINQ

LINQ(Language Integrated Query)은 C#과 다른 .NET 언어에서 데이터 집합을 쿼리하는 데 사용되는 강력하고 표현력 있는 기능입니다. LINQ를 사용하면 데이터베이스, XML 문서, 컬렉션 등 다양한 데이터 소스에 대해 일관된 방식으로 쿼리를 수행할 수 있습니다.

LINQ의 주요 특징은 다음과 같습니다:

1. **통합된 쿼리 언어:**
   - LINQ는 C# 코드 안에 SQL과 비슷한 쿼리 구문을 통합하여 사용할 수 있습니다. 이러한 통합된 방식으로 데이터를 쿼리하면 코드의 가독성이 향상되고 유지보수가 쉬워집니다.

   ```csharp
   var query = from person in people
               where person.Age > 18
               orderby person.LastName
               select person;
   ```

2. **객체와 컬렉션 쿼리:**
   - LINQ는 데이터베이스 쿼리뿐만 아니라 메모리 내의 객체나 컬렉션에 대해서도 동일한 쿼리 기능을 제공합니다. 이는 데이터 소스에 상관없이 일관된 코드를 작성할 수 있도록 합니다.

   ```csharp
   var query = from student in students
               where student.Grade == "A"
               select student.Name;
   ```

3. **타입 안정성:**
   - LINQ는 컴파일 시간에 타입 안전성을 보장합니다. 쿼리에서 사용되는 속성이나 메서드가 컴파일 시점에 존재하지 않으면 컴파일 오류가 발생합니다.

   ```csharp
   var query = from person in people
               where person.Age > 18
               orderby person.LastName
               select person.NonexistentProperty;  // 컴파일 오류 발생
   ```

4. **확장 메서드 구문:**
   - LINQ는 쿼리 구문뿐만 아니라 확장 메서드 구문을 사용하여 쿼리를 작성할 수 있습니다. 이를 통해 간결하고 유연한 쿼리를 작성할 수 있습니다.

   ```csharp
   var query = people
                .Where(person => person.Age > 18)
                .OrderBy(person => person.LastName)
                .Select(person => person);
   ```

5. **다양한 연산자:**
   - LINQ는 다양한 연산자를 제공하여 데이터를 필터링, 정렬, 그룹화하거나 변형할 수 있습니다. `Where`, `OrderBy`, `Select`, `GroupBy`, `Join` 등의 연산자를 활용할 수 있습니다.

   ```csharp
   var adults = people.Where(person => person.Age > 18);
   var sortedByName = people.OrderBy(person => person.LastName);
   var groupedByAge = people.GroupBy(person => person.Age);
   ```

6. **다양한 데이터 소스 지원:**
   - LINQ는 다양한 데이터 소스에 적용할 수 있습니다. 데이터베이스, XML 문서, 메모리 내의 컬렉션 등을 통일된 방식으로 쿼리할 수 있어서 개발자에게 편의성을 제공합니다.

LINQ는 데이터 쿼리와 조작을 간단하고 일관된 방식으로 수행할 수 있도록 해주며, 코드의 가독성을 높여 유지보수를 쉽게 만듭니다. LINQ는 C# 3.0부터 지원되었으며, .NET Framework와 .NET Core, .NET 5 이후 버전에서도 계속 발전하고 있습니다.