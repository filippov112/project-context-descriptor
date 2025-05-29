# ProjectContextDescriptor

## Описание

Консольное приложение на C# для формирования контекста проекта: генерирует JSON-описание структуры и текстовое содержимое исходных файлов. Учитывает `.gitignore` и автоматически определяет кодировки файлов. Полезно для подготовки данных для нейросетей или анализа проекта.

## Функционал

- Рекурсивный обход структуры проекта
- Формирование JSON-файла с описанием каталогов и файлов
- Сбор текста из файлов в форматированных кодовых блоках
- Поддержка параметра списка расширений (или автоматическое определение текстовых файлов)
- Автоматическое определение кодировок
- Учет игнорируемых файлов по `.gitignore`
- Перезапись выходных файлов при повторном запуске
- Кроссплатформенность (Windows/Linux)

## Технологии

- Язык: C# (.NET 6/7/8)
- Библиотеки:
  - `Ude.NetStandard` — определение кодировки
  - `Ignore` — поддержка синтаксиса `.gitignore`

## Установка и запуск

### Требования
- [.NET SDK 6.0+](https://dotnet.microsoft.com/download)

### Windows

Чтобы запускать приложение в Windows через одну команду в PowerShell, нужно:
1. Скомпилировать приложение как самостоятельный `.exe`. После этого в папке `bin\Release\netX\win-x64\publish` появится один `.exe` файл (например, `ProjectContextDescriptor.exe`).
	```bash
	dotnet publish -c Release -r win-x64 --self-contained true -p:PublishSingleFile=true
	```

2. Добавить путь к `.exe` в переменную окружения `PATH`
	1. Поместить `ProjectContextDescriptor.exe`, например, в `C:\Tools\ContextTool\`.
	2. Добавить каталог в `PATH`:
	3. После этого можно вызывать:
	```powershell
	ProjectContextDescriptor ".cs,.json"
	```

## Руководство пользователя

📦 Пример вызова:
```bash
# Запуск по рабочему каталогу без расширений — будут обрабатываться все текстовые файлы
dotnet run --

# Запуск с указанием расширений:
dotnet run -- "/path/to/project" ".cs,.json,.csproj"
```
Выходные файлы:
- `project_structure.json`
- `project_content.txt`

🔍 Пример структуры JSON:
```json
{
  ".": ["Program.cs", ".gitignore"],
  "Subfolder": {
    ".": ["Utils.cs"]
  }
}
```

📝 Пример фрагмента текстового контекста:
```
	File: Program.cs
	```
	using System;
	
	class Program {
	    static void Main() {
	        Console.WriteLine("Hello, world!");
	    }
	}
	```
```
