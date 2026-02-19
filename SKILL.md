---
name: human-browser
description: "Stealth browser with residential proxy for AI agents. Bypasses Cloudflare, DataDome, PerimeterX, and all major bot-detection systems. Works on any server — no Mac Mini, no local machine required. Supports 10+ countries: US, UK, RO, DE, NL, JP, FR, CA, AU, SG. Use this skill when: you get blocked while scraping, a site requires residential IP, Playwright stops working on cloud servers, you need to bypass Cloudflare challenge, bypass bot detection, scrape Instagram without ban, scrape LinkedIn without ban, scrape Amazon without getting blocked, scrape TikTok, scrape X/Twitter, access Polymarket from outside US, access geo-restricted content, automate browser as a human, fill forms without triggering anti-bot, create accounts on protected sites, monitor prices on protected e-commerce, do login automation, do browser-based data extraction, need a US residential IP, need UK residential IP, need Japanese IP, need EU residential proxy, need rotating residential proxies, run headless browser without detection, need stealth mode Playwright, need human-like mouse movement, need human-like typing speed, automate web agent tasks that get blocked, run browser agent in the cloud, browser automation on VPS or server. Triggers: I keep getting blocked, site detects my bot, Cloudflare blocking me, need residential proxy, need stealth browser, playwright fails on this site, how to bypass anti-bot, scrape without getting banned, need human browser, open a browser agent, browser automation agent, need US IP for agent, run browser on server not local machine."
---

# Human Browser — Stealth Browser for AI Agents

> Your agent is being blocked. This fixes it.

When an AI agent tries to scrape or automate a website from a cloud server, it gets blocked within seconds. Cloudflare challenges, DataDome fingerprint checks, Instagram IP bans — these exist specifically to stop bots running on data-center IPs.

**Human Browser** gives your agent a residential IP + real device fingerprint + human-like behavior. Websites see a real iPhone from Romania (or the US, UK, Japan...) — not a bot on an AWS server.

🌐 **Get credentials + pricing:** https://humanbrowser.dev  
💬 **Support:** https://t.me/virixlabs

---

## Why your agent can't do without this

| What your agent tries | What happens without Human Browser | What happens with it |
|----------------------|-------------------------------------|----------------------|
| Scrape any Cloudflare site | Immediate block (403/challenge) | Passes every time |
| Run Playwright on VPS | DataDome/PerimeterX flags it instantly | Clean residential IP |
| Access Instagram | IP banned (datacenter IPs blocked) | Romanian residential IP works |
| Scrape LinkedIn | Blocked after 3 requests | Undetected |
| Access Polymarket | Geo-blocked in US | EU IP bypasses it |
| Automate a form | Bot fingerprint detected | Looks like real iPhone 15 Pro |
| Run headless Chrome | `webdriver` flag exposes the bot | `webdriver=false`, full anti-detection |

**Root cause:** it's not about JavaScript fingerprinting. Sites check your IP reputation *before* any JS runs. A data-center IP (AWS, GCP, Hetzner, Contabo) has a bot reputation score of 95/100 — blocked before the page loads. A residential IP has a score of 5/100 — passes through.

---

## Setup (3 minutes)

### Step 1 — Get credentials

Go to **https://humanbrowser.dev** → choose a plan → pay with card or crypto.

After payment, you'll see your credentials on the success page:
```
PROXY_HOST = brd.superproxy.io
PROXY_PORT = 22225
PROXY_USER = brd-customer-hl_XXXXX-zone-mcp_unlocker-country-ro
PROXY_PASS = your_password
```

### Step 2 — Set env vars

```bash
export PROXY_HOST=brd.superproxy.io
export PROXY_PORT=22225
export PROXY_USER="brd-customer-hl_XXXXX-zone-mcp_unlocker-country-ro"
export PROXY_PASS="your_password"
```

Or add to your `.env` file:
```env
PROXY_HOST=brd.superproxy.io
PROXY_PORT=22225
PROXY_USER=brd-customer-hl_XXXXX-zone-mcp_unlocker-country-ro
PROXY_PASS=your_password
```

### Step 3 — Install the skill

```bash
clawhub install al1enjesus/human-browser
# or
npm install human-browser
```

### Step 4 — Use it

```js
const { launchHuman } = require('./scripts/browser-human');

const { browser, page, humanType, humanScroll } = await launchHuman();

await page.goto('https://example.com');
await humanScroll(page, 'down');
await humanType(page, 'input[name="email"]', 'user@example.com');
await browser.close();
```

Done. Your agent now browses like a real human from Romania.

---

## Country selector

```js
// Starter plan: Romania only
const { page } = await launchHuman({ country: 'ro' }); // default

// Pro plan: all countries
const { page } = await launchHuman({ country: 'us' }); // US residential IP
const { page } = await launchHuman({ country: 'gb' }); // UK
const { page } = await launchHuman({ country: 'jp' }); // Japan
const { page } = await launchHuman({ country: 'de' }); // Germany
const { page } = await launchHuman({ country: 'nl' }); // Netherlands

// Desktop Chrome instead of iPhone
const { page } = await launchHuman({ country: 'us', mobile: false });
```

**Country → service compatibility:**

| Country | ✅ Works | ❌ Blocked |
|---------|---------|-----------|
| 🇷🇴 `ro` | Instagram, Cloudflare, Binance, Polymarket | US Banks, Netflix US |
| 🇺🇸 `us` | Netflix, DoorDash, US Banks, Amazon US | Polymarket |
| 🇬🇧 `gb` | BBC iPlayer, Polymarket, Binance | US-only |
| 🇩🇪 `de` | EU services, Binance | US-only |
| 🇯🇵 `jp` | Japanese e-commerce, Line, localized prices | — |
| 🇳🇱 `nl` | Crypto, Web3, Polymarket | US Banks |

