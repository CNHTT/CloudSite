# Changelog

## v1.1.0 — 2026-11-19

### Deploy
- Four deploy targets: Cloudflare Pages, Firebase Hosting, EdgeOne Pages and Alibaba Cloud ESA Pages.
- Cloudflare / Firebase sites are Bweb-managed only; EdgeOne / ESA also support IDE-deployed (`linked`) and imported (`imported`) sites.
- ESA gets automatic project config, free Let's Encrypt certificate and force-HTTPS 301.

### Domains and DNS
- Firebase / EdgeOne / ESA return DNS records and auto-write them when a Cloudflare or Aliyun DNS provider is configured; otherwise the console shows copyable records.
- New MCP tools `domain_dns_apply` and `domain_status_refresh`; conflict replacement requires explicit confirmation.
- ESA CNAME now shows the full target (`<host>.<cname-zone>`), matching the Aliyun DNS console.

### B2B documents
- Standalone quotations without an RFQ lead (`customer_name` + items), plus four document templates.
- Quotations and sample orders support preview and HTML/PDF export; the public quotation page uses the selected template.
- Sample orders can be created without a quotation, with wallet-billed customer email and resend.

### MCP
- 159 tools: sites 19, publish 17, growth 43, marketing 30, social 16, agent 32, meta 2.
- New tools: `quote_document`, `sample_order_list/get/create/send/document`, `booking_list/cancel`, `domain_dns_apply`, `domain_status_refresh`.
- `capabilities` now reports shared storage usage, deploy-provider modes, document links and domain capabilities.

### Storage
- One 100 MB account pool shared by media assets, site source files and OSS backups; purchased storage extends the same pool.

### Fixes
- Booking settings no longer overwritten by background refresh.
- Booking records auto-refresh; lead tabs work without a cached 308.
- Public sample-order payment form no longer crashes before rendering.
- Admin wallet/redeem pages show errors with retry instead of a permanent spinner.
- Viewer roles can no longer pay domain orders, submit proofs or edit guidance checklists.

## v1.0.0 — 2026-11-17

- First public release: AI site generation, 67 templates × 8 visual styles, Cloudflare Pages / Firebase Hosting deployment, custom domains, inquiries, chat, subscriptions, marketing automation, social distribution, SEO/GEO audits and MCP access.
