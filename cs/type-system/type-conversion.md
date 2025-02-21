# 타입 변환

타입 변환(Type Conversion)은 하나의 데이터 형식을 다른 데이터 형식으로 변환하는 프로세스를 말합니다. C#에서는 다양한 타입 간의 변환을 지원하고 있습니다. 이러한 타입 변환은 크게 암시적 캐스팅(implicit casting)과 명시적 캐스팅(explicit casting)으로 나눌 수 있습니다.

### 1. 암시적 캐스팅 (Implicit Casting):

암시적 캐스팅은 데이터 형식이 더 큰 범위를 갖는 경우 또는 자동으로 형식이 변환되는 경우를 의미합니다. 이는 데이터 손실이 없거나 최소화됩니다.

```csharp
int intValue = 10;
float floatValue = intValue; // 암시적 캐스팅, int를 float로 변환
```

### 2. 명시적 캐스팅 (Explicit Casting):

명시적 캐스팅은 데이터 형식이 더 작은 범위를 갖는 경우 또는 명시적으로 형식을 변환해야 할 때 사용됩니다. 이 때, 변환을 진행하기 위해 명시적으로 캐스팅 연산자를 사용해야 합니다.

```csharp
double doubleValue = 123.45;
int intValue = (int)doubleValue; // 명시적 캐스팅, double을 int로 변환
```

#### 주의사항:

1. **데이터 손실 가능성:** 명시적 캐스팅에서는 형식의 크기가 더 작은 형식으로 캐스팅하는 경우 데이터 손실이 발생할 수 있습니다. 예를 들어, `double`을 `int`로 변환하면 소수 부분이 잘려나가게 됩니다.

2. **런타임 오류:** 무조건적인 캐스팅은 런타임 오류를 발생시킬 수 있습니다. 캐스팅할 수 없는 데이터 형식 사이의 캐스팅을 시도하면 `InvalidCastException`이 발생할 수 있습니다.

```csharp
object objValue = "Hello";
int intValue = (int)objValue; // 런타임 오류, string을 int로 변환할 수 없음
```

3. **안전한 캐스팅을 위한 `as` 연산자:** 참조 형식 간의 안전한 캐스팅을 위해 `as` 연산자를 사용할 수 있습니다. 이는 형식이 맞지 않을 경우 `null`을 반환하므로 예외를 방지할 수 있습니다.

```csharp
object objValue = "Hello";
string stringValue = objValue as string;

if (stringValue != null)
{
    Console.WriteLine($"Converted string: {stringValue}");
}
else
{
    Console.WriteLine("Conversion failed");
}
```

캐스팅은 데이터 형식을 유연하게 다룰 수 있도록 도와주지만, 적절한 사용과 예외 처리가 필요합니다. 특히, 캐스팅은 프로그램의 실행 중에 동적으로 이루어지기 때문에 안전한 방식으로 사용해야 합니다.

### 3. Convert 클래스를 이용한 변환:

`Convert` 클래스를 이용하여 다양한 데이터 형식 간의 변환을 수행할 수 있습니다.

```csharp
string stringValue = "123";
int intValue = Convert.ToInt32(stringValue);
```

### 4. Parse 메서드를 이용한 변환:

문자열을 다른 데이터 형식으로 변환할 때는 각 데이터 형식에 해당하는 `Parse` 메서드를 사용할 수 있습니다.

```csharp
string stringValue = "123";
int intValue = int.Parse(stringValue);
```

### 5. TryParse 메서드를 이용한 안전한 변환:

`TryParse` 메서드는 변환이 성공하면 `true`를 반환하고, 실패하면 `false`를 반환하며 결과는 out 매개변수를 통해 전달됩니다. 이를 통해 예외를 방지할 수 있습니다.

```csharp
string stringValue = "123";
int intValue;

if (int.TryParse(stringValue, out intValue))
{
    // 변환 성공
}
else
{
    // 변환 실패
}
```

타입 변환은 데이터의 다양한 형식을 유연하게 처리할 수 있게 해주지만, 불필요한 변환이나 잘못된 변환은 예기치 못한 결과를 초래할 수 있으므로 주의가 필요합니다. 특히, 변환 중 발생하는 예외를 적절히 처리하는 것이 중요합니다.