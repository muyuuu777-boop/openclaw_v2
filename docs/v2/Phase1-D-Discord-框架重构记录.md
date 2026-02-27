# Phase1-D · Discord 框架重构记录（Lobster V2）

更新时间：2026-02-27
负责人：AME（main）
变更范围：Discord 服务器分组/频道命名与职责重构（不重建、不换 Bot）

---

## 0. 变更目标

建立可持续的“系统治理 + 项目执行 + 生产流水线 + 杂聊缓冲 + 个人运维”结构，避免上下文污染，方便后续扩展客户与项目。

---

## 1. 这次改了什么（What Changed）

### 1.1 Category（组别）

- `Control` → `SYSTEM`（ID: `1476908858222968983`）
- `Managers` → `CLIENTS`（ID: `1476908947066851378`）
- `Piplines` → `PRODUCTION`（ID: `1476909010182733884`）
- 新增 `COMMON`（ID: `1476952707129671692`）
- 新增 `PERSONAL-OPS`（ID: `1476952708454809610`）

### 1.2 Channel（频道）

#### SYSTEM
- `ame-hq`（ID: `1476909205779906613`）
- `dispatch-center` → `system-ops`（ID: `1476909286297960570`）
- `boards-global` → `system-lab`（ID: `1476909339284340796`）

#### CLIENTS
- `ks-manager` → `client-ks`（ID: `1476909453889507389`）
- `br-manager` → `client-br`（ID: `1476909491734839407`）
- `synthsnap-studio-manager` → `client-film`（ID: `1476909639894306898`）

#### PRODUCTION
- `material` → `image-room`（ID: `1476909825576275970`）
- `prompt` → `prompt-room`（ID: `1476909847151906907`）
- `render` → `render-room`（ID: `1476909884791328798`）
- `video` → `video-room`（ID: `1476909905737683056`）
- `qc` → `delivery-qc`（ID: `1476909922967879803`）
- `reporter` → `delivery-reporter`（ID: `1476909949182283897`）

#### COMMON
- 新增 `chat-room`（ID: `1476952783704821923`）
- `research-manager` → `research-room`（ID: `1476909740192960562`）
- `fun-manager` → `fun-room`（ID: `1476909772719521822`）

#### PERSONAL-OPS
- 新增 `personal-ops`（ID: `1476952784879358085`）

---

## 2. 这次做了什么（What Was Done）

1. 保留现有 3 Bot（AME / Dispatch / Studio），未新增、未下线。
2. 仅做频道层面的重命名、分组重排、新建频道。
3. 所有路由保持原 channel ID 兼容策略（改名不改 ID），降低中断风险。
4. 给关键频道补充 topic 说明，形成职责边界。

---

## 3. 为什么改（Why Changed）

1. **减少上下文污染**：系统讨论和项目执行分离。
2. **可扩展**：未来新增客户只需加 `client-xxx` 频道，不必重建架构。
3. **可追责**：按功能区拆分后，任务来源/决策来源更清晰。
4. **对齐记忆治理**：频道语义与 memory scopes（project/topic）一致。

---

## 4. 什么情况下改回去（Why Roll Back）

仅在以下情况触发回滚：

1. 路由异常：Bot 在关键频道持续无法响应（>24h）
2. 团队效率显著下降：消息分流后造成严重信息丢失
3. 外部协作不适配：客户/团队无法适应新结构并影响交付

### 回滚策略（最小化）
- 只回滚“频道名和分类”，不回滚 Bot/Agent 架构。
- 保留新频道消息，避免数据丢失。
- 回滚后 48h 内复盘并给出第二版命名标准。

---

## 5. 运行规则（短版）

推荐消息前缀：
- `[SYSTEM] [OPS] [LAB] [KS] [BR] [FILM] [PROMPT] [IMAGE] [VIDEO] [QC] [REPORT] [CHAT] [RESEARCH] [FUN] [PERSONAL]`

原则：
- `#ame-system` 只谈系统治理；
- 杂聊先在 `#chat-room`，形成可执行项后转发到对应频道。

---

## 6. `#ame-system` 置顶使用规范（短版）

> 频道：`#ame-system`（SYSTEM 总控）

1. 只讨论系统治理：架构、记忆、插件、技能、权限、稳定性、升级与回滚。
2. 业务执行不要放这里（客户需求、提示词细节、素材渲染请去对应频道）。
3. 每条消息建议加前缀：`[SYSTEM]` / `[OPS]` / `[LAB]`。
4. 任何系统改动都必须记录 4 件事：改了什么、做了什么、为什么改、是否/为何回滚。
5. 发现异常先报 `#system-ops`，需要决策再回 `#ame-system`。
6. 新想法先在 `#system-lab` 验证，通过后再进入正式流程。
7. 杂聊/头脑风暴先去 `#chat-room`，形成可执行项后转发到对应频道。
8. 默认原则：不重建、不破坏、可回滚、可追踪。

---

## 7. 更新日志模板（以后每次更新都按这个记）

```md
## YYYY-MM-DD HH:mm
- 改了什么：
- 做了什么：
- 为什么改：
- 风险评估：
- 是否回滚：
- 如果回滚，为什么回滚：
- 执行人：
```

> 维护建议：所有系统变更都追加在本文件底部，保持单一审计入口。
