# Marketplace Context for Hawker

Context from the Money/marketplace repo — real-world selling experience that informs Hawker's design.

## What happened (2026-03-27)

Created a separate `marketplace` repo (github.com/pleasedodisturb/marketplace) to track buying/selling.
18 items inventoried, 12 listed on Kleinanzeigen with bilingual (DE+EN) descriptions.

## Key learnings for Hawker

### Listing automation
- **Playwright MCP `browser_run_code`** is the reliable way to batch-edit Kleinanzeigen listings
- BrowserMCP (Chrome extension CDP) is too flaky — disconnects between every interaction
- Kleinanzeigen textarea selector: `#pstad-descrptn`
- Kleinanzeigen save button: `button:has-text("Anzeige speichern")`
- Edit URL pattern: `https://www.kleinanzeigen.de/p-anzeige-bearbeiten.html?adId={AD_ID}`
- Login URL: `https://www.kleinanzeigen.de/m-einloggen.html`
- My listings URL: `https://www.kleinanzeigen.de/m-meine-anzeigen.html`

### Pricing insights
- Scam listings at 1/3 market price are everywhere — ignore them for pricing
- Items with 0 saves after a week need price drops or different platforms
- Backpacks/fashion do better on Vinted/Grailed than Kleinanzeigen
- Tech items (Stream Deck, Sync Box) get high traffic on Kleinanzeigen
- Bikes get the most saves — hold firm on price

### Description format that works
- German body with bullet points for specs
- Condition clearly stated
- Original price mentioned (anchoring)
- "Privatverkauf — keine Garantie, keine Rücknahme" footer
- English translation at the bottom (signals international audience)
- Neutral sell reasons ("switching setup", "clearing space") — never desperate

### Combo deals
- Bundle related items (TV + ambilight kit) for higher total sale
- Discount 10-15% on bundles to incentivize
- "Sweeteners" (throw in a Hue Bridge) close deals

### Platform recommendations
- **Kleinanzeigen**: tech, home, bikes, electronics
- **Vinted**: bags, fashion, accessories
- **Grailed**: designer/niche bags
- **r/mechmarket**: keyboards, switches

### Marketplace repo structure
```
marketplace/
├── sell/           ← one .md per item (specs, pricing, KA link, status)
├── buy/            ← items to buy (research, price tracking)
├── sold/           ← completed sales
├── bought/         ← completed purchases
├── templates/      ← listing templates
└── docs/           ← kleinanzeigen-descriptions.md (paste-ready bilingual texts)
```

## Current inventory (for Hawker to eventually manage)

12 live listings, 6 pending photos, total potential €4,400-5,800.
See marketplace repo for full details.
