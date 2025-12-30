# Opencode Research Extension

Extension for [opencode](https://opencode.ai/) providing research capabilities with multiple web search and GitHub tools.

Uses parallel agent logic from [opencode-parallel-agents](https://github.com/aptdnfapt/opencode-parallel-agents).

## Tools

| Tool | Description | Setup |
|------|-------------|-------|
| web-search-prime | High-quality web search with domain filters | Requires [ZAI subscription](https://z.ai/subscribe) |
| zread | GitHub repo search, docs, and file reading | Requires [ZAI subscription](https://z.ai/subscribe) |
| context7 | Free OSS documentation search | No setup required |
| searxng | Open-source web search engine | Self-hosted SearXNG instance |
| qwen-web-search | **2000 free requests/day** per account | See [qwen-code-oai-proxy](https://github.com/aptdnfapt/qwen-code-oai-proxy) |
| exa | Powerful AI-powered web search | Free on opencode, just enable |

## Installation

```bash
git clone https://github.com/your-username/opencode-research-extension.git
cd opencode-research-extension
```

## Setup Environment Variables

Choose the tools you want to enable and set their environment variables.

### web-search-prime & zread

[ZAI](https://z.ai/subscribe) provides both web-search-prime and zread for researching GitHub repositories. Get your API key from the subscription dashboard.

```bash
export ZAI_KEY="your_zai_api_key_here"
```

### searxng

SearXNG is an open-source metasearch engine. You need to run your own instance or use a public one.

```bash
export SEARXNG_URL="https://your-searxng-instance.com"
```

### qwen-web-search (FREE - 2000 requests/day)

This is completely free! Each account gets 2000 web search requests per day. Setup guide at [qwen-code-oai-proxy](https://github.com/aptdnfapt/qwen-code-oai-proxy).

```bash
export QWEN_PROXY_URL="https://your-qwen-proxy-url.com"
export QWEN_KEY="your_qwen_api_key_here"
```

### context7

Free OSS documentation search. No setup required - it works out of the box in `opencode.jsonc`.

### exa (FREE on opencode)

Exa is free when using opencode. Just enable it:

```bash
export OPENCODE_ENABLE_EXA="true"
```

## How to Use

### Step 1: Launch Opencode

```bash
opencode
```

### Step 2: Select Research Agent

Press tab multiple times until you see **"Research agent"** in the agent selector.

### Step 3: Provide Detailed Research Instructions

Tell the Research agent exactly what you want to research. Be specific and detailed.

**Example prompts:**

Finding OSS projects:
```
Find GitHub repos for building modern web apps with React and Next.js that have good documentation, active maintenance, and at least 1k stars. I want to compare them for best practices and architecture.  use 8 agents for this-.
```

 researching a topic:
```
Research the state of AI agents in 2025. I want to know about the latest developments, key players, common architectures, and open-source projects. Focus on practical implementations and code examples.  use 8 agents for this.-
```

Comparing technologies:
```
Compare PostgreSQL vs MongoDB for event-driven microservices. Look for performance benchmarks, scalability considerations, real-world use cases, and community opinions. use 8 agents for this .
```

### Step 4: Specify Number of Agents

Tell the agent how many parallel subagents you want to run. More agents = faster but more API calls.

```
Use 5 agents for this research
```

```
Run 8 parallel searches
```

**Typical recommendations:**
- Quick research: 2-4 agents
- Moderate research: 5-8 agents
- Deep research: 10+ agents

### Step 5: Let It Work

The agent will:

1. **Think & Plan** - It first analyzes your request and determines the best approach
2. **Generate Search Strategy** - Divides the research into logical angles (e.g., pros, cons, tutorials, benchmarks, real-world examples)
3. **Launch Parallel Agents** - Spawns X webresearch subagents that work simultaneously
4. **Assign Specific Tasks** - Each subagent gets a focused task with specific keywords and source types (blogs, docs, GitHub, forums, etc.)
5. **Collect & Synthesize** - Gathers all results and combines them into a comprehensive summary
6. **Provide Sources** - Includes all relevant links so you can dive deeper

### Timing

Expect **3-4 minutes** for the complete research process, depending on:
- Number of agents running
- Complexity of the topic
- Model you're using (same model controls both primary and subagents)
- Network latency for web searches

## Customization

### Changing the Model

To use a different AI model for research, check the [opencode-parallel-agents](https://github.com/aptdnfapt/opencode-parallel-agents) repository. You may need to:
- Edit the markdown files in `.opencode/agent/` directory
- Configure model settings in opencode.jsonc or your opencode config

### Modifying Agent Behavior

The agent instructions are in:
- `.opencode/agent/research.md` - Primary research orchestrator
- `.opencode/agent/webresearch.md` - Web search subagent

Edit these files to customize prompts, add tools, or change behavior.

## Workflow Diagram

```
┌─────────────────────────────────────────────────────────────┐
│  YOU: Provide detailed research request + agent count       │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│  Research Agent (Primary)                                   │
│  - Analyzes your request                                     │
│  - Planning: divides into focused topics/angles             │
│  - Strategy: determines search queries and sources          │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼ (launches X parallel agents)
    ┌────────────────┼────────────────┬────────────────┐
    ▼                ▼                ▼                ▼
┌────────┐      ┌────────┐      ┌────────┐      ┌────────┐
│ Agent 1│      │ Agent 2│      │ Agent 3│  ...   │ Agent X│
│ topic A│      │ topic B│      │ topic C│        │ topic Z│
└────┬───┘      └────┬───┘      └────┬───┘      └────┬───┘
     │               │               │               │
     └───────────────┴───────────────┴───────────────┘
                     │
                     ▼ (results return)
┌─────────────────────────────────────────────────────────────┐
│  Research Agent (Primary)                                   │
│  - Synthesizes all results                                  │
│  - Organizes by category/relevance                          │
│  - Provides comprehensive summary with all links            │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│  YOU: Read comprehensive research with source links          │
└─────────────────────────────────────────────────────────────┘
```

## Links

- [opencode.ai](https://opencode.ai/) - All about opencode
- [opencode-parallel-agents](https://github.com/aptdnfapt/opencode-parallel-agents) - Parallel agent logic and customization
- [qwen-code-oai-proxy](https://github.com/aptdnfapt/qwen-code-oai-proxy) - Free 2000 req/day web search setup
- [Discord](https://discord.gg/vDXSX7AfJC) - AI dev / news / future colab
