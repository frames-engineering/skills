---
name: registry
version: 1.0.0
description: Pay-per-call API gateway for AI agents. 6 services available via x402 — no API keys, no subscriptions.
homepage: https://registry.frames.ag
metadata:
  category: api-gateway
  api_base: https://registry.frames.ag/api
  x402:
    supported: true
    chains:
      - evm
      - solana
    networks:
    - eip155:8453
    - eip155:84532
    - solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp
    - solana:EtWTRABZaYq6iMfeYKouRu166VU2xqa1
    tokens:
      - USDC
      - USDT
      - CASH
  services:
    count: 6
    slugs:
    - twitter
    - ai-gen
    - test
    - exa
    - wordspace
    - openrouter
    endpoints:
    twitter: /api/service/twitter
    ai-gen: /api/service/ai-gen
    test: /api/service/test
    exa: /api/service/exa
    wordspace: /api/service/wordspace
    openrouter: /api/service/openrouter
    skill_docs: /api/service/{slug}/skill.md
  wallet:
    recommended: agentwallet
    skill: https://agentwallet.mcpay.tech/skill.md
    endpoint: /x402/fetch
---

# Frames Registry

Pay-per-call API gateway for AI agents. 6 services available via the x402 payment protocol. No API keys, no subscriptions — just pay per request with crypto.

## Base URL

```
https://registry.frames.ag
```

## Prerequisites

A crypto wallet funded with USDC is required to use paid endpoints. Two options:

