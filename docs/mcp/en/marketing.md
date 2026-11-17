# Marketing email and automation

Subscribers, lists, templates, sending channels, campaigns, automations and price quotes. **30 tools**. Preflight checks, test sends, review and wallet checks use the same business rules as the console.

## Overview, channels and pricing

| Tool | R/W | What it does |
| --- | --- | --- |
| `marketing_overview` | Read | Wallet, channels, campaigns, compliance and frequency settings |
| `marketing_providers_list` | Read | Sending channels (no credentials) |
| `marketing_provider_create` | Write | Add a BYO SMTP / ESP channel; platform-billed channels are console-admin only |
| `marketing_provider_test` | Write | Channel connectivity and send test |
| `marketing_pricing_quote` | Read | Quote by channel and volume; BYO channels include the platform service fee |

## Subscribers, lists and templates

| Tool | R/W | What it does |
| --- | --- | --- |
| `marketing_subscribers_list` | Read | Query subscribers with `q` / `status` / `listId` / `limit` |
| `marketing_subscriber_create` | Write | Add a subscriber |
| `marketing_subscribers_import` | Write | Bulk import subscribers |
| `marketing_lists_list` | Read | Subscription lists |
| `marketing_list_create` | Write | Create a list |
| `marketing_templates_list` | Read | Email templates |
| `marketing_template_create` | Write | Create a template |

## Campaigns

| Tool | R/W | What it does |
| --- | --- | --- |
| `marketing_campaigns_list` | Read | Campaign list |
| `marketing_campaign_get` | Read | Campaign details with stats and send records |
| `marketing_campaign_preflight` | Read | Preflight: recipients, suppression, balance, review rules |
| `marketing_campaign_create` | Write | Save a draft |
| `marketing_campaign_update` | Write | Edit a draft; clears any existing review result |
| `marketing_campaign_test_send` | Write | Send a test to specific addresses |
| `marketing_campaign_send` | Write | Send now; requires `confirm=true`; may return pending review |
| `marketing_campaign_control` | Write | `pause` (operator), `resume` / `cancel` (admin) |

**Recommended order:**

```text
marketing_campaign_create     …
marketing_campaign_preflight  campaign_id="c_123"
marketing_campaign_test_send  campaign_id="c_123"  emails=["me@example.com"]
marketing_campaign_send       campaign_id="c_123"  confirm=true
```

You can also set `scheduled_at` and let the scheduler send automatically; if the scheduler is not running, `marketing_campaign_send` can still be called manually.

## Automations

| Tool | R/W | What it does |
| --- | --- | --- |
| `marketing_automations_list` | Read | Automation list |
| `marketing_automation_get` | Read | Details: steps, enrollment summary and run records |
| `marketing_automation_create` | Write | Create a draft with steps embedded in `steps[]` |
| `marketing_automation_update` | Write | Edit a draft |
| `marketing_automation_activate` | Write | Activate; requires `confirm=true`; may return `pending_review` |
| `marketing_automation_control` | Write | `pause` (operator), `resume` / `archive` (admin) |
| `marketing_automation_enroll` | Write | Manual enrollment; requires `confirm=true` |
| `marketing_automation_test_send` | Write | Test the first email step |

- Automations run on the platform scheduler; MCP only configures, activates and enrolls — it does not send directly.
- Before activation, show the estimated volume, estimated cost, wallet balance and any risk rules hit, then wait for confirmation.
- Activation may enter `automation_activation` review; the scheduler continues after approval.
- When monthly volume, daily / monthly / per-campaign spend caps or complaint-rate circuit breakers are hit, the automation is paused with a reason in `lastError`; MCP does not auto-resume.

## Suppression and compliance

| Tool | R/W | What it does |
| --- | --- | --- |
| `marketing_suppressions_list` | Read | Suppression list |
| `marketing_suppression_create` | Write | Manually add an address to suppression |

## Rules

- **Preflight first** — sending requires a successful `marketing_campaign_preflight`; platform-billed channels also need send permission and enough wallet balance, otherwise `insufficient_balance`.
- **Explicit confirmation** — sending, activating an automation and manual enrollment require `confirm=true`. Do not treat confirmation as optional.
- **Reviews cannot be bypassed** — a `review_pending` / `pending_review` result means wait for the review; do not retry in a loop.
- **Channel boundary** — platform-billed channels (`platform_smtp` / `platform_api`) are configured by platform admins only; MCP can add BYO channels only.
- **Credential safety** — channel tools never return SMTP passwords, ESP API keys or encrypted credentials.
- **Costs** — marketing spend is frozen and settled from the main wallet; failures return an explicit error instead of charging silently.

## Example workflows

**Send a product launch email**

```text
marketing_overview            …
marketing_lists_list          …
marketing_campaign_create     name="November launch"  subject="…"  templateId="tpl_1"  listIds=["list_vip"]
marketing_campaign_preflight  campaign_id="c_123"
marketing_campaign_test_send  campaign_id="c_123"  emails=["me@example.com"]
marketing_campaign_send       campaign_id="c_123"  confirm=true
```

**Create a welcome automation**

```text
marketing_automation_create  name="Welcome series"  triggerType="list_join"  triggerConfig={ "listId": "list_123" }
                             providerId="prv_123"  dailyLimit=1000  steps=[…]
marketing_automation_activate  id="aut_123"  confirm=true
```

**Check performance**

```text
marketing_campaigns_list  …
marketing_campaign_get    campaign_id="c_123"
```
