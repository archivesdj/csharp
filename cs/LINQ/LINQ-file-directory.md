# LINQ와 파일 디렉토리

LINQ를 파일 시스템에 적용하는 경우 일반적으로 `System.IO` 네임스페이스의 클래스들과 함께 사용됩니다. 파일 시스템에서 파일이나 디렉터리를 쿼리하거나 조작하는 작업에 LINQ를 활용할 수 있습니다. 아래는 간단한 예제입니다.

## 특정 확장자를 가진 파일들 선택

예를 들어, 특정 디렉터리에서 특정 파일 확장자를 가진 파일들을 LINQ를 사용하여 선택하는 경우를 살펴봅시다. 다음은 `Directory.GetFiles` 메서드와 LINQ를 사용하여 특정 디렉터리에서 `.txt` 파일들을 선택하는 예제입니다.

```csharp
using System;
using System.IO;
using System.Linq;

class Program
{
    static void Main()
    {
        // 특정 디렉터리 경로
        string directoryPath = @"C:\ExampleDirectory";

        // LINQ를 사용하여 디렉터리에서 .txt 파일들을 선택
        var txtFiles = from file in Directory.GetFiles(directoryPath)
                       where file.EndsWith(".txt", StringComparison.OrdinalIgnoreCase)
                       select file;

        // 결과 출력
        Console.WriteLine("Text Files in the Directory:");
        foreach (var txtFile in txtFiles)
        {
            Console.WriteLine(txtFile);
        }
    }
}
```

이 코드에서 `Directory.GetFiles` 메서드는 지정된 디렉터리에서 파일 경로의 배열을 반환합니다. 그 후 LINQ의 `where` 절을 사용하여 파일 확장자가 `.txt`로 끝나는 파일들을 선택합니다. 선택된 파일들은 `foreach` 루프를 통해 출력됩니다.

이 예제에서는 파일 시스템에서 파일을 선택하는 간단한 작업을 보여주었습니다. 파일 시스템을 조작하거나 더 복잡한 쿼리를 수행하려면 LINQ를 사용하면서 `System.IO`의 다양한 클래스와 메서드를 조합하여 필요한 작업을 수행할 수 있습니다.

## 두 폴더의 파일 내용 비교

두 폴더의 파일 내용을 비교하려면 각 폴더의 파일 목록을 가져와서 파일 내용을 비교하면 됩니다. 다음은 두 폴더의 파일 내용을 비교하는 간단한 예제 코드입니다. 이 코드는 두 폴더에서 동일한 파일명을 가진 파일들을 선택하고 각 파일의 내용을 비교합니다.

```csharp
using System;
using System.IO;
using System.Linq;

class Program
{
    static void Main()
    {
        // 비교할 두 폴더의 경로
        string folderPath1 = @"C:\Folder1";
        string folderPath2 = @"C:\Folder2";

        // 두 폴더의 파일 목록 가져오기
        var files1 = Directory.GetFiles(folderPath1);
        var files2 = Directory.GetFiles(folderPath2);

        // 두 폴더에서 동일한 파일명을 가진 파일들 선택
        var commonFiles = files1.Intersect(files2, StringComparer.OrdinalIgnoreCase);

        // 각 파일의 내용을 비교
        foreach (var filePath in commonFiles)
        {
            string content1 = File.ReadAllText(Path.Combine(folderPath1, filePath));
            string content2 = File.ReadAllText(Path.Combine(folderPath2, filePath));

            // 내용이 다른 경우 출력
            if (content1 != content2)
            {
                Console.WriteLine($"File: {filePath} has different content.");
            }
        }

        Console.WriteLine("Comparison complete.");
    }
}
```

이 코드에서는 `Directory.GetFiles` 메서드를 사용하여 각 폴더의 파일 목록을 가져온 후, `Intersect` 메서드를 사용하여 두 폴더에서 동일한 파일명을 가진 파일들을 선택합니다. 그리고 선택된 각 파일의 내용을 `File.ReadAllText` 메서드를 사용하여 읽어와 비교합니다. 만약 파일 내용이 다르다면 해당 파일의 정보를 출력합니다.

이 코드는 간단한 예제일 뿐이며, 파일 내용을 비교할 때 고려해야 할 다양한 측면이 있을 수 있습니다. 파일이 매우 큰 경우 메모리 부담이 생길 수 있으므로 실제 적용 시에는 적절한 예외 처리와 성능 고려가 필요합니다.