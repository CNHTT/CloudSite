# 建站、文件与发布

覆盖站点的完整生命周期：查看、生成、改站、上传、预览、发布和绑定域名。共 **15 个工具**。

**可以用自己的工具改站：** 在自己的编辑器、脚本或 AI 工具里改好本地文件，再通过 MCP 小助手 `upload_site` / `create_upload_link` 上传；不需要学习平台编辑器，也不需要安装 CLI。

```text
本地修改 → upload_site / create_upload_link → preview_site → deploy_site
```

## 工具

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `list_sites` | 读 | 列出账号下（或团队授权范围内）的站点 |
| `get_site` | 读 | 站点详情：状态、域名、部署记录与增强配置 |
| `list_site_files` | 读 | 列出站点文件与大小 |
| `read_site_file` | 读 | 读取单个文件；文本返回 utf8，二进制返回 base64，单文件上限 2MB |
| `preview_site` | 读 | 生成公开的签名预览链接，默认 24 小时，可设 1–72 小时 |
| `get_task` | 读 | 查询生成 / 改站异步任务的进度与结果 |
| `create_site` | 写 | 创建站点（名称、产品、目标语言等） |
| `generate_site` | 写 | 用平台 AI 生成整站；可指定风格、品牌色与语言 |
| `chat_site` | 写 | 对话式改站，按区块定位修改，不整页重写 |
| `upload_site` | 写 | 内联上传文本文件或 base64 二进制，可同时发布 |
| `create_upload_link` | 写 | 生成单次使用的 ZIP 上传链接，适合整套静态站 |
| `write_site_file` | 写 | 写入 / 替换单个文本文件，并标记为待部署 |
| `delete_site_file` | 写 | 删除单个文件；`index.html` 不会被删除 |
| `deploy_site` | 写 | 发布到 Cloudflare Pages 或 Firebase Hosting |
| `bind_domain` | 写 | 绑定自定义域名；Cloudflare 托管时自动写 DNS 并签发 HTTPS |

> 只读令牌只能使用表中的读工具。发布与绑定域名要求账号已在控制台配置好 Cloudflare / Firebase 凭据。

## 典型建站流程

```text
create_site    name="Acme Robotics"  product="工业机械臂"  language="English"
generate_site  slug="acme-robotics"  style="现代极简"  accent="#f97316"
preview_site   slug="acme-robotics"  path="/"  expires_hours=24
deploy_site    slug="acme-robotics"
bind_domain    slug="acme-robotics"  domain="www.acme-robotics.com"
```

## 生成与改站

- `create_site` 先建空站点，再由 `generate_site` 生成页面；也可以在生成时直接指定语言、风格与品牌色。
- `chat_site` 适合“改首屏标题”“把发货时间改成 3–5 个工作日”这类请求。它只改对应区块，CSS / JS / 内联 SVG 保持不变。
- 客户端工具超时较短时，两个生成类工具都支持 `wait=false`：

```text
generate_site  slug="acme-robotics"  wait=false
→ { "task_id": "…", "status": "running" }

get_task  task_id="…"
→ { "status": "completed", "result": { "site": …, "chars": … } }
```

- 每个账号最多同时运行 2 个长任务；任务结果在内存中保留 30 分钟，服务重启会丢失未完成任务。
- 生成和改站会消耗账号的 AI 配额，受会员套餐与控制台相同的规则约束。

## 上传已有站点

适合本地已经生成、或用自己的编辑器 / AI 工具改好的静态站点（`index.html`、CSS、图片等），需要原样上传并发布。

**方式一：ZIP 上传链接（推荐，适合整套目录）**

```text
create_upload_link  slug="acme-robotics"  deploy=true  expires_minutes=30
→ { "upload_url": "…", "curl_example": "…" }
```

```bash
cd /path/to/my-site
zip -r /tmp/site.zip .
curl -F "archive=@/tmp/site.zip" "https://bweb.help/api/mcp/upload?ticket=..."
```

- 链接单次使用，默认 30 分钟有效，可设 5–120 分钟；`deploy=true` 会在上传完成后自动发布。
- ZIP 根目录或单一子目录中必须包含 `index.html`，最外层目录会自动去掉。
- 单文件 ≤25MB，解压后总量 ≤100MB，文件数 ≤2000。
- 上传会**替换**站点现有全部文件；`.DS_Store` 等系统文件自动忽略。

**方式二：`upload_site` 内联上传（适合少量文本文件）**

```text
upload_site  slug="acme-robotics"  deploy=true  files=[
  {"path":"index.html","content":"<!doctype html>…"},
  {"path":"assets/app.css","content":"…"}
]
```

图片、字体等二进制文件把 `encoding` 设为 `base64`。内联上传总量上限 25MB，更大的站点请用 ZIP 链接。

上传后建议先 `preview_site` 检查，再 `deploy_site`。

## 文件级修改

适合补齐 `robots.txt`、`sitemap.xml`、`llms.txt` 或修正单个 HTML 文件：

```text
read_site_file   slug="acme-robotics"  path="index.html"
write_site_file  slug="acme-robotics"  path="robots.txt"  content="User-agent: *\nAllow: /\n"
deploy_site      slug="acme-robotics"
```

写入或删除后，站点会标记为待部署；需要再次调用 `deploy_site` 才会生效。

## 预览与域名

- `preview_site` 返回无需登录的签名链接，CSS、图片等资源同样可用；链接只对该站点有效，默认 24 小时失效，可设 1–72 小时。拿到链接的人都能查看，请勿分享给不信任的人。
- `bind_domain` 支持一个站点绑定多个自定义域名。Cloudflare 托管的域名会自动写入代理 CNAME 并签发证书；Firebase 域名会尝试写入 A / TXT 记录，无法自动配置时返回明确的手动指引。
- 站点是静态文件，域名登记在用户名下，可随时导出或迁移。
