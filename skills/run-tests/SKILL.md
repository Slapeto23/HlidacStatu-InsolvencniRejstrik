---
name: run-tests
description: Run the xUnit test suite for InsolvencniRejstrik. Use when the user wants to run tests or verify changes.
compatibility: Requires .NET Framework 4.6.2 SDK and xUnit runner.
metadata:
  author: HlidacStatu
  version: 1.0.0
---

# Run Tests

Run the xUnit test suite for the InsolvencniRejstrik project.

## Steps

1. Ensure the solution is built
2. Run the xUnit tests

## Commands

### Build and run tests

```bash
msbuild src/InsolvencniRejstrik.sln /p:Configuration=Debug
dotnet test src/InsolvencniRejstrikTest/InsolvencniRejstrikTest.csproj
```

### Run tests with verbose output

```bash
dotnet test src/InsolvencniRejstrikTest/InsolvencniRejstrikTest.csproj --verbosity detailed
```

## Guidelines

- The test project is `src/InsolvencniRejstrikTest/InsolvencniRejstrikTest.csproj`
- Tests use xUnit 2.4.1 as the test framework
- The test project references the main project directly
- Always build before running tests to ensure the latest code is tested
- Test files are located under `src/InsolvencniRejstrikTest/ByEvents/`
