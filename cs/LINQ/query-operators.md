# 쿼리 연산자

LINQ(Language Integrated Query)에서 사용 가능한 주요 쿼리 연산자들은 다양한 목적으로 사용되며, 이들은 데이터를 필터링하고 정렬하며 변형하는 등의 작업을 수행합니다. 아래에 LINQ에서 주로 사용되는 연산자들을 설명합니다:

1. **`Where`:**
   - 조건을 기반으로 데이터를 필터링합니다. 주어진 조건에 맞는 요소만을 선택합니다.

   ```csharp
   var adults = people.Where(person => person.Age > 18);
   ```

2. **`OrderBy` 및 `OrderByDescending`:**
   - 요소를 정렬합니다. `OrderBy`는 오름차순 정렬을 하며, `OrderByDescending`는 내림차순 정렬을 수행합니다.

   ```csharp
   var sortedByName = people.OrderBy(person => person.LastName);
   var sortedByAgeDescending = people.OrderByDescending(person => person.Age);
   ```

3. **`Select`:**
   - 원하는 속성이나 변환을 통해 새로운 형태의 데이터를 선택합니다.

   ```csharp
   var names = people.Select(person => person.Name);
   ```

4. **`GroupBy`:**
   - 지정된 키에 따라 데이터를 그룹화합니다.

   ```csharp
   var groupedByAge = people.GroupBy(person => person.Age);
   ```

5. **`Join`:**
   - 두 개의 컬렉션을 조인하여 관련된 요소들을 결합합니다.

   ```csharp
   var result = from person in people
                join country in countries on person.CountryCode equals country.Code
                select new { person.Name, country.CountryName };
   ```

6. **`Aggregate`:**
   - 시퀀스의 모든 요소에 대해 누적 작업을 수행합니다.

   ```csharp
   var sum = numbers.Aggregate((acc, num) => acc + num);
   ```

7. **`Any` 및 `All`:**
   - `Any`는 조건에 맞는 요소가 하나라도 있는지 여부를 확인하며, `All`은 모든 요소가 조건을 만족하는지 여부를 확인합니다.

   ```csharp
   bool hasAdults = people.Any(person => person.Age > 18);
   bool allAdults = people.All(person => person.Age > 18);
   ```

8. **`Distinct`:**
   - 시퀀스에서 중복된 요소를 제거합니다.

   ```csharp
   var uniqueAges = people.Select(person => person.Age).Distinct();
   ```

9. **`Skip` 및 `Take`:**
   - `Skip`은 시퀀스에서 처음 몇 개의 요소를 건너뛰고 나머지를 반환하며, `Take`는 처음 몇 개의 요소만 선택합니다.

   ```csharp
   var result = numbers.Skip(2).Take(3);  // index 2부터 3개의 요소를 선택
   ```

10. **`First`, `FirstOrDefault`, `Last`, `LastOrDefault`:**
    - `First`는 시퀀스의 첫 번째 요소를 반환하며, `Last`는 마지막 요소를 반환합니다. `OrDefault` 버전은 해당 조건을 만족하는 요소가 없는 경우 기본값을 반환합니다.

    ```csharp
    var firstPerson = people.First();
    var lastPerson = people.LastOrDefault(person => person.Age > 30);
    ```

11. **`Count`:**
    - 시퀀스의 요소 수를 반환합니다.

    ```csharp
    var count = people.Count();
    ```

12. **`Concat`:**
    - 두 개의 시퀀스를 연결하여 새로운 시퀀스를 생성합니다.

    ```csharp
    var combined = sequence1.Concat(sequence2);
    ```

13. **`Reverse`:**
    - 시퀀스의 순서를 뒤집습니다.

    ```csharp
    var reversed = numbers.Reverse();
    ```

이것은 LINQ의 주요 연산자 중 일부일 뿐이며, LINQ는 다양한 다른 연산자와 메서드를 제공하여 데이터를 유연하게 처리할 수 있도록 합니다. LINQ는 다양한 데이터 소스에 적용할 수 있으며, 코드를 간결하고 가독성 있게 유지하면서 강력한 쿼리 작업을 가능하게 합니다.