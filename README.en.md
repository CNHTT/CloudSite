<div align="center">

<img src="https://bweb.help/icon-192.png" width="84" alt="Bweb logo" />

# Bweb

**One sentence to build. One path to grow.**

Lumei runs a cross-border e-commerce business and her own independent site. Every new product and every new market comes with one question: when can the site start bringing customers in?

Lulu is a programmer. He wired AI generation, domains, deployment and growth into one path. Now a new product gets an ad-ready link in minutes.

Cross-border B2B / independent sites · AI generation · Batch building · Cloudflare Pages / Firebase Hosting / EdgeOne Pages / Alibaba Cloud ESA · Domains and HTTPS

[简体中文](README.md) · [English](README.en.md)

[![Next.js](https://img.shields.io/badge/Next.js-16-000000?logo=nextdotjs&logoColor=white)](https://nextjs.org)
[![React](https://img.shields.io/badge/React-19-087EA4?logo=react&logoColor=white)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.9-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Cloudflare Pages](https://img.shields.io/badge/Cloudflare-Pages-F38020?logo=cloudflarepages&logoColor=white)](https://pages.cloudflare.com)
[![Firebase Hosting](https://img.shields.io/badge/Firebase-Hosting-FFCA28?logo=firebase&logoColor=black)](https://firebase.google.com/docs/hosting)
[![EdgeOne Pages](https://img.shields.io/badge/EdgeOne-Pages-0052D9)](https://edgeone.ai)
[![Alibaba Cloud ESA](https://img.shields.io/badge/Alibaba%20Cloud-ESA-FF6A00)](https://www.aliyun.com/product/esa)

[Website](https://bweb.help) · [Get started free](https://bweb.help/en/register) · [Pricing](https://bweb.help/en/pricing) · [MCP setup](#quick-start) · [Changelog](CHANGELOG.md)

</div>

---

## Why Bweb exists

The story starts with a question: "Is the site up?"

It was 2 a.m. Samples for the next day's shipment were piled up in the living room. Lumei was staring at the ad dashboard — campaign built, budget set, one link short. Lulu was staring at the terminal. "Almost." The certificate was still being issued; DNS had just finished propagating.

Lumei sells cross-border: she has a store on Amazon, and she runs her own independent site to take B2B inquiries. Every new product, every ad campaign, every new market needs a landing page she can plug into an ad account or send to a customer. The page itself isn't the hard part — AI can write one in ten minutes. The hard part is everything after it: swapping images and styling, exporting and uploading, installing the CLI, deploying, binding the domain, waiting for the certificate. If any step stalls, the campaign sits there spending nothing and selling nothing, and inquiries never arrive.

What she asked that night wasn't really a technical question. It was: "When can customers start coming in?"

That's when Lulu saw it: AI had already done the step that needed a person most. The next six steps still needed someone to babysit them — and every new product reset the whole queue.

That weekend he wired generation, deployment, domains, and HTTPS into one path. The first time it worked, he typed "build a cross-border site that sells ceramic mugs," and a few minutes later the site opened on his phone.

He sent Lumei the link. She replied "whoa," then asked, "can we add a coupon?"

She became the first user — and the first person to ask for more.

Then more people started asking. Export sellers, cross-border e-commerce teams, factory sales reps, solo operators juggling dozens of landing pages. They were all stuck in the same place: not at writing the page, but at everything after it — nobody wanted to be the human deployment pipeline.

Bweb grew out of those repeated late nights. It puts the whole path in one console:

- **Generate** — build a full site through an AI conversation, or upload static pages you already have
- **Batch** — paste a list or import a CSV; generate, deploy, and bind domains for dozens or hundreds of sites
- **Ship** — call Cloudflare Pages, Firebase Hosting, EdgeOne Pages and Alibaba Cloud ESA (official CLI) directly; no wrangler or Firebase CLI install required
- **Operate** — inquiry forms, live chat, email subscriptions, conversion tracking, SEO/GEO audits, and marketing automation, ready after deploy

We don't hold your domain for you, and we don't lock your customers inside the platform: sites are static files, domains are registered in your name, your email list can be exported at any time, and you can leave whenever you want. Bweb only smooths the road between "it's built" and "it's live."

Lumei rarely asks "is the site up?" anymore. Now she asks: "When can we launch the next market?"

> The sites you publish can run inside Cloudflare's free tier: static hosting, custom domains, automatic HTTPS, and DNS cost nothing extra.

## Who it is for

| You are... | What Bweb removes |
| --- | --- |
| **A cross-border B2B or export seller (including Amazon off-platform traffic)** | Landing pages for every product, market and ad campaign, turning traffic into your own domain and email list |
| **Running cross-border site networks** | Generate and deploy dozens of independent sites, each on its own domain |
| **An indie developer or small team** | No more build pipelines, deploy scripts, and DNS edits for a single landing page |
| **Already generating pages with AI** | Hand over HTML / ZIP; Bweb deploys it, binds the domain, adds forms and chat |
| **An agency or site-building provider** | Multi-tenant isolation, team permissions, wallet and billing, a unified review desk |
| **Automating with agents** | Use your own AI tools — Claude Code, Codex, Workbuddy, Cursor, n8n or any MCP client — to build, edit, publish, and audit sites |

## How export sellers turn a site into inquiries

Traffic inside the marketplace keeps getting more expensive, and the rules — and the account itself — are not yours. An independent site puts the ad traffic, customer emails, and brand assets in your hands.

Bweb handles the heavy lifting:

- **One landing page per campaign** — product launches, promotions, and different audiences, live in minutes
- **Your own domain and HTTPS** — ready for the ad platform, no dev queue
- **Forms that capture leads** — inquiries, email subscriptions, and WhatsApp
- **Multilingual** — one product across markets, with automatic hreflang
- **Batch building** — many sites and markets without hand-deploying each one

[Sign up free and ship your next landing page →](https://bweb.help/en/register)

## From idea to ad-ready site, in one console

| Stage | What you get |
| --- | --- |
| **Generate** | AI builds or rewrites whole pages; multilingual sites generate up to 4 language versions in one pass; attach library images and icons to the prompt |
| **Assemble** | 67 templates (industry sites, cross-border ad pages, event launch pages, company sites and e-commerce landing pages) × 8 visual styles; ZIP / folder upload and site-group import / export |
| **Deploy** | Cloudflare Pages Direct Upload (BLAKE3 asset hashing + manifest), Firebase Hosting REST (gzip + SHA-256), EdgeOne Pages and Alibaba Cloud ESA (official CLI); edit locally with your own tools and upload through the MCP assistant; batch jobs with concurrency, live logs, and cancellation |
| **Domains** | Multiple custom domains per project. Cloudflare writes the proxied CNAME; Firebase/EdgeOne/ESA records are auto-written when a Cloudflare or Aliyun DNS provider is configured, otherwise copyable; ESA applies a free certificate and force-HTTPS 301. Domain services include availability lookup, registration guidance and assisted registration — the domain stays in your name |
| **Grow** | Inquiry forms, live chat, WhatsApp Business, email subscriptions and campaigns, ad conversion tracking, social distribution with UTM, data export, SEO/GEO audits |
| **Collaborate** | Per-account data isolation, team permissions, a single wallet and billing, refunds and credit notes, a unified review desk; pay by WeChat / PayPal / Web3 payments / bank transfer, with invoices |

## What's inside

### 🧱 Build

- **AI site generation and editing** — works with the Anthropic Messages API or any OpenAI-compatible endpoint (OpenAI, DeepSeek, local models). Describe a change on the site page and the AI rewrites the full HTML; save and the preview refreshes.
- **Multilingual** — language pages configured for the target markets, each rendered as its own static page (`index.html`, `en/index.html`, …) with `hreflang`, a shared language switcher, and RTL support.
- **Industry templates** — 62 production-ready templates covering industry sites, cross-border ad pages, company sites, and e-commerce landing pages, with copy, product sections, FAQ, and inquiry blocks; switch between 8 visual styles or keep editing with AI.
- **Manual content editing** — edit page text, titles, meta descriptions, and images block by block; only the matching source is touched, while CSS / JS / inline SVG stay intact.
- **Asset library** — manage images, icons, and SVG / ICO assets; attach up to 8 assets to a single AI request.
- **Site-group portability** — export a group of sites as a ZIP and import it into another account.

### 🚀 Deploy

- **Four targets** — each site can use Cloudflare Pages, Firebase Hosting, Tencent EdgeOne Pages or Alibaba Cloud ESA Pages. Cloudflare/Firebase are Bweb-managed only; EdgeOne/ESA also support IDE deployment and imported sites.
- **No CLI required** — Cloudflare goes through the Pages Direct Upload API, Firebase through the official Hosting REST API. No local wrangler or firebase-tools install.
- **Bring your own toolchain** — edit the site locally with your editor, scripts or AI tools, then upload it through the MCP assistant with `upload_site` (small text sites) or `create_upload_link` (full ZIP) and deploy in the same call. No platform editor required.
- **Batch building** — paste a list or import CSV, choose AI generation / template reuse / built-in template per row; concurrency, domain conflict strategy, live progress, logs, and cancellation.
- **Certificates and DNS** — Cloudflare writes the proxied CNAME automatically; Firebase/EdgeOne/ESA return records and auto-write them when a Cloudflare or Aliyun DNS provider is configured, otherwise you get copyable records. ESA also applies a free Let's Encrypt certificate and force-HTTPS 301.
- **Live preview** — desktop and mobile views, with a shareable preview link.

### 📈 Grow (site enhancement)

Drop one `enhance.js` on the deployed page and you get:

- **Inquiry forms** — detect forms already on the page or generate a standard inquiry form; submissions land in the console
- **Live chat** — on-site conversations plus WhatsApp Business Cloud API, with AI replies, asset attachments, and message revocation
- **Email subscriptions and campaigns** — subscription capture, confirmation emails, campaigns, A/B tests, send-time windows, bounce circuit breakers, DMARC / blocklist checks
- **Conversion tracking** — ad-platform conversion events and attribution
- **SEO / GEO audit** — check `index.html`, `robots.txt`, `llms.txt` / `llms-full.txt`, and `sitemap.xml` locally or against a live domain; get a total score, per-item evidence, and prioritized fixes that can be handed back to the AI
- **Analytics and export** — inquiries, conversations, subscriptions, traffic, and conversions in one place, with export
- **Quotations / sample orders / bookings** — standalone documents, four templates, preview plus HTML/PDF export, customer accept/decline, sample payments and shipments, booking records
- **Social distribution** — schedule content, generate UTM links, and record performance

### 🤖 Agents and APIs

- **MCP** — a standard MCP Streamable HTTP endpoint at `https://bweb.help/api/mcp`. **No AI platform lock-in**: connect Claude Code, Codex, Workbuddy, Cursor, n8n or your own MCP client with one command. 159 tools cover sites, files, publishing, domains, inquiries, chat, subscriptions, quotations, sample orders, bookings, marketing email, social distribution, analytics and the Agent workspace; module endpoints are available at `/api/mcp/sites|publish|growth|marketing|social|agent`.
- **Bring your own AI** — Bweb does not require a specific model or client. Built-in models power site generation, Agent tasks and on-site AI features; day-to-day operations, analytics and customer conversations run through your own AI over MCP. Switching clients does not change the setup.
- **Organized by capability** — sites and publishing 19, launch verification and adoption 17, site growth 43, marketing and automation 30, social distribution 16, Agent workspace 32, account 2. Each domain has its own doc under “MCP docs” below.
- **Read-write and read-only tokens** — read-only tokens never expose write tools in `tools/list`, so they are safe to hand to a third party for review. Tokens can be scoped to specific sites, given an expiry, and revoked at any time.
- **Explicit confirmation and audit** — sending campaigns, activating automations and social dispatch require `confirm=true`; every call records the token, tool, site, IP and `request_id`.
- **Plugin-free API** — `/api/v1` with a site key lets pages generated by third-party tools use the enhancement features without a backend.
- **Zero-dependency bridge** — `mcp/cloudsite-mcp.mjs` is included for clients that only speak stdio. The file name and `CLOUDSITE_` env vars keep the legacy prefix for backward compatibility; the product brand is Bweb.

## Quick start

Bweb exposes a standard MCP Streamable HTTP endpoint with no AI platform lock-in. Nothing to deploy: create an account, get a token, point your own AI tools (Claude Code, Codex, Workbuddy, Cursor, n8n and others) at the endpoint, and start building, publishing, binding domains, and handling inquiries, chat, subscriptions and campaigns.

### 1. Create an access token

Sign in to the [Bweb console](https://bweb.help) → **Settings → MCP / Agent** → **Create token**.

- Tokens start with `cs_` and are shown only once
- A **read-write token** can create, generate, upload, publish, and bind domains
- A **read-only token** can inspect sites and business data; `tools/list` never exposes write tools

### 2. Connect a client

Claude Code (HTTP, recommended):

```bash
claude mcp add --transport http cloudsite https://bweb.help/api/mcp \
  --header "Authorization: Bearer cs_your_token"
```

Codex, or any client that only supports stdio:

```bash
curl -O https://bweb.help/cloudsite-mcp.mjs
```

The script keeps the `cloudsite-mcp.mjs` filename and `CLOUDSITE_` env prefix for backward compatibility.

Then add this to `~/.codex/config.toml`:

```toml
[mcp_servers.cloudsite]
command = "node"
args = ["/absolute/path/cloudsite-mcp.mjs"]
env = { CLOUDSITE_URL = "https://bweb.help", CLOUDSITE_API_TOKEN = "cs_your_token" }
```

Other MCP clients that speak HTTP (including Workbuddy, Cursor, Claude Desktop and custom agents):

```json
{
  "mcpServers": {
    "cloudsite": {
      "type": "http",
      "url": "https://bweb.help/api/mcp",
      "headers": { "Authorization": "Bearer cs_your_token" }
    }
  }
}
```

> **The list above is not exhaustive.** As long as a client speaks MCP (Streamable HTTP or stdio), it works: Workbuddy, Cursor, Claude Desktop, n8n, Make, Zapier, ChatGPT when it supports remote MCP, or your own scripts. Tools, permissions, quotas and audit are identical — switching clients does not change the setup.

### 3. Call the tools

Once connected, just describe what you want:

> Use `create_site` to create "Acme Robotics" for industrial robot arms, in English, then `generate_site` to build the pages.

> Upload `/path/to/site` as `my-site`, publish it with `deploy_site`, and bind `demo.example.com` with `bind_domain`.

> Run `enhance_seo_audit` on `my-site` with `mode=live`, then hand the fixes to `chat_site`.

You can also send JSON-RPC directly:

```bash
curl https://bweb.help/api/mcp \
  -H "Authorization: Bearer cs_your_token" \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "tools/call",
    "params": {
      "name": "list_sites",
      "arguments": {}
    }
  }'
```

**Edit with your own tools, then let the MCP assistant upload it**

No platform editor required. Change the site locally with your editor, scripts or AI tools, then tell the MCP client:

> Upload `/path/to/my-site` as `my-site`, publish it, and give me a preview link.

The MCP assistant calls `upload_site` (a few text files) or `create_upload_link` (a full ZIP and a single-use upload URL). Preview with `preview_site`, then publish with `deploy_site`; pass `deploy=true` on upload to do it in one step. For pages generated by other tools, `enhance_embed_inject` can add `enhance.js`.

Common tools:

| Tool | What it does |
| --- | --- |
| `list_sites` / `get_site` | Inspect sites and details |
| `create_site` / `generate_site` | Create a site and generate all pages with AI |
| `upload_site` / `create_upload_link` | Upload a local static site (text files or full ZIP), optionally deploying in the same call |
| `chat_site` | Edit a site through conversation |
| `deploy_site` | Publish to Cloudflare Pages / Firebase Hosting / EdgeOne Pages / ESA Pages |
| `bind_domain` | Attach a custom domain |
| `enhance_seo_audit` | SEO / GEO audit |
| `marketing_*` / `enhance_*` | Marketing email, inquiries, chat, subscriptions, analytics |

The full tool list is available in the console under **Settings → MCP / Agent**.

### MCP docs

| Capability | Doc | Tools | Coverage |
| --- | --- | --- | --- |
| Sites, files and publishing | [docs/mcp/en/sites.md](docs/mcp/en/sites.md) | 15 | Site and file inspection, AI generation, chat edits, ZIP upload, preview, deploy, custom domains |
| Site growth | [docs/mcp/en/growth.md](docs/mcp/en/growth.md) | 31 | Inquiries and leads, live chat, visitor accounts, subscriptions, tracking and consent, SEO/GEO audits, external-site embedding, exports, analytics |
| Marketing email and automation | [docs/mcp/en/marketing.md](docs/mcp/en/marketing.md) | 30 | Subscribers, lists, templates, sending channels, campaigns, automations, suppression, price quotes |
| Social distribution | [docs/mcp/en/social.md](docs/mcp/en/social.md) | 16 | Post drafts, compliance checks, job claiming, publish reporting, metrics |
| Agent workspace | [docs/mcp/en/agent.md](docs/mcp/en/agent.md) | 29 | Tasks, skill library, per-site knowledge, plans, approvals, artifacts and reviews |
| Setup overview | [docs/mcp/en/README.md](docs/mcp/en/README.md) | 159 | Endpoint, tokens, client setup, permissions, limits and troubleshooting |

The authoritative tool list is whatever `tools/list` returns.

No account yet? [Sign up free](https://bweb.help/en/register), then create a token under **Settings → MCP / Agent**.

## Add enhancements to an existing page

Already have a backend, or building pages with another tool? Create a site key in the site details, use it with `/api/v1`, drop `enhance.js` into the page, and you get inquiries, chat, subscriptions, and tracking without touching the backend.

## Learn more

| Page | Contents |
| --- | --- |
| [Features and pricing](https://bweb.help/en/pricing) | Plans, quotas, and billing |
| [Guide](https://bweb.help/en/guide) | End-to-end: create a site, publish it, bind a domain |
| [Use cases](https://bweb.help/en/use-cases) | Cross-border B2B lead generation, site networks, multilingual sites |
| MCP setup | [Setup overview](docs/mcp/en/README.md), client config, tokens and per-domain docs (see “MCP docs” above) |
| Public API | `/api/v1` site keys and plugin-free embedding (create a key in site details) |

## Contact and support

- Email: **cnhttt@163.com**
- Questions, requests, or partnerships: open an issue or email us
- Happy to talk about site building, SEO/GEO, or site-network automation

## Get started

[**Sign up free**](https://bweb.help/en/register) · [Pricing](https://bweb.help/en/pricing) · [Connect MCP](#quick-start)

If Bweb saves you time, a **Star ⭐** is appreciated.