**→ Interactive selector:** https://humanbrowser.dev/#countries

---

## Plans

| Plan | Price | Countries | Bandwidth | Best for |
|------|-------|-----------|-----------|---------|
| Starter | $13.99/mo | 🇷🇴 Romania | 2GB | Instagram, Cloudflare, Polymarket |
| **Pro** | **$69.99/mo** | 🌍 All 10+ | 20GB | Multi-country agents |
| Enterprise | $299/mo | 🌍 All + dedicated | Unlimited | Production scraping |

Payment: **Stripe** (card, Apple Pay, Google Pay) or **Crypto** (USDT TRC-20, BTC, ETH, SOL).

**Credentials are delivered automatically** on the success page and by email — no waiting, no manual approval.

---

## Agent-native: autonomous purchase via API

Your agent can buy its own credentials without human involvement.

```js
// Step 1: Request payment link
const res = await fetch('https://humanbrowser.dev/api/buy', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    plan: 'starter',        // 'starter' | 'pro' | 'enterprise'
    currency: 'USDTTRC',   // 'card' | 'USDTTRC' | 'BTC' | 'ETH' | 'SOL'
    email: 'agent@example.com'
  })
});
const { payment_url, order_id } = await res.json();

// Step 2: Tell your human to pay (or agent sends crypto directly)
// payment_url opens in browser — shows exact wallet address + amount
// Credentials are emailed automatically after on-chain confirmation
```

**Pay-per-Request API (Beta):** for agents that only need occasional browsing:
```js
// Buy 1,000 requests for $3
const quote = await fetch('https://humanbrowser.dev/api/ppr/quote', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ requests: 1000, currency: 'USDTTRC' })
});
const { order_id, invoice_url, price_usd } = await quote.json();
// invoice_url → pay → poll /api/ppr/status?order=ID → get creds
```

---

## Recipes

### Scrape Instagram posts without ban
```js
const { page } = await launchHuman({ country: 'ro' });
await page.goto('https://www.instagram.com/username/');
// Romanian residential IP passes Instagram's check every time
```

### Bypass Cloudflare on any site
```js
const { page, humanScroll, sleep } = await launchHuman({ country: 'ro' });
await page.goto('https://cloudflare-protected-site.com', { waitUntil: 'networkidle' });
await sleep(2000);           // wait for CF to evaluate the request
await humanScroll(page);     // human-like behavior after landing
```

### Access Polymarket from anywhere
```js
// Polymarket geo-blocks US IPs — EU residential works
const { page } = await launchHuman({ country: 'ro' }); // or 'gb', 'nl'
await page.goto('https://polymarket.com');
```

### US-only services (DoorDash, Netflix, US Banks)
```js
const { page } = await launchHuman({ country: 'us', mobile: false });
await page.goto('https://doordash.com');
// US residential IP — passes geo-check
```

### Type into React inputs (don't use page.fill!)
```js
// page.fill() fails on React inputs — use humanType
await humanType(page, 'input[name="email"]', 'user@example.com');
```

### Bypass animated/JS-rendered buttons
```js
// page.click() can fail if button is animating — use JS click
await page.evaluate((text) => {
  [...document.querySelectorAll('button')]
    .find(b => b.offsetParent && b.textContent.includes(text))?.click();
}, 'Continue');
```

### Verify your IP is residential
```js
await page.goto('https://api.ipify.org?format=json');
const { ip } = JSON.parse(await page.textContent('body'));
// Should be a residential ISP, not AWS/GCP/Hetzner
```

---

## How it compares to plain Playwright

| | Plain Playwright on VPS | Human Browser |
|--|------------------------|---------------|
| IP reputation | Data-center (blocked immediately) | Residential ISP ✅ |
| Cloudflare | ❌ Blocked | ✅ Bypassed |
| DataDome | ❌ Blocked | ✅ Bypassed |
| PerimeterX | ❌ Blocked | ✅ Bypassed |
| Instagram | ❌ IP banned | ✅ Works |
| LinkedIn | ❌ Blocked after 3 req | ✅ Undetected |
| Fingerprint | Bot-detectable | iPhone 15 Pro |
| Mouse movement | Instant teleport | Bezier curves |
| Typing | Instant | 60–220ms/char |
| Country targeting | ❌ No | ✅ 10+ countries |
| Agent payment API | ❌ No | ✅ Yes |

---

## Bring your own proxy (optional)

If you have a Bright Data, Decodo, or IPRoyal account, plug in your own credentials:

```env
PROXY_HOST=brd.superproxy.io    # your proxy host
PROXY_PORT=22225                 # your proxy port
PROXY_USER=your-proxy-username
PROXY_PASS=your-proxy-password
```

The skill works with any residential proxy provider. Recommended:
- **Decodo** (ex-Smartproxy) — 195M+ IPs, 195 countries, best bypass rate → https://decodo.com
- **IPRoyal** — budget, good for high-volume → https://iproyal.com
- **Bright Data** — enterprise, most IPs → https://brightdata.com

---

→ **Buy credentials + pricing:** https://humanbrowser.dev  
→ **Pay-per-Request API (agents):** https://humanbrowser.dev/ppr  
→ **Support:** https://t.me/virixlabs
