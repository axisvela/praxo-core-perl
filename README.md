# PRAXO-CORE for Perl

PRAXO-CORE is an embeddable, MIT-licensed agent framework. This distribution is its native Perl Core: an agent loop with tool registration and dispatch, policy hooks, typed events, memory, checkpoints, context budgets, middleware, OTel and Harmovela sinks, MCP, retriever and synchronous delegation seams, JSON Schema validation, and plugin manifest parsing.

## At a glance

| Field | Value |
| --- | --- |
| Package | `Praxo::Core` |
| Registry | [CPAN (MetaCPAN index)](https://metacpan.org/dist/Praxo-Core) |
| Install | `cpanm Praxo::Core` |
| Source version | `0.4.0` |
| Published version | `0.4.0` |
| Source tag | `perl/v0.4.0` |
| Tier | Core |
| Contract | `SPEC_VERSION` `0.2.0` |
| Documentation | https://axisvela.github.io/praxo-core/languages/perl/ |
| License | MIT |

## Highlights

- OpenAI-compatible model: native
- Anthropic model: native
- Gemini model: native
- MCP client: native
- Harmovela sink: native
- OpenTelemetry sink: native (transport seam)
- Subagent delegation: native (synchronous seam)
- Retriever: native

## Quick start

Install the published package:

```bash
cpanm Praxo::Core
```

```perl
use lib 'language/perl/lib';
use Praxo::Models ();
use Praxo::Agent ();

my $model = Praxo::Agent::StaticModel->new('hello');
my $options = Praxo::Agent::AgentOptions->new($model);
my $result = Praxo::Agent::run_agent(
    $options,
    Praxo::Models::session(id => 'demo'),
    'hello',
);
print $result->{output};
```

See the [full Perl README](language/perl/README.md) for complete installation, build, and verification commands.

## What's included

| Capability | Status | Detail |
| --- | --- | --- |
| OpenAI-compatible model | native | `Praxo::Adapters::OpenAICompatible` |
| Anthropic model | native | `Praxo::Adapters::Anthropic` |
| Gemini model | native | `Praxo::Adapters::Gemini` |
| MCP client | native | `Praxo::Adapters::MCP`; stdio, plus `Praxo::Adapters::MCPHTTP` for Streamable HTTP 2025-03-26 |
| Harmovela sink | native | `Praxo::Adapters::Harmovela` |
| OpenTelemetry sink | native (transport seam) | `Praxo::Adapters::Otel`; caller supplies transport |
| Subagent delegation | native (synchronous seam) | `subagent_run`; no asynchronous manager |
| Retriever | native | `document`, `func_retriever`, `retrieve_documents` |

## Examples

Runnable examples live under [`language/perl/examples`](language/perl/examples).

| Example | What it shows |
| --- | --- |
| [checkpoint](language/perl/examples/checkpoint) | This example uses the Perl Core checkpoint allowlist for a registered payload round trip. |
| [event-sink](language/perl/examples/event-sink) | This example uses Perl Core sink composition to fan out events and filter the tool-only stream. |
| [identity-policy](language/perl/examples/identity-policy) | This example binds a trusted principal to policy decisions and rejects missing, role-mismatched, and tenant-mismatched actions. |
| [mcp](language/perl/examples/mcp) | This example uses a caller-owned in-process transport with the Perl MCP client. |
| [provider-fallback](language/perl/examples/provider-fallback) | This example calls a fallback only after the primary fails and preserves the primary failure when both fail. |
| [retry](language/perl/examples/retry) | This example retries a transient failure with a bounded attempt count and keeps the exhausted failure state. |
| [service](language/perl/examples/service) | This example defines a transport-neutral request handler with health, principal, and run cases. |
| [session-checkpoint](language/perl/examples/session-checkpoint) | This example saves and restores a conversation history across two agent turns. It uses the Core allowlist for payload encoding and a teaching in-memory payload. |
| [streaming](language/perl/examples/streaming) | This example accumulates streamed chunks and checks that they reconstruct the final output. |
| [structured-output](language/perl/examples/structured-output) | This example validates a final JSON answer against a schema and rejects invalid output. |

## Verify

Run the checks from `language/perl`:

```bash
perl language/perl/conformance/run.pl
perl language/perl/api-snapshot.pl --check
perl language/perl/tests/run.pl
```

This mirror contains the language source and the shared `spec/` vectors, so the implementation can be built and tested here. See [`language/perl/README.md`](language/perl/README.md) for the exact commands. The monorepo CI runs conformance, API snapshot, and native tests for this implementation.

## Community

- X: <https://x.com/axisvela>
- Weibo: <https://weibo.com/u/1936025761>

## Repository layout

- `language/perl/` — implementation source, tests, API snapshot, and examples
- `spec/` — shared contract, vectors, and parity inventories
- `LICENSE` — MIT license

## Canonical source

- Canonical source: https://github.com/axisvela/praxo-core/tree/main/language/perl
- Registry introduction: `language/perl/REGISTRY.md`
- Machine-readable entry: `language/perl/llms.txt` and `language/perl/llms.md`
- Mirror repository: https://github.com/axisvela/praxo-core-perl
- Release index: https://axisvela.github.io/praxo-core/languages/registry-status/

This repository is a discovery mirror of the canonical Perl source. The monorepo remains the source of truth and the release workflow source.

PRAXO-CORE is not a hosted model, workflow engine, identity provider, or safety controller. Do not infer exactly-once execution, complete sandbox isolation, production security certification, live-provider behavior, or physical safety from this package.

MIT licensed.
