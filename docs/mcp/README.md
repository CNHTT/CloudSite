# Bweb MCP 接入

Bweb 提供标准的 **MCP Streamable HTTP** 端点。注册后创建一个令牌，Claude Code、Codex、Workbuddy、Cursor、n8n 等客户端就能用自然语言建站、改站、发布、绑定域名，并直接处理询盘、客服、订阅、营销邮件、社媒分发和经营分析——不需要安装插件，也不需要浏览器扩展，更不限制你使用哪家 AI。

当前服务端共 **123 个工具**，按能力分域如下：

| 能力 | 能做什么 | 工具数 | 文档 |
| --- | --- | --- | --- |
| 建站与发布 | 查看站点与文件、AI 生成、对话改站、上传 ZIP、预览、发布、绑定域名 | 15 | [sites.md](./sites.md) |
| 站点增强 | 询盘与线索、在线客服、访客登录、订阅、追踪与合规、SEO/GEO 体检、外部建站接入、导出、经营分析 | 31 | [growth.md](./growth.md) |
| 营销邮件与自动化 | 订阅者、列表、模板、发信通道、活动发送、自动化、抑制名单、费用试算 | 30 | [marketing.md](./marketing.md) |
| 社媒分发 | 内容草稿、合规检测、任务领取、发布回传、表现数据 | 16 | [social.md](./social.md) |
| Agent 工作台 | 任务、技能仓库、按站点知识库、计划、审批、交付物与周复盘 | 29 | [agent.md](./agent.md) |
| 账号 | `whoami`、`capabilities` | 2 | 本文 |

## 端点与认证

```text
POST https://bweb.help/api/mcp
Authorization: Bearer cs_xxxxxxxx
Content-Type: application/json
```

- 协议：MCP Streamable HTTP + JSON-RPC 2.0，支持 `tools/list` 与 `tools/call`。
- 自建实例把 `https://bweb.help` 换成你的站点地址。
- 只支持本地 stdio 的客户端使用零依赖桥接脚本 `cloudsite-mcp.mjs`，它会把本地 JSON-RPC 转发到上面的 HTTP 端点。

## 自带 AI，不绑定平台

Bweb 不限制你使用哪家模型或哪个客户端。MCP 是开放协议，接上之后由你自己的 AI 决定如何调用工具：

| 客户端 | 接入方式 |
| --- | --- |
| Claude Code / Codex / Workbuddy / Cursor / Claude Desktop | 支持 HTTP 或 stdio，任选其一 |
| n8n / Make / Zapier | 用 HTTP Request 节点直接调用 `/api/mcp` |
| ChatGPT 等远程客户端 | 支持远程 MCP 时使用 Streamable HTTP + Bearer |
| 自研脚本 / 内部 Agent | 直接发送 JSON-RPC，或复用 `cloudsite-mcp.mjs` |

平台内置模型负责建站生成、Agent 任务与站内 AI 能力；通过 MCP 做运营、分析、客服和营销时，使用你自己的 AI。无论换哪个客户端，工具清单、scope、站点范围、配额与审计都一致，换客户端不需要改接入方式。

### 改站也可以用自己的工具

在自己的编辑器、脚本或 AI 工具里修改本地 `index.html`、CSS 和图片，然后让 MCP 小助手把文件传上去：

| 你的工作方式 | MCP 调用 |
| --- | --- |
| 本地改好整套站点 | `create_upload_link`（ZIP，单次链接）或 `upload_site`（少量文本），传 `deploy=true` 一步发布 |
| 只改单个文件 | `write_site_file`，再 `deploy_site` |
| 用平台 AI 生成或改站 | `generate_site` / `chat_site` |
| 第三方工具生成，需要询盘与埋点 | `enhance_embed_inject` 注入 `enhance.js` |

上传后可先 `preview_site` 检查，再 `deploy_site` 发布。整套上传会替换站点现有文件，预览链接默认 24 小时有效。

## 5 分钟接入

### 1. 创建令牌

