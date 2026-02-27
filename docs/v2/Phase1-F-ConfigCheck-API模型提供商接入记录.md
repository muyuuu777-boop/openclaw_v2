# Phase1-F · Config Check：API/模型提供商接入记录

更新时间：2026-02-27
负责人：AME（main）

## 本次变更
- 在 `~/.openclaw-lobster-v2/openclaw.json` 新增自定义模型提供商：`models.providers.claude-proxy`
- 接口类型：OpenAI-compatible（`api: openai-responses`）
- 目标模型：`claude-opus-4.6-fast-thinking`（200k 上下文）
- 凭据已写入配置（文档中不记录明文）

## 设计目的
- 给后续不同 Agent 分配不同模型做准备
- 保留现有默认主模型（`openai-codex/gpt-5.3-codex`）不变，降低迁移风险

## 当前状态
- 配置已生效（`openclaw config get models` 可见 provider）
- 尚未切换任何 Agent 到新 provider（安全渐进）

## 下一步（建议顺序）
1. 先给 `research-manager` 或 `fun-manager` 做灰度切换
2. 通过 3 条标准用例验证：
   - 普通对话
   - 工具调用
   - 长上下文稳定性
3. 通过后再分配到业务 Agent

## 风险与回滚
- 风险：代理服务不稳定或模型兼容性差异
- 回滚：移除 `models.providers.claude-proxy` 或将 Agent 模型改回原值
