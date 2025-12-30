# Opencode Research Extension

Extension for [opencode](https://opencode.ai/) providing research capabilities with multiple web search and GitHub tools.

Uses parallel agent logic from [opencode-parallel-agents](https://github.com/aptdnfapt/opencode-parallel-agents).

## Tools

| Tool | Description | Setup |
|------|-------------|-------|
| web-search-prime | High-quality web search with domain filters | Requires [ZAI subscription](https://z.ai/subscribe) |
| zread | GitHub repo search, docs, and file reading | Requires [ZAI subscription](https://z.ai/subscribe) |
| context7 | OSS documentation search | Free, no setup required |
| searxng | Open-source web search engine | Self-hosted SearXNG instance |
| qwen-web-search | **2000 free requests/day** per account | See [qwen-code-oai-proxy](https://github.com/aptdnfapt/qwen-code-oai-proxy) |
| exa | Powerful AI-powered web search | Free on opencode, just enable |

## Setup

### web-search-prime & zread

[ZAI](https://z.ai/subscribe) provides both web-search-prime and zread. Get your API key from the subscription dashboard.

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

## Usage

1. Run `opencode` from this directory
2. Press tab until you see "Research agent"
3. Tell Research agent what you want to research and how many agents you want it to work for it . 
4. Press tab to "webresearch" subagent → multiple websearch agents run in parallel

The agent automatically uses whatever tools you have enabled. No need to specify which tools to use.

## How It Works

- **Research agent** (primary) runs first → asks clarifying questions about your research needs
- Launches X parallel **webresearch** subagents (X = number you specify)
- Each subagent uses available tools to research different angles/sources
- Results are synthesized into a comprehensive summary with all links

## Links

- [opencode.ai](https://opencode.ai/) - All about opencode
- [opencode-parallel-agents](https://github.com/aptdnfapt/opencode-parallel-agents) - Parallel agent logic
- [qwen-code-oai-proxy](https://github.com/aptdnfapt/qwen-code-oai-proxy) - Free 2000 req/day web search
- [Discord](https://discord.gg/vDXSX7AfJC) - AI dev / news / future colab
