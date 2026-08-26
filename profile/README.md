# axonpush

Real-time event infrastructure for AI agent systems.

Agents emit events. Those events land durably, fan out to subscribers in real
time and to outbound webhooks, and stay searchable and traceable afterwards.

## Sending events

Point an existing setup at axonpush rather than rewriting your instrumentation.
Three ingest dialects are supported:

- the native REST API
- OTLP/HTTP, at `/v1/traces` and `/v1/logs`
- Sentry SDK envelopes, pointed at an axonpush DSN

```python
from axonpush import AxonPush

with AxonPush() as client:
    client.events.publish(
        identifier="research.step",
        channel_id=CHANNEL_ID,
        payload={"query": "who cited this paper", "tokens": 412},
    )
```

Subscribe to the same channel over MQTT and the event arrives as it is written.

## SDKs

| Package | Registry | Install |
|---|---|---|
| [`@axonpush/sdk`](https://www.npmjs.com/package/@axonpush/sdk) | npm | `npm install @axonpush/sdk` |
| [`axonpush`](https://pypi.org/project/axonpush/) | PyPI | `pip install axonpush` |
| `AxonPush` | NuGet | `dotnet add package AxonPush` |

All three live in [`sdks`](https://github.com/axonpush/sdks) and generate from
one OpenAPI contract.

The generated client is the floor, not the product. On top of it sit resource
classes, a realtime client, and a shared error tree. Integrations cover
LangChain, LangGraph, OpenAI Agents, Anthropic, CrewAI, Mastra, LlamaIndex,
Vercel AI, Semantic Kernel, OpenTelemetry, and the usual logging libraries.

Cross-language drift is checked rather than hoped for. CI compares the resource
surfaces across languages, so a method that exists in one SDK and not another
fails the build.

## Wiring it into an existing project

```
npx @axonpush/wizard
```

This installs [`skills`](https://github.com/axonpush/skills) into your coding
agent. The agent then reads your project, picks the right integration,
provisions credentials, and writes `.env`. It finishes by publishing a test
event and reading it back, so you find out immediately if the path is wrong.

Works in Claude Code, Cursor, Codex, and around fifty other agents.

## Links

- [axonpush.xyz](https://axonpush.xyz)
- [Dashboard](https://app.axonpush.xyz)
- [Documentation](https://axonpush.xyz/docs)
