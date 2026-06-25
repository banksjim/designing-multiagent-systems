# Multi-Agent Systems — Learning Plan & Progress Log

> **This file is the single source of truth for Jim's interactive study of multi-agent
> systems, built on Victor Dibia's `designing-multiagent-systems` repo (PicoAgents).**
> It is designed to survive context loss. Any Claude session — in Claude Code, Cowork, or
> chat — should be able to read this file and resume with zero re-explanation.

---

## ⏱️ RESUME HERE — Current State

> **Claude: read this block FIRST on every session start, then read the most recent
> entry in the Session Log at the bottom before doing anything else.**

| Field | Value |
|---|---|
| **Status** | NOT STARTED — environment not yet set up |
| **Current Phase** | Phase 0 — Setup |
| **Current Step** | 0.1 — Fork & clone the repo |
| **Last Completed** | (none yet) |
| **Next Action** | Fork `victordibia/designing-multiagent-systems`, clone the fork, create venv, install PicoAgents, set Anthropic API key |
| **Blocked On** | (nothing) |
| **Last Updated** | (set on first working session) |

**How to update this block:** at the end of every working session, overwrite the table
above and append a new Session Log entry at the bottom. Keep the two in sync.

---

## 🎯 Goal & Teaching Contract

**Goal.** Develop a working, first-principles understanding of how LLM agents and
multi-agent systems are designed, built, evaluated, and run in production — deep enough
to design and maintain a personal "AI Operating System" and compliance-aware agents.

**Method (the teaching contract).**
- **Build-as-you-go, Socratic.** Jim runs real code, then we discuss *why* it's built
  that way, what trade-off it makes, and where it breaks. No passive lecturing.
- **Repo is the spine; Claude is the tutor.** Every concept is anchored to a runnable
  file in the repo. Claude supplies theory, trade-offs, and connections to Jim's stack.
- **One modification per step.** After each file runs, Jim changes one thing and re-runs
  to build intuition before moving on.
- **Compounding.** New concepts get logged in the Concept Ledger so understanding accrues.

**Pace.** Self-directed over weeks. No deadline. Optimize for retention, not speed.

---

## 👤 Learner Context (for Claude)

- Engineering Director at a fintech company; technically strong, comfortable with Python,
  Git, and systems design. Treat as an advanced learner — skip beginner hand-holding.
- Building a personal Compliance AI Operating System (Obsidian + GitHub + Google Workspace).
- **Anthropic API approved for personal use** — run all PicoAgents examples on the Claude
  API via PicoAgents' `AnthropicChatCompletionClient`. (Use a current Claude model string,
  not the dated one in the repo README.)
- Cares about production concerns relevant to financial services: observability,
  human-in-the-loop approval, auditability, evaluation, cost control.
- Prefers brief, conversational explanations and tracked deliverables.

---

## 🛠️ Environment

- **Repo:** https://github.com/victordibia/designing-multiagent-systems (Apache-2.0)
- **Fork target:** Jim's GitHub → clone locally → this plan file lives in the repo root.
- **Key directories:**
  - `code_along/` — minimal agent built in 4 progressive steps (best starting point)
  - `picoagents/` — the full from-scratch framework source
  - `examples/` — 50+ runnable examples organized by chapter
  - `course/` — author's structured course materials
- **Setup commands:**
  ```bash
  git clone https://github.com/<jim>/designing-multiagent-systems.git
  cd designing-multiagent-systems/picoagents
  python -m venv venv && source venv/bin/activate
  pip install -e ".[all]"
  export ANTHROPIC_API_KEY="sk-..."
  ```
- **Recommended:** keep this plan in the repo root and commit it after every session, so
  progress is version-controlled and unloseable.

---

## 🗺️ Curriculum

Five phases. Each step has a **file**, a **learning outcome**, and a **Done when** test.
Check the box only when the "Done when" condition is genuinely met.

### Phase 0 — Setup
- [ ] **0.1** Fork & clone repo, create venv, install PicoAgents, set Anthropic key.
  **Done when:** `python examples/agents/basic-agent.py` runs against the Claude API.

### Phase 1 — The Agent Loop From Zero  *(answers the "loops" question)*
- [ ] **1.1** `code_along/ch04_v1_agent.py` — the bare perceive → reason → act loop.
  **Outcome:** explain the loop's control flow and when it terminates.
  **Done when:** Jim can describe each iteration in his own words.
