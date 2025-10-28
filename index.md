+++
title = "Signal-Driven Weather Automation"
date = "2025-10-28"
description = "Integrating a structured-tool weather service into a Signal-based assistant."
author = "Justin Napolitano"
categories = ["projects"]
tags = ["signal","fastapi","langchain","docker","automation"]
[extra]
lang = "en"
toc = true
comment = false
copy = true
outdate_alert = false
outdate_alert_days = 120
math = false
mermaid = false
featured = false
reaction = false
+++

## Summary
The stack now includes a **weather-service** container and an updated **assistant-core** that can call it directly or through a LangChain structured tool.

`weather-service` runs a FastAPI app with:
- `/today?city=&state=` → returns JSON and a formatted summary  
- a background cron job (`CRON_SCHEDULE`) posting daily forecasts to `notifier-gateway`

`assistant-core` exposes `/inbox` for Signal messages.  
When it receives `/weather Orlando, FL`, or a natural-language query like “what’s the weather in Orlando?”, it:
1. Parses or forwards the text to the `weather_tool`
2. Calls `weather_service` (`http://weather-service:8789/today`)
3. Relays the formatted result back to `notifier-gateway` → Signal

The assistant also runs `poll_loop()` for inbound messages from `signal-api`, but `/inbox` provides a push path via the gateway.

## Architecture
```
signal-api ─┬─> notifier-gateway (HTTP /send)
             │
             └─> assistant-core (FastAPI /inbox)
                     ├─ LangChain structured agent
                     └─ tools → weather-service → Open-Meteo
```

All services share the `assistant-net` Docker network.  
`NOTIFY_URL` inside each container targets the internal host, not localhost.

## Notes
- Structured-chat agent (`create_structured_chat_agent`) replaces the deprecated zero-shot type.  
- `/weather` command uses the direct client for low latency; the LLM tool path handles natural-language prompts.  
- Gateway timeouts don’t block delivery; the send occurs before the read timeout.  
- Daily updates still post independently from the weather-service cron.

This setup demonstrates a clean pattern: **small, single-purpose containers** that publish data via the gateway and can be composed under a common LLM agent.
