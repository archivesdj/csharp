# Group 연산자

`group` 연산자는 LINQ에서 사용되는 강력한 연산자 중 하나로, 데이터를 특정 기준에 따라 그룹화합니다. 그룹화된 데이터는 키-값 쌍의 형태로 반환되며, 각 그룹에 대해 특정 연산을 수행할 수 있습니다.

다음은 `group` 연산자의 사용 예제를 설명합니다. 가정해보겠습니다. 다음과 같이 `Person` 클래스가 있습니다.

```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
    public string Country { get; set; }
}
```

또한 다음과 같이 `people` 컬렉션이 있다고 가정합니다.

```csharp
List<Person> people = new List<Person>
{
    new Person { Name = "John", Age = 25, Country = "US" },
    new Person { Name = "Alice", Age = 30, Country = "CA" },
    new Person { Name = "Bob", Age = 22, Country = "US" },
    new Person { Name = "Charlie", Age = 28, Country = "CA" },
    new Person { Name = "David", Age = 35, Country = "US" }
};
```

이제 `group` 연산자를 사용하여 국가 별로 그룹화된 사람들을 출력하는 예제를 살펴봅시다.

```csharp
var groupedByCountry = from person in people
                       group person by person.Country;

foreach (var group in groupedByCountry)
{
    Console.WriteLine($"Country: {group.Key}");
    foreach (var person in group)
    {
        Console.WriteLine($"  {person.Name}, {person.Age}");
    }
    Console.WriteLine();
}
```

이 쿼리는 `people` 컬렉션을 국가(`Country`)를 기준으로 그룹화하고, 각 그룹에 대해 국가 이름과 해당 국가에 속한 사람들의 이름과 나이를 출력합니다. 결과는 다음과 같을 것입니다:

```
Country: US
  John, 25
  Bob, 22
  David, 35

Country: CA
  Alice, 30
  Charlie, 28
```

이것은 `group` 연산자를 사용하여 데이터를 그룹화하고 각 그룹에 대한 작업을 수행하는 간단한 예제입니다. `group` 연산자는 데이터베이스에서의 GROUP BY와 유사한 역할을 하며, 데이터를 효율적으로 구조화하고 처리할 수 있는 강력한 기능을 제공합니다.