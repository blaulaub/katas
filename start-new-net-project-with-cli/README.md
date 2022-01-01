# Aim
Stay familiar with the dotnet CLI subcommands that are required to bootstrap a new .NET solution.

Takes about ~5 to ~10 minutes.

# Prerequisites

Either have a .Net SDK installed, or use the Debian container provided by Microsoft (the latter has no editor pre-installed, `vim` is used here):

```
podman run -it mcr.microsoft.com/dotnet/sdk
app update && apt install vim
```

# Tasks
- create a new dotnet solution
- create an executable project
- create a test project
- create a central build properties file

# Questions
- which directories and files will be produced?
- what is the syntax to reference variables from the central build properties file in a project file?

# Verify
- build it
- test it
- execute it

# Further reading
- The F# getting-started guide on dotnet CLI: <https://docs.microsoft.com/en-us/dotnet/fsharp/get-started/get-started-command-line>
- About build customization: <https://docs.microsoft.com/en-us/visualstudio/msbuild/customize-your-build>

# What you should have learned or remembered
- `dotnet new sln`
- `dotnet new console`, `dotnet new nunit`
- `dotnet sln add`
- `Directory.Build.props`, `<Project>`, `<PropertyGroup>
- `dotnet test`, `dotnet run --project`

# Solution

On the command line (for this kata, option `-lang "F#"` is optional):
```
dotnet new sln -o MyKata
cd MyKata
dotnet new console -lang "F#" -o MyProgram
dotnet sln add MyProgram/MyProgram.fsproj
dotnet new nunit -lang "F#" -o MyTest
dotnet sln add MyTest/MyTest.fsproj
touch Directory.Build.props
```

Common Properties can be put into `Directory.Build.props`, e.g.:
```
<Project>
  <PropertyGroup>
    <TargetFramework>net6.0</TargetFramework>
    <NUnit-Version>3.13.2</NUnit-Version>
  </PropertyGroup>
</Project>
```

Build, test and execute:
```
dotnet build
dotnet test
dotnet run --project MyProgram
```

# Further exercises

- include the console application project in the test; add some console code and test it
- the CLI also already prepares coverage testing; test coverage and generate a report

---
Note: convert this MarkDown into a PDF with `pandoc`.
