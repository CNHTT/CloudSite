# 营销邮件与自动化

覆盖订阅者、列表、模板、发信通道、活动、自动化与费用试算，共 **30 个工具**。发送前检查、测试发送、审核与钱包余额校验与控制台共用同一套业务规则。

## 总览、通道与费用

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `marketing_overview` | 读 | 钱包、通道、活动、合规与频次配置概览 |
| `marketing_providers_list` | 读 | 发信通道列表（不含凭据） |
| `marketing_provider_create` | 写 | 新增 BYO SMTP / ESP 通道；平台计费通道只能由管理员在控制台配置 |
| `marketing_provider_test` | 写 | 通道连通性与发信测试 |
| `marketing_pricing_quote` | 读 | 按通道与数量试算费用；自有通道会包含平台服务费 |

## 订阅者、列表与模板

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `marketing_subscribers_list` | 读 | 查询订阅者，支持 `q` / `status` / `listId` / `limit` |
| `marketing_subscriber_create` | 写 | 新增订阅者 |
| `marketing_subscribers_import` | 写 | 批量导入订阅者 |
| `marketing_lists_list` | 读 | 订阅列表 |
| `marketing_list_create` | 写 | 新建列表 |
| `marketing_templates_list` | 读 | 邮件模板列表 |
| `marketing_template_create` | 写 | 新建邮件模板 |

## 活动

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `marketing_campaigns_list` | 读 | 活动列表 |
| `marketing_campaign_get` | 读 | 活动详情，含统计与发送记录 |
| `marketing_campaign_preflight` | 读 | 发送前检查：收件人、抑制名单、余额、审核规则 |
| `marketing_campaign_create` | 写 | 保存活动草稿 |
| `marketing_campaign_update` | 写 | 修改草稿；更新会清空原有审核结论 |
| `marketing_campaign_test_send` | 写 | 向指定邮箱测试发送 |
| `marketing_campaign_send` | 写 | 立即发送，必须 `confirm=true`；命中审核时返回待审核 |
| `marketing_campaign_control` | 写 | `pause`（operator）、`resume` / `cancel`（admin） |

**推荐顺序：**

```text
marketing_campaign_create     …                    # 保存草稿
marketing_campaign_preflight  campaign_id="c_123"  # 检查收件人、抑制、余额、审核
marketing_campaign_test_send  campaign_id="c_123"  emails=["me@example.com"]
marketing_campaign_send       campaign_id="c_123"  confirm=true
```

也可以设置 `scheduled_at` 让调度器自动排期；未运行调度时仍可再次调用 `marketing_campaign_send` 手动发送。

## 自动化

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `marketing_automations_list` | 读 | 自动化列表 |
| `marketing_automation_get` | 读 | 自动化详情：步骤、入组摘要与运行记录 |
| `marketing_automation_create` | 写 | 创建草稿，步骤内嵌在 `steps[]` |
| `marketing_automation_update` | 写 | 修改草稿 |
| `marketing_automation_activate` | 写 | 激活，必须 `confirm=true`；命中审核返回 `pending_review` |
| `marketing_automation_control` | 写 | `pause`（operator）、`resume` / `archive`（admin） |
| `marketing_automation_enroll` | 写 | 手动入组，必须 `confirm=true` |
| `marketing_automation_test_send` | 写 | 测试发送第一个邮件步骤 |

- 自动化由平台内置调度器执行；MCP 只负责配置、激活与入组，不直接发信。
- 激活前应先展示预计发送量、预计费用、钱包余额与命中的风控项，等待用户确认。
- 激活可能转入 `automation_activation` 审核，审核通过后由调度器继续执行。
- 命中月发信量、日 / 月 / 活动消费上限或投诉率熔断时，自动化转 `paused` 并在 `lastError` 给出原因；MCP 不会自动恢复。

## 抑制与合规

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `marketing_suppressions_list` | 读 | 抑制名单 |
| `marketing_suppression_create` | 写 | 手动加入抑制名单 |

## 规则

- **先预检再发送**：发送前必须通过 `marketing_campaign_preflight`；平台计费通道还要求账号具备发送权限且钱包可用余额充足，否则返回 `insufficient_balance`。
- **显式确认**：发送活动、激活自动化、手动入组必须 `confirm=true`；不要把确认当成可选步骤。
- **审核不绕过**：命中审核规则时返回 `review_pending` 或 `pending_review`，应等待审核结论，不要重复重试。
- **通道边界**：平台计费通道（`platform_smtp` / `platform_api`）只能由平台管理员在控制台配置；MCP 只允许新增自有通道。
- **凭据安全**：通道工具永不返回 SMTP 密码、ESP API Key 或加密后的凭据。
- **费用**：营销费用从主钱包冻结 / 结算；发送失败会返回明确错误，不静默扣费。

## 典型工作流

**发一封新品邮件**

```text
marketing_overview            …
marketing_lists_list          …
marketing_campaign_create     name="November 新品"  subject="…"  templateId="tpl_1"  listIds=["list_vip"]
marketing_campaign_preflight  campaign_id="c_123"
marketing_campaign_test_send  campaign_id="c_123"  emails=["me@example.com"]
marketing_campaign_send       campaign_id="c_123"  confirm=true
```

**创建欢迎自动化**

```text
marketing_automation_create  name="欢迎序列"  triggerType="list_join"  triggerConfig={ "listId": "list_123" }
                             providerId="prv_123"  dailyLimit=1000  steps=[…]
marketing_automation_activate  id="aut_123"  confirm=true
```

**查看发送表现**

```text
marketing_campaigns_list  …
marketing_campaign_get    campaign_id="c_123"
```
