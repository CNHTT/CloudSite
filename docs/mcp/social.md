# 社媒分发

不需要浏览器扩展：MCP 客户端可以作为「外部执行器」领取发布任务，用自己的浏览器自动化（Codex、WorkBuddy 等）或人工接力完成发布，再回传真实链接与表现数据。Bweb 负责内容、合规检测、任务队列与记录，不代替用户点击第三方平台按钮。共 **16 个工具**。

## 两种执行模式

| 模式 | 适用 | 做法 |
| --- | --- | --- |
| AI 自带浏览器自动化 | Codex、WorkBuddy 等可以操作浏览器的客户端 | 领取任务后打开 `compose_url`，上传图片、填写内容、点击发布，再回传链接 |
| 人工接力 | 客户端没有浏览器能力，或账号需要人工确认 | 把 `social_job_get` / `social_claim_job` 返回的内容与发布页交给运营人员，发布后由 AI 回传 |

## 工具

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `social_guide` | 读 | 无插件分发流程、两种执行模式与合规规则 |
| `social_platforms` | 读 | 平台可用性、发布页、字数上限与是否必须有图片 |
| `social_posts_list` | 读 | 内容列表：草稿 / 排队 / 部分发布 / 已发布 / 失败 |
| `social_post_get` | 读 | 单条内容、任务与表现数据 |
| `social_jobs_list` | 读 | 任务列表，可按内容、平台、状态筛选 |
| `social_job_get` | 读 | 发布包：`compose_url`、内容、上限、图片要求与步骤 |
| `social_metrics_list` | 读 | 已记录的表现数据 |
| `social_post_create` | 写 | 创建内容草稿；图片必须是公开 http(s) URL |
| `social_post_update` | 写 | 修改草稿或排队中的内容；已发布内容不可改 |
| `social_post_delete` | 写 | 删除内容及其任务与指标；不删除平台上的内容 |
| `social_accept_risk` | 写 | 记录平台发布风险授权，必须 `confirm=true` |
| `social_dispatch` | 写 | 合规检测后创建各平台任务，必须 `confirm=true` |
| `social_claim_job` | 写 | 外部执行器领取一个任务；同时只保留一个 |
| `social_report_job` | 写 | 回传 `filled` / `published` / `failed`；`published` 必须带真实链接 |
| `social_cancel_job` | 写 | 取消尚未发布的任务 |
| `social_add_metric` | 写 | 追加浏览、点赞、评论、分享、点击数据 |

## 典型流程

```text
social_platforms
→ 平台状态、发布页、字数上限、图片要求

social_accept_risk  platforms=["x"]  confirm=true
→ 获得用户明确同意后，记录当前风险版本的发布授权

social_post_create  title="…"  body="…"  url="https://…"
                    images=["https://cdn.example.com/cover.jpg"]  platforms=["x"]
social_dispatch     post_id="post_123"  platforms=["x"]  confirm=true
→ 合规检测通过后创建任务

social_claim_job    platforms=["x"]
→ { job_id, compose_url, limits, content, requires_media, steps }

# AI 客户端打开 compose_url 发布，或把发布包交给运营人员

social_report_job   job_id="job_9"  status="published"  url="https://x.com/acme/status/123"
social_add_metric   post_id="post_123"  platform="x"  views=120  likes=8
```

## 规则

- **风险确认是前置条件**：`social_accept_risk` 是法律意义上的风险确认，调用前必须获得用户明确同意；`social_dispatch` 也必须显式传 `confirm=true`。
- **不绕过平台风控**：登录、验证码、滑块与登录墙由执行者处理；遇到时停止并以 `failed` 回传原因，禁止绕过。
- **时效**：任务只能被一个执行器领取；10 分钟未领取、30 分钟未回传会过期，不自动重试。
- **频率**：同一平台每天最多 5 条任务；合规检测命中时派发会被拦截。
- **图片**：只接受公开 http(s) URL；Instagram、Pinterest、TikTok、小红书、头条号要求至少一张图片。
- **回传**：`published` 必须带平台真实链接；`failed` 请在 `message` 写明验证码、登录墙、页面结构变化等原因。
- **权限**：MCP 令牌继承团队成员角色；`viewer` 只能调用只读工具，不能领取或回传任务。
- **YouTube**：视频上传仍需官方 API；MCP 只提供平台状态与任务记录。

## 内容与合规

- 内容草稿可包含标题、正文、链接、图片与目标平台；不同平台的字数上限与图片要求可通过 `social_platforms` 查询。
- 派发前会做合规检测；命中规则时先调整内容，不要反复重试。
- 已发布内容不能被修改或删除平台侧内容；Bweb 只删除自己的记录与指标。
