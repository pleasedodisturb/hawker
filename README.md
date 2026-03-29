# Hawker

**Autonomous AI marketplace agent — snap a photo, get it sold.**

Hawker is an open-source AI agent that automates selling used items across multiple marketplaces. From a single photo, it identifies the item, researches market prices, generates bilingual listings, publishes across platforms, communicates with buyers, adjusts pricing, and tracks sales to completion.

Built as a suite of [MCP](https://modelcontextprotocol.io/) servers. Works with [Goose](https://github.com/block/goose) and any MCP-compatible agent.

---

## The Problem

You have 10 things to sell. For each one you need to:

1. Research what it's worth across 3-4 platforms
2. Write a compelling title + description in the right language
3. Take photos and upload to each platform separately
4. Copy-paste with platform-specific formatting
5. Answer "Ist noch da?" 47 times
6. Negotiate with lowballers
7. Coordinate pickup or shipping
8. Track what sold, what didn't, what needs a price drop

Multiply by 10 items. **Nobody does this.** The stuff sits in a corner. 117 million unused electronics in German households alone.

## The Solution

Hawker reduces selling to **two touchpoints**:

1. **Photograph your items** (batch 10 in 10 minutes)
2. **Hand off the packages** when they sell

Everything in between is handled by the agent.

```
Camera → Identify → Price → List → Publish → Negotiate → Sell → Track
  📸       🔍        💰      ✍️       🚀        💬         🤝      📊
```

## How It Works

| Stage | What Happens |
|-------|-------------|
| **Photo Input** | Point camera at item. Optional voice notes for condition details. |
| **Identification** | Vision AI identifies brand, model, condition, specs. |
| **Price Research** | Scrapes comparable listings across platforms, filters scam prices, sets optimal price. |
| **Listing Generation** | Generates DE+EN title, description, SEO keywords, platform-specific formatting. |
| **Cross-Platform Publish** | Publishes to Kleinanzeigen, eBay, Vinted simultaneously. |
| **Buyer Communication** | Auto-replies, negotiates within your bounds, detects scams, schedules pickups. |
| **Sale Tracking** | Auto-delists on other platforms when sold. Tracks revenue and suggests price adjustments. |

## Autonomy Modes

| Mode | Agent Does | You Do |
|------|-----------|--------|
| **Supervised** | Generate listings, suggest prices | Approve everything |
| **Semi-auto** | Publish, chat with buyers | Approve sales |
| **Full auto** | Everything including negotiation | Hand off packages |

## Target Platforms

| Platform | Integration | Market |
|----------|------------|--------|
| **Kleinanzeigen** | Browser automation (Playwright) | 36M monthly users, dominant in DE |
| **eBay Germany** | Official REST API | Full API, zero seller fees |
| **Vinted** | Browser automation | Fashion/accessories, integrated shipping |
| **FB Marketplace** | Best-effort | Lower priority in Germany |

## Architecture

Hawker is built as composable **MCP servers** — each marketplace capability is an independent tool:

- **`marketplace-publisher`** — publish, edit, delist, read/send messages per platform
- **`pricing-research`** — search comparables, estimate prices, track price history
- **`listing-generator`** — generate listings, optimize titles, translate DE↔EN
- **`inventory-manager`** — track items, record sales, suggest actions

Any MCP-compatible agent (Goose, Claude Code, etc.) can use these tools independently.

## Tech Stack

- **Language:** Rust (core) + Python (AI/scraping)
- **Agent Platform:** [Goose](https://github.com/block/goose) (MCP-native)
- **AI:** Claude API (vision, listing generation, buyer communication)
- **Browser Automation:** Playwright (Kleinanzeigen, Vinted)
- **Marketplace API:** eBay REST API
- **Database:** SQLite
- **Frontend:** PWA (mobile-first, camera-native)
- **Notifications:** Telegram

## Status

**Research & planning complete. Ready to build.**

- [x] Domain research — German C2C marketplace ecosystem analyzed
- [x] Market gap confirmed — no AI-powered cross-platform seller tool exists
- [x] Real-world validation — 18 items inventoried, 12 listed on Kleinanzeigen
- [x] Automation proven — Playwright scripts for Kleinanzeigen batch editing
- [x] Product brainstorming — 103 ideas organized into V1/V2/V3 roadmap
- [ ] MVP development — in progress

## Why "Hawker"

A hawker is a street vendor who sells goods by calling out to passersby. Loud, efficient, knows their market, closes deals fast. That's the vibe.

## Origin

2026-03-13, 6am, Frankfurt. After manually listing the 9th item on Kleinanzeigen — a Samsung TV, a Stream Deck, two suitcases, a CalDigit dock, an OptiGrill — the thought hit: *"this should be a product."*

The pain is real. The market gap is confirmed. The agent is coming.

---

**License:** MIT | **Author:** [Vitalik](https://github.com/pleasedodisturb)
