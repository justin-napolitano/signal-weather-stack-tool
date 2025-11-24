---
slug: github-signal-weather-stack-tool
id: github-signal-weather-stack-tool
title: Signal Weather Stack Tool
repo: justin-napolitano/signal-weather-stack-tool
githubUrl: https://github.com/justin-napolitano/signal-weather-stack-tool
generatedAt: '2025-11-24T21:36:21.269Z'
source: github-auto
summary: >-
  A Signal-based assistant integrated with a structured weather service for
  automated weather updates and queries. This project combines FastAPI,
  LangChain, and Docker to deliver weather information via Signal messaging.
tags: []
seoPrimaryKeyword: ''
seoSecondaryKeywords: []
seoOptimized: false
topicFamily: null
topicFamilyConfidence: null
kind: project
entryLayout: project
showInProjects: true
showInNotes: false
showInWriting: false
showInLogs: false
---

A Signal-based assistant integrated with a structured weather service for automated weather updates and queries. This project combines FastAPI, LangChain, and Docker to deliver weather information via Signal messaging.

---

## Features

- FastAPI-based `weather-service` providing daily weather forecasts and JSON responses.
- Signal assistant (`assistant-core`) capable of parsing direct weather commands and natural language queries.
- Structured LangChain agent for handling weather queries.
- Background cron job for daily weather notifications.
- Dockerized microservices communicating over a shared Docker network.

## Tech Stack

- Python
- FastAPI
- LangChain (structured chat agent)
- Docker
- Signal API (for messaging integration)

## Getting Started

### Prerequisites

- Docker and Docker Compose installed
- Access to Signal API credentials/configuration

### Installation & Running

1. Clone the repository:

```bash
git clone https://github.com/justin-napolitano/signal-weather-stack-tool.git
cd signal-weather-stack-tool
```

2. Build and start the Docker containers:

```bash
docker-compose up --build
```

3. The services will run on the `assistant-net` Docker network, with:
   - `weather-service` exposing `/today?city=&state=` endpoint
   - `assistant-core` exposing `/inbox` for Signal message handling

4. Configure environment variables such as `CRON_SCHEDULE` and `NOTIFY_URL` as needed.

## Project Structure

- `index.md`: Project documentation and overview.
- `weather-service`: FastAPI app providing weather data and daily forecast notifications.
- `assistant-core`: Signal message handler that routes weather queries and sends responses.
- `notifier-gateway`: HTTP gateway forwarding messages to Signal.

## Future Work / Roadmap

- Complete and extend documentation and usage examples.
- Add support for more natural language commands and additional weather data.
- Improve error handling and retry mechanisms for gateway communication.
- Enhance scheduling flexibility and configuration management.
- Integrate more advanced LangChain agents or alternative LLM tools.

---

For detailed usage and architecture, refer to the `index.md` file within the repository.
