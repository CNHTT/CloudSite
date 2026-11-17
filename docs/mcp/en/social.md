# Social distribution

No browser extension required: an MCP client can act as an **external executor**, claim publishing jobs, use its own browser automation (Codex, WorkBuddy, etc.) or hand off to a human, then report the real URL and metrics. Bweb owns the content, compliance checks, job queue and records; it never clicks third-party buttons for you. **16 tools**.

## Two execution modes

| Mode | Best for | How |
| --- | --- | --- |
| AI browser automation | Clients that can drive a browser, such as Codex or WorkBuddy | Claim a job, open `compose_url`, upload images, fill content, publish, then report the URL |
| Human relay | Clients without browser control, or accounts that need human confirmation | Show the content and compose URL from `social_job_get` / `social_claim_job` to an operator; the AI reports the link afterward |

## Tools

| Tool | R/W | What it does |
| --- | --- | --- |
| `social_guide` | Read | Plugin-free flow, execution modes and compliance rules |
| `social_platforms` | Read | Platform availability, compose URL, character limit and image requirements |
| `social_posts_list` | Read | Posts: draft / queued / partially published / published / failed |
| `social_post_get` | Read | One post with jobs and metrics |
| `social_jobs_list` | Read | Jobs, filterable by post, platform and status |
| `social_job_get` | Read | Publishing package: `compose_url`, content, limits, media requirements and steps |
| `social_metrics_list` | Read | Recorded performance data |
| `social_post_create` | Write | Create a draft; images must be public http(s) URLs |
| `social_post_update` | Write | Edit a draft or queued post; published posts cannot change |
| `social_post_delete` | Write | Delete a post with its jobs and metrics; platform content is unaffected |
| `social_accept_risk` | Write | Record publishing risk acceptance; requires `confirm=true` |
| `social_dispatch` | Write | Run compliance checks and create platform jobs; requires `confirm=true` |
| `social_claim_job` | Write | Claim one job as an external executor; only one at a time |
| `social_report_job` | Write | Report `filled` / `published` / `failed`; `published` requires the real URL |
| `social_cancel_job` | Write | Cancel a job that has not been published |
| `social_add_metric` | Write | Append views, likes, comments, shares and clicks |

## Typical flow

```text
social_platforms
→ platform status, compose URL, limits, image requirements

social_accept_risk  platforms=["x"]  confirm=true
→ record risk acceptance for the current version after explicit user consent

social_post_create  title="…"  body="…"  url="https://…"
                    images=["https://cdn.example.com/cover.jpg"]  platforms=["x"]
social_dispatch     post_id="post_123"  platforms=["x"]  confirm=true
→ compliance check passes, jobs created

social_claim_job    platforms=["x"]
→ { job_id, compose_url, limits, content, requires_media, steps }

# The AI client opens compose_url to publish, or hands the package to an operator

social_report_job   job_id="job_9"  status="published"  url="https://x.com/acme/status/123"
social_add_metric   post_id="post_123"  platform="x"  views=120  likes=8
```

## Rules

- **Risk acceptance is a prerequisite** — `social_accept_risk` is a legal-risk acknowledgment. Get explicit user consent first. `social_dispatch` also needs `confirm=true`.
- **Do not bypass platform controls** — login, CAPTCHA, sliders and login walls are handled by the executor. Stop and report `failed` with the reason; never bypass them.
- **Timing** — a job can be claimed by one executor only; unclaimed jobs expire after 10 minutes, unreported jobs after 30 minutes. There is no automatic retry.
- **Frequency** — at most 5 jobs per platform per day; dispatch is blocked when compliance checks fail.
- **Images** — public http(s) URLs only; Instagram, Pinterest, TikTok, Xiaohongshu and Toutiao require at least one image.
- **Reporting** — `published` must include the real platform URL; `failed` should explain CAPTCHA, login wall or page-structure changes in `message`.
- **Permissions** — MCP tokens inherit team roles; `viewer` can only call read tools and cannot claim or report jobs.
- **YouTube** — video upload still requires the official API; MCP only provides platform status and job records.

## Content and compliance

- Drafts can include title, body, URL, images and target platforms; character limits and image rules are available from `social_platforms`.
- Dispatch runs compliance checks; if a rule is hit, adjust the content instead of retrying repeatedly.
- Published content cannot be edited or removed on the platform; Bweb only deletes its own records and metrics.
