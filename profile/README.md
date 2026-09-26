# axonpush

See your app, your AI calls, and your errors in one trace.

axonpush brings your OpenTelemetry and Sentry data together with your model and
tool calls, so a production failure and the AI call behind it sit on the same
run. Add inline controls at the gateway when you want to block, redact, or cap.

## Get your traffic in

Three ingest paths. Use any one, or all three on the same trace.

- **Gateway** — point your OpenAI or Anthropic client's base URL at the axonpush
  gateway and add your key. Every model and tool call is captured, and can be
  governed inline. No SDK, no code changes beyond the base URL.
- **OpenTelemetry** — send OTLP from your existing exporter (`/v1/traces`,
  `/v1/logs`). Your app, database, and queue spans land next to the model calls.
- **Sentry** — point a Sentry SDK at an axonpush DSN. Exceptions group into
  issues, with user feedback, on the same trace as the calls that caused them.

```python
# Gateway: one base-URL change
from openai import OpenAI

client = OpenAI(
    base_url="https://api.axonpush.xyz/gw/openai/v1",
    default_headers={"x-axonpush-api-key": "ak_..."},
)
```

## What you get

- **Traces** — model calls, tool calls, and agent handoffs in one run, with a
  plain-language summary of what happened and where it broke.
- **Issues** — errors grouped by fingerprint, with triage, on the same trace.
- **Analytics** — slice usage by model, provider, or your own dimensions
  (tenant, plan, workflow); drag the latency heatmap to explain a slow cohort.
- **Controls** — moderation rules, request-governance and spend policies,
  enforced inline before a call reaches the provider.
- **Proof** — an immutable, exportable decision trail of every allow, redact,
  block, and flag.

## SDKs

| Package | Registry | Install |
|---|---|---|
| [`@axonpush/sdk`](https://www.npmjs.com/package/@axonpush/sdk) | npm | `npm install @axonpush/sdk` |
| [`axonpush`](https://pypi.org/project/axonpush/) | PyPI | `pip install axonpush` |
| `AxonPush` | NuGet | `dotnet add package AxonPush` |

All three live in [`sdks`](https://github.com/axonpush/sdks) and generate from
one OpenAPI contract, with cross-language parity checked in CI.

## Instrument an existing project

```
npx @axonpush/wizard
```

This installs [`skills`](https://github.com/axonpush/skills) into your coding
agent. The agent reads your project, wires the gateway, OpenTelemetry, and
Sentry so everything correlates on one trace, sets the environment safely, then
publishes a test event and reads it back, so you find out immediately if the
path is wrong. Works in Claude Code, Cursor, Codex, and around fifty other
agents.

## Links

- [axonpush.xyz](https://axonpush.xyz)
- [Dashboard](https://app.axonpush.xyz)
- [Documentation](https://docs.axonpush.xyz)
