# MEMORY

## Principles
- Store decisions and reusable experience only.
- Keep control-layer memory concise and verifiable.
- Do not store raw chat logs as final memory.

## Phase-1 Curated Seeds (2026-02-27)

### 1) `#ame-hq` mandatory response
- Date: 2026-02-27
- Topic: Control channel discipline
- Decision: In `#ame-hq`, owner maintenance messages must always receive a structured reply, never `NO_REPLY`.
- Why: Control instructions are governance-critical and cannot be silently dropped.
- Reuse Rule: Apply to every owner message in channel `1476909205779906613`.

### 2) Three-lens impact contract
- Date: 2026-02-27
- Topic: Control reply quality
- Decision: Before finalizing any control reply, explicitly evaluate `memory`, `session`, and `workspace` impact.
- Why: This avoids partial decisions and makes rollback/review practical.
- Reuse Rule: Use for all architecture, routing, and governance changes.

### 3) Governance and execution separation
- Date: 2026-02-27
- Topic: Channel boundary
- Decision: Keep `#ame-hq` for governance only; push execution details to manager/dispatch/pipeline channels.
- Why: Control channel needs short, decision-ready information.
- Reuse Rule: If output includes worker-level detail, redirect it out of `#ame-hq`.

### 4) Rollback-first multi-agent changes
- Date: 2026-02-27
- Topic: Change safety
- Decision: Any change touching multiple agents/channels must declare scope, non-scope, and immediate rollback point.
- Why: Prevents long outage during migration and keeps blast radius clear.
- Reuse Rule: Required for config/binding/session-policy changes.

### 5) Verifiability over fluency
- Date: 2026-02-27
- Topic: Evidence discipline
- Decision: Do not state unverified outcomes; do not fabricate links, IDs, or execution status.
- Why: A confident wrong control decision causes routing drift.
- Reuse Rule: If evidence is missing, mark unknown and request/collect proof first.

### 6) Memory hygiene
- Date: 2026-02-27
- Topic: Long-term memory quality
- Decision: `MEMORY.md` keeps durable decisions and rules; daily logs stay in date files.
- Why: Mixed raw logs degrade recall quality and cause noisy prompts.
- Reuse Rule: When updating memory, summarize to reusable rules instead of copying chat.

### 7) AI 内容生产铁律（Lobster）
- Date: 2026-02-27
- Topic: AI 网红/电影方向的执行原则
- Decision: Adopt a production-first doctrine: sample-first, traceable-delivery, two-layer memory capture, and rollback-first system changes.
- Why: Our primary business is image/video delivery, not pure software development; process must optimize output quality + speed + recoverability.
- Reuse Rule:
  - Every pitfall stores TWO memories (fact + decision) and verifies recall.
  - Completion requires artifact + receipt + parameters + owner + timestamp.
  - Client scopes stay isolated (KS/BR/FILM); methods may transfer, raw context may not.
  - Any plugin `.ts` change requires clearing `/tmp/jiti` before gateway restart.