登录 [Bweb 控制台](https://bweb.help) → **设置 → MCP / Agent**，创建令牌：

- **读写令牌**：可以建站、生成、上传、改站、发布、绑定域名，以及回复会话、修改设置、发送营销邮件等。
- **只读令牌**：可以查看站点与业务数据；`tools/list` 不会返回任何写工具，适合交给外包或第三方审计。
- 令牌以 `cs_` 开头，**只显示一次**；可限制站点范围、设置过期时间，并随时撤销。
- 建议每个客户端单独创建一个令牌，方便分别撤销。

### 2. 接入 Claude Code（HTTP，推荐）

```bash
claude mcp add --transport http cloudsite https://bweb.help/api/mcp \
  --header "Authorization: Bearer cs_你的令牌"
```

用 `claude mcp list` 检查，或在会话里用 `/mcp` 查看连接状态。

### 3. 接入只支持 stdio 的客户端（Codex、Workbuddy、Claude Desktop 等）

先下载桥接脚本：

```bash
curl -O https://bweb.help/cloudsite-mcp.mjs
```

Codex 在 `~/.codex/config.toml` 中写入：

```toml
[mcp_servers.cloudsite]
command = "node"
args = ["/绝对路径/cloudsite-mcp.mjs"]
env = { CLOUDSITE_URL = "https://bweb.help", CLOUDSITE_API_TOKEN = "cs_你的令牌" }
```

Workbuddy / Claude Desktop / Cursor 风格客户端：

```json
{
  "mcpServers": {
    "cloudsite": {
      "command": "node",
      "args": ["/绝对路径/cloudsite-mcp.mjs"],
      "env": {
        "CLOUDSITE_URL": "https://bweb.help",
        "CLOUDSITE_API_TOKEN": "cs_你的令牌"
      }
    }
  }
}
```

### 4. 接入其他 HTTP 客户端

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

也可以直接发 JSON-RPC：

```bash
curl https://bweb.help/api/mcp \
  -H "Authorization: Bearer cs_你的令牌" \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "tools/call",
    "params": { "name": "list_sites", "arguments": {} }
  }'
```

### 5. 先问两个问题

接好后，建议先让 AI 调用：

```text
capabilities   → 当前令牌的 scope、可用工具、会员状态、钱包余额与配额
agent_guide    → 推荐工作流、写工具说明与安全规则
```

之后直接用自己的话下指令，例如：

> 用 `create_site` 建一个「Acme Robotics」站点，产品是工业机械臂，英文，然后用 `generate_site` 生成页面。

> 把 `/path/to/site` 上传为 `my-site`，用 `deploy_site` 发布，再用 `bind_domain` 绑定 `demo.example.com`。

> 对 `my-site` 跑一次 `enhance_seo_audit`（`mode=live`），把修复建议交给 `chat_site` 直接改。

> 列出昨天的询盘，标记为跟进中，并导出 10 月的订阅者 CSV。

## 权限与安全

- **最小权限**：只读令牌只看到读工具；写工具不会出现在 `tools/list`，直接调用返回 `scope_denied`。
- **站点范围**：令牌可绑定全部站点或指定 `site_id`，跨站请求返回 `site_scope_denied`。
- **高危确认**：发送营销邮件、激活自动化、社媒派发、创建导出等操作要求 `confirm=true` 或明确的确认字符串。
- **凭据隔离**：工具不会返回 SMTP 密码、ESP API Key、站点 Key、Google Secret 或令牌原文。
- **审计**：每次 `tools/call` 记录令牌、工具、站点、行数、IP 与 `request_id`；设置页可查看最近使用。
- **限流**：读工具 120 次/分钟/令牌，写工具 60 次/分钟/令牌；导出、营销发送、充值等另有独立限额。
- **配额一致**：MCP 不绕过套餐配额与控制台业务规则；会员到期、账号停用或令牌删除后立即失效。

## 长任务与链接

| 场景 | 用法 |
| --- | --- |
| AI 生成或改站耗时较长 | `generate_site` / `chat_site` 传 `wait=false`，得到 `task_id` 后用 `get_task` 轮询 |
| 并发限制 | 每个账号最多同时运行 2 个长任务；任务结果在内存保留 30 分钟 |
| 预览 | `preview_site` 返回带签名令牌的公开链接，默认 24 小时有效，可设 1–72 小时 |
| 整套 ZIP 上传 | `create_upload_link` 返回单次使用的上传链接，默认 30 分钟有效（可设 5–120 分钟） |

## 排查

| 现象 | 处理 |
| --- | --- |
| `401` / 令牌无效 | 检查令牌是否完整、是否已撤销、账号是否被停用 |
| `403` / 只读令牌 | 当前令牌只能读，改用读写令牌 |
| `402` / 会员到期 | 在控制台续费后重试 |
| 生成或改站超时 | 改用 `wait=false` + `get_task`，或提高客户端工具超时 |
| 上传返回 `413` | 调大反向代理请求体限制（如 Nginx `client_max_body_size`） |
| 上传链接已使用 | 上传链接单次有效，重新调用 `create_upload_link` |
| 桥接脚本无输出 | 先手动运行 `CLOUDSITE_API_TOKEN=... node cloudsite-mcp.mjs`，错误输出在 stderr |

## 相关文档

- [建站、文件与发布](./sites.md)
- [站点增强：询盘、客服、订阅、分析与 SEO](./growth.md)
- [营销邮件与自动化](./marketing.md)
- [社媒分发](./social.md)
- [Agent 工作台](./agent.md)
- 完整工具清单以 `tools/list` 返回为准，也可在控制台 **设置 → MCP / Agent** 查看。
