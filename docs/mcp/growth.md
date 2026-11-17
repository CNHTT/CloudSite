# 站点增强：询盘、客服、订阅、分析与 SEO

部署后注入的 `enhance.js` 会把询盘、在线客服、订阅、访客登录、转化事件与页面分析写回 Bweb。这组工具让 AI 直接读取和处理这些数据，共 **31 个工具**。

所有工具都在令牌所属账号、及令牌限定的站点范围内执行；只读令牌只能调用读工具。

## 总览与分析

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `enhance_overview` | 读 | 各站点的线索、会话、转化、事件与访客汇总 |
| `enhance_analytics_summary` | 读 | 单站点分析：每日浏览 / 表单 / 线索 / 转化、金额、来源、漏斗、热门页；可按 `days` 与 `language` 过滤 |

## 询盘表单与线索

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `enhance_forms_list` | 读 | 表单列表；返回字段定义（key / label / kind / required / options） |
| `enhance_form_get` | 读 | 单个表单及字段定义 |
| `enhance_form_create` | 写 | 创建含内置或自定义字段的表单 |
| `enhance_form_update` | 写 | 修改表单；省略字段保持原值 |
| `enhance_form_delete` | 写 | 删除表单（已收集的线索保留） |
| `enhance_leads_list` | 读 | 线索列表，可按 `site` / `status` / `limit` 过滤，最多 1000 条 |
| `enhance_lead_update` | 写 | 更新状态、备注、负责人与下次跟进时间 |
| `enhance_lead_assignees` | 读 | 可分配给线索的团队成员 |

- 线索状态：`new`、`contacted`、`qualified`、`closed`、`spam`。
- `enhance_lead_update` 支持 `assignee_email`（空字符串取消分配）与 `next_follow_up_at`（ISO 8601，空字符串取消）。设置跟进时间后，调度器会向负责人（未分配时为账号所有者）发送提醒邮件。
- MCP 返回的线索包含邮箱、电话等完整联系方式，以及 `custom` 字段中的自定义询盘内容；请按业务数据妥善保管令牌。

## 在线客服

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `enhance_chat_conversations` | 读 | 会话列表，含未读数与最后一条消息 |
| `enhance_chat_messages` | 读 | 单个会话的摘要与最近消息 |
| `enhance_chat_settings_get` | 读 | 客服开关、WhatsApp、欢迎语、服务时间、离线邮箱与位置 |
| `enhance_chat_reply` | 写 | 回复访客并清零未读 |
| `enhance_chat_close` | 写 | 结束或重新打开会话 |

## 访客登录

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `enhance_visitors_list` | 读 | 访客账号列表（邮箱验证码 / Google 登录） |
| `enhance_visitor_update` | 写 | 启用或停用访客账号 |
| `enhance_visitor_settings_get` | 读 | 访客登录设置；Google Secret 只返回是否已配置 |
| `enhance_visitor_settings_update` | 写 | 修改访客登录设置；Secret 只写不回显 |

## 订阅

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `enhance_subscribe_summary` | 读 | 订阅设置，以及已订阅 / 待确认 / 退订 / 累计统计 |
| `enhance_subscribe_settings_get` | 读 | 开关、双重确认、目标列表与同意文案 |
| `enhance_subscribe_settings_update` | 写 | 修改上述订阅设置 |

订阅人本身属于营销联系人，查询请使用营销域的 `marketing_subscribers_list`。

## 追踪、合规与监控

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `enhance_tracking_summary` | 读 | 最近事件、同意记录、追踪设置与最近监控结果 |
| `enhance_tracking_settings_get` | 读 | 追踪 / 弹窗 / 合规 / SEO / 监控设置；Turnstile 不返回密钥 |
| `enhance_tracking_settings_update` | 写 | 更新上述设置（补丁式） |

## SEO / GEO 体检

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `enhance_seo_audit` | 读 | 检查 `index.html`、`robots.txt`、`sitemap.xml`、`llms.txt` / `llms-full.txt`，返回总分、逐项证据与按严重程度排序的修复建议 |

- `mode=local` 检查站点本地文件，无需部署；`mode=live` 抓取已部署站点。
- `mode=live` 的 `url` 只能是当前站点绑定的域名或部署地址。
- 典型闭环：

```text
enhance_seo_audit  site="acme-site"  mode="local"  locale="zh"
read_site_file     slug="acme-site"  path="index.html"
write_site_file    slug="acme-site"  path="index.html"  content="…"
write_site_file    slug="acme-site"  path="llms.txt"  content="…"
deploy_site        slug="acme-site"
enhance_seo_audit  site="acme-site"  mode="live"
```

## 外部建站接入

适合页面由第三方工具、脚本或已有后端生成，但希望获得询盘、客服、订阅与埋点能力：

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `enhance_api_keys_list` | 读 | 查看站点 `/api/v1` Key 的类型、前缀、开放模块、来源白名单、启用 / 吊销状态与最近使用；不返回密钥 |
| `enhance_embed_get` | 读 | 返回 `enhance.js` 片段、询盘 / 订阅表单片段与 `/api/v1` 接入信息，并检查页面是否已加载脚本、表单是否绑定 |
| `enhance_embed_inject` | 写 | 向外部生成的 HTML 页面注入 `enhance.js`；默认处理所有 HTML，幂等跳过已包含脚本的页面 |

- 没有可用 Key 时，`enhance_api_keys_list` 返回控制台 `createUrl`，引导用户在 **站点增强 → API 接入** 创建。
- 注入后页面会标记待部署；用 `enhance_embed_get` 复核后再 `deploy_site`。
- 平台不会把站点 Key 或令牌返回给 MCP；也不要把它写进源码。

## 导出

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `enhance_export_create` | 写 | 创建异步导出任务：`submissions` / `subscribers` / `auth_users`，格式 `csv` / `json` |
| `enhance_exports_list` | 读 | 查看导出任务状态与短时下载地址 |

## 典型工作流

**跟进线索**

```text
enhance_leads_list    site="acme-site"  status="new"  limit=50
enhance_lead_update   lead_id="lead_123"  status="contacted"  note="已邮件联系"
```

**查看经营情况**

```text
enhance_overview            site="acme-site"
enhance_analytics_summary   site="acme-site"  days=7
```

**处理客服会话**

```text
enhance_chat_conversations  site="acme-site"  status="open"
enhance_chat_messages       conversation_id="conv_123"
enhance_chat_reply          conversation_id="conv_123"  message="…"
enhance_chat_close          conversation_id="conv_123"
```

**导出月度询盘**

```text
enhance_export_create  site="acme-site"  type="submissions"  format="csv"  from="2026-10-01"  to="2026-10-31"
enhance_exports_list   site="acme-site"
```

## 边界

- 只读令牌可以查看全部读数据，但不能修改线索、回复会话、改设置或创建导出。
- 设置类工具不会返回 Google Secret、Turnstile Secret、站点 Key 等敏感值。
- 导出只返回带时效的签名下载链接，不直接返回文件内容。
- 数据范围由账号与站点权限决定；团队角色低于要求的成员不能查看或修改对应数据。
