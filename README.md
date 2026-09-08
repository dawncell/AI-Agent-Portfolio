<div align="center">


# 👋 Hi, I'm MHJ

### Agent Systems · Long-term Memory · Edge AI

**电子信息 硕士 · AI Agent & Edge AI 工程实践**

我关注的不是单一模型能力，而是一个更完整的问题：

> **如何让 AI 真正进入长期任务与真实世界——能做事、能记忆、能感知。**

`Agent Runtime` · `Harness Engineering` · `Agent Reliability` · `Long-term Memory` · `RAG` · `Edge AI` · `Windows`

</div>

---

## 🚀 About Me

目前主要围绕 **Agent Systems Engineering** 进行工程实践，同时持续探索 Edge AI / Embedded AI。

我的项目逐渐形成了三条相互关联的技术主线：

```text
                    Agent Systems
                         │
          ┌──────────────┼──────────────┐
          │              │              │
          ▼              ▼              ▼
       MA-20            HUI          Edge AI
     Reliable        Long-term       Physical
     Execution        Memory        Perception
          │              │              │
       做事情           记忆与理解        感知现实
```

可以简单理解为：

> **MA-20 负责“可靠地做事”**  
> **HUI 负责“长期地记忆与理解”**  
> **Edge AI 负责“感知并进入真实世界”**

这也是我目前希望继续深入的方向：

> **Agent Runtime / Reliability + Memory / Context + Edge AI**

---

# ⭐ Featured Projects

## 01 · MA-20

### Reliable Agent Runtime for Multi-Agent Software Engineering

`Agent Runtime` `Harness Engineering` `Multi-Agent` `Recovery` `Verification` `Windows`

MA-20 是一个面向 Windows 环境的多智能体软件工程平台，也是我围绕 **Agent Runtime / Harness Engineering / Agent Reliability** 的主要工程实践。

它关注的核心问题不是：

> “如何让多个 Agent 一起对话？”

而是：

> **如何让不完全可靠的 LLM Agent，在真实软件工程环境中长期、可控、可恢复、可观测、可验证地完成任务？**

核心机制包括：

- Requirement Compiler
- Task DAG
- TaskContract
- Structured Handoff
- ExecutionCell
- Git Worktree Isolation
- Process / Port Ownership
- Persistent Execution State
- Approval Boundary
- Repair / Retry / Recovery
- Evidence-backed Completion
- Verifier / Evaluation
- Recovery Circuit
- Execution Trace / Observability

### Engineering Evidence

| Validation                    |                             Result |
| ----------------------------- | ---------------------------------: |
| Automated regression          |               **853 tests passed** |
| SQLite targeted repair        |      **41 tests passed after fix** |
| ExecutionCell qualification   | **32 / 32 core invariants passed** |
| Hard Violation                |                              **0** |
| Process / Port / Temp residue |                              **0** |

> **Agent says "done" ≠ task is complete.**

📖 **[查看 MA-20 完整项目介绍](projects/ma20.md)**

---

## 02 · HUI

### Long-term Personal AI with Memory, Self Model & Evidence Evolution

`Long-term Memory` `Self Model` `RAG` `Evidence` `Context Engineering` `Local-first`

HUI 是一个面向长期个人使用的 Personal AI / Long-term Agent Memory 项目。

它最初来自一个问题：

> **如果存在“另一个更完整、更理性的自己”，它应该如何真正理解我？**

项目没有把 Memory 简化成“保存更多聊天记录”，而是探索：

```text
Experience
    ↓
Evidence
    ↓
Memory
    ↓
Self Model
    ↓
Contextual Understanding
    ↓
Interaction
    ↓
New Evidence
    ↓
Self Evolution
```

核心设计包括：

- Genesis 冷启动
- Base Self
- Base Self Calibration
- Self Belief / Observed Self
- Evidence Priority
- Contextual Self
- supports / challenges / refines
- first_seen / last_confirmed / trend / confidence
- SQLite Authoritative Store
- Chunk / Embedding / Retrieval
- Evidence Provenance
- Local-first
- Per-user Data Isolation

HUI 的几个核心原则：

> **Memory is not conversation history.**  
> **Retrieval is not understanding.**  
> **Model inference is not user fact.**  
> **People change. Memory should evolve.**

📖 **[查看 HUI 完整项目介绍](projects/hui.md)**

