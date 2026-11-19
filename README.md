<div align="center">

<img src="https://bweb.help/icon-192.png" width="84" alt="Bweb logo" />

# Bweb（必网）

**一句话建站，一条链路获客。**

噜妹做外贸电商，也做自己的独立站。每上一个新品、每进一个新市场，她只关心一件事：网站什么时候能接住客户。

噜噜是程序员。他把 AI 生成、域名、发布和获客接成了一条线。现在噜妹上新品，几分钟就能拿到能投广告的链接。

跨境 B2B / 外贸独立站 · AI 生成 · 批量建站 · Cloudflare Pages / Firebase Hosting / EdgeOne Pages / Aliyun ESA · 域名与 HTTPS

[简体中文](README.md) · [English](README.en.md)

[![Next.js](https://img.shields.io/badge/Next.js-16-000000?logo=nextdotjs&logoColor=white)](https://nextjs.org)
[![React](https://img.shields.io/badge/React-19-087EA4?logo=react&logoColor=white)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.9-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Cloudflare Pages](https://img.shields.io/badge/Cloudflare-Pages-F38020?logo=cloudflarepages&logoColor=white)](https://pages.cloudflare.com)
[![Firebase Hosting](https://img.shields.io/badge/Firebase-Hosting-FFCA28?logo=firebase&logoColor=black)](https://firebase.google.com/docs/hosting)
[![EdgeOne Pages](https://img.shields.io/badge/EdgeOne-Pages-0052D9)](https://edgeone.ai)
[![Alibaba Cloud ESA](https://img.shields.io/badge/Alibaba%20Cloud-ESA-FF6A00)](https://www.aliyun.com/product/esa)

[官网](https://bweb.help) · [免费注册](https://bweb.help/register) · [查看定价](https://bweb.help/pricing) · [MCP 接入](#快速开始) · [更新记录](CHANGELOG.md)

</div>

---

## 为什么会有 Bweb

故事开始于一句催促：「网站好了吗？」

那天凌晨两点，客厅里堆着第二天要发的样品，噜妹盯着广告后台——计划建好了，预算设好了，只差一个能填进去的链接。噜噜盯着终端：「快了。」其实证书还在签发，DNS 也刚改完。

噜妹做外贸电商：亚马逊上有店，也在做自己的独立站接 B2B 询盘。每上一款新品、每投一波广告、每进一个新市场，都需要一个能马上挂到广告后台、发给客户的落地页。页面本身不难，AI 十分钟就能写一版。难的是页面之后：换图调样式、导出上传、装 CLI、部署、绑域名、等证书。任何一步卡住，广告计划就只能开着空转，询盘也进不来。

那天她问的其实不是技术问题，是「客户什么时候能进来」。

噜噜才意识到：AI 已经把最需要人的那一步做完了，剩下六步却还要一个人守着；而且每上一个新品，这六步都要重来一遍。

那个周末，他把生成、部署、域名和 HTTPS 接成了一条线。第一次跑通时，他随手敲了一句「做一个卖陶瓷杯的外贸独立站」，几分钟后，手机打开了那个站。

他把链接发给噜妹。她回了一个「哇」，然后问：「能再加个优惠券吗？」

噜妹成了第一个用户，也成了第一个催更的人。

后来来问的人多了：做外贸的、做跨境电商的、工厂里的业务员、一个人管着几十个落地页的。大家卡住的地方几乎一样——不是不会写页面，而是页面写完之后，没人愿意再当那个人肉发布系统。

Bweb 就是从这些重复的夜里长出来的。它把整条链路收进一个控制台：

- **生成**：AI 对话生成整站，或直接上传你已有的静态页面
- **批量**：粘贴列表或导入 CSV，几十上百个站自动生成、部署、绑域名
- **上线**：直接调用 Cloudflare Pages、Firebase Hosting、EdgeOne Pages 与阿里云 ESA API / CLI，不需要在本机安装 wrangler 或 Firebase CLI
- **运营**：部署后的询盘表单、在线客服、邮箱订阅、转化回传、SEO/GEO 体检与营销自动化，全部开箱可用

我们不替你持有域名，也不把你的客户锁在平台里：站点是静态文件，域名登记在你名下，邮箱列表可以随时导出，想搬走就搬走。Bweb 只负责把「做出来」到「投出去」之间的路修平。

现在噜妹很少再问「网站好了吗」。她问的是：「下一个市场，什么时候能上？」

> 生成站点的托管可以跑在 Cloudflare 的免费额度内：静态托管、自定义域名、自动 HTTPS 与 DNS 都不额外收费。

## 适合谁

| 场景 | Bweb 能帮你省掉什么 |
| --- | --- |
| **跨境 B2B / 外贸卖家（含亚马逊站外引流）** | 给每个新品、市场和广告计划快速做独立站落地页，把流量沉淀到自己的域名和邮箱 |
| **外贸 / 跨境站群** | 一次生成并部署几十个独立站，每个站绑定自己的域名 |
| **独立开发者 / 小团队** | 不再为一张落地页折腾构建、部署与 DNS |
| **已经用 AI 写页面的人** | 把 HTML / ZIP 交给 Bweb，部署、绑域名、加询盘与客服 |
| **建站代理 / 服务商** | 多租户账号隔离、团队权限、钱包账单、统一审核台 |
| **自动化玩家** | 用自己的 AI 工具（Claude Code、Codex、Workbuddy、Cursor、n8n 等）直接建站、改站、发布、体检 |

## 外贸卖家，怎么做独立站获客

平台内的流量越来越贵，规则和账号风险也不在自己手里。独立站的意义，是把广告流量、客户邮箱和品牌资产留在自己手里。

Bweb 把重活接了过去：

- **每个广告一条落地页**：新品、活动、不同受众各做一个，几分钟上线
- **独立域名 + HTTPS**：广告后台直接填，不用等开发排期
- **表单沉淀线索**：询盘、邮箱订阅、WhatsApp 一键接住站外流量
- **多语言**：一套产品打不同市场，自动 hreflang
- **批量建站**：多个站点、多个市场，不用逐个手工部署

[免费注册，先把下一个广告落地页跑起来 →](https://bweb.help/register)

## 从想法到广告上线，都在一个控制台里

| 阶段 | 能力 |
| --- | --- |
| **生成** | AI 对话生成或整体改写页面；多语言站点按目标市场生成语言页面；素材库图片 / 图标可直接附加给 AI |
| **装配** | 67 套模板（行业站、跨境广告页、活动发布站、公司信息站与电商落地页）× 8 种视觉风格；支持 ZIP / 文件夹上传与站群模板导入导出 |
| **部署** | Cloudflare Pages Direct Upload（BLAKE3 资源哈希 + manifest）、Firebase Hosting REST（gzip + SHA-256）、EdgeOne Pages 与阿里云 ESA（官方 CLI）四平台；也支持用自己的工具改好本地文件后，通过 MCP 小助手上传发布；支持批量任务、并发、实时日志与取消 |
| **域名** | 一个项目绑定多个自定义域名；Cloudflare 自动写入代理 CNAME；Firebase/EdgeOne/ESA 返回记录并在配置 Cloudflare 或阿里云 DNS 后自动写入，失败时给出可复制记录；ESA 自动申请免费证书并开启强制 HTTPS 301；域名登记在用户名下 |
| **增长** | 询盘表单、在线客服、WhatsApp Business、邮箱订阅、营销邮件与自动化、广告转化回传、社媒分发与 UTM、数据导出、SEO/GEO 体检 |
| **协作** | 账号级数据隔离、团队权限、单一钱包与账单、退款与红冲、统一审核台；支持微信 / PayPal / Web3 支付 / 对公转账与发票 |

## 功能细节

### 🧱 建站

- **AI 建站 / 改站**：接入 Anthropic Messages API 或任意 OpenAI 兼容接口（OpenAI、DeepSeek、本地模型均可）。在站点详情里描述修改要求，AI 直接输出完整 HTML，保存即刷新预览。
- **多语言**：语言页面按目标市场配置，每种语言生成独立静态页面（`index.html`、`en/index.html`…），自动写入 `hreflang`、语言切换器与 RTL 样式。
- **行业模板**：67 套可直接上线的模板，覆盖行业站、跨境广告页、活动发布站、公司信息站与电商落地页，内置文案、产品区、FAQ 与询盘区；8 种视觉风格可切换，也可继续交给 AI 改写。
- **手动内容编辑**：按区块列出页面文字、标题、搜索描述与图片，只改对应源码位置，CSS / JS / 内联 SVG 保持不变。
- **素材库**：图片、图标、SVG / ICO 统一管理，建站小助手可一次附加最多 8 个素材。
- **站群迁移**：整组站点打包为 ZIP 导出，在另一个账号导入。

### 🚀 部署

- **四平台**：每个站点可独立选择 Cloudflare Pages、Firebase Hosting、腾讯云 EdgeOne Pages 或阿里云 ESA Pages，随时切换。Cloudflare/Firebase 仅支持 Bweb 部署；EdgeOne/ESA 还支持 IDE 部署与导入后托管。
- **无 CLI 依赖**：Cloudflare 走 Pages Direct Upload API，Firebase 走官方 Hosting REST API，不要求本机安装 wrangler / firebase-tools。
- **自带工具改站**：用自己的编辑器、脚本或 AI 工具在本地修改站点，再通过 MCP 小助手 `upload_site`（少量文本）或 `create_upload_link`（整套 ZIP）上传，`deploy=true` 一步发布；不需要学习平台编辑器。
- **批量建站**：粘贴列表或导入 CSV，按行选择 AI 生成 / 复用模板 / 内置模板；支持并发数、域名冲突策略、实时进度、日志与取消任务。
- **证书与 DNS**：Cloudflare 自动写入代理 CNAME；Firebase/EdgeOne/ESA 返回记录，并在配置 Cloudflare 或阿里云 DNS 后自动写入，否则给出可复制的记录；ESA 还会自动申请免费 Let's Encrypt 证书并开启强制 HTTPS 301。
- **在线预览**：桌面 / 手机双视图，预览链接可直接分享。

### 📈 增长（站点增强）

部署完成后，在页面注入一个 `enhance.js` 即可获得：

- **询盘表单**：自动识别页面上已有的表单，或生成标准询盘表单，提交直达后台
- **在线客服**：站内会话 + WhatsApp Business Cloud API，支持 AI 对话、素材附件与消息撤销
- **邮箱订阅与营销邮件**：订阅收集、确认邮件、营销活动、A/B 测试、发送时区窗口、退信熔断、DMARC / 黑名单检测
- **转化回传**：广告平台转化事件回传与归因
- **SEO / GEO 体检**：本地文件或线上域名检查 `index.html`、`robots.txt`、`llms.txt` / `llms-full.txt`、`sitemap.xml`，输出总分、逐项证据与修复建议，可一键交给 AI 修复
- **数据分析与导出**：询盘、会话、订阅、访问与转化数据统一查看，支持导出
- **报价 / 样品单 / 预约**：独立报价与样品单、四套文档模板、预览与 HTML/PDF 导出；客户页接受/拒绝、样品单收款与物流、预约会议记录
- **社媒分发**：把内容排进分发计划，生成带 UTM 的链接并记录表现

### 🤖 Agent 与 API

- **MCP 接入**：标准 MCP Streamable HTTP 端点 `https://bweb.help/api/mcp`。**不绑定 AI 平台**——Claude Code、Codex、Workbuddy、Cursor、n8n 或你自己的 MCP 客户端，一条命令接入。共 159 个工具，覆盖建站、文件、发布、域名、询盘、客服、订阅、报价、样品单、预约、营销邮件、社媒分发、经营分析与 Agent 工作台；也可按 `/api/mcp/sites|publish|growth|marketing|social|agent` 分模块接入。
- **自带 AI（BYO AI）**：Bweb 不要求你使用某一家模型或客户端。平台内置模型负责建站生成、Agent 任务与站内 AI 能力；日常运营、分析和服务客户，用你自己的 AI 工具通过 MCP 完成。换客户端不需要改接入方式。
- **按能力分域**：建站与发布 19 个、上线验收与接管 17 个、站点增强与获客 43 个、营销与自动化 30 个、社媒分发 16 个、Agent 工作台 32 个、账号 2 个；每个域都有独立端点与文档，见下方「MCP 能力文档」。
- **读写 / 只读令牌**：只读令牌的 `tools/list` 不包含任何写工具，适合交给第三方审计；令牌可限定站点范围、设置过期时间并随时撤销。
- **高危确认与审计**：发送营销邮件、激活自动化、社媒派发等操作要求 `confirm=true`；每次调用记录令牌、工具、站点、IP 与 `request_id`。
- **免插件 API**：`/api/v1` + 站点 Key，已有后端或第三方工具生成的页面也能接入增强能力。
- **零依赖桥接**：仓库内的 `mcp/cloudsite-mcp.mjs` 用于只支持 stdio 的客户端。脚本文件名与环境变量名保留 `cloudsite` / `CLOUDSITE_` 前缀以兼容旧配置，产品品牌为 Bweb。

## 快速开始

Bweb 提供标准的 MCP Streamable HTTP 端点，不限制 AI 平台或客户端。不用部署任何服务：注册账号、创建令牌，把端点交给你自己的 AI 工具（Claude Code、Codex、Workbuddy、Cursor、n8n 等），就能直接建站、发布、绑定域名，也能处理询盘、客服、订阅和营销。

### 1. 创建访问令牌

登录 [Bweb 控制台](https://bweb.help) → **设置 → MCP / Agent** → 创建令牌。

- 令牌以 `cs_` 开头，只显示一次
- **读写令牌**可以建站、生成、上传、发布和绑定域名
- **只读令牌**只能查看站点与业务数据，`tools/list` 不会暴露任何写工具

### 2. 接入客户端

Claude Code（HTTP，推荐）：

```bash
claude mcp add --transport http cloudsite https://bweb.help/api/mcp \
  --header "Authorization: Bearer cs_你的令牌"
```

Codex 或只支持 stdio 的客户端：

```bash
curl -O https://bweb.help/cloudsite-mcp.mjs
```

脚本文件名沿用 `cloudsite-mcp.mjs` 以兼容旧配置；环境变量名同样保留 `CLOUDSITE_` 前缀。

然后在 `~/.codex/config.toml` 中写入：

```toml
[mcp_servers.cloudsite]
command = "node"
args = ["/绝对路径/cloudsite-mcp.mjs"]
env = { CLOUDSITE_URL = "https://bweb.help", CLOUDSITE_API_TOKEN = "cs_你的令牌" }
```

其他支持 HTTP 的 MCP 客户端（含 Workbuddy、Cursor、Claude Desktop、自研 Agent）：

```json
{
  "mcpServers": {
    "cloudsite": {
      "type": "http",
      "url": "https://bweb.help/api/mcp",
      "headers": { "Authorization": "Bearer cs_你的令牌" }
    }
  }
}
```

> **客户端不限于以上几种。** 只要支持 MCP（Streamable HTTP 或 stdio），Workbuddy、Cursor、Claude Desktop、n8n、Make、Zapier、ChatGPT（支持远程 MCP 时）或你自己写的脚本都能接入。工具清单、权限、配额与审计完全一致，换客户端不需要改接入方式。

### 3. 调用工具

接好后直接用自己的话下指令：

> 用 `create_site` 建一个「Acme Robotics」站点，产品是工业机械臂，英文，然后用 `generate_site` 生成页面。

> 把 `/path/to/site` 上传为 `my-site`，用 `deploy_site` 发布，再用 `bind_domain` 绑定 `demo.example.com`。

> 对 `my-site` 跑一次 `enhance_seo_audit`（`mode=live`），把修复建议交给 `chat_site` 直接改。

也可以直接发 JSON-RPC 请求：

```bash
curl https://bweb.help/api/mcp \
  -H "Authorization: Bearer cs_你的令牌" \
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

**用自己的工具改站，再让 MCP 小助手传上去**

不需要在平台里编辑。用自己的编辑器、脚本或 AI 工具在本地改好站点，然后对 MCP 客户端说：

> 把 `/path/to/my-site` 上传到 `my-site`，发布，并给我预览链接。

MCP 小助手会调用 `upload_site`（少量文本文件）或 `create_upload_link`（整套 ZIP，单次上传链接）；上传后可先 `preview_site` 检查，再 `deploy_site` 发布；上传时传 `deploy=true` 可以一步到位。页面由外部工具生成时，还可以用 `enhance_embed_inject` 注入 `enhance.js`。

常用工具：

| 工具 | 作用 |
| --- | --- |
| `list_sites` / `get_site` | 查看站点与详情 |
| `create_site` / `generate_site` | 新建站点并用 AI 生成整站 |
| `upload_site` / `create_upload_link` | 上传本地静态站（文本文件或整套 ZIP），可一步发布 |
| `chat_site` | 对话式改站 |
| `deploy_site` | 发布到 Cloudflare Pages / Firebase Hosting / EdgeOne Pages / 阿里云 ESA |
| `bind_domain` | 绑定自定义域名；配置 DNS 服务商后自动写入记录，ESA 自动证书与强制 HTTPS |
| `enhance_seo_audit` | SEO / GEO 体检 |
| `marketing_*` / `enhance_*` | 营销邮件、询盘、会话、订阅与分析 |

完整工具清单可在控制台「设置 → MCP / Agent」中查看。

### MCP 能力文档

| 能力 | 文档 | 工具数 | 覆盖 |
| --- | --- | --- | --- |
| 建站、文件与发布 | [docs/mcp/sites.md](docs/mcp/sites.md) | 15 | 站点与文件、AI 生成、对话改站、ZIP 上传、预览、发布、绑定域名 |
| 站点增强 | [docs/mcp/growth.md](docs/mcp/growth.md) | 31 | 询盘与线索、在线客服、访客登录、订阅、追踪与合规、SEO/GEO 体检、外部建站接入、导出、分析 |
| 营销邮件与自动化 | [docs/mcp/marketing.md](docs/mcp/marketing.md) | 30 | 订阅者、列表、模板、发信通道、活动发送、自动化、抑制名单、费用试算 |
| 社媒分发 | [docs/mcp/social.md](docs/mcp/social.md) | 16 | 内容草稿、合规检测、任务领取、发布回传、表现数据 |
| Agent 工作台 | [docs/mcp/agent.md](docs/mcp/agent.md) | 29 | 任务、技能仓库、按站点知识库、计划、审批、交付物与周复盘 |
| 接入总览 | [docs/mcp/README.md](docs/mcp/README.md) | 159 | 端点、令牌、客户端配置、权限、限流与排查 |

完整工具清单以 `tools/list` 返回为准。

还没有账号？[免费注册](https://bweb.help/register) 后即可在「设置 → MCP / Agent」创建令牌。

## 免插件接入已有页面

已经有后端、或页面由第三方工具生成？在站点详情创建站点 Key，用 Key 调用 `/api/v1`，在页面里注入 `enhance.js`，就能获得询盘、客服、订阅与埋点能力，不需要改后端。

## 了解更多

| 页面 | 内容 |
| --- | --- |
| [功能与定价](https://bweb.help/pricing) | 套餐、额度与计费方式 |
| [使用指南](https://bweb.help/guide) | 从创建站点到绑定域名的完整流程 |
| [适用场景](https://bweb.help/use-cases) | 跨境 B2B 获客、外贸站群、多语言独立站 |
| MCP 接入 | [接入总览](docs/mcp/README.md)、客户端配置、令牌与分域文档（见上方「MCP 能力文档」） |
| 公开 API | `/api/v1` 站点 Key 与免插件接入（在站点详情创建 Key） |

## 联系与支持

- 邮箱：**cnhttt@163.com**
- 问题、需求或合作：直接开 Issue 或来信
- 也欢迎交流建站、SEO/GEO 与站群自动化

## 开始使用

[**免费注册**](https://bweb.help/register) · [查看定价](https://bweb.help/pricing) · [接入 MCP](#快速开始)

如果 Bweb 帮你省下了时间，欢迎点一个 **Star ⭐**。
