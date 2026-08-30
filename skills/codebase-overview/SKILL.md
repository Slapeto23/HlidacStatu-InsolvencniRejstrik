---
name: codebase-overview
description: Navigate and understand the InsolvencniRejstrik codebase structure. Use when the user wants to explore the project or understand how components connect.
metadata:
  author: HlidacStatu
  version: 1.0.0
---

# Codebase Overview

Guide for navigating the InsolvencniRejstrik codebase.

## Project Structure

```
src/
├── InsolvencniRejstrik.sln          # Visual Studio Solution
├── InsolvencniRejstrik/             # Main application
│   ├── Program.cs                   # Entry point, CLI argument parsing
│   ├── BaseConnector.cs             # Base class for connectors
│   ├── App.config                   # WCF endpoints, Elasticsearch config
│   ├── ByEvents/                    # Event-based processing mode
│   │   ├── Dto/                     # Data Transfer Objects
│   │   │   ├── Dokument.cs          # Document entity
│   │   │   ├── Osoba.cs             # Person entity
│   │   │   └── Rizeni.cs            # Proceedings entity
│   │   ├── Persistence/             # Data storage layer
│   │   │   ├── IRepository.cs       # Repository interface
│   │   │   ├── Repository.cs        # Main repository implementation
│   │   │   ├── RepositoryCache.cs   # Cached repository
│   │   │   ├── ElasticConnector.cs  # Elasticsearch connection
│   │   │   └── EventsRepository.cs  # Events persistence
│   │   ├── Isir/                    # ISIR client layer
│   │   │   ├── IIsirClient.cs       # ISIR client interface
│   │   │   ├── IsirClient.cs        # ISIR client implementation
│   │   │   └── IsirClientCache.cs   # Cached ISIR client
│   │   ├── Ws/                      # Web Service client layer
│   │   │   ├── IWsClient.cs         # WS client interface
│   │   │   ├── WsClient.cs          # WS client implementation
│   │   │   ├── WsClientCache.cs     # Cached WS client
│   │   │   └── WsResult.cs          # WS response model
│   │   ├── IsirWsConnector.cs       # Events mode orchestrator
│   │   └── Stats.cs                 # Processing statistics
│   ├── FromSearch/                  # Search-based processing mode
│   │   ├── SearchConnector.cs       # Search mode orchestrator
│   │   ├── InsolvencniRejstrikDataset.cs  # Dataset definition
│   │   ├── Rizeni.cs                # Search result model
│   │   ├── SenatniZnacka.cs         # Senate reference number
│   │   └── SpisovaZnacka.cs         # File reference number
│   └── Connected Services/          # Auto-generated WCF proxies (DO NOT EDIT)
└── InsolvencniRejstrikTest/         # xUnit test project
    └── ByEvents/Ws/WsResultTest.cs  # WS result parsing tests
```

## Key Patterns

- **Two operating modes**: Search mode saves to Hlidac Statu API, Events mode saves to Elasticsearch
- **Repository pattern**: `IRepository` interface with caching decorator (`RepositoryCache`)
- **Client pattern**: `IIsirClient` and `IWsClient` interfaces with caching decorators
- **WCF services**: SOAP-based communication with Czech Insolvency Register
- **CLI parsing**: NDesk.Options for command-line argument handling

## Guidelines

- Start at `Program.cs` to understand the entry point and mode selection
- For events processing flow: `Program.cs` → `IsirWsConnector` → `WsClient`/`IsirClient` → `Repository`
- For search processing flow: `Program.cs` → `SearchConnector` → ISIR search → HlidacStatu API
- Comments and UI strings are in Czech language
