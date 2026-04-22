# openapi

The canonical [OpenAPI 3.1](https://spec.openapis.org/oas/v3.1.0) spec for [**AIgateway**](https://aigateway.sh) — one API in front of 150+ AI models.

- **Live spec:** [`aigateway.sh/openapi.json`](https://aigateway.sh/openapi.json)
- **GitHub mirror:** [`openapi.json`](./openapi.json) in this repo
- **Base URL:** `https://api.aigateway.sh`
- **OpenAI-compatible subset:** `POST /v1/chat/completions`, `POST /v1/embeddings`

## What's in the spec

The spec documents the full AIgateway surface:

- **Inference** — `/v1/chat/completions`, `/v1/embeddings` (OpenAI-compatible)
- **Jobs** — async long-running tasks with idempotency and webhooks
- **Sub-accounts** — mint scoped API keys with spend caps and tags
- **Evals & replays** — snapshot a trace, re-run against another model
- **Usage & billing** — pull per-key usage for invoicing
- **Models** — discover what's routable right now

## Generate a client

```bash
# TypeScript (openapi-typescript)
npx openapi-typescript https://aigateway.sh/openapi.json -o ./aigateway.d.ts

# Python (openapi-python-client)
openapi-python-client generate --url https://aigateway.sh/openapi.json

# Go / Rust / Java / anything else
# Use https://openapi-generator.tech/ with:
#   openapi-generator-cli generate -i https://aigateway.sh/openapi.json -g <lang>
```

## Import into an API client

- **Postman** — `File → Import` → paste `https://aigateway.sh/openapi.json`
- **Insomnia** — `Import → From URL` → paste the same URL
- **Hoppscotch / Bruno / Paw / HTTPie Desktop** — all accept OpenAPI 3.1

## First-party SDKs

If you'd rather not generate a client, we ship hand-written SDKs for the most common languages — they use the same API described by this spec:

- **Node / TS** — [`aigateway-js`](https://www.npmjs.com/package/aigateway-js) · [source](https://github.com/aigateway-sh/sdk-node)
- **Python** — [`aigateway-py`](https://pypi.org/project/aigateway-py/) · [source](https://github.com/aigateway-sh/sdk-python)
- **CLI** — [`aigateway-cli`](https://www.npmjs.com/package/aigateway-cli) · [source](https://github.com/aigateway-sh/cli)

## Feeding this to a coding agent

The spec pairs nicely with our [`llms.txt` capability map](https://github.com/aigateway-sh/llms-txt):

```
https://aigateway.sh/openapi.json    → machine-readable contract
https://aigateway.sh/llms.txt        → human+agent readable capability map
https://aigateway.sh/llms-full.txt   → full model catalog with pricing
https://api.aigateway.sh/mcp         → MCP tools (every primitive, agent-callable)
```

Agents that accept OpenAPI at config time (Claude Code custom tools, OpenAI Assistants, LangChain, LlamaIndex, Mastra) can import this spec directly.

## Versioning

- The spec is **backward-compatible within a major version**.
- Breaking changes cut a new `/v2` base path — `/v1` routes keep working for ≥12 months.
- Subscribe to changes: [github.com/aigateway-sh/openapi/releases](https://github.com/aigateway-sh/openapi/releases) or watch this repo.

## Contributing

Found a drift between docs and runtime behavior? [Open an issue](https://github.com/aigateway-sh/openapi/issues) with a repro. Spec fixes land here and on `aigateway.sh/openapi.json` together.

## License

MIT. Copy, cite, generate clients freely.
