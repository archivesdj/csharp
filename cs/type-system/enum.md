# 열거형

열거형(Enum)은 상수들의 집합을 정의하고, 각 상수에 정수 값을 할당할 수 있는 사용자 정의 형식입니다. C#에서 열거형은 코드를 읽고 이해하기 쉽도록 상수 값에 이름을 부여할 때 주로 사용됩니다.

### 열거형의 선언:

열거형은 `enum` 키워드를 사용하여 선언합니다.

```csharp
public enum Days
{
    Sunday,
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday
}
```

위의 예제에서 `Days` 열거형은 일주일의 요일을 나타내는 상수들로 구성되어 있습니다.

### 열거형의 사용:

```csharp
Days today = Days.Wednesday;

if (today == Days.Wednesday)
{
    Console.WriteLine("It's Wednesday!");
}
```

위의 예제에서 `today` 변수에는 `Days` 열거형의 상수 중 하나인 `Wednesday`가 할당되어 있습니다. 열거형 상수는 기본적으로 0부터 시작하는 정수 값으로 표현되지만, 각 상수에 특정 값을 지정할 수도 있습니다.

### 열거형의 기본 값:

열거형은 기본적으로 0부터 시작하여 1씩 증가하는 값을 가집니다. 다음과 같이 각 상수에 특정 값을 지정할 수 있습니다.

```csharp
public enum Days
{
    Sunday = 1,
    Monday = 2,
    Tuesday = 3,
    Wednesday = 4,
    Thursday = 5,
    Friday = 6,
    Saturday = 7
}
```

### 열거형의 형식 변환:

열거형은 기본적으로 정수 형식과 호환됩니다. 열거형 변수를 정수로 변환하거나, 정수를 열거형으로 변환할 수 있습니다.

```csharp
Days today = Days.Wednesday;
int dayValue = (int)today; // 열거형을 정수로 변환
Days convertedDay = (Days)5; // 정수를 열거형으로 변환
```

### 플래그 열거형:

플래그 열거형은 여러 개의 값을 가질 수 있으며, 각 값은 비트 단위로 OR(|) 연산을 사용하여 조합됩니다. `[Flags]` 특성을 이용하여 플래그 열거형을 선언할 수 있습니다.

```csharp
[Flags]
public enum Permissions
{
    Read = 1,
    Write = 2,
    Delete = 4,
    Execute = 8
}

Permissions userPermissions = Permissions.Read | Permissions.Write;
```

플래그 열거형은 주로 비트 연산을 통해 여러 가지 옵션을 조작할 때 사용됩니다.

열거형은 코드를 더 읽기 쉽고 유지보수하기 쉽게 만들어줍니다. 주로 서로 연관된 상수 값들을 그룹화하고, 의미 있는 이름을 부여하기 위해 사용됩니다. 특히, 열거형을 사용하면 상수값을 하드코딩하는 것보다 가독성이 높은 코드를 작성할 수 있습니다.

## 열거형과 문자열 간의 변환

열거형(Enum)과 문자열(string) 간의 변환은 주로 열거형 상수의 이름을 문자열로 가져오거나, 반대로 문자열을 열거형 상수로 변환하는 두 가지 상황에서 이루어집니다.

### 1. Enum에서 String으로 변환:

열거형 상수의 이름을 문자열로 가져오려면 `Enum.GetName` 메서드를 사용합니다.

```csharp
public enum Days
{
    Sunday,
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday
}

Days today = Days.Wednesday;
string dayString = Enum.GetName(typeof(Days), today);
Console.WriteLine(dayString); // 출력: Wednesday
```

또는 `ToString` 메서드를 사용할 수도 있습니다.

```csharp
string dayString = today.ToString();
Console.WriteLine(dayString); // 출력: Wednesday
```

### 2. String에서 Enum으로 변환:

문자열을 열거형 상수로 변환하려면 `Enum.Parse` 메서드를 사용합니다.

```csharp
string dayString = "Wednesday";
Days today = (Days)Enum.Parse(typeof(Days), dayString);
Console.WriteLine(today); // 출력: Wednesday
```

주의사항:
- `Enum.Parse` 메서드를 사용할 때, 대소문자 구분이므로 문자열이 정확하게 일치해야 합니다. 만약 대소문자를 무시하고 싶다면 `Enum.Parse(typeof(Days), dayString, true)`와 같이 세 번째 매개변수에 `true`를 전달합니다.
- `Enum.TryParse` 메서드를 사용하여 안전하게 변환할 수도 있습니다.

```csharp
string dayString = "Wednesday";
if (Enum.TryParse(dayString, out Days today))
{
    Console.WriteLine(today); // 출력: Wednesday
}
else
{
    Console.WriteLine("Invalid day string");
}
```

이러한 방법을 사용하면 열거형과 문자열 간의 변환을 안전하게 수행할 수 있습니다. 하지만 변환 작업 시에는 주의해야 하며, 예상치 못한 값이나 오류를 처리할 수 있는 코드를 추가하는 것이 좋습니다.