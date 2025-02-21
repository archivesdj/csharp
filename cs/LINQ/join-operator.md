# Join 연산자

`join` 연산자는 두 개의 컬렉션에서 특정 조건을 충족하는 요소들을 결합하여 새로운 결과를 생성하는 LINQ 연산자입니다. `join` 연산자는 SQL에서의 INNER JOIN과 유사한 역할을 합니다.

다음은 `join` 연산자의 사용 예제를 설명합니다. 가정해보겠습니다. 두 개의 클래스 `Person`과 `Country`가 있습니다.

```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
    public string CountryCode { get; set; }
}

public class Country
{
    public string Code { get; set; }
    public string CountryName { get; set; }
}
```

또한 다음과 같이 두 개의 컬렉션 `people`와 `countries`가 있다고 가정합니다.

```csharp
List<Person> people = new List<Person>
{
    new Person { Name = "John", Age = 25, CountryCode = "US" },
    new Person { Name = "Alice", Age = 30, CountryCode = "CA" },
    new Person { Name = "Bob", Age = 22, CountryCode = "US" }
};

List<Country> countries = new List<Country>
{
    new Country { Code = "US", CountryName = "United States" },
    new Country { Code = "CA", CountryName = "Canada" }
};
```

이제 `join` 연산자를 사용하여 사람들의 국적을 국가 이름과 함께 결합하는 예제를 살펴봅시다.

```csharp
var query = from person in people
            join country in countries on person.CountryCode equals country.Code
            select new { person.Name, person.Age, CountryName = country.CountryName };

foreach (var result in query)
{
    Console.WriteLine($"{result.Name}, {result.Age}, {result.CountryName}");
}
```

이 쿼리는 `people` 컬렉션과 `countries` 컬렉션을 `CountryCode`와 `Code`를 기준으로 조인하고, 각 사람의 이름, 나이, 그리고 국적의 이름을 포함하는 새로운 익명 객체를 생성합니다. 결과를 출력하면 다음과 같은 내용이 나올 것입니다:

```
John, 25, United States
Alice, 30, Canada
Bob, 22, United States
```

이것은 간단한 `join` 연산자의 예제이며, 두 개의 컬렉션에서 특정 조건에 맞는 요소들을 결합하여 새로운 결과를 만드는 방법을 보여줍니다.