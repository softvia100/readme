<div align="center">

<br />

```
  ██████╗ ██████╗ ███████╗███╗   ██╗ █████╗  ██████╗ ███████╗███╗   ██╗████████╗
 ██╔═══██╗██╔══██╗██╔════╝████╗  ██║██╔══██╗██╔════╝ ██╔════╝████╗  ██║╚══██╔══╝
 ██║   ██║██████╔╝█████╗  ██╔██╗ ██║███████║██║  ███╗█████╗  ██╔██╗ ██║   ██║   
 ██║   ██║██╔═══╝ ██╔══╝  ██║╚██╗██║██╔══██║██║   ██║██╔══╝  ██║╚██╗██║   ██║   
 ╚██████╔╝██║     ███████╗██║ ╚████║██║  ██║╚██████╔╝███████╗██║ ╚████║   ██║   
  ╚═════╝ ╚═╝     ╚══════╝╚═╝  ╚═══╝╚═╝  ╚═╝ ╚═════╝ ╚══════╝╚═╝  ╚═══╝   ╚═╝   
```

**The open-source operating system for AI agents.**

*Not a framework. Not a library. Infrastructure.*

<br />

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-3D5AFE.svg?style=for-the-badge)](https://opensource.org/licenses/Apache-2.0)
[![Version](https://img.shields.io/badge/version-0.1.0-00E5FF.svg?style=for-the-badge)](https://github.com/openagent/openagent/releases)
[![Go Version](https://img.shields.io/badge/Go-1.23+-00ADD8?style=for-the-badge&logo=go)](https://golang.org)
[![Python Version](https://img.shields.io/badge/Python-3.12+-3776AB?style=for-the-badge&logo=python)](https://python.org)
[![Discord](https://img.shields.io/badge/Discord-Join_Community-5865F2?style=for-the-badge&logo=discord)](https://discord.gg/openagent)
[![CI](https://img.shields.io/github/actions/workflow/status/openagent/openagent/ci.yml?branch=main&style=for-the-badge&label=CI)](https://github.com/openagent/openagent/actions)

<br />

[**Documentation**](https://docs.openagent.io) · [**Quick Start**](#-quick-start) · [**Examples**](./examples) · [**Discord**](https://discord.gg/openagent) · [**Changelog**](./CHANGELOG.md)

<br />

</div>

---

## What is OpenAgent?

OpenAgent is a **production-grade, distributed runtime** for AI agents. It lets you define agents in YAML, deploy them to any infrastructure, route across any model provider, and observe every token, tool call, and dollar spent — all with a single CLI.

```bash
npm install -g @openagent/cli
openagent init my-agent --template research
openagent dev agent.yaml
```

That's it. You're running a production-quality AI agent with full observability, automatic failover, and cost tracking in under 5 minutes.

---

## Why OpenAgent?

Every team building AI agents solves the same three problems from scratch:

| Problem | What teams do today | What OpenAgent does |
|---|---|---|
| **Provider lock-in** | Hard-code to OpenAI, panic when pricing changes | Unified abstraction layer — switch providers in one config line |
| **No production runtime** | Wrap LangChain in custom retry logic, hope it works | Distributed execution engine with checkpointing, failover, and crash recovery |
| **Zero observability** | `print()` statements and guesswork | Full traces, token-level cost attribution, debug replay |

OpenAgent is the substrate every agent application runs on — the same way Kubernetes is the substrate every cloud application runs on. It is not a framework you import. It is infrastructure you deploy.

---

## Features

<table>
<tr>
<td width="50%">

### 🔀 Model Abstraction Layer
Route across **11+ providers** with a single unified interface. Automatic failover, circuit breakers, and real-time health tracking. Switch from GPT-4o to Claude to Llama with a one-line config change.

```yaml
model:
  provider: anthropic
  name: claude-3-7-sonnet-20250219
routing:
  fallback:
    - openai/gpt-4o
    - groq/llama-3.1-70b-versatile
  cost_limit_per_run: 1.00
```

</td>
<td width="50%">

### ⚡ Distributed Runtime
Workers are stateless. State is persisted. A crashed worker is recovered in under 30 seconds — the task resumes from the last checkpoint with no duplicated side effects.

```bash
$ openagent cluster status
Workers:  12 active  (4 busy, 8 idle)
Queue:    3 pending tasks
Uptime:   99.97% (30d)
```

</td>
</tr>
<tr>
<td width="50%">

### 🧠 Memory Architecture
Three-tier memory: **session** (in-context), **vector** (long-term semantic, pgvector), and **graph** (relational entity store). All configured in YAML, managed automatically.

```yaml
memory:
  vector:
    backend: pgvector
    top_k: 5
  graph:
    backend: kuzu
    enabled: true
```

</td>
<td width="50%">

### 🔧 Tool Execution Engine
50+ built-in tools. Sandboxed execution (process isolation, Docker containers, WebAssembly). Per-tool resource limits, network allowlists, and idempotency guarantees.

```bash
$ openagent tool test web_search \
  --input '{"query": "AI agent runtime"}'
✓ Executed in 0.83s — 10 results
```

</td>
</tr>
<tr>
<td width="50%">

### 📊 Full-Stack Observability
Every agent run is a root OpenTelemetry span. Every LLM call, tool execution, and memory operation is a child span. Real-time token usage, cost per run, and debug replay.

```bash
$ openagent trace show run_abc123
Run: 42.3s | $0.087 | 17,451 tokens

├─ Step 1 — LLM call          2.1s  $0.012
│   └─ web_search              1.2s
├─ Step 2 — LLM call          3.8s  $0.041
│   ├─ read_url                2.1s
│   └─ read_url                1.9s
└─ Step 3 — LLM call          4.2s  $0.034
```

</td>
<td width="50%">

### 🔒 Enterprise Ready
RBAC, SSO (OIDC), Vault integration, mTLS everywhere, audit logs (cryptographically signed), on-premises deployment, air-gap support. SOC2 architecture designed in from day one.

```bash
$ openagent secrets set prod-db-url \
  --from-env DATABASE_URL
✓ Secret stored (Vault backend)

$ openagent agent list --namespace prod
NAME              STATUS    LAST RUN
research-agent    IDLE      2 min ago
support-agent     RUNNING   now
```

</td>
</tr>
</table>

---

## Quick Start

### Install

```bash
# npm (recommended)
npm install -g @openagent/cli

# Homebrew
brew install openagent/tap/openagent

# Linux (apt)
sudo apt install openagent

# Verify
openagent --version
openagent doctor
```

### Your first agent in 5 minutes

**Step 1 — Initialize**

```bash
openagent login --api-key $OPENAGENT_API_KEY
openagent init research-agent \
  --template research \
  --model anthropic/claude-3-7-sonnet-20250219 \
  --tools web_search,read_url
```

This creates `agent.yaml`:

```yaml
apiVersion: openagent/v1
kind: Agent
metadata:
  name: research-agent
  version: "1.0.0"

spec:
  model:
    provider: anthropic
    name: claude-3-7-sonnet-20250219

  routing:
    fallback: [openai/gpt-4o, groq/llama-3.1-70b-versatile]
    cost_limit_per_run: 1.00

  system_prompt: |
    You are a meticulous research analyst. Search the web,
    read sources, and synthesize findings into clear reports.

  tools: [web_search, read_url, write_file]

  memory:
    vector:
      backend: pgvector
      top_k: 5

  lifecycle:
    timeout_seconds: 300
    max_iterations: 20
```

**Step 2 — Develop locally**

```bash
openagent dev agent.yaml \
  --model groq/llama-3.1-8b-instant \   # cheap model for dev
  --input '{"query": "AI agent runtimes 2026"}'
```

**Step 3 — Run it**

```bash
openagent ask "What are the best open-source agent frameworks?" \
  --agent research-agent
```

**Step 4 — Deploy to production**

```bash
openagent deploy agent.yaml --namespace production --wait
openagent agent list --namespace production
```

**Step 5 — Observe**

```bash
openagent stats research-agent --watch
openagent cost --period 7d --group-by model
openagent trace show $(openagent trace list research-agent --output json | jq -r 'first | .run_id')
```

---

## Supported Model Providers

| Provider | Status | Models |
|---|---|---|
| **Anthropic** | ✅ Stable | Claude 3.7, Claude 3.5, Claude 3 Haiku |
| **OpenAI** | ✅ Stable | GPT-4o, GPT-4o-mini, GPT-4 Turbo |
| **Groq** | ✅ Stable | Llama 3.1 70B/8B, Mixtral, Gemma |
| **Ollama** | ✅ Stable | Any locally-hosted model |
| **Google Gemini** | 🔜 v0.2 | Gemini 2.0, Gemini 1.5 Pro |
| **Cohere** | 🔜 v0.2 | Command R+, Command R |
| **Mistral** | 🔜 v0.2 | Mistral Large, Mistral Small |
| **Azure OpenAI** | 🔜 v0.3 | GPT-4o, GPT-4 (via Azure endpoints) |
| **AWS Bedrock** | 🔜 v0.3 | Claude, Llama, Titan |
| **vLLM** | 🔜 v0.3 | Any model served via vLLM |
| **llama.cpp** | 🔜 v0.3 | Any GGUF model |

Adding a new provider = implementing one Python class. [Contribution guide →](./CONTRIBUTING.md#adding-a-provider)

---

## Architecture

```
┌──────────────────────────────────────────────────────┐
│                  CLI  ·  API  ·  Dashboard            │
└────────────────────────┬─────────────────────────────┘
                         │
┌────────────────────────▼─────────────────────────────┐
│                    API Gateway                        │
│           REST · WebSocket · gRPC · Auth              │
└────────────────────────┬─────────────────────────────┘
                         │
┌────────────────────────▼─────────────────────────────┐
│                   Control Plane                       │
│          Agent Controller · Scheduler · Router        │
└───────┬────────────────────────────────┬─────────────┘
        │                                │
┌───────▼──────────┐          ┌──────────▼──────────────┐
│   Worker Pool    │          │    Persistence Layer     │
│  (stateless, N)  │          │  PostgreSQL · Redis      │
│                  │          │  etcd · NATS JetStream   │
│  ┌────────────┐  │          └─────────────────────────┘
│  │  LLM Call  │  │
│  │  Tool Exec │  │          ┌─────────────────────────┐
│  │  Memory R/W│  │          │  Observability Pipeline  │
│  └────────────┘  │          │  OTel · Prometheus · Loki│
└──────────────────┘          └─────────────────────────┘
```

Every worker is stateless. State lives in PostgreSQL. A worker can crash at any point — the task is reclaimed, state is rehydrated from the last checkpoint, and execution continues. No runs are lost.

**Full architecture documentation:** [`TDD.md`](./TDD.md)

---

## CLI Reference

OpenAgent is entirely CLI-driven. Every operation available in the dashboard is available in the CLI.

```bash
# Agent lifecycle
openagent init <name>          # Scaffold a new agent
openagent deploy <file>        # Deploy to namespace
openagent agent list           # List deployed agents
openagent agent validate <file># Validate YAML schema

# Running agents
openagent run <agent>          # Trigger a run
openagent ask "<question>"     # One-shot query
openagent dev <file>           # Local dev with hot reload
openagent batch submit <agent> # Submit batch job

# Observability
openagent logs <agent>         # Stream logs
openagent trace show <run-id>  # Full execution trace
openagent stats                # Runtime statistics
openagent cost --period 7d     # Cost breakdown

# Model routing
openagent routing show <agent> # Current routing config
openagent routing set priority # Change routing strategy
openagent routing test <agent> # Simulate routing decisions

# Memory
openagent memory show <agent>  # Memory summary
openagent memory search "<q>"  # Semantic memory search
openagent memory clear <agent> # Clear memory tiers

# Tools
openagent tools list           # List registered tools
openagent tool test <name>     # Test a tool directly
openagent tool create <name>   # Scaffold a new tool

# Cluster
openagent cluster init         # Initialize cluster
openagent cluster status       # Cluster health
openagent cluster scale        # Scale worker count
```

**Full CLI reference:** [`CLI.md`](./CLI.md)

---

## Deployment

### Local (Docker Compose)

```bash
git clone https://github.com/openagent/openagent
cd openagent
make dev        # starts full stack
```

Starts: API Gateway, Controller, 2 Workers, PostgreSQL+pgvector, Redis, NATS, etcd.

### Kubernetes (Helm)

```bash
helm repo add openagent https://charts.openagent.io
helm repo update

helm install openagent openagent/openagent \
  --namespace openagent \
  --create-namespace \
  --set worker.replicaCount=5 \
  --set postgresql.primary.persistence.size=50Gi
```

**Production-grade Helm chart** with HPA, PodDisruptionBudget, NetworkPolicy, and horizontal autoscaling on queue depth.

### Kubernetes (kubectl)

```bash
kubectl apply -f https://raw.githubusercontent.com/openagent/openagent/main/deployments/k8s/install.yaml
```

---

## Examples

Ready-to-run agent definitions in [`/examples`](./examples):

| Agent | Description | Tools |
|---|---|---|
| [`research-analyst`](./examples/research-analyst.yaml) | Web research → structured reports | web_search, read_url, write_file |
| [`customer-support`](./examples/customer-support.yaml) | Tier-1 support with escalation | lookup_order, send_email, escalate |
| [`code-reviewer`](./examples/code-reviewer.yaml) | PR review against style guide | read_file, bash, write_file |
| [`data-extractor`](./examples/data-extractor.yaml) | Structured extraction from docs | read_file, python_exec |
| [`sql-analyst`](./examples/sql-analyst.yaml) | Natural language → SQL queries | query_database, python_exec |
| [`changelog-writer`](./examples/changelog-writer.yaml) | Git commits → release notes | bash, write_file |

```bash
# Run any example in 60 seconds
openagent init research-analyst \
  --from examples/research-analyst.yaml

openagent dev agent.yaml \
  --input '{"query": "What are the top AI papers this week?"}'
```

---

## Observability

OpenAgent ships full observability out of the box. No third-party SaaS required.

**Traces (OpenTelemetry → Jaeger / Grafana Tempo)**

Every run is a root span. Every LLM call, tool execution, and memory operation is a child span with token counts, cost attribution, and latency.

**Metrics (Prometheus)**

```
openagent_agent_runs_total          # Total runs by agent, status
openagent_llm_cost_usd_total        # Cost by provider, model, agent
openagent_tool_duration_seconds     # Tool execution latency
openagent_queue_depth               # Per-priority queue depth
openagent_worker_active_tasks       # Worker utilization
```

**Logs (structured JSON → Loki / Elasticsearch)**

```json
{
  "timestamp": "2026-03-03T10:00:01Z",
  "level": "info",
  "event": "tool_call_completed",
  "run_id": "run_abc123",
  "tool": "web_search",
  "duration_ms": 820,
  "success": true
}
```

**Cost tracking**

```bash
$ openagent cost --period 30d --group-by model

MODEL                              RUNS    TOKENS        COST
anthropic/claude-3-7-sonnet        1,240   21,552,000    $156.40
openai/gpt-4o-mini                 15,200  16,600,000     $62.10
groq/llama-3.1-70b-versatile        6,800   5,040,000     $18.90
────────────────────────────────────────────────────────────────
TOTAL                              23,240  43,192,000    $237.40
```

---

## Comparison

|  | OpenAgent | LangChain | CrewAI | OpenAI Assistants |
|---|---|---|---|---|
| **Type** | Distributed Runtime | Python Library | Framework | Managed API |
| **Production ready** | ✅ | ❌ | ⚠️ | ⚠️ Lock-in |
| **Model agnostic** | ✅ | ⚠️ Leaky | ⚠️ OpenAI-centric | ❌ OpenAI only |
| **Distributed execution** | ✅ | ❌ | ❌ | ❌ |
| **State persistence** | ✅ PostgreSQL | ❌ In-memory | ❌ In-memory | ✅ Managed |
| **Crash recovery** | ✅ | ❌ | ❌ | ✅ Managed |
| **Full observability** | ✅ Built-in | ⚠️ LangSmith (paid) | ❌ | ⚠️ Basic |
| **On-premises** | ✅ | ✅ (no runtime) | ✅ (no runtime) | ❌ |
| **Cost tracking** | ✅ Real-time | ⚠️ LangSmith (paid) | ❌ | ⚠️ Basic |
| **Kubernetes native** | ✅ | ❌ | ❌ | ❌ |
| **Apache 2.0** | ✅ | ✅ | ✅ | ❌ |

The distinction matters: LangChain is a library you import. OpenAI Assistants is a SaaS you depend on. OpenAgent is infrastructure you own.

---

## Contributing

OpenAgent is Apache 2.0 and actively maintained. Contributions are welcome and deeply appreciated.

### Ways to contribute

- **Report bugs** — [Open an issue](https://github.com/openagent/openagent/issues/new?template=bug_report.md)
- **Request features** — [Start a discussion](https://github.com/openagent/openagent/discussions)
- **Add a model provider** — [Contribution guide](./CONTRIBUTING.md#adding-a-provider)
- **Add a built-in tool** — [Tool development guide](./CONTRIBUTING.md#adding-a-tool)
- **Improve docs** — Every docs page has an "Edit on GitHub" link
- **Share examples** — Submit to [`/examples`](./examples) or the [Showcase](https://openagent.io/showcase)

### Development setup

```bash
# Prerequisites: Go 1.23+, Python 3.12+, Docker, Node.js 18+

git clone https://github.com/openagent/openagent
cd openagent

# Install all dependencies
make install

# Start infrastructure (PostgreSQL, Redis, NATS, etcd)
make dev-infra

# Run all tests
make test

# Run end-to-end tests
make e2e

# Lint and format
make lint
make fmt
```

### Architecture decision records

All significant architectural decisions are documented in [`/docs/adr`](./docs/adr). If you want to make a significant change, open an ADR PR first.

### Code of Conduct

We follow the [Contributor Covenant](./CODE_OF_CONDUCT.md). Be excellent to each other.

---

## Roadmap

| Version | Target | Highlights |
|---|---|---|
| **v0.1** | ✅ March 2026 | Core runtime, 4 providers, CLI, Docker Compose |
| **v0.2** | Q2 2026 | Distributed execution engine, Kubernetes Helm chart, web dashboard, 8 providers |
| **v0.3** | Q3 2026 | Enterprise RBAC + Vault + audit logs, batch API, 11 providers, SOC2 Type I |
| **v0.4** | Q4 2026 | Multi-agent orchestration, plugin marketplace, VS Code extension |
| **v1.0** | Q1 2027 | Visual agent builder, agent-to-agent protocol, federated clusters |

Track progress on the [public roadmap →](https://github.com/openagent/openagent/projects/1)

---

## License

OpenAgent core is **Apache License 2.0**. This means:

- ✅ Free to use commercially
- ✅ Free to modify and distribute
- ✅ Explicit patent grants (unlike MIT)
- ✅ Compatible with enterprise legal review

The Enterprise Edition (RBAC, Vault, SSO, audit logs, on-premises support) is commercially licensed. [Details →](https://openagent.io/enterprise)

---

## Community

| Channel | Purpose |
|---|---|
| [**Discord**](https://discord.gg/openagent) | Questions, help, announcements, community showcase |
| [**GitHub Discussions**](https://github.com/openagent/openagent/discussions) | Architecture proposals, feature requests, RFCs |
| [**GitHub Issues**](https://github.com/openagent/openagent/issues) | Bug reports, confirmed feature requests |
| [**Blog**](https://openagent.io/blog) | Deep-dives, release announcements, case studies |
| [**Twitter / X**](https://twitter.com/openagent) | Updates, community highlights |

---

## Security

Security issues must be reported privately. Do **not** open a public GitHub issue for security vulnerabilities.

**Email:** security@openagent.io  
**PGP key:** [keybase.io/openagent](https://keybase.io/openagent)  
**Bug bounty:** [hackerone.com/openagent](https://hackerone.com/openagent)  
**Response SLA:** Critical vulnerabilities acknowledged within 24 hours, patched within 48 hours.

See [`SECURITY.md`](./SECURITY.md) for the full disclosure policy.

---

<div align="center">

<br />

**Built with obsession by engineers who got tired of solving the same infrastructure problems over and over.**

<br />

If OpenAgent saves you time, [give it a star ⭐](https://github.com/openagent/openagent) — it helps more engineers find it.

<br />

[openagent.io](https://openagent.io) · [docs.openagent.io](https://docs.openagent.io) · [discord.gg/openagent](https://discord.gg/openagent)

<br />

</div>
