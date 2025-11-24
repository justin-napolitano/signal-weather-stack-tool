---
slug: github-signal-weather-stack-tool-note-technical-overview
id: github-signal-weather-stack-tool-note-technical-overview
title: Signal Weather Stack Tool
repo: justin-napolitano/signal-weather-stack-tool
githubUrl: https://github.com/justin-napolitano/signal-weather-stack-tool
generatedAt: '2025-11-24T18:46:26.445Z'
source: github-auto
summary: >-
  This repository hosts an automated weather assistant that operates through
  Signal messaging. It leverages FastAPI, LangChain, and Docker for structured
  weather updates and queries.
tags: []
seoPrimaryKeyword: ''
seoSecondaryKeywords: []
seoOptimized: false
topicFamily: null
topicFamilyConfidence: null
kind: note
entryLayout: note
showInProjects: false
showInNotes: true
showInWriting: false
showInLogs: false
---

This repository hosts an automated weather assistant that operates through Signal messaging. It leverages FastAPI, LangChain, and Docker for structured weather updates and queries.

## Key Components

- **FastAPI**: Serves as the `weather-service` for daily forecasts.
- **LangChain**: Powers the `assistant-core` for parsing both direct commands and natural language.
- **Docker**: Manages microservices across a shared network.

## Quick Start

1. Clone the repo:

    ```bash
    git clone https://github.com/justin-napolitano/signal-weather-stack-tool.git
    cd signal-weather-stack-tool
    ```

2. Build and run the services:

    ```bash
    docker-compose up --build
    ```

3. Available endpoints:
   - `/today?city=&state=` for weather forecasts.
   - `/inbox` for Signal message handling.

### Gotchas

- Make sure to set up your Signal API credentials.
- Configure environment variables like `CRON_SCHEDULE` for notifications.

Check `index.md` for more on usage and architecture.
