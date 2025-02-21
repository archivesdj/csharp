Avalonia UI는 기본적으로 [ReactiveUI](https://www.reactiveui.net/)가 적용되어 있습니다만, ReactiveUI는 내용이 방대하고 복잡하여 이해하기 어렵고 따로서 원하는 대로 변형하여 기능을 구현하기 까다롭습니다. 이에 반해 [CommunityToolkit.Mvvm](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/mvvm/)은 사용이 쉽고 코드 생성기가 있어서 코드의 사용량을 줄여 줍니다.

여기서는 Avalonia UI에서 ReactiveUI를 제거하고 CommunityToolkit.Mvvm를 적용하는 방법을 알아봅니다.

## 1. 프로젝트에서 ReactiveUI 제거

먼저, 프로젝트에서 ReactiveUI 패키지를 제거해야 합니다.

- NuGet 패키지 관리자 사용:
  - 솔루션 탐색기에서 프로젝트를 우클릭하고 "NuGet 패키지 관리"를 선택합니다.
  - 설치된 패키지 목록에서 `Avalonia.ReactiveUI`를 찾아 제거합니다.
- CLI 사용:
  - 터미널에서 다음 명령어를 실행합니다:

```bash
dotnet remove package Avalonia.ReactiveUI
```

- Program.cs 수정:
  - `Program.cs` 파일에서 `UseReactiveUI()` 확장 메서드를 제거합니다. 기본적으로 Avalonia MVVM 템플릿을 사용했다면 다음과 같은 코드가 있을 수 있습니다:

```csharp
public static AppBuilder BuildAvaloniaApp()
    => AppBuilder.Configure<App>()
        .UsePlatformDetect()
        .LogToTrace()
        .UseReactiveUI(); // 이 줄 제거
```

수정 후:

```csharp
public static AppBuilder BuildAvaloniaApp()
    => AppBuilder.Configure<App>()
        .UsePlatformDetect()
        .LogToTrace();
```

## 2. CommunityToolkit.Mvvm 패키지 추가

이제 CommunityToolkit.Mvvm 패키지를 프로젝트에 추가합니다.

- NuGet 패키지 관리자 사용:
  - "NuGet 패키지 관리"에서 `CommunityToolkit.Mvvm`를 검색하고 최신 버전을 설치합니다.
- CLI 사용:
  - 터미널에서 다음 명령어를 실행합니다:

```bash
dotnet add package CommunityToolkit.Mvvm
```

## 3. ViewModelBase 클래스 수정

Avalonia MVVM 템플릿은 기본적으로 `ReactiveObject`를 기반으로 한 `ViewModelBase` 클래스를 제공합니다. 이를 `CommunityToolkit.Mvvm`의 `ObservableObject`로 변경해야 합니다.

- `ViewModels/ViewModelBase.cs` 파일을 열고 다음과 같이 수정합니다:

```csharp
// 기존 ReactiveUI 기반 코드
using ReactiveUI;

namespace YourAppName.ViewModels
{
    public class ViewModelBase : ReactiveObject
    {
    }
}
```

수정 후:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace YourAppName.ViewModels
{
    public class ViewModelBase : ObservableObject
    {
    }
}
```

- `ObservableObject`는 `INotifyPropertyChanged`를 구현하며, 속성 변경 알림을 쉽게 처리할 수 있는 기본 클래스입니다.

## 4. ViewModel 코드 업데이트

ReactiveUI에서 사용하던 속성과 명령을 CommunityToolkit.Mvvm 방식으로 변환합니다. 예를 들어, `MainWindowViewModel`을 수정하는 방법을 보겠습니다.

**ReactiveUI 기반 예제:**

```csharp
using ReactiveUI;

namespace YourAppName.ViewModels
{
    public class MainWindowViewModel : ViewModelBase
    {
        private string _greeting = "Welcome to Avalonia!";
        public string Greeting
        {
            get => _greeting;
            set => this.RaiseAndSetIfChanged(ref _greeting, value);
        }
    }
}
```

**CommunityToolkit.Mvvm으로 변환:**

```csharp
using CommunityToolkit.Mvvm.ComponentModel;

namespace YourAppName.ViewModels
{
    public partial class MainWindowViewModel : ViewModelBase
    {
        [ObservableProperty]
        private string _greeting = "Welcome to Avalonia!";
    }
}
```

- `[ObservableProperty]` 속성:
  - `CommunityToolkit.Mvvm`는 소스 제너레이터를 사용해 속성의 getter/setter와 `INotifyPropertyChanged` 구현을 자동 생성합니다.
  - 클래스에 `partial` 키워드를 추가해야 소스 제너레이터가 제대로 작동합니다.

**명령 추가 (옵션):**

ReactiveUI에서는 `ReactiveCommand`를 사용했지만, CommunityToolkit.Mvvm에서는 `[RelayCommand]`를 사용합니다.

예제:

```csharp
using CommunityToolkit.Mvvm.ComponentModel;
using CommunityToolkit.Mvvm.Input;

namespace YourAppName.ViewModels
{
    public partial class MainWindowViewModel : ViewModelBase
    {
        [ObservableProperty]
        private string _greeting = "Welcome to Avalonia!";

        [RelayCommand]
        public void UpdateGreeting()
        {
            Greeting = "Hello, CommunityToolkit!";
        }
    }
}
```

- XAML에서 버튼에 바인딩:
 
```xaml
<Button Command="{Binding UpdateGreetingCommand}" Content="Update Greeting" />
```

## 5. XAML 파일 확인

XAML 파일은 일반적으로 그대로 사용할 수 있습니다. `DataContext`가 올바르게 설정되어 있는지 확인하세요. 예를 들어, `MainWindow.axaml.cs`에서:

```csharp
public partial class MainWindow : Window
{
    public MainWindow()
    {
        InitializeComponent();
        DataContext = new MainWindowViewModel();
    }
}
```

## 6. 빌드 및 테스트

- 프로젝트를 빌드하고 실행하여 오류가 없는지 확인합니다.
- 속성 변경과 명령이 예상대로 작동하는지 테스트합니다.

## 추가 팁

- ReactiveUI와의 차이점:
  - ReactiveUI는 반응형 프로그래밍(Reactive Programming)에 강력한 기능을 제공하지만, CommunityToolkit.Mvvm은 더 간단하고 직관적이며 소스 제너레이터를 활용해 보일러플레이트 코드를 줄입니다.
  - 복잡한 비동기 작업이나 스트림 처리가 필요하다면 ReactiveUI를 유지하거나 `System.Reactive`를 추가로 사용할 수 있습니다.
- 문제 해결:
  - 속성이 업데이트되지 않는다면, `[ObservableProperty]`가 제대로 적용되었는지, 네임스페이스가 정확한지 확인하세요.
  - 명령이 작동하지 않으면 `[RelayCommand]`와 메서드 이름이 XAML 바인딩과 일치하는지 점검하세요.
