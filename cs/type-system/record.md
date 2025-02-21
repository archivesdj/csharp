# 레코드

`record`는 C# 9.0 버전에서 도입된 새로운 참조 형식(Reference Type)으로, 불변(immutable) 데이터를 표현하기 위한 간단하고 강력한 기능을 제공합니다. `record`를 사용하면 데이터의 불변성을 보장하면서도 클래스보다 간단한 구문으로 코드를 작성할 수 있습니다.

`record`의 주요 특징과 사용법은 다음과 같습니다:

### 1. 불변성 (Immutability):

`record`는 기본적으로 불변 데이터를 나타내는데, 이는 한 번 생성된 인스턴스의 상태를 변경할 수 없다는 것을 의미합니다. 이는 개체의 값이 변경되지 않고 참조로 공유됨을 의미하며, 데이터의 안전성과 예측 가능한 동작을 제공합니다.

```csharp
public record Person
{
    public string FirstName { get; init; }
    public string LastName { get; init; }
}

// 불변성을 유지한 데이터 생성
var person1 = new Person { FirstName = "John", LastName = "Doe" };
var person2 = person1 with { LastName = "Smith" }; // 새로운 인스턴스 생성, LastName 변경
```

### 2. 값 기반 비교:

`record`는 기본적으로 값 기반 비교를 수행합니다. 즉, 두 인스턴스의 값이 동일한지 비교하는 데 사용되는 메서드가 자동으로 생성됩니다.

```csharp
var person1 = new Person { FirstName = "John", LastName = "Doe" };
var person2 = new Person { FirstName = "John", LastName = "Doe" };

bool areEqual = person1.Equals(person2); // 값 기반 비교
```

### 3. 간결한 구문:

`record`는 간결한 구문으로 데이터 클래스를 정의할 수 있도록 지원합니다. 속성의 초기화와 비교 메서드, 패턴 매칭 등을 자동으로 생성하여 코드의 양을 줄일 수 있습니다.

```csharp
public record Point(int X, int Y);

var point1 = new Point(1, 2);
var point2 = new Point(1, 2);

bool areEqual = point1.Equals(point2); // 값 기반 비교
```

### 4. `with` 키워드:

`with` 키워드를 사용하여 불변 데이터의 수정된 복사본을 쉽게 생성할 수 있습니다. 이를 통해 불필요한 코드 중복을 피하면서도 불변성을 유지할 수 있습니다.

```csharp
var updatedPerson = person1 with { LastName = "Smith" }; // 새로운 인스턴스 생성, LastName 변경
```

### 5. 기타 기능:

`record`는 패턴 매칭, 분해(deconstruction), 상속 등 다양한 기능을 지원합니다. 이를 통해 코드의 가독성을 높이고 확장성을 향상시킬 수 있습니다.

```csharp
// 패턴 매칭
string message = person switch
{
    { FirstName: "John" } => "Hello John!",
    _ => "Hello!"
};
```

`record`를 사용하면 데이터의 불변성과 코드의 간결성을 동시에 유지할 수 있습니다. 특히 데이터 전송 객체(Data Transfer Object, DTO)나 값 객체(Value Object)를 표현할 때 유용하며, 코드의 가독성을 높여 유지보수성을 향상시킬 수 있습니다.