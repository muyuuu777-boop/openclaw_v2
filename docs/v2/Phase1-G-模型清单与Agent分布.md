# Phase1-G · 模型清单与 Agent 分布（Lobster V2）

更新时间：2026-02-27
维护人：AME（main）
用途：给后续模型调配/Agent 分配提供固定参考，避免每次重复检索。

---

## 1) 可用模型清单（当前）

> 说明：以下来自实时接口与 OpenClaw 模型目录查询。

### A. 自定义 Claude Provider（`claude-proxy`）

来源：`GET http://heibai.natapp1.cc/v1/models`

- amazonq-claude-3-7-sonnet-20250219
- amazonq-claude-sonnet-4-20250514
- claude-3-7-sonnet-20250219
- claude-haiku-3.5
- claude-haiku-4.5
- claude-opus-4-5
- claude-opus-4.5
- claude-opus-4.6
- claude-sonnet-4
- claude-sonnet-4-20250514
- claude-sonnet-4-5
- claude-sonnet-4-5-20250929
- claude-sonnet-4.5
- claude-sonnet-4.6

额外实测可用（虽未在 `/models` 列表中）：
- claude-opus-4.6-fast-thinking

### B. OpenAI-Codex Provider（`openai-codex/*`）

来源：`openclaw --profile lobster-v2 models list --all --provider openai-codex`

- openai-codex/gpt-5.1
- openai-codex/gpt-5.1-codex-max
- openai-codex/gpt-5.1-codex-mini
- openai-codex/gpt-5.2
- openai-codex/gpt-5.2-codex
- openai-codex/gpt-5.3-codex
- openai-codex/gpt-5.3-codex-spark

### C. Embedding（内置 memory_search）

- provider: openai-compatible
- model: text-embedding-v4
- baseUrl: https://dashscope-intl.aliyuncs.com/compatible-mode/v1
- 状态：`memory status --deep` 显示 Embeddings ready

---

## 2) Agent 分布（当前结构）

### 顶层
- `main`（AME，默认）
  - 可调度：dispatch / ks-manager / br-manager / synsnap-manager / research-manager / fun-manager

### 管理层
- `dispatch`
  - 可调度：material / prompt / render / video / qc / reporter
- `ks-manager` → dispatch
- `br-manager` → dispatch
- `synsnap-manager` → dispatch
- `research-manager` → dispatch
- `fun-manager` → dispatch

### 执行层
- `material`
- `prompt`
- `render`
- `video`
- `qc`
- `reporter`

---

## 3) 当前默认模型策略

- 全局默认：`openai-codex/gpt-5.3-codex`
- 重点候选（你指定）：
  - Claude: `claude-opus-4.6` / `claude-sonnet-4.6`
  - OpenAI: `gpt-5.2` / `gpt-5.3`

---

## 4) 维护规则（以后照这个更）

每次模型或 Agent 调整后，追加：

```md
## YYYY-MM-DD HH:mm
- 变更类型：模型新增/下线/Agent改绑
- 改了什么：
- 验证结果：
- 风险与回滚：
- 执行人：
```
