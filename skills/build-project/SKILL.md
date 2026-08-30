---
name: build-project
description: Build the InsolvencniRejstrik .NET solution. Use when the user wants to compile the project or check for build errors.
compatibility: Requires .NET Framework 4.6.2 SDK or MSBuild.
metadata:
  author: HlidacStatu
  version: 1.0.0
---

# Build Project

Build the InsolvencniRejstrik solution using MSBuild.

## Steps

1. Restore NuGet packages for the solution
2. Build the solution in the requested configuration (Debug by default)

## Commands

### Restore packages and build (Debug)

```bash
msbuild src/InsolvencniRejstrik.sln /t:Restore
msbuild src/InsolvencniRejstrik.sln /p:Configuration=Debug
```

### Build in Release mode

```bash
msbuild src/InsolvencniRejstrik.sln /p:Configuration=Release
```

## Guidelines

- Always restore NuGet packages before building if this is a fresh checkout
- The solution file is located at `src/InsolvencniRejstrik.sln`
- The main project targets .NET Framework 4.6.2
- Build output goes to `src/InsolvencniRejstrik/bin/<Configuration>/`
- Do not modify auto-generated files under `Connected Services/`
