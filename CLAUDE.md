# HlidacStatu - Insolvencni Rejstrik

Czech Insolvency Register data scraper and processor for Hlidac Statu (State Watcher).

## Project Overview

- **Language**: C# (.NET Framework 4.6.2)
- **Build System**: MSBuild / Visual Studio Solution
- **Solution**: `src/InsolvencniRejstrik.sln`
- **Test Framework**: xUnit 2.4.1

## Architecture

The application has two operating modes:

1. **Search mode** (`-s`/`--search`): Downloads records from the ISIR search engine and saves to the Hlidac Statu dataset via API
2. **Events mode** (`-e`/`--events`): Processes change events from the ISIR_WS service and stores in Elasticsearch

### Key Directories

- `src/InsolvencniRejstrik/` - Main application project
  - `ByEvents/` - Event-based processing (DTOs, persistence, ISIR clients, WS clients)
  - `FromSearch/` - Search-based processing
  - `Connected Services/` - Auto-generated WCF service proxies (do not edit manually)
- `src/InsolvencniRejstrikTest/` - xUnit test project

### External Dependencies

- **Elasticsearch** (via NEST 6.3.1) - Data storage for events mode
- **HlidacStatu API** - Dataset storage for search mode
- **ISIR Web Services** - Czech Insolvency Register SOAP services (WCF)
- **HtmlAgilityPack** - HTML parsing for detail pages

## Build

```bash
msbuild src/InsolvencniRejstrik.sln
```

## Test

```bash
dotnet test src/InsolvencniRejstrikTest/InsolvencniRejstrikTest.csproj
```

## Important Notes

- Do not edit files under `Connected Services/` - these are auto-generated WCF proxies
- The `App.config` contains WCF endpoint configurations for ISIR services
- Comments and UI strings are in Czech language
