# DOTNET CLI

**Check installed sdk's**

```bash
dotnet --info
```

**Project Options**

```bash
dotnet new list
```

**Create a new Solution File**
```bash
dotnet new sln
```
**Create a project**
```bash
dotnet new <TEMPLATE> -n <OUTPUT_NAME>
```
e.g.
```bash
dotnet new webapi -n API
```

`TEMPLATE` can be `webapi`, `classlib`, `console`, and so on, [check](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-new#arguments).
`OUTPUT_NAME` can be the name of the project
**Add the projects to the solution file**
e.g.
```
dotnet sln add API/API.csproj
```
**
## TERMS

- `sln` a solution is a structure for organizing projects in Visual Studio. The solution maintains the state information for projects in two files: `.sln` file and `.suo` file.

## Links

- [.NET CLI overview](https://learn.microsoft.com/en-us/dotnet/core/tools/)

* Reviewing the project files and startup
