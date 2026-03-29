# Goose Open Source Grant Proposal

## Hawker: Autonomous AI Marketplace Agent

**One-liner:** Snap a photo of something you want to sell — an AI agent identifies it, prices it, lists it across marketplaces, negotiates with buyers, and closes the sale.

---

## 1. The Problem

There are 117 million unused electronics sitting in German households right now (Bitkom, 2024). Globally, the number is in the billions. Most people know they should sell their old phone, that camera they upgraded from, the kitchen appliance they replaced. But they don't.

Why? Because selling used items is a multi-hour, multi-platform grind:

1. **Research** comparable prices across 3-4 platforms
2. **Write** a compelling title and description (in the right language, with the right keywords)
3. **Photograph** the item and upload to each platform separately
4. **Copy-paste** the listing with platform-specific formatting
5. **Respond** to "Ist noch da?" ("Is it still available?") 47 times
6. **Negotiate** with lowballers who offer 30% of asking price
7. **Coordinate** pickup times or generate shipping labels
8. **Track** what sold where, what needs a price drop, what to delist

For 10 items, that's 20+ hours of tedious work. So the items rot in closets, end up in landfills, and the circular economy loses.

**The friction isn't in the transaction — it's in the labor around it.**

---

## 2. The Solution

**Hawker** is an open-source autonomous AI agent that reduces selling used items to two touchpoints:

1. **Photograph your items** (batch 10 items in 10 minutes)
2. **Hand off the packages** when they sell

Everything in between — identification, pricing, listing, publishing, buyer communication, negotiation, price adjustments, cross-platform management — is handled by the agent.

### How It Works

```
┌─────────────────────────────────────────────────────────────────────┐
│                        HAWKER AGENT PIPELINE                        │
│                                                                     │
│  ┌──────────┐    ┌──────────────┐    ┌───────────────┐              │
│  │  CAMERA   │    │   IDENTIFY   │    │    PRICE      │              │
│  │  INPUT    │───▶│   & ASSESS   │───▶│   RESEARCH    │              │
│  │          │    │              │    │               │              │
│  │ Photo(s) │    │ Brand, model │    │ Scrape comps  │              │
│  │ + voice  │    │ condition,   │    │ across 4      │              │
│  │ notes    │    │ specs via    │    │ platforms,    │              │
│  │          │    │ vision AI    │    │ filter scams, │              │
│  │          │    │              │    │ set price     │              │
│  └──────────┘    └──────────────┘    └───────┬───────┘              │
│                                              │                      │
│                                              ▼                      │
│  ┌──────────┐    ┌──────────────┐    ┌───────────────┐              │
│  │  SALE     │    │   BUYER      │    │   LISTING     │              │
│  │  CLOSE    │◀───│   COMMS      │◀───│   GENERATION  │              │
│  │          │    │              │    │               │              │
│  │ Auto-    │    │ Auto-reply,  │    │ DE+EN title,  │              │
│  │ delist   │    │ negotiate    │    │ description,  │              │
│  │ other    │    │ within       │    │ SEO keywords, │              │
│  │ platforms│    │ bounds,      │    │ platform-     │              │
│  │ track    │    │ detect       │    │ specific      │              │
│  │ revenue  │    │ scams,       │    │ formatting    │              │
│  │          │    │ schedule     │    │               │              │
│  │          │    │ pickup       │    │               │              │
│  └──────────┘    └──────────────┘    └───────┬───────┘              │
│                                              │                      │
│                                              ▼                      │
│                                      ┌───────────────┐              │
│                                      │   PUBLISH     │              │
│                                      │               │              │
│                                      │ Kleinanzeigen │              │
│                                      │ eBay DE       │              │
│                                      │ Vinted        │              │
│                                      │ FB Marketplace│              │
│                                      └───────────────┘              │
└─────────────────────────────────────────────────────────────────────┘
```

### Graduated Autonomy

Users control how much the agent does independently:

| Mode | Agent Does | User Does |
|------|-----------|-----------|
| **Supervised** | Generate listings, suggest prices | Approve everything before publish |
| **Semi-auto** | Publish listings, chat with buyers | Approve sales, handle escalations |
| **Full auto** | Everything including negotiation | Get notified on sales, hand off packages |

---

## 3. Grant Category Alignment

### Primary: Automate Everything

Hawker is "automate everything" taken to its logical conclusion in real-world commerce. This isn't automating a developer workflow — it's automating physical-world marketplace interactions:

- **Browser automation** to publish and manage listings on platforms without APIs (Kleinanzeigen, Vinted)
- **API integration** with platforms that offer them (eBay)
- **Autonomous buyer communication** — the agent responds to messages, negotiates prices, detects scams, and schedules pickups
- **Long-running background operation** — the agent monitors listings 24/7, adjusts prices on stale items, bumps listings, responds to buyer inquiries within minutes regardless of whether the seller is online
- **Cross-platform state management** — one inventory, four platforms, automatic delisting when an item sells

This is a self-flying agent that operates in the real world for days or weeks per item lifecycle.

### Secondary: New Interaction Paradigms

The primary input is a **camera/photo**:

- Point phone camera at item → agent identifies brand, model, condition, and specs
- Multi-angle photo capture with voice notes for condition details
- Batch mode: photograph 10 items in a session, agent processes all asynchronously
- The interaction model is physical-first: the user interacts with physical objects, the agent handles the digital marketplace

This is a fundamentally different interaction paradigm from text prompts. The user's "prompt" is pointing a camera at a real-world object.

### Tertiary: Self-Improving Agents

Hawker improves through operational feedback loops:

- **Pricing accuracy** improves as the agent tracks actual sale prices vs. estimates
- **Listing quality** improves by correlating listing text/photos with engagement metrics (views, saves, inquiries)
- **Negotiation strategy** adapts based on what closing tactics work in different price ranges and categories
- **Platform selection** optimizes over time — learning which item categories perform best on which platforms

---

## 4. Goose / MCP Integration Plan

Hawker will be built as a suite of **MCP servers** that integrate natively with Goose, making marketplace operations available to any MCP-compatible agent.

### MCP Server Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    GOOSE AGENT                           │
│                                                         │
│  Uses MCP tools to orchestrate the full selling pipeline │
└────────┬──────────┬──────────┬──────────┬───────────────┘
         │          │          │          │
         ▼          ▼          ▼          ▼