---

## 03 · Edge AI / ESP32

### On-device Perception & Intelligent Terminal Exploration

`ESP32-S3` `MobileNetV3` `Computer Vision` `Model Compression` `Embedded AI`

这一方向关注 AI 如何从纯软件系统进入真实设备。

目前实践包括：

- ESP32-S3
- Camera / Sensor Input
- Emotion Recognition
- Fatigue Estimation
- Health-related State Estimation
- MobileNetV3-Small
- Knowledge Distillation
- Lightweight Model
- Edge Inference
- Hardware / Software Integration

长期希望形成：

```text
Camera / Sensor / Voice
          ↓
   Local Perception
          ↓
      User State
          ↓
    Local Memory
          ↓
        Agent
       ↙     ↘
Cloud Reasoning  Local Decision
          ↓
     Device Action
```

目标不是只做一个分类模型，而是进一步探索：

> **Agent + Edge AI + Intelligent Terminal**

📖 **[查看 Edge AI 项目介绍](projects/xiaozhi.md)**

---

# 🧠 What I'm Exploring

当前最关注三个技术问题。

### ① Agent Reliability / Harness Engineering

```text
State
Task Contract
Tool
Permission
Approval
Retry
Repair
Recovery
Verifier
Evidence
Observability
```

核心问题：

> **如何让概率性的 LLM Agent 在确定性的 Runtime Boundary 中可靠执行？**

---

### ② Long-term Memory / Context Engineering

```text
Write
Retrieve
Update
Conflict
Confidence
Provenance
Temporal State
Contextual Self
Evidence Evolution
```

核心问题：

> **Agent 如何在长期交互中形成可追溯、可修正、会演化的 Memory？**

---

### ③ Edge Agent / Intelligent Terminal

```text
Sensor
Perception
On-device Model
Local State
Agent
Cloud Reasoning
Device Action
```

核心问题：

> **Agent 如何从软件环境进一步进入真实设备和物理世界？**

---

# 🛠️ Technical Stack

### Agent / AI

`LLM API` · `Multi-Agent` · `RAG` · `Embedding` · `Knowledge Distillation` · `Computer Vision`

### Backend / Runtime

`Python` · `SQLite` · `SSE` · `WebSocket` · `REST API`

### Agent Engineering

`Task DAG` · `TaskContract` · `Git Worktree` · `Recovery` · `Verifier` · `Evidence`

### Windows Runtime

`Windows` · `ConPTY` · `Windows Job Object` · `Process Management` · `Port Management`

### Edge / Embedded

`ESP32-S3` · `MobileNetV3` · `Edge Inference`

### Development

`Git` · `GitHub` · `Docker` · `WSL2` · `PowerShell`

---

# 🔬 Engineering Interests

我更关注 AI 从“模型能力”进入“系统能力”之后出现的问题。

例如：

```text
How does an Agent fail?

How should execution state be persisted?

How should an Agent recover after failure?

How can completion be verified?

How should long-term memory evolve?

How should evidence conflict be handled?

How can AI interact with physical devices?
```

因此，我目前更希望继续深入：

**Agent Engineer / Agent Infra / Harness Engineering / AI Platform / Edge AI**

等工程方向。

---

# 📂 Repository Structure

```text
AI-Agent-Portfolio/
│
├── README.md
│
├── projects/
│   ├── ma20.md
│   ├── hui.md
│   └── xiaozhi.md
│
├── demos/
│   └── hui-demo.mp4
│
├── assets/
│   ├── ma20/
│   ├── hui/
│   └── edge-ai/
│
└── portfolio/
    └── Ma_Huijie_AI_Agent_Portfolio.pdf
```

---

# 🎯 Current Direction

我目前希望逐渐形成自己的技术主线：

```text
                 Agent Systems Engineer
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        ▼                ▼                ▼
 Agent Runtime       Agent Memory       Edge Agent
        │                │                │
 Reliability          Context          Perception
 Recovery             Evidence          Device
 Verification         Evolution         Action
```

不是同时追逐所有 AI 方向，而是围绕一个问题持续深入：

> **怎样让 AI 从“会回答”，逐渐走向“会做事、记得住、能进入真实世界”。**

---

<div align="center">


### Thanks for visiting.

**Agent Systems · Reliable Execution · Long-term Memory · Edge AI**

</div>