- **[AgentWallet](https://agentwallet.mcpay.tech/skill.md) (recommended for agents)** — server-side wallet that handles 402 detection, payment signing, and retries automatically via a single `POST /x402/fetch` call. No private key management needed on your side.
- **Self-managed wallet** — any EVM wallet (Base) or Solana wallet with USDC. You sign x402 payment headers directly.

## Quick Start

1. **Set up a wallet** — create an [AgentWallet](https://agentwallet.mcpay.tech/skill.md) or fund your own wallet with USDC
2. **Discover services:** `GET https://registry.frames.ag/api/services`
3. **Read service docs:** `GET https://registry.frames.ag/api/service/{slug}/skill.md`
4. **Check pricing:** `GET https://registry.frames.ag/api/pricing`
5. **Make a paid request** — via AgentWallet's `/x402/fetch` or directly with x402 headers (see Payment Protocol below)

## Services (6)

| Service | Slug | Description | Endpoints | Price Range |
|---------|------|-------------|-----------|-------------|
| [Twitter API](https://registry.frames.ag/api/service/twitter/skill.md) | `twitter` | Full Twitter API access - users, tweets, search, trends, and more via twitterapi.io | 17 | $0.005 - $0.02 |
| [AI Generation API](https://registry.frames.ag/api/service/ai-gen/skill.md) | `ai-gen` | Run AI models for image, video, audio, and 3D generation | 1 | $0.01 |
| [x402 Test Service](https://registry.frames.ag/api/service/test/skill.md) | `test` | Test x402 payment flows on Base Sepolia (EVM) and Solana Devnet. Use this service to verify your x402 client integration is working correctly. | 2 | $0.001 |
| [Exa API](https://registry.frames.ag/api/service/exa/skill.md) | `exa` | Semantic web search via Exa | 4 | $0.002 - $0.01 |
| [Wordspace Agent](https://registry.frames.ag/api/service/wordspace/skill.md) | `wordspace` | AI agent loop with sandboxed execution and OpenProse skills | 1 | $2 |
| [OpenRouter](https://registry.frames.ag/api/service/openrouter/skill.md) | `openrouter` | Text generation via 300+ models (OpenAI, Anthropic, Google, Meta, etc.) | 0 | free |

## Service Endpoints

Each service lives at `https://registry.frames.ag/api/service/{slug}` and exposes:

| Endpoint | Description |
|----------|-------------|
| `GET /` | Service info |
| `GET /health` | Health check |
| `GET /docs` | Interactive API docs |
| `GET /openapi.json` | OpenAPI 3.x spec |
| `GET /skill.md` | Agent-friendly documentation |

## Pricing Details

### Twitter API (`twitter`)

Base: `https://registry.frames.ag/api/service/twitter` | [Docs](https://registry.frames.ag/api/service/twitter/docs) | [OpenAPI](https://registry.frames.ag/api/service/twitter/openapi.json) | [Skill](https://registry.frames.ag/api/service/twitter/skill.md)

| Endpoint | Price | Description |
|----------|-------|-------------|
| `POST /api/user-info` | $0.005 | Get user info by username |
| `POST /api/user-tweets` | $0.01 | Get user's recent tweets |
| `POST /api/user-followers` | $0.01 | Get user's followers |
| `POST /api/user-following` | $0.01 | Get users that user follows |
| `POST /api/search-users` | $0.01 | Search for users by keyword |
| `POST /api/user-mentions` | $0.01 | Get tweets mentioning a user |
| `POST /api/check-follow` | $0.005 | Check if one user follows another |
| `POST /api/batch-users` | $0.02 | Batch get users by IDs |
| `POST /api/tweets-by-ids` | $0.01 | Get tweets by their IDs |
| `POST /api/tweet-replies` | $0.01 | Get replies to a tweet |
| `POST /api/search-tweets` | $0.01 | Advanced tweet search with filters |
| `POST /api/tweet-quotes` | $0.01 | Get quote tweets of a tweet |
| `POST /api/tweet-thread` | $0.01 | Get tweet thread context |
| `POST /api/list-tweets` | $0.01 | Get tweets from a Twitter List |
| `POST /api/trends` | $0.01 | Get trending topics by location |
| `POST /api/invoke` | $0.01 | Search tweets (legacy, use /api/search-tweets) |
| `POST /api/search` | $0.01 | Search tweets (legacy, use /api/search-tweets) |

### AI Generation API (`ai-gen`)

Base: `https://registry.frames.ag/api/service/ai-gen` | [Docs](https://registry.frames.ag/api/service/ai-gen/docs) | [OpenAPI](https://registry.frames.ag/api/service/ai-gen/openapi.json) | [Skill](https://registry.frames.ag/api/service/ai-gen/skill.md)

| Endpoint | Price | Description |
|----------|-------|-------------|
| `POST /api/invoke` | $0.01 | Run AI model prediction (price varies by model) |

### x402 Test Service (`test`)

Base: `https://registry.frames.ag/api/service/test` | [Docs](https://registry.frames.ag/api/service/test/docs) | [OpenAPI](https://registry.frames.ag/api/service/test/openapi.json) | [Skill](https://registry.frames.ag/api/service/test/skill.md)

| Endpoint | Price | Description |
|----------|-------|-------------|
| `POST /api/invoke` | $0.001 | Test x402 payment flow (Base Sepolia & Solana Devnet) |
| `POST /api/echo` | $0.001 | Echo data with payment verification |

### Exa API (`exa`)

Base: `https://registry.frames.ag/api/service/exa` | [Docs](https://registry.frames.ag/api/service/exa/docs) | [OpenAPI](https://registry.frames.ag/api/service/exa/openapi.json) | [Skill](https://registry.frames.ag/api/service/exa/skill.md)

| Endpoint | Price | Description |
|----------|-------|-------------|
| `POST /api/search` | $0.01 | Semantic web search |
| `POST /api/find-similar` | $0.01 | Find similar pages |
| `POST /api/contents` | $0.002 | Extract URL contents |
| `POST /api/answer` | $0.01 | AI-powered answer |

### Wordspace Agent (`wordspace`)

Base: `https://registry.frames.ag/api/service/wordspace` | [Docs](https://registry.frames.ag/api/service/wordspace/docs) | [OpenAPI](https://registry.frames.ag/api/service/wordspace/openapi.json) | [Skill](https://registry.frames.ag/api/service/wordspace/skill.md)

| Endpoint | Price | Description |
|----------|-------|-------------|
| `POST /api/invoke` | $2 | Run wordspace AI agent loop |

### AI Model Pricing (`ai-gen`)

Price is set dynamically based on the `model` field in the request body.

**Image Models:**

| Model | Price |
|-------|-------|
| `flux/schnell` | $0.004/image |
| `flux/2-pro` | $0.02 |
| `flux/kontext-pro` | $0.05/image |
| `bytedance/seedream-4` | $0.04/image |
| `google/nano-banana` | $0.05/image |
| `google/nano-banana-pro` | $0.18/image |
| `google/imagen-4-fast` | $0.03/image |
| `ideogram/v3-turbo` | $0.04/image |
| `prunaai/z-image-turbo` | $0.006/image |
| `prunaai/p-image` | $0.006/image |
| `fofr/sdxl-emoji` | $0.01 |
| `qwen/qwen-image-edit-2511` | $0.04/image |
| `xai/grok-2-image` | $0.09/image |
| `openai/dall-e-3` | $0.15/image |
| `nightmareai/real-esrgan` | $0.003/image |

**Video Models:**

| Model | Price |
|-------|-------|
| `google/veo-3` | $0.48/sec (audio), $0.24/sec (no audio) |
| `google/veo-3-fast` | $0.18/sec (audio), $0.12/sec (no audio) |
| `google/veo-3.1` | $0.48/sec (audio), $0.24/sec (no audio) |
| `google/veo-3.1-fast` | $0.18/sec (audio), $0.12/sec (no audio) |
| `openai/sora-2` | $0.12/sec |
| `openai/sora-2-pro` | $0.36/sec (720p), $0.60/sec (1080p) |
| `kwaivgi/kling-v2.5-turbo-pro` | $0.09/sec |
| `kwaivgi/kling-v2.6` | $0.09/sec |
| `kwaivgi/kling-v2.6-motion-control` | $0.09/sec (std), $0.15/sec (pro) |
| `bytedance/seedance-1-pro` | $0.04/sec (480p), $0.08/sec (720p), $0.18/sec (1080p) |
| `bytedance/seedance-1-lite` | $0.03/sec (480p), $0.05/sec (720p), $0.09/sec (1080p) |
| `bytedance/seedance-1-pro-fast` | $0.02/sec (480p), $0.03/sec (720p), $0.08/sec (1080p) |
| `bytedance/seedance-1.5-pro` | $0.04/sec (720p), $0.07/sec (720p+audio) |
| `minimax/video-01` | $0.60 |
| `wan-video/wan-2.2-t2v-fast` | $0.12 |
| `wan-video/wan-2.2-i2v-fast` | $0.07 |
| `wan-video/wan-2.5-i2v-fast` | $0.09/sec (720p), $0.13/sec (1080p) |
| `runwayml/gen4-turbo` | $0.06/sec |
| `runwayml/gen4-aleph` | $0.22/sec |
| `veed/fabric-1.0` | $0.10/sec (480p), $0.18/sec (768p) |
| `shreejalmaharjan-27/tiktok-short-captions` | $0.002/sec |

## Payment Protocol (x402)

All paid endpoints use the [x402](https://www.x402.org/) payment protocol. No API keys needed.

**Flow:**

1. Call any paid endpoint without a payment header
2. Receive `402 Payment Required` with a `PAYMENT-REQUIRED` header (Base64 JSON with price, network, payTo address)
3. Sign a payment for the requested amount on your chosen network
4. Retry the same request with the `PAYMENT-SIGNATURE` header
5. Receive the response plus a `PAYMENT-RESPONSE` confirmation header

Failed requests are automatically refunded.

**Supported Networks:**

| Network | ID | Type | Environment |
|---------|----|------|-------------|
| Base | `eip155:8453` | EVM | Mainnet |
| Base Sepolia | `eip155:84532` | EVM | Testnet |
| Solana | `solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp` | Solana | Mainnet |
| Solana Devnet | `solana:EtWTRABZaYq6iMfeYKouRu166VU2xqa1` | Solana | Devnet |

**Accepted Tokens:** USDC, USDT, CASH (availability varies by network)

## Platform Endpoints (FREE)

| Endpoint | Description |
|----------|-------------|
| `GET https://registry.frames.ag/api` | Platform info and version |
| `GET https://registry.frames.ag/api/services` | List all services with metadata |
| `GET https://registry.frames.ag/api/services/:slug` | Single service details |
| `GET https://registry.frames.ag/api/pricing` | All pricing policies |
| `GET https://registry.frames.ag/api/networks` | Supported payment networks |
| `GET https://registry.frames.ag/api/health` | Health check |
| `GET https://registry.frames.ag/api/packages` | Skill/agent package catalog |
| `GET https://registry.frames.ag/api/packages/:slug/bundle` | Download package bundle |
| `GET https://registry.frames.ag/.well-known/x402` | x402 discovery document |
| `GET https://registry.frames.ag/docs` | Interactive docs (HTML) |

## Agent Integration

### With AgentWallet (recommended)

[AgentWallet](https://agentwallet.mcpay.tech/skill.md) is a server-side wallet for AI agents. It manages keys, balances, and x402 payment signing so agents don't need to handle crypto directly.

1. Authenticate with AgentWallet (email OTP → API token)
2. Fund your wallet with USDC on Base or Solana
3. Call any Frames Registry endpoint through AgentWallet's proxy:

```
POST https://agentwallet.mcpay.tech/x402/fetch
{
  "url": "https://registry.frames.ag/api/service/twitter/api/search-tweets",
  "method": "POST",
  "body": { "query": "AI agents" }
}
```

AgentWallet detects the 402 response, signs payment, and retries automatically.

### Direct x402 (self-managed wallet)

Requires an EVM or Solana wallet with USDC and the ability to sign EIP-3009 or SPL transfers.

1. Make the request to the paid endpoint
2. Parse the `PAYMENT-REQUIRED` header from the 402 response (Base64 JSON with price, network, payTo)
3. Sign a payment authorization for the exact amount
4. Retry with the `PAYMENT-SIGNATURE` header
