# Agent workspace

Agent mode (the intelligent organization) shares tasks, the skill library, per-site knowledge, plans and automation data with the console. These tools let MCP clients drive the Agent workspace, not just site operations. **32 tools**.

## Onboarding and overview

| Tool | R/W | What it does |
| --- | --- | --- |
| `agent_guide` | Read | Agent guidance: roles, rules, recommended workflows and write-tool notes |
| `agent_overview` | Read | Coverage of spaces, tasks, skills, automations and knowledge |
| `agent_org_overview` | Read | Four departments, nine roles, load, pending approvals, weekly artifacts and results |
| `agent_roles_list` | Read | Roles, departments, skills, risk limits, enabled state and metrics |
| `agent_spaces_list` | Read | Build / acquire / convert / operate spaces: stage, console modules and linked skills |

## Tasks

| Tool | R/W | What it does |
| --- | --- | --- |
| `agent_tasks_list` | Read | Tasks filtered by `status` / `site`, up to 100 |
| `agent_task_get` | Read | Details: status, timeline, logs, input, knowledge snapshot and result |
| `agent_task_create` | Write | Create a task; deploy / GEO / content generation returns `awaiting_approval` |
| `agent_task_approve` | Write | Approve a pending task; requires `confirm=true` |
| `agent_task_cancel` | Write | Cancel a pending / queued task, or request a running task stop at a safe point; requires `confirm=true` |

Task types: `deploy_site`, `deploy_pending`, `deploy_failed`, `seo_audit`, `geo_visibility`, `content_draft`, `marketing_review`, `space_review`.

## Skills, knowledge and automation

| Tool | R/W | What it does |
| --- | --- | --- |
| `agent_skills_list` | Read | Skill entries: type, category, target site, version and import source |
| `agent_skill_create` | Write | Save a skill to the library |
| `agent_skill_run` | Write | Run a skill and return a `task_id` |
| `agent_knowledge_get` | Read | Read brand, website, products, target customers, tone and notes for a site; omit `site` to list sites with knowledge |
| `agent_knowledge_update` | Write | Partially update a site's knowledge; omitted fields keep values, empty strings clear |
| `agent_automations_list` | Read | Automations: schedule, enabled state, next run and recent tasks |
| `agent_automation_run` | Write | Run an automation now; requires `confirm=true` |

- Knowledge is isolated per site; reads and writes require `site`. Legacy account-level records are flagged `legacy_present` and must be imported to a site in the console.
- Each update keeps the last 20 versions, restorable in the console; MCP reads and writes only the current version.

## Plans, grants and approvals

| Tool | R/W | What it does |
| --- | --- | --- |
| `agent_plans_list` | Read | Plans: goal, steps, tasks, artifacts, budget and status |
| `agent_plan_get` | Read | Plan details |
| `agent_plan_create` | Write | Generate a plan draft from registered skills; does not execute |
| `agent_plan_update` | Write | Edit a draft's goal, site, department, budget or explicit steps |
| `agent_plan_approve` | Write | Approve a plan and start the first runnable step; requires `confirm=true` |
| `agent_plan_cancel` | Write | Stop a plan and request the current step stop; requires `confirm=true` |
| `agent_plan_retry_step` | Write | Retry a failed step in a paused / failed plan; requires `confirm=true` |
| `agent_grant_request` | Write | Request a grant with site, tools, risk and purpose; cannot self-approve |
| `agent_grants_list` | Read | Grants with status, tools, risk, purpose and expiry |
| `agent_grant_decide` | Write | Approve, reject or revoke a grant; `confirm=true`; Admin/Owner only, never self-approval |
| `agent_governance_overview` | Read | Governance: plan completion, artifact adoption, approval latency, stop rate, budgets, role KPIs and failure clusters |

## Artifacts and reviews

| Tool | R/W | What it does |
| --- | --- | --- |
| `agent_artifacts_list` | Read | Artifacts filtered by site / type / status / task |
| `agent_artifact_get` | Read | One artifact's self-check, source task and acceptance state |
| `agent_reviews_list` | Read | Weekly reviews: metrics, findings, suggestions and adoption state |
| `agent_review_create` | Write | Generate a review from tasks, artifacts and blockers; reads data only, takes no action |

## Example workflows

**Create and approve a deployment task**

```text
agent_task_create   type="deploy_site"  site="acme-site"  title="Publish new homepage"
→ { "status": "awaiting_approval", "task_id": "task_123" }

agent_task_get      task_id="task_123"
agent_task_approve  task_id="task_123"  confirm=true
agent_task_get      task_id="task_123"
```

**Run a site audit**

```text
agent_skill_run     skill_id="seo_audit"  site="acme-site"
→ { "task_id": "task_456" }

agent_task_get      task_id="task_456"
agent_artifacts_list  site="acme-site"
```

## Rules

- **Approval boundary** — deployment, GEO and content generation are approval-gated. After creating one, explain the impact to the user, then call `agent_task_approve` (`confirm=true`). `agent_grant_request` only files a request; approval happens in the Agent inbox and cannot be granted by the same token.
- **Risk levels** — deployment and GEO are T2, content drafts T1, audits / marketing reviews / space reviews T0. T2 requires Admin or above, T3 requires Owner; non-Owners cannot approve tasks they created; solo accounts and platform admins are exempt from team-role limits.
- **Concurrency** — up to 5 in-progress tasks per account; beyond that returns 429. Wait for completion or cancel.
- **Read-only skills** — audits, marketing reviews and space reviews queue and run automatically; poll `agent_task_get` instead of creating duplicates.
- **Artifacts** — completed tasks generate artifacts with self-check results. `agent_artifacts_list` / `agent_artifact_get` are read-only; acceptance and rejection happen in the console or REST API.
- **Automation notifications** — tasks with `source=automation` send a completion email to the account; records appear under Agent → Automation → notification email log.
- **Read-only tokens** — see only the read tools above; every write tool needs a read-write token.