┌────────────┐ ┌─────────┐ ┌────────┐ ┌──────────────┐
│ marketplace│ │ pricing │ │listing │ │ inventory    │
│ -publisher │ │-research│ │-gen    │ │ -manager     │
│            │ │         │ │        │ │              │
│ MCP Server │ │MCP Srvr │ │MCP Srvr│ │  MCP Server  │
│            │ │         │ │        │ │              │
│ Tools:     │ │Tools:   │ │Tools:  │ │Tools:        │
│ • publish  │ │• search │ │• gen   │ │• add_item    │
│ • edit     │ │• compare│ │• format│ │• update_item │
│ • delist   │ │• price  │ │• photo │ │• list_items  │
│ • status   │ │• history│ │• seo   │ │• track_sale  │
│ • messages │ │         │ │        │ │• analytics   │
└────────────┘ └─────────┘ └────────┘ └──────────────┘
```

### MCP Tools (Examples)

**marketplace-publisher** (per-platform adapters):
- `publish_listing(platform, listing_data)` — publish to Kleinanzeigen/eBay/Vinted
- `edit_listing(platform, listing_id, changes)` — update price, description, photos
- `delist(platform, listing_id)` — remove listing
- `get_messages(platform)` — fetch buyer messages
- `send_message(platform, conversation_id, text)` — reply to buyers
- `get_listing_stats(platform, listing_id)` — views, saves, inquiries

**pricing-research**:
- `search_comparables(query, platforms[])` — find similar active/sold listings
- `estimate_price(item_description, photos[])` — AI-powered price estimate
- `price_history(item_query)` — price trends over time

**listing-generator**:
- `generate_listing(photos[], notes, target_platforms[])` — AI-generated listing
- `optimize_title(title, platform)` — SEO optimization per platform
- `translate_listing(listing, source_lang, target_lang)` — bilingual support

**inventory-manager**:
- `add_item(photos[], notes)` — add to inventory
- `track_sale(item_id, platform, price)` — record sale
- `suggest_actions()` — "drop price on item X", "relist item Y on Vinted"

### Why Goose

Goose's architecture is ideal for Hawker:

1. **Rust performance** — browser automation and multi-platform scraping benefit from Goose's Rust core
2. **MCP-native** — marketplace operations become composable tools any agent can use
3. **Extension system** — each marketplace platform is a natural Goose extension
4. **Long-running agent support** — Hawker needs to run for days/weeks per item lifecycle, monitoring listings and responding to buyers
5. **Open-source alignment** — Hawker's value is in the agent logic and MCP tools, not proprietary data. Open-source maximizes ecosystem impact

### Community Value

The MCP servers built for Hawker are independently useful:

- **marketplace-publisher** — any agent can publish to German C2C platforms
- **pricing-research** — any agent can research second-hand market prices
- **listing-generator** — any agent can generate optimized marketplace listings

This extends Goose's capability into real-world commerce — a category no existing MCP server covers.

---

## 5. Quarterly Milestones

### Q1: Foundation (Months 1-3)

**Theme:** Core pipeline — photo to published listing on one platform

**Deliverables:**
- [ ] Photo input → AI item identification (brand, model, condition, specs) using vision models
- [ ] Price research engine: scrape Kleinanzeigen + eBay for comparable listings, filter scam prices, return price range
- [ ] Bilingual listing generator (DE+EN): title, description, category suggestion, SEO keywords
- [ ] eBay Germany integration via official API (publish, edit, delist)
- [ ] MCP server: `listing-generator` with tools for generation, translation, optimization
- [ ] MCP server: `pricing-research` with tools for comparable search and price estimation
- [ ] SQLite inventory database with item lifecycle tracking
- [ ] CLI interface for the full pipeline: `hawker sell <photo>`

**Success Metric:** Publish a real listing on eBay Germany from a single photo input in under 60 seconds.

**Goose Integration:** First two MCP servers operational, usable from any Goose agent.

### Q2: Multi-Platform & Communication (Months 4-6)

**Theme:** Cross-platform publishing + autonomous buyer communication

**Deliverables:**
- [ ] Kleinanzeigen browser automation via Playwright (publish, edit, delist, read messages)
- [ ] Vinted browser automation (publish, edit, delist)
- [ ] MCP server: `marketplace-publisher` with platform adapters and unified tool interface
- [ ] Cross-platform inventory sync (auto-delist on other platforms when sold)
- [ ] Buyer communication agent: auto-reply to common messages ("Ist noch da?"), handle negotiation within seller-defined bounds
- [ ] Scam detection: link scanning, off-platform redirect detection, "too good to be true" heuristics
- [ ] Graduated autonomy modes (supervised / semi-auto / full-auto)
- [ ] Web dashboard MVP: pipeline view (Draft → Listed → Negotiating → Sold)

**Success Metric:** List one item across 3 platforms simultaneously; agent autonomously handles buyer messages for 48 hours without seller intervention.

**Goose Integration:** Full marketplace MCP server with multi-platform support. Demonstration of Goose running Hawker as a self-flying background agent.

### Q3: Intelligence & Self-Improvement (Months 7-9)

**Theme:** The agent gets smarter through operational data

**Deliverables:**
- [ ] Pricing feedback loop: track estimated vs. actual sale prices, improve estimation model
- [ ] Listing quality scoring: correlate listing text/photos with engagement (views, saves, messages)
- [ ] Smart relisting: auto price drops on stale listings (configurable schedule), seasonal awareness
- [ ] Platform performance analytics: learn which categories sell best on which platforms
- [ ] Batch mode: photograph 10 items, agent processes all asynchronously overnight
- [ ] MCP server: `inventory-manager` with analytics and action suggestion tools
- [ ] DAC7 tax compliance tracking (report threshold: 30 sales or €2,000/year)
- [ ] Notification system via Telegram: buyer messages that need human attention, sale confirmations

**Success Metric:** Agent pricing estimates within 15% of actual sale price on 80%+ of items. Batch processing of 10 items from photos to live listings in under 10 minutes.

**Goose Integration:** Self-improving agent demonstration — show pricing accuracy improvement over time using Goose's agent observability.

### Q4: Polish, Scale & Community (Months 10-12)

**Theme:** Production readiness, mobile experience, ecosystem contribution

**Deliverables:**
- [ ] PWA mobile app: camera capture → agent pipeline (phone-first experience)
- [ ] Voice notes for item condition/details (speak instead of type)
- [ ] Seller philosophy profiles: "hold for full price" vs. "quick turnover" behavior presets
- [ ] Shipping integration: DHL label generation, batch pickup scheduling
- [ ] Facebook Marketplace integration (best-effort, given Meta's restrictions)
- [ ] Comprehensive documentation: setup guides, MCP server docs, platform adapter development guide
- [ ] Published to Goose extension registry
- [ ] Community marketplace adapter template (for adding new platforms/countries)
- [ ] Performance benchmarks and case study: items sold, revenue generated, time saved

**Success Metric:** End-to-end autonomous sale — from photo to cash in hand — with zero manual listing work. Published as Goose extension with community adoption.

**Goose Integration:** Published to Goose extension ecosystem. Adapter template enables community contributions for marketplace platforms in other countries.

---

## 6. About the Applicant

**Vitalik** — Solo AI developer based in Frankfurt, Germany.

- **Former Amazon engineer** — shipped production systems at scale
- **Active AI builder** — using Claude, Goose, and MCP tools daily in real projects
- **Real domain expertise** — not theorizing about marketplace selling; actively selling 18 items on Kleinanzeigen right now, with documented learnings about what works (pricing, descriptions, buyer behavior, platform quirks, scam patterns)
- **Already built automation** — wrote Playwright scripts to batch-edit Kleinanzeigen listings, discovered reliable selectors and workflows through trial and error
- **Bilingual market access** — lives in Frankfurt, sells in German and English, understands both buyer populations
- **Open-source contributor** — building in public, MIT-licensed from day one

### Why This Person for This Project

Most marketplace automation projects are built by developers who've never actually sold anything on these platforms. Vitalik has:

- Manually listed 12 items and inventoried 18 on Kleinanzeigen
- Discovered that items with 0 saves after a week need either price drops or different platforms
- Learned that scam listings at 1/3 market price must be filtered from pricing research
- Found that backpacks sell on Vinted (not Kleinanzeigen) but tech items thrive on Kleinanzeigen
- Proven that Playwright's `browser_run_code` is the reliable path for Kleinanzeigen automation (not Chrome DevTools Protocol, which is too flaky)
- Developed a listing format that works: German body with specs bullets, condition statement, original price anchor, "Privatverkauf" footer, English translation at bottom

This isn't a grant proposal from someone who might build something. The pain is real, the research is done, and the first automation scripts already exist.

---

## 7. Budget Breakdown

| Category | Amount | Details |
|----------|--------|---------|
| **Developer compensation** | $70,000 | Full-time solo development for 12 months |
| **AI API costs** | $12,000 | Claude API for vision, listing generation, buyer communication (~$1K/month) |
| **Infrastructure** | $6,000 | Cloud hosting, browser automation instances, database ($500/month) |
| **Platform test accounts** | $3,000 | eBay store fees, Vinted shipping tests, listing promotion experiments |
| **Testing & QA** | $4,000 | Real-world selling tests (actual items listed and sold on all platforms) |
| **Community & docs** | $3,000 | Documentation, video demos, Goose extension registry publication |
| **Contingency** | $2,000 | Unexpected platform changes, additional API costs |
| **Total** | **$100,000** | |

### Notes on Budget Efficiency

- **Solo developer** — no coordination overhead, all funds go to building
- **Real-world testing is the product** — every dollar spent on "testing" generates actual marketplace data that improves the agent
- **AI costs are the product** — API spend directly delivers user value (better listings, smarter pricing, buyer communication)
- **Open-source from day one** — no spend on proprietary infrastructure or licensing

---

## 8. Why This Matters

### For the Circular Economy

The biggest barrier to the circular economy isn't willingness — it's friction. 73% of Germans have engaged in second-hand commerce, but most have a drawer/closet/garage of items they "should sell someday." Hawker eliminates the labor that makes "someday" never come.

Every item sold instead of discarded is:
- **Less waste** in landfills
- **Less manufacturing** of new goods
- **More money** in the seller's pocket
- **More affordable goods** for buyers

### For the Goose Ecosystem

Hawker demonstrates that AI agents can operate in the real world, not just in developer tooling:

- **First commerce MCP servers** — marketplace operations become composable building blocks
- **Self-flying agent reference** — a production example of an agent that runs autonomously for weeks
- **Physical-digital bridge** — camera input to real-world transactions, the kind of agent interaction that defines the next era
- **International template** — the platform adapter pattern means the community can extend Hawker to any country's marketplaces

### For Open Source

No open-source tool provides AI-powered cross-platform selling for C2C marketplaces — anywhere in the world. Existing tools are either:
- Single-platform (kleinanzeigen-bot, Dotb)
- US-focused and proprietary (Vendoo, Crosslist)
- Buyer-side only (Faircado)
- Margin-eating services (Sellpy, Cirkular — they buy your items cheap and resell)

Hawker fills a confirmed market gap with an open-source, agent-native approach that keeps sellers in control of their margins.

### The Vision

Today: one person in Frankfurt selling a Samsung TV, a keyboard, and some suitcases with an AI agent.

Tomorrow: anyone, anywhere can point their phone at something they no longer need and have it sold — autonomously, fairly, across every marketplace that matters.

**That's the kind of agent the world actually needs.**

---

## Links

- **Repository:** [github.com/pleasedodisturb/hawker](https://github.com/pleasedodisturb/hawker)
- **License:** MIT
- **Status:** Research complete, architecture planned, ready to build

---

*Submitted for the Block Goose Open Source Grants Program, March 2026.*
