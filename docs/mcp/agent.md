# Agent 工作台

Agent 模式（智能组织）与控制台共用同一套任务、技能仓库、按站点知识库、计划与自动化数据。这组工具让 MCP 客户端直接驱动 Agent 工作台，而不只是做站点运营。共 **32 个工具**。

## 引导与总览

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `agent_guide` | 读 | Agent 引导：角色、规则、推荐工作流与写工具说明 |
| `agent_overview` | 读 | 空间、任务、技能、自动化与知识库覆盖度总览 |
| `agent_org_overview` | 读 | 四部门、九岗位、负载、待审批、本周交付物与结果 |
| `agent_roles_list` | 读 | 岗位、部门、技能、风险上限、启停状态与指标 |
| `agent_spaces_list` | 读 | 建站 / 获客 / 转化 / 经营四个空间的阶段、模块与关联技能 |

## 任务

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `agent_tasks_list` | 读 | 任务列表，按 `status` / `site` 筛选，最多 100 条 |
| `agent_task_get` | 读 | 任务详情：状态、时间线、日志、输入、知识快照与结果 |
| `agent_task_create` | 写 | 创建任务；部署 / GEO / 内容生成返回 `awaiting_approval` |
| `agent_task_approve` | 写 | 批准待确认任务，必须 `confirm=true` |
| `agent_task_cancel` | 写 | 取消待确认 / 排队中的任务，或请求运行中任务在安全点停止，必须 `confirm=true` |

任务类型：`deploy_site`、`deploy_pending`、`deploy_failed`、`seo_audit`、`geo_visibility`、`content_draft`、`marketing_review`、`space_review`。

## 技能、知识库与自动化

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `agent_skills_list` | 读 | 技能仓库条目：类型、分类、目标站点、版本与导入来源 |
| `agent_skill_create` | 写 | 保存技能到技能仓库 |
| `agent_skill_run` | 写 | 运行技能并返回 `task_id` |
| `agent_knowledge_get` | 读 | 按站点读取品牌、官网、产品、目标客户、语气与补充说明；省略 `site` 时列出有知识库的站点 |
| `agent_knowledge_update` | 写 | 部分更新指定站点知识库；省略字段保持原值，空字符串清空 |
| `agent_automations_list` | 读 | 自动化：计划、启用状态、下次运行与最近任务 |
| `agent_automation_run` | 写 | 立即运行自动化，必须 `confirm=true` |

- 知识库按站点隔离，读写都必须带 `site`；旧版账号级记录以 `legacy_present` 标记，需要在控制台导入到具体站点。
- 每次更新保留最近 20 个旧版本，控制台可恢复；MCP 只读写当前版本。

## 计划、授权与审批

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `agent_plans_list` | 读 | 计划列表：目标、步骤、任务、交付物、预算与状态 |
| `agent_plan_get` | 读 | 计划详情 |
| `agent_plan_create` | 写 | 用已注册技能生成计划草稿；不执行 |
| `agent_plan_update` | 写 | 编辑草稿目标、站点、部门、预算或显式步骤 |
| `agent_plan_approve` | 写 | 批准计划并启动第一个可运行步骤，必须 `confirm=true` |
| `agent_plan_cancel` | 写 | 停止计划并请求当前步骤停止，必须 `confirm=true` |
| `agent_plan_retry_step` | 写 | 重试暂停 / 失败计划中的失败步骤，必须 `confirm=true` |
| `agent_grant_request` | 写 | 发起带站点、工具、风险与用途的授权申请；不能自行批准 |
| `agent_grants_list` | 读 | 授权列表：状态、工具、风险、用途与到期时间 |
| `agent_grant_decide` | 写 | 批准 / 拒绝 / 撤销授权，必须 `confirm=true`；仅 Admin/Owner，不能自批 |
| `agent_governance_overview` | 读 | 治理中心：计划完成率、交付物采纳率、审批时长、停止率、预算、岗位 KPI 与失败聚类 |

## 交付物与复盘

| 工具 | 读/写 | 作用 |
| --- | --- | --- |
| `agent_artifacts_list` | 读 | 交付物列表，按站点 / 类型 / 状态 / 任务筛选 |
| `agent_artifact_get` | 读 | 单个交付物的自检结果、来源任务与验收状态 |
| `agent_reviews_list` | 读 | 周复盘的指标、发现、建议与采纳状态 |
| `agent_review_create` | 写 | 按任务、交付物与阻塞生成复盘；只读数据，不执行动作 |

## 典型流程

**创建并批准一个部署任务**

```text
agent_task_create   type="deploy_site"  site="acme-site"  title="发布新版首页"
→ { "status": "awaiting_approval", "task_id": "task_123" }

agent_task_get      task_id="task_123"
agent_task_approve  task_id="task_123"  confirm=true
agent_task_get      task_id="task_123"
```

**运行一次站点体检**

```text
agent_skill_run     skill_id="seo_audit"  site="acme-site"
→ { "task_id": "task_456" }

agent_task_get      task_id="task_456"
agent_artifacts_list  site="acme-site"
```

## 规则

- **审批边界**：部署、GEO 与内容生成属于审批类任务；创建后先向用户说明影响，再调用 `agent_task_approve`（`confirm=true`）。`agent_grant_request` 只能发起申请，不能自行批准；批准在 Agent 收件箱完成。
- **风险分级**：部署与 GEO 为 T2，内容草稿为 T1，体检 / 营销检查 / 空间巡检为 T0。T2 需 Admin 及以上批准，T3 需 Owner；非 Owner 不能批准自己创建的任务；solo 账号与平台管理员不受团队角色限制。
- **并发**：同一账号最多 5 个进行中的任务；超过时返回 429，需等待完成或取消。
- **只读技能**：体检、营销检查、空间巡检创建后自动排队执行；用 `agent_task_get` 轮询，不要重复创建。
- **交付物**：任务完成会自动生成交付物并保存自检结果；`agent_artifacts_list` / `agent_artifact_get` 只读，验收与驳回必须由人在控制台或 REST 接口完成。
- **自动化通知**：来源为 `source=automation` 的任务完成后会向账号邮箱发送通知邮件；发送记录在 Agent → 自动化的「通知邮件记录」中。
- **只读令牌**：只能看到上述读工具；所有写工具都需要读写令牌。
