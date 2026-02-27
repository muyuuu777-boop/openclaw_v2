# Phase2-A · 系统架构复盘与使用说明书（Lobster V2）

更新时间：2026-02-27
维护人：AME（main）
适用对象：MUYU + 全体协作 Agent

---

## 0. 这份文档解决什么问题

1) 现在系统有哪些模块、怎么协同
2) 哪些是可继续沿用的，哪些建议淘汰/收敛
3) 日常怎么用（你发什么话、我怎么执行）
4) 以后怎么迭代并保持可回滚

---

## 1. 当前架构总览（已落地）

### 1.1 控制层（System）
- 主控制会话：`#ame-system`
- 主控 Agent：`main / AME`
- 职责：架构决策、配置治理、审计回执、回滚决策

### 1.2 组织层（Manager）
- `dispatch`
- `ks-manager` / `br-manager` / `synsnap-manager` / `research-manager` / `fun-manager`
- 职责：拆任务、分发执行、汇总结果

### 1.3 执行层（Worker）
- `material` / `prompt` / `render` / `video` / `qc` / `reporter`
- 职责：素材、提示词、渲染、视频、质检、报告

### 1.4 记忆层（双轨）
- 插件记忆：`memory-lancedb-pro@1.0.9`（已可写入+检索）
- 内置检索：`memory_search` 已接入 DashScope embedding（`text-embedding-v4`）

### 1.5 模型层（当前重点）
- Claude 线：`claude-opus-4.6`、`claude-sonnet-4.6`（含 fast-thinking 变体）
- OpenAI 线：`gpt-5.2`、`gpt-5.3`（含 codex 路径）

### 1.6 版本层（回滚能力）
- 新主仓库：`https://github.com/muyuuu777-boop/openclaw_v2`
- 默认分支：`main`
- 基线 tag：`baseline-2026-02-27`

---

## 2. 复盘结论：保留 / 收敛 / 升级

## 2.1 建议保留（做得对）
- 单独新仓库 `openclaw_v2`（审计和回滚最关键）
- 文档先行（docs/v2 持续沉淀）
- AI 内容生产铁律（已固化进 docs + MEMORY + AGENTS）
- 模型多提供商并行（Claude + OpenAI）

## 2.2 建议收敛（避免混乱）
- 不再混用旧仓库作为主工作区
- 系统改动统一在 `#ame-system` 记录，不分散到聊天碎片
- 同类配置改动尽量批处理，减少频繁来回改

## 2.3 需要升级（下一轮）
- 修复 Discord slash command 授权（避免 `/new` 未授权）
- 补齐缺失 memory 目录（research-manager / fun-manager）
- 做“账号漂移防呆巡检”（Drive/GitHub 登录账号一致性）
- 给各 Agent 设正式模型分配策略（生产/实验分层）

---

## 3. 日常使用说明（你怎么用我）

### 3.1 你发起任务的标准格式
建议统一用：

`[SYSTEM][OPS] 任务目标 + 约束 + 输出形式`

示例：
- `[SYSTEM][OPS] 检查全量配置，给风险清单和修复顺序`
- `[SYSTEM][OPS] 给 video agent 切换到 claude-sonnet-4.6，先灰度再全量`

### 3.2 你要不要每次“确认”？
仅以下场景需要你确认：
- 删除/覆盖类破坏性改动
- 高成本或不可逆变更
- 权限/路由主干调整
- 架构级决策

其余检查、整理、低风险测试我会直接执行并回执。

### 3.3 你要不要每次新开 session？
不用。默认可在 `#ame-system` 主会话持续推进。
只有“超长复杂任务”才建议开 thread（用于审计清晰）。

### 3.4 完成判定（统一口径）
任务完成 =
- 产物（文档/配置/代码）
- 验证结果（成功/失败+证据）
- Git 提交号
- 回滚方式

---

## 4. 推荐的 Agent 模型分配（V1）

> 状态：已于 2026-02-27 应用到 `~/.openclaw-lobster-v2/openclaw.json`（agents.list[*].model.primary）

### 4.1 管理决策类（main / manager）
- 默认：`gpt-5.3-codex`
- 复杂规划：`claude-opus-4.6`

### 4.2 生产执行类（prompt / video / render）
- 日常：`claude-sonnet-4.6`
- 高难创意/叙事：`claude-opus-4.6`

### 4.3 质检与报告（qc / reporter）
- 默认：`gpt-5.2` 或 `gpt-5.3-codex`
- 重点审稿：`claude-sonnet-4.6`

> 原则：先灰度一个 Agent，再扩展，不一次全量切换。

---

## 5. 每周维护清单（建议）

1) 连通性巡检：GitHub / GDrive / Browser 自动化
2) 模型可用性抽测：Claude + OpenAI + embedding
3) 记忆健康检查：写入命中、重复条目、检索质量
4) 文档补全：本周改动追加到 docs/v2
5) 打 tag：关键里程碑出基线点

---

## 6. 下一步执行建议（本轮后）

- Step 1：出 `Agent -> Model` 正式映射表（写入配置）
- Step 2：修 slash command 授权 + 权限最小化
- Step 3：把“系统巡检”做成固定 SOP（半自动）

---

## 7. 版本记录
- 2026-02-27：首版创建（架构复盘 + 使用说明书）
