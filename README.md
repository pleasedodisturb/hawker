# Hawker

**AI-powered second-hand selling assistant — from photo to cash.**

Hawker automates the entire resale workflow: market research, listing creation, cross-platform publishing, buyer communication, and sale tracking. One photo in, money out.

---

## The Problem

You have 10 things to sell. For each item you need to:
1. Research what it's worth (check Kleinanzeigen, eBay, FB Marketplace, Vinted)
2. Write a listing title + description (in the right language, with the right keywords)
3. Take photos and upload them to 2-3 platforms
4. Copy-paste the listing across platforms with platform-specific formatting
5. Answer "Ist noch da?" 47 times
6. Negotiate with lowballers
7. Coordinate pickup/shipping
8. Track what sold, what didn't, what needs a price drop

Multiply by 10 items. Nobody does this. The stuff sits in a corner.

## The Solution

Hawker is a CLI/web tool that handles the mechanical parts so you just make decisions.

### Core Features

#### 1. Smart Pricing (Market Research)
- Snap a photo or describe the item
- Hawker scrapes Kleinanzeigen, eBay Kleinanzeigen, FB Marketplace, Vinted for comparable sold/active listings
- Returns: estimated price range, average time to sell, recommended asking price
- "Your Philips OptiGrill Elite + waffle plates: €60-90 on Kleinanzeigen, avg 5 days to sell. Suggest: €79 VB"

#### 2. Listing Generator
- Photo(s) → AI generates title, description, category, shipping options
- Multi-language support (DE/EN at minimum — Frankfurt has both markets)
- SEO-optimized titles (the right keywords that Kleinanzeigen search actually finds)
- Platform-specific formatting (Kleinanzeigen vs FB Marketplace vs Vinted vs eBay)
- One approval flow: review generated listing, edit if needed, approve

#### 3. Cross-Platform Publishing
- Publish to multiple platforms in one action
- Platform adapters: Kleinanzeigen, FB Marketplace, Vinted, eBay Kleinanzeigen
- Track which platforms each item is listed on
- Auto-delist from other platforms when sold on one

#### 4. Buyer Communication Bot
- Auto-reply to "Ist noch da?" → "Ja, noch verfügbar! Wann passt Abholung?"
- Handle lowball offers with configurable floor price ("Unter €60 gehe ich nicht")
- Negotiate within parameters you set
- Escalate to you only for serious buyers ready to commit
- Multi-platform inbox aggregation

#### 5. Sale Tracker Dashboard
- Pipeline view: Draft → Listed → Negotiating → Sold → Complete
- Per-item: asking price, offers received, days listed, platform performance
- Total: items listed, sold, revenue, avg days to sell
- Nudges: "OptiGrill listed 14 days, no offers. Drop price to €59?"
- Revenue goal tracking

#### 6. Smart Relisting
- Auto price drops on stale listings (configurable schedule)
- Bump/refresh listings on platforms that support it
- Seasonal awareness ("winter jackets sell better in October")
- Cross-platform A/B testing (different prices on different platforms)

### Stretch Features
- **Shipping integration**: auto-generate DHL/Hermes labels for Vinted sales
- **Batch mode**: photograph 10 items, Hawker processes all overnight
- **Voice listing**: describe item verbally, Hawker creates the listing
- **Receipt/warranty finder**: "I bought this on Amazon, find the order for warranty transfer"
- **Donation mode**: items that don't sell after X days → auto-list as "Zu verschenken" or suggest Oxfam

---

## Tech Stack (Ideas)

- **Backend**: Python (FastAPI) or TypeScript
- **AI**: Claude API for listing generation, image analysis, buyer chat
- **Scraping**: Playwright/Puppeteer for market research
- **Platform APIs**: Where available (eBay API, Vinted API), scraping where not (Kleinanzeigen)
- **Frontend**: Simple web dashboard or CLI-first
- **Database**: SQLite (keep it simple)
- **Notifications**: Telegram bot for buyer messages that need attention

---

## Why "Hawker"

A hawker is a street vendor who sells goods by calling out to passersby. Loud, efficient, knows their market, closes deals fast. That's the vibe.

---

## Status

**Idea phase.** Born from the pain of manually listing 10+ items on Kleinanzeigen at 6am.

Up next. Building this as both a real tool and a portfolio piece — shipping products is the best proof you're a builder.

---

## Origin Story

2026-03-13, 6am, Frankfurt. Vitalik has a Samsung Q95T, Homey Pro, Philips Syncbox, CalDigit TS3, two Horizn suitcases, bike seats, an OptiGrill, an IKEA Poäng, and a BenQ Halo to sell. After adding the 9th item to a sell list in a financial tracking repo, the thought hit: "this should be a product."
