# Supported AI Model Providers

The IDS assistant is **model-agnostic**. Conversation handling runs through the Convex Agent, which
is built on the Vercel AI SDK, so the underlying large language model can be swapped without changing
application logic. This lets each organization pick the provider that best fits its cost, latency,
and quality needs.

## Providers

| Provider | Company | Example models | Integration |
| --- | --- | --- | --- |
| **ChatGPT** | OpenAI | GPT-4o, GPT-4.1, o-series | `@ai-sdk/openai` — currently wired as the default. |
| **Grok** | xAI | Grok 2, Grok 3 | `@ai-sdk/xai` |
| **Claude** | Anthropic | Claude Sonnet, Claude Opus | `@ai-sdk/anthropic` |
| **Gemini** | Google | Gemini 1.5 / 2.0 | `@ai-sdk/google` |

Additional providers supported by the Vercel AI SDK (Mistral, Cohere, Groq-hosted open models, and
others) can be added the same way.

## How it works

- **One abstraction, many models** — Because every provider is accessed through the AI SDK's common
  interface, switching from ChatGPT to Grok (or any other provider) is a configuration change, not a
  rewrite.
- **Retrieval-augmented answers** — Whichever model is selected, responses are grounded in the
  organization's own knowledge base via the Convex RAG component, so answers stay accurate and
  on-brand.
- **Per-organization keys** — Provider API keys are stored securely, per organization, in AWS
  Secrets Manager through the plugins system rather than as shared global secrets.

## Configuration

Select the active provider for a deployment and supply the matching credentials. Representative
environment variables:

| Variable | Provider |
| --- | --- |
| `OPENAI_API_KEY` | ChatGPT (OpenAI) |
| `XAI_API_KEY` | Grok (xAI) |
| `ANTHROPIC_API_KEY` | Claude (Anthropic) |
| `GOOGLE_GENERATIVE_AI_API_KEY` | Gemini (Google) |

> The default configuration ships with OpenAI (ChatGPT). Enabling another provider only requires
> installing its AI SDK adapter and providing the corresponding API key.
