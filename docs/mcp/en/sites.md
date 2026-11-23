# Sites, files and publishing

The full site lifecycle: inspect, generate, edit, upload, preview, deploy and bind domains. **21 tools**.

**Edit with your own tools:** change the files locally with your editor, scripts or AI tools, then upload them through the MCP assistant with `upload_site` / `create_upload_link`. No platform editor and no CLI required.

```text
edit locally → upload_site / create_upload_link → preview_site → deploy_site
```

## Tools

| Tool | R/W | What it does |
| --- | --- | --- |
| `list_sites` | Read | List sites in the account (or team scope) |
| `get_site` | Read | Site details: status, domains, deployments and enhancement settings |
| `list_site_files` | Read | List site files and sizes |
| `read_site_file` | Read | Read one file; text as utf8, binary as base64, up to 2MB |
| `preview_site` | Read | Create a public signed preview link, 24 hours by default (1–72 hours) |
| `get_task` | Read | Poll an async generation or edit task |
| `create_site` | Write | Create a site (name, product, target languages) |
| `generate_site` | Write | Generate a full site with the platform AI; style, accent color and language supported |
| `chat_site` | Write | Edit a site conversationally with section-level targeting, not a full rewrite |
| `site_content_get` | Read | List language pages and editable fields (`t0` ids, tags, styles, language) |
| `site_content_translate` | Write | Detect the language of one text field and translate it into the site's other language pages |
| `upload_site` | Write | Inline upload of text files or base64 binaries, optionally deploy |
| `create_upload_link` | Write | Create a single-use ZIP upload link for a full static site |
| `write_site_file` | Write | Write or replace one text file and mark the site for deployment |
| `delete_site_file` | Write | Delete one file; `index.html` is protected |
| `deploy_site` | Write | Publish to Cloudflare Pages / Firebase Hosting / EdgeOne Pages / ESA Pages; CF/FB are Bweb-managed only, EO/ESA also support IDE deployments |
| `bind_domain` | Write | Attach a custom domain. Cloudflare writes the CNAME; Firebase/EdgeOne/ESA auto-write when a DNS provider is configured and return copyable records otherwise. ESA also applies a free certificate and force-HTTPS |
| `domain_dns_apply` | Write | Retry writing a bound domain's DNS records through Cloudflare/Aliyun DNS; replacing conflicts needs user confirmation |
| `domain_status_refresh` | Read | Refresh DNS, certificate and ESA force-HTTPS status |

> Read-only tokens can only use the read tools. Deployment and domain binding require credentials for the site's chosen provider (Cloudflare / Firebase / EdgeOne / ESA) already configured in the console.

## Typical build flow

```text
create_site    name="Acme Robotics"  product="industrial robot arms"  language="English"
generate_site  slug="acme-robotics"  style="modern minimal"  accent="#f97316"
preview_site   slug="acme-robotics"  path="/"  expires_hours=24
deploy_site    slug="acme-robotics"
bind_domain    slug="acme-robotics"  domain="www.acme-robotics.com"
```

## Generation and editing

- `create_site` creates the site, then `generate_site` builds the pages. You can set language, style and brand color in the same flow.
- `chat_site` is for requests like "shorten the hero headline" or "change shipping to 3–5 business days". It edits only the affected sections; CSS, JS and inline SVG stay untouched.
- When the client tool timeout is short, both generation tools support `wait=false`:

```text
generate_site  slug="acme-robotics"  wait=false
→ { "task_id": "…", "status": "running" }

get_task  task_id="…"
→ { "status": "completed", "result": { "site": …, "chars": … } }
```

- Up to 2 long-running tasks per account. Task results stay in memory for 30 minutes; unfinished tasks are lost on restart.
- Generation and edits consume the account's AI quota under the same plan rules as the console.

## Uploading an existing site

For static files already generated locally, or edited with your own editor / AI tools (`index.html`, CSS, images, etc.), that should be uploaded as-is.

**Option 1: ZIP upload link (recommended for a full folder)**

```text
create_upload_link  slug="acme-robotics"  deploy=true  expires_minutes=30
→ { "upload_url": "…", "curl_example": "…" }
```

```bash
cd /path/to/my-site
zip -r /tmp/site.zip .
curl -F "archive=@/tmp/site.zip" "https://bweb.help/api/mcp/upload?ticket=..."
```

- The link is single-use, valid for 30 minutes by default (5–120 minutes); `deploy=true` publishes after upload.
- The ZIP root or a single subdirectory must contain `index.html`; the outer folder is stripped automatically.
- File ≤25MB, ZIP ≤120MB, extracted total ≤100MB, at most 2000 files.
- The account also has a 100MB base storage pool shared by media assets, site source files and OSS backups; purchases extend it and over-quota writes return `storage_quota_exceeded`.
- Uploads **replace all existing files**; system files such as `.DS_Store` are ignored.

**Option 2: `upload_site` inline (small text-only sites)**

```text
upload_site  slug="acme-robotics"  deploy=true  files=[
  {"path":"index.html","content":"<!doctype html>…"},
  {"path":"assets/app.css","content":"…"}
]
```

Set `encoding` to `base64` for images and fonts. Inline uploads are capped at 25MB total; use the ZIP link for larger sites.

Preview with `preview_site`, then publish with `deploy_site`.

## File-level edits

Useful for `robots.txt`, `sitemap.xml`, `llms.txt` or a targeted HTML fix:

```text
read_site_file   slug="acme-robotics"  path="index.html"
write_site_file  slug="acme-robotics"  path="robots.txt"  content="User-agent: *\nAllow: /\n"
deploy_site      slug="acme-robotics"
```

Writes and deletes mark the site for deployment; call `deploy_site` to make them live.

## Preview and domains

- `preview_site` returns a signed link that works without login, including CSS and images. It is scoped to one site, expires in 24 hours by default (1–72 hours), and anyone with the link can view it.
- `bind_domain` supports multiple custom domains per site. Cloudflare-hosted domains get a proxied CNAME and an automatic certificate; Firebase domains get A / TXT records where possible, otherwise clear manual instructions.
- Sites are static files, domains stay in your name, and everything can be exported or moved at any time.