- [ ] **1.2** `code_along/ch04_v2_tools.py` — tool calling.
  **Outcome:** how the model requests a tool and how results re-enter the loop.
  **Done when:** Jim adds one custom tool and the agent calls it.
- [ ] **1.3** `code_along/ch04_v3_memory.py` — conversation memory.
  **Outcome:** what "memory" actually is (message list management).
  **Done when:** Jim can explain why memory ≠ infinite context.
- [ ] **1.4** `code_along/ch04_v4_streaming.py` — streaming responses.
  **Outcome:** event-driven output and why it matters for UX/observability.
  **Done when:** all four versions run; Jim can diff v1→v4 from memory.

### Phase 2 — The Production Agent (PicoAgents, Ch 4–5)
- [ ] **2.1** `examples/agents/basic-agent.py` + `middleware.py` — middleware system.
- [ ] **2.2** `examples/otel/` — OpenTelemetry observability (ties to audit/compliance).
- [ ] **2.3** `examples/tools/approval_example.py` — human-in-the-loop approval loops.
- [ ] **2.4** `examples/agents/structured-output.py` — typed outputs (Pydantic).
- [ ] **2.5** `examples/agents/computer_use.py` — browser-automation / multimodal agent.
  **Phase Done when:** Jim can assemble an agent with tools + memory + middleware +
  observability + an approval gate, and explain each layer's purpose.

### Phase 3 — Multi-Agent Coordination (Ch 6–7)
- [ ] **3.1** `examples/workflows/` — type-safe deterministic workflows (DAGs).
- [ ] **3.2** `examples/orchestration/round-robin.py` — sequential turn-taking.
- [ ] **3.3** `examples/orchestration/ai-driven.py` — LLM-driven speaker selection.
- [ ] **3.4** `examples/orchestration/plan-based.py` — plan-based (Magentic One) pattern.
  **Phase Done when:** Jim can state the trade-off between deterministic workflows and
  autonomous orchestration, and pick the right one for a given task.

### Phase 4 — Evaluation, Context Engineering & Production (Ch 8–10 + frontier)
- [ ] **4.1** `examples/evaluation/agent-evaluation.py` — LLM-as-judge & metrics.
- [ ] **4.2** `examples/contextengineering/` — context management strategies.
- [ ] **4.3** v0.4.0 features (Feb 2026): **hooks, compaction, context tools** — the
  current frontier of agent-loop design. Read the release notes + relevant examples.
  **Phase Done when:** Jim can design an eval for an agent and explain how compaction +
  context tools keep a long-running loop from degrading.

### Phase 5 — Apply It To Jim's Stack
- [ ] **5.1** Design a small agent that touches Obsidian / GitHub / Workspace.
- [ ] **5.2** Add compliance-grade guardrails: observability, approval gates, eval harness.
- [ ] **5.3** Write up the architecture as a reusable pattern for the AI OS.
  **Phase Done when:** a working, documented agent exists in Jim's environment.

---

## ✅ Progress Tracker (quick glance)

| Phase | Steps Done | Status |
|---|---|---|
| 0 — Setup | 0 / 1 | ⬜ Not started |
| 1 — Agent Loop | 0 / 4 | ⬜ Not started |
| 2 — Production Agent | 0 / 5 | ⬜ Not started |
| 3 — Coordination | 0 / 4 | ⬜ Not started |
| 4 — Eval & Production | 0 / 3 | ⬜ Not started |
| 5 — Apply | 0 / 3 | ⬜ Not started |

---

## 📓 Session Log

> Append a new entry at the END of every working session. Newest at the bottom.
> Template:
> ```
> ### Session N — YYYY-MM-DD
> - Covered: <steps / files>
> - Key insight: <the one thing that clicked>
> - Modification made: <what Jim changed and what happened>
> - Stopped at: <exact file/line/idea>
> - Next action: <single concrete next step — copy this into the RESUME block>
> ```

*(no sessions yet)*

---

## 🧠 Concept Ledger

> Running list of concepts as they're covered, so understanding compounds. Each entry:
> one-line definition in Jim's eventual words + the file where it first appeared.

*(empty — fill as we go)*

---

## ❓ Parking Lot

> Open questions and tangents to revisit, so we don't lose them or derail a session.

*(empty)*
