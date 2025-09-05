
## Language Fundamentals
* The C# Compiler (name **Roslyn**) used by the dotnet CLI tools convert your C# source code into **intermediate language(IL)** code and stores the IL in an **assembly**(a DDL or EXE file).
## Strings

**String Interpolation**
```cs
string name = "kuroneko";
Console.WriteLine($"the cat's name is: {name}");
```
**Verbatim String**
```cs
string newFilePath = @"C:\televisions\sony\bravia.txt";
Console.WriteLine($"This is the new file path: {newFilePath}");
```
**Raw string literals**
```cs
string xml = """
    <person age="50">
        <first_name>nanocat</first_name>
    </person>
    """;
Console.WriteLine($"This is a xml file:\n{xml}");
```
## 