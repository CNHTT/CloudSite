<div align="center">

<img src="https://cloudsite.editorapi.com/icon-192.png" width="84" alt="CloudSite logo" />

# CloudSite

**One idea in. A landing page ready to run ads.**

My girlfriend runs an Amazon store and an independent site. Every new product comes with one question: when can we start running ads?

So I wired AI generation, deployment, and domains into one path. Now she has an ad-ready link in minutes.

Amazon / DTC landing pages · AI generation · Batch building · Cloudflare Pages / Firebase Hosting · Automatic domains and HTTPS

[简体中文](README.md) · [English](README.en.md)

[![Next.js](https://img.shields.io/badge/Next.js-16-000000?logo=nextdotjs&logoColor=white)](https://nextjs.org)
[![React](https://img.shields.io/badge/React-19-087EA4?logo=react&logoColor=white)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.9-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Cloudflare Pages](https://img.shields.io/badge/Cloudflare-Pages-F38020?logo=cloudflarepages&logoColor=white)](https://pages.cloudflare.com)
[![Firebase Hosting](https://img.shields.io/badge/Firebase-Hosting-FFCA28?logo=firebase&logoColor=black)](https://firebase.google.com/docs/hosting)

[Website](https://cloudsite.editorapi.com) · [Get started free](https://cloudsite.editorapi.com/en/register) · [Pricing](https://cloudsite.editorapi.com/en/pricing) · [MCP setup](#quick-start)

</div>

---

## Why CloudSite exists

The story starts at 2 a.m.

"Is the landing page up?"

She asked without looking up. The living room was full of boxes waiting to ship. I stared at my screen. "Almost." The certificate hadn't even gone live yet.

She sells on Amazon, and she also runs an independent store to build traffic she owns. Every new product, every ad campaign, every new market needed a landing page she could plug into an ad account or send to a group chat. The page itself was easy — AI could write it in ten minutes. Everything after it was the problem: swapping images, exporting, uploading, binding the domain, waiting for the certificate. Her ad campaigns were ready; her landing pages were still queued behind me. She wanted a link she could launch immediately. What she got was "almost there — DNS is still propagating."

And that's when it hit me: AI can already write the page. Why am I still babysitting everything after it?

That weekend I wired generation, deployment, domains, and HTTPS into one path. The first time it worked, I typed "make me a landing page that sells mugs," and a few minutes later the site opened on my phone.

I sent her the link. She replied "whoa," then asked, "can we add a coupon?"

She became the first user — and the first person to ask for more features.

Then friends started asking. People selling on Amazon, running independent stores, or juggling a pile of landing pages were all repeating my routine.

That's how CloudSite grew from a boyfriend's shortcut into what it is now: fewer late nights for me, fewer headaches for anyone else selling on Amazon or building their own site.

It puts the whole path in one console:

- **Generate** — build a full site through an AI conversation, or upload static pages you already have
- **Batch** — paste a list or import a CSV; generate, deploy, and bind domains for dozens or hundreds of sites
- **Ship** — call the Cloudflare Pages / Firebase Hosting APIs directly; no wrangler or Firebase CLI required
- **Operate** — inquiry forms, live chat, email subscriptions, conversion tracking, SEO/GEO audits, and marketing automation, ready after deploy

> The sites you publish can run inside Cloudflare's free tier: static hosting, custom domains, automatic HTTPS, and DNS cost nothing extra.

## Who it is for

| You are... | What CloudSite removes |
| --- | --- |
| **An Amazon or cross-border seller** | Landing pages for every product and ad campaign, turning off-platform traffic into your own domain and email list |
| **Running cross-border site networks** | Generate and deploy dozens of independent sites, each on its own domain |
| **An indie developer or small team** | No more build pipelines, deploy scripts, and DNS edits for a single landing page |
| **Already generating pages with AI** | Hand over HTML / ZIP; CloudSite deploys it, binds the domain, adds forms and chat |
| **An agency or site-building provider** | Multi-tenant isolation, team permissions, wallet and billing, a unified review desk |
| **Automating with agents** | Use Claude Code, Codex, or any MCP client to build, edit, publish, and audit sites |

## How Amazon sellers drive traffic to their own site

Traffic inside the marketplace keeps getting more expensive, and the rules — and the account itself — are not yours. An independent site puts the ad traffic, customer emails, and brand assets in your hands.

CloudSite handles the heavy lifting:

- **One landing page per campaign** — product launches, promotions, and different audiences, live in minutes
- **Your own domain and HTTPS** — ready for the ad platform, no dev queue
- **Forms that capture leads** — inquiries, email subscriptions, and WhatsApp
- **Multilingual** — one product across markets, with automatic hreflang
- **Batch building** — many sites and markets without hand-deploying each one

[Sign up free and ship your next landing page →](https://cloudsite.editorapi.com/en/register)

## From idea to ad-ready site, in one console

| Stage | What you get |
| --- | --- |
| **Generate** | AI builds or rewrites whole pages; multilingual sites generate up to 4 language versions in one pass; attach library images and icons to the prompt |
| **Assemble** | 11 industry templates (industrial machinery, home & living, consumer electronics, apparel, food & beverage, beauty, medical, construction, agriculture, auto parts, packaging); ZIP / folder upload and site-group import / export |
| **Deploy** | Cloudflare Pages Direct Upload (BLAKE3 asset hashing + manifest) and Firebase Hosting REST (gzip + SHA-256), no CLI dependency; batch jobs with concurrency, live logs, and cancellation |
| **Domains** | Multiple custom domains per project; Cloudflare proxied CNAME plus certificate handled automatically; Firebase A / TXT records written automatically or explained clearly |
| **Grow** | Inquiry forms, live chat, WhatsApp Business, email subscriptions and campaigns, ad conversion tracking, data export, SEO/GEO audits |
| **Collaborate** | Per-account data isolation, team permissions, a single wallet and billing, refunds and credit notes, a unified review desk, Alipay and invoices |

## What's inside

### 🧱 Build

- **AI site generation and editing** — works with the Anthropic Messages API or any OpenAI-compatible endpoint (OpenAI, DeepSeek, local models). Describe a change on the site page and the AI rewrites the full HTML; save and the preview refreshes.
- **Multilingual** — up to 4 languages, each rendered as its own static page (`index.html`, `en/index.html`, …) with `hreflang`, a shared language switcher, and RTL support.
- **Industry templates** — 11 production-ready landing pages with copy, product sections, FAQ, and inquiry blocks; keep editing them with AI.
- **Manual content editing** — edit page text, titles, meta descriptions, and images block by block; only the matching source is touched, while CSS / JS / inline SVG stay intact.
- **Asset library** — manage images, icons, and SVG / ICO assets; attach up to 8 assets to a single AI request.
- **Site-group portability** — export a group of sites as a ZIP and import it into another account.

### 🚀 Deploy

- **Two targets** — each site can use Cloudflare Pages or Firebase Hosting, and can switch at any time.
- **No CLI required** — Cloudflare goes through the Pages Direct Upload API, Firebase through the official Hosting REST API. No local wrangler or firebase-tools install.
- **Batch building** — paste a list or import CSV, choose AI generation / template reuse / built-in template per row; concurrency, domain conflict strategy, live progress, logs, and cancellation.
- **Certificates and DNS** — proxied CNAME written automatically for Cloudflare-hosted domains; for Firebase, DNS is written automatically when the domain is in a connected Cloudflare account, otherwise you get clear manual instructions.
- **Live preview** — desktop and mobile views, with a shareable preview link.

### 📈 Grow (site enhancement)

Drop one `enhance.js` on the deployed page and you get:

- **Inquiry forms** — detect forms already on the page or generate a standard inquiry form; submissions land in the console
- **Live chat** — on-site conversations plus WhatsApp Business Cloud API, with AI replies, asset attachments, and message revocation
- **Email subscriptions and campaigns** — subscription capture, confirmation emails, campaigns, A/B tests, send-time windows, bounce circuit breakers, DMARC / blocklist checks
- **Conversion tracking** — ad-platform conversion events and attribution
- **SEO / GEO audit** — check `index.html`, `robots.txt`, `llms.txt` / `llms-full.txt`, and `sitemap.xml` locally or against a live domain; get a total score, per-item evidence, and prioritized fixes that can be handed back to the AI
- **Analytics and export** — inquiries, conversations, subscriptions, traffic, and conversions in one place, with export

### 🤖 Agents and APIs

- **MCP** — a standard MCP Streamable HTTP endpoint at `/api/mcp`. Claude Code, Codex, Workbuddy, and other clients can list sites, generate pages, upload ZIPs, publish, bind domains, and run SEO audits.
- **Read-write and read-only tokens** — read-only tokens never expose write tools, so they are safe to hand to a third party for review.
- **Plugin-free API** — `/api/v1` with a site key lets pages generated by third-party tools use the enhancement features without a backend.
- **Zero-dependency bridge** — `mcp/cloudsite-mcp.mjs` is included for clients that only speak stdio.

## Quick start

CloudSite exposes a standard MCP Streamable HTTP endpoint. Nothing to deploy: create an account, get a token, connect your AI client, and start building, publishing, and binding domains.

### 1. Create an access token

Sign in to the [CloudSite console](https://cloudsite.editorapi.com) → **Settings → MCP / Agent** → **Create token**.

- Tokens start with `cs_` and are shown only once
- A **read-write token** can create, generate, upload, publish, and bind domains
- A **read-only token** can inspect sites and business data; `tools/list` never exposes write tools

### 2. Connect a client

Claude Code (HTTP, recommended):

```bash
claude mcp add --transport http cloudsite https://cloudsite.editorapi.com/api/mcp \
  --header "Authorization: Bearer cs_your_token"
```

Codex, or any client that only supports stdio:

```bash
curl -O https://cloudsite.editorapi.com/cloudsite-mcp.mjs
```

Then add this to `~/.codex/config.toml`:

```toml
[mcp_servers.cloudsite]
command = "node"
args = ["/absolute/path/cloudsite-mcp.mjs"]
env = { CLOUDSITE_URL = "https://cloudsite.editorapi.com", CLOUDSITE_API_TOKEN = "cs_your_token" }
```

Other MCP clients that speak HTTP:

```json
{
  "mcpServers": {
    "cloudsite": {
      "type": "http",
      "url": "https://cloudsite.editorapi.com/api/mcp",
      "headers": { "Authorization": "Bearer cs_your_token" }
    }
  }
}
```

### 3. Call the tools

Once connected, just describe what you want:

> Use `create_site` to create "Acme Robotics" for industrial robot arms, in English, then `generate_site` to build the pages.

> Upload `/path/to/site` as `my-site`, publish it with `deploy_site`, and bind `demo.example.com` with `bind_domain`.

> Run `enhance_seo_audit` on `my-site` with `mode=live`, then hand the fixes to `chat_site`.

You can also send JSON-RPC directly:

```bash
curl https://cloudsite.editorapi.com/api/mcp \
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

Common tools:

| Tool | What it does |
| --- | --- |
| `list_sites` / `get_site` | Inspect sites and details |
| `create_site` / `generate_site` | Create a site and generate all pages with AI |
| `upload_site` / `create_upload_link` | Upload a local static site (text files or ZIP) |
| `chat_site` | Edit a site through conversation |
| `deploy_site` | Publish to Cloudflare Pages / Firebase Hosting |
| `bind_domain` | Attach a custom domain |
| `enhance_seo_audit` | SEO / GEO audit |
| `marketing_*` / `enhance_*` | Marketing email, inquiries, chat, subscriptions, analytics |

The full tool list is available in the console under **Settings → MCP / Agent**.

No account yet? [Sign up free](https://cloudsite.editorapi.com/en/register), then create a token under **Settings → MCP / Agent**.

## Add enhancements to an existing page

Already have a backend, or building pages with another tool? Create a site key in the site details, use it with `/api/v1`, drop `enhance.js` into the page, and you get inquiries, chat, subscriptions, and tracking without touching the backend.

## Learn more

| Page | Contents |
| --- | --- |
| [Features and pricing](https://cloudsite.editorapi.com/en/pricing) | Plans, quotas, and billing |
| [Guide](https://cloudsite.editorapi.com/en/guide) | End-to-end: create a site, publish it, bind a domain |
| [Use cases](https://cloudsite.editorapi.com/en/use-cases) | Amazon off-platform traffic, site networks, multilingual sites |
| MCP setup | Client setup, tokens, and the full tool list (see Quick start) |
| Public API | `/api/v1` site keys and plugin-free embedding (create a key in site details) |

## Contact and support

- Email: **cnhttt@163.com**
- Questions, requests, or partnerships: open an issue or email us
- Happy to talk about site building, SEO/GEO, or site-network automation

## Get started

[**Sign up free**](https://cloudsite.editorapi.com/en/register) · [Pricing](https://cloudsite.editorapi.com/en/pricing) · [Connect MCP](#quick-start)

If CloudSite saves you time, a **Star ⭐** is appreciated.
