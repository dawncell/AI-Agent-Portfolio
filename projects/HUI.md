<div align="center">

# HUI

### Long-term Personal AI with Memory, Self Model & Evidence Evolution

**一个本地优先、能够长期理解并持续更新“我是谁”的个人 AI 系统**

`Long-term Memory` · `Self Model` · `RAG` · `Evidence Evolution` · `Context Engineering` · `Local-first` · `SQLite`

> **不是让 AI “记住更多聊天”，而是让它逐渐形成一个有证据、可修正、会演化的长期自我模型。**

</div>

---

## 📌 项目定位

HUI 是一个面向长期个人使用的 Personal AI / Long-term Agent Memory 项目。

它最初来自一个很个人化的问题：

> **如果存在“另一个更完整、更理性的自己”，它应该如何真正理解我？**

普通 Chatbot 可以在一次 Conversation 中表现得很懂用户，但长期使用后会遇到更困难的问题：

- 什么信息值得记住？
- 一次随口说的话应该成为长期事实吗？
- 用户自我评价和真实行为冲突时相信谁？
- 人会改变，旧 Memory 应该怎么办？
- 同一个人在工作、关系、压力等不同 Context 下可能完全不同，系统应该如何表示？
- AI 如何解释“为什么我认为你是这样的人”？
- 如何避免模型把自己的推测逐渐写成用户事实？
- RAG 找到了历史内容，并不等于真正理解了一个人。

因此 HUI 的核心不只是聊天，而是构建一个：

> **Evidence-driven、Context-aware、Evolvable Personal Self Model**

---

## ⚡ 30 秒看懂 HUI

| 问题 | HUI 的处理方式 |
|---|---|
| AI 冷启动不了解用户 | `Genesis` 建立初始 Self Model |
| 自我描述可能不准确 | `Base Self Calibration` |
| 一次聊天不能代表长期人格 | `Evidence + Confidence` |
| AI 推测不能直接成为事实 | `Self Belief / Observed Self` 分离 |
| 新证据和旧认知冲突 | `supports / challenges / refines` |
| 人会随时间变化 | `first_seen / last_confirmed / trend` |
| 不同场景下表现不同 | `Contextual Self` |
| 历史内容越来越多 | `Chunk → Embedding → Retrieval` |
| 需要知道结论从哪里来 | `Evidence Provenance` |
| 多用户测试数据不能混 | `Per-user SQLite Isolation` |
| 个人数据隐私敏感 | `Local-first` |

一句话概括：

> **HUI 研究的不是“AI 怎么记住一句话”，而是“AI 如何长期、可解释地形成并更新对一个人的理解”。**

---

# 1. 为什么要做 HUI？

传统 AI 对话通常可以表示为：

```text
User Message
     ↓
LLM
     ↓
Response
```

加入简单 Memory 后：

```text
Conversation
     ↓
Memory
     ↓
LLM
     ↓
Response
```

但 HUI 想解决的问题更进一步：

```text
Conversation / Experience / Profile
              ↓
            Evidence
              ↓
        Memory Processing
              ↓
           Self Model
              ↓
      Contextual Understanding
              ↓
             HUI
              ↓
       Response / Reflection
              ↓
          New Evidence
              ↓
        Self Model Evolution
```

这形成一个长期闭环：

> **Experience → Evidence → Understanding → Interaction → New Evidence → Evolution**

---

# 2. HUI 的核心设计问题

如果用户今天说：

> “我其实很喜欢冒险。”

系统是否应该立即永久记录：

```text
User = Risk-taking
```

HUI 的答案是：

> **不应该。**

因为这句话可能是：

- 稳定人格
- 当前情绪
- 自我期待
- 对某次事件的解释
- 特定 Context 下的行为
- 一次偶然表达

因此 HUI 不把“模型听到一句话”直接等价为“用户事实”。

系统需要考虑：

```text
Source
Context
Time
Evidence Type
Confidence
Repetition
Conflict
Correction
```

---

# 3. Genesis —— 冷启动

长期 Personal AI 面临第一个问题：

> 第一次见面时，AI 对用户几乎一无所知。

如果完全依赖自然聊天慢慢积累，需要非常长的冷启动时间。

因此 HUI 设计了 Genesis。

Genesis 用结构化输入建立最初的 Base Self。

当前探索过的信息包括：

```text
Basic Identity
Self View
IPIP-50
Self-reported MBTI
Values
Decision Scenarios
Constitution
Optional Life Story
```

但 HUI 并不认为这些测试结果等于“真实人格”。

它们只是：

> **Cold-start Evidence**

而不是最终结论。

---

# 4. Base Self

Genesis 完成后，系统生成初始 Base Self。

Base Self 可以理解为：

> **HUI 在当前证据下，对“你可能是怎样的人”的第一版结构化理解。**

例如：

```text
Genesis Evidence
      ↓
Interpretation
      ↓
Base Self v1
```

它不是永久 Profile。

后续用户可以：

- 确认
- 质疑
- 修正
- 补充

因此 Base Self 是：

> **Versioned Self Model**

而不是一次生成后永久不变的 Persona。

---

# 5. Base Self Calibration

模型生成的人格描述很容易出现：

> “听起来很合理，但不像我。”

因此 HUI 在 Base Self v1 后增加 Calibration。

用户可以逐条判断：

```text
像我
不确定
不像我
```

如果“不像我”，可以进一步给出 Correction。

流程：

```text
Base Self v1
      ↓
User Calibration
  ↙      ↓       ↘
像我    不确定    不像我
                   ↓
               Correction
                   ↓
              Base Self v2
```

Calibration 的意义不是简单修改一段文本。

用户主动 Correction 会成为高优先级 Self Belief Evidence。

---

# 6. Descriptive Self ≠ Constitution

HUI 明确区分两个容易混在一起的概念。

### Descriptive Self

回答：

> **“我实际上是怎样的人？”**

例如：

- 行为倾向
- 决策模式
- 性格特征
- Contextual Pattern

### HUI Constitution

回答：

> **“HUI 应该怎样成为另一个更完整、更理性的我？”**

它描述的是 HUI 的行为原则与价值约束。

因此：

```text
Descriptive Self
        ≠
HUI Constitution
```

一个描述现实中的“我”。

另一个约束 HUI 应该“如何思考和回应”。

---

# 7. Self Belief 与 Observed Self

HUI 不希望把所有关于用户的信息塞进一个 Profile。

因此 Self Model 中区分：

### Self Belief

用户明确表达的自我认知。

例如：

> “我觉得自己做决定比较果断。”

### Observed Self

从长期真实行为和重复经历中形成的观察。

例如：

```text
User repeatedly delays decisions
when uncertainty is high
```

这两者可能一致：

```text
Self Belief
     ↓
supports
     ↓
Observed Pattern
```

也可能冲突：

```text
Self Belief
     ↓
challenges
     ↓
Observed Pattern
```

这种冲突本身就是有价值的信息。

---

# 8. Evidence-driven Self Model

HUI 的核心不是：

```text
Memory → Profile
```

而是：

```text
Evidence
   ↓
Interpretation
   ↓
Self Belief / Observation
   ↓
Confidence
   ↓
Self Model
```

当前 Evidence Priority 的设计思想是：

```text
Repeated Real Behavior
        ↓
Real Experience + Reflection
        ↓
Long-term Self Belief
        ↓
Genesis Decision Scenario
        ↓
Structured Self-report
        ↓
Symbolic Description
```

也就是说：

> **真实、重复发生的行为证据，通常比一次测试标签更值得信任。**

---

# 9. Self Evolution

人不是静态 Profile。

因此 HUI 不希望 Memory 只支持：

```text
ADD
```

还要支持：

```text
supports
challenges
refines
```

例如：

```text
Existing Belief
"我在压力下通常非常果断"
        ↓
New Evidence
"连续几次高风险决策中明显延迟"
        ↓
Challenge
        ↓
Refined Belief
"在一般压力下果断，
但高不确定性 + 高风险时更谨慎"
```

这比简单覆盖旧 Memory 更接近真实的人。

---

# 10. Temporal Evidence

一个关于人的判断还需要时间维度。

HUI 的 Self Evolution 可以维护：

```text
first_seen
last_confirmed
confidence
trend
```

例如：

```text
Belief:
High need for control

first_seen:
2026-03

last_confirmed:
2026-08

confidence:
0.82

trend:
stable
```

这样 HUI 才可能逐渐区分：

> “你一直如此。”

和：

> “你最近开始变得如此。”

---

# 11. Contextual Self

同一个人在不同 Context 中可能表现完全不同。

例如：

```text
Work
→ decisive / structured

Close Relationship
→ emotionally sensitive

High Uncertainty
→ cautious

Learning
→ exploratory
```

如果系统把这些全部压成：

```text
User = decisive
```

就会损失大量真实信息。

因此 HUI 探索 Contextual Self：

```text
Global Self
   ├── Work Self
   ├── Relationship Self
   ├── Learning Self
   └── High-pressure Self
```

目标不是制造多个人格，而是：

> **允许一个人的不同侧面同时成立。**

---

# 12. Memory Architecture

HUI 将 SQLite 作为原始事实与 Evidence 的权威存储。

整体思路：

```text
Conversation / Memory / Profile / Documents
                    ↓
          SQLite：Raw Facts & Evidence
                    ↓
           Normalized Evidence
                    ↓
                  Chunk
                    ↓
            Dense Embedding
                    ↓
              Vector Index
                    ↓
                Retrieval
                    ↓
             Context Builder
                    ↓
                   LLM
```

这里非常重要的一点是：

> **Vector Database / Embedding 不是 Memory 本身。**

Embedding 解决的是：

> “怎样找到相关内容？”

而 Self Model 解决的是：

> “这些内容意味着什么？”

---

# 13. Chunking & Retrieval

当长期数据越来越多时，不可能把全部历史内容放进 Context Window。

因此 HUI 的 RAG Pipeline 会经历：

```text
Original Text
      ↓
Chunk
      ↓
Embedding
      ↓
Vector Retrieval
      ↓
Relevant Evidence
      ↓
Context Assembly
      ↓
LLM
```

Chunk 需要保留：

```text
source
start
end
timestamp
evidence_id
```

以保证 Retrieval 后能够追溯原始信息。

核心原则：

> **Retrieval 应该返回 Evidence，而不是制造新的事实。**

---

# 14. Memory ≠ RAG

HUI 中需要特别区分：

```text
RAG
```

和：

```text
Long-term Memory
```

RAG 更关注：

> 找到与当前问题语义相关的历史内容。

Long-term Memory 还需要处理：

- Write
- Update
- Conflict
- Confidence
- Temporal Change
- Provenance
- Context
- Forgetting / Decay
- User Correction

所以：

> **RAG 是 HUI Memory Architecture 的一部分，但不是全部。**

---

# 15. Evidence Provenance

如果 HUI 说：

> “你在高不确定性情况下通常会更加谨慎。”

用户应该有机会继续问：

> “你为什么这么认为？”

因此长期目标是让 HUI 能够追溯：

```text
Belief
  ↓
Supporting Evidence
  ├── Evidence A
  ├── Evidence B
  └── Evidence C
```

而不是：

```text
LLM:
"根据我的了解，你就是这样。"
```

这让 Self Model 从“模型印象”逐渐变成：

> **Evidence-backed Understanding**

---

# 16. Local-first

HUI 涉及的数据可能包括：

- Personal Reflection
- Life Experience
- Self Belief
- Long-term Conversation
- Decision Pattern

这些内容比普通 Chat History 更敏感。

因此项目采用 **Local-first** 思路。

当前核心数据以 SQLite 为主，优先保存在本地环境。

设计目标：

```text
User Data
    ↓
Local Storage
    ↓
Explicit Processing
    ↓
Controlled Model Context
```

而不是默认将所有长期个人数据暴露给外部系统。

---

# 17. Tester Mode

当 HUI 从“只有我自己使用”走向 5–10 人测试时，会出现一个新的问题：

> **不同用户的长期 Memory 绝对不能混在一起。**

因此 Tester Mode 采用 Per-user SQLite：

```text
data/
└── users/
    ├── user_A/
    │   └── hui.db
    ├── user_B/
    │   └── hui.db
    └── user_C/
        └── hui.db
```

系统级数据库只保存最少的用户索引信息。

例如：

```text
system.db
├── uuid
├── nickname
├── role
└── active_time
```

个人 Memory / Self Model 则保存在各自独立数据库。

核心原则：

> **User Identity Boundary = Memory Boundary**

---

# 18. Current Evolution

HUI 当前经历的主要阶段：

| Version | 核心变化 |
|---|---|
| **V0.01** | CLI + SQLite + 基础 Memory 操作 |
| **V0.04** | Web Chat + SSE Streaming |
| **V0.06** | Profile / Self Belief / Observed Self 分离 |
| **V0.07** | Genesis + Base Self v1 |
| **V0.08** | Base Self Calibration + Versioned Self |
| **V0.09** | Evidence Priority + Contextual Self + Self Evolution |
| **Current** | RAG / Chunk / Embedding / Retrieval 基础能力继续完善 |

---

# 19. Current Data State

当前开发阶段已经形成：

```text
Genesis Answers
        ↓
Base Self v1
        ↓
Calibration
        ↓
Base Self v2
        ↓
Self Belief
        ↓
Evidence Evolution
```

当前系统重点不是追求“大量用户数据”，而是先验证：

> **长期 Self Model 的数据结构和演化逻辑是否合理。**

Observed Self 与 Self Evolution 仍需要通过后续真实长期使用积累更多 Evidence。

---

# 20. Engineering Decisions

HUI 的一些关键设计选择并不是“功能”，而是为了避免长期 Agent 中容易出现的问题。

<details>
<summary><b>Decision 01：为什么不直接把 MBTI 当人格？</b></summary>

MBTI、IPIP 等结构化测试可以帮助冷启动。

但它们只能作为 Evidence Source。

```text
MBTI
  ↓
Cold-start Evidence
  ↓
Base Self
```

而不是：

```text
MBTI
  ↓
Permanent User Identity
```

长期真实行为可以支持、挑战或修正初始判断。

</details>

<details>
<summary><b>Decision 02：为什么 User Correction 具有高优先级？</b></summary>

如果 HUI 描述：

> “你非常喜欢社交。”

用户明确回答：

> “这不像我。”

系统不能继续因为历史模型推断而坚持原结论。

因此 Calibration Correction 会进入高优先级 Self Belief Evidence。

但 Correction 仍然与 Observed Behavior 分离保存。

</details>

<details>
<summary><b>Decision 03：为什么不直接覆盖旧 Memory？</b></summary>

因为人的变化本身有价值。

```text
Old Belief
   ↓
New Evidence
   ↓
Refinement
```

比：

```text
Old Belief → DELETE
New Belief → INSERT
```

保留了更多长期演化信息。

</details>

<details>
<summary><b>Decision 04：为什么 Conversation 不能直接等于 Memory？</b></summary>

Conversation 中包含：

- 临时情绪
- 假设
- 玩笑
- 模型推测
- 一次性事件
- 长期事实

如果全部直接进入长期 Memory，会迅速污染 Self Model。

因此 Conversation 更适合作为：

> **Potential Evidence Source**

而不是自动成为长期事实。

</details>

<details>
<summary><b>Decision 05：为什么 SQLite 是 Authoritative Store？</b></summary>

Embedding 和 Vector Index 更适合 Retrieval。

但它们不适合作为事实的唯一来源。

HUI 将原始事实、Evidence 和结构化 Self Model 保存在 SQLite，使：

- Source 可追踪
- 数据可检查
- Evidence 可重新计算
- Embedding 可重新生成

因此：

> **SQLite stores truth; Vector Index helps retrieve it.**

</details>

---

# 21. Architecture Boundary

```text
┌───────────────────────────────────────────┐
│                 Interface                 │
│                                           │
│ Web Chat · Calibration · Reflection       │
├───────────────────────────────────────────┤
│              Self / Memory Layer          │
│                                           │
│ Genesis · Base Self · Self Belief         │
│ Observed Self · Contextual Self            │
│ Evidence · Confidence · Evolution         │
├───────────────────────────────────────────┤
│              Retrieval Layer              │
│                                           │
│ Chunk · Embedding · Vector Retrieval      │
│ Context Builder · Provenance              │
├───────────────────────────────────────────┤
│                 Data Layer                │
│                                           │
│ SQLite · Raw Facts · Evidence · Versions  │
└───────────────────────────────────────────┘
```

---

# 22. HUI 与普通 AI Memory 的区别

普通 Memory 常见思路：

```text
User said X
    ↓
Remember X
```

HUI 更关注：

```text
User said / did X
       ↓
What kind of evidence is X?
       ↓
How reliable is it?
       ↓
What context did it happen in?
       ↓
Does it support / challenge an existing belief?
       ↓
Should confidence change?
       ↓
Should the Self Model evolve?
```

所以 HUI 的目标不是：

> **Remember more**

而是：

> **Understand better over time**

---

# 23. HUI 与 MA-20 的关系

HUI 与 MA-20 是两个独立项目，但它们研究的是 Agent System 的两个不同问题。

```text
MA-20
│
├── Execution
├── Reliability
├── Recovery
├── Verification
└── Runtime
```

```text
HUI
│
├── Memory
├── Context
├── Evidence
├── Self Model
└── Evolution
```

可以简单理解为：

> **MA-20 研究 Agent 如何可靠地“做事”。**  
> **HUI 研究 Agent 如何长期地“记住并理解”。**

未来两者可以共享部分 Agent Infrastructure，但当前保持独立演化。

---

# 24. What HUI Does NOT Claim

HUI 当前仍是个人长期实验项目。

它目前不宣称：

- 能准确预测人格
- 心理学诊断能力
- Self Model 等于客观真实人格
- MBTI / IPIP 可以定义一个人
- AI 可以完全理解用户
- RAG 可以解决所有长期 Memory 问题
- 当前 Evidence Ranking 已经过大规模用户验证
- 当前 Self Evolution 算法已经达到生产级稳定性

更准确的定义是：

> **HUI 是对 Long-term Agent Memory、Evidence-driven Self Model 与 Personal AI Architecture 的工程探索。**

---

# 25. Current Technical Focus

| Direction | Current Focus |
|---|---|
| **Long-term Memory** | Write / Retrieve / Update / Conflict |
| **Self Model** | Base Self / Self Belief / Observed Self |
| **Evidence** | Priority / Provenance / Confidence |
| **Self Evolution** | supports / challenges / refines |
| **Temporal Modeling** | first_seen / last_confirmed / trend |
| **Context Engineering** | Contextual Self / Context Builder |
| **RAG** | Chunk / Embedding / Retrieval |
| **Privacy** | Local-first / User Isolation |
| **Testing** | Tester Mode / Multi-user Boundary |

---

# 26. Engineering Principles

> **01 · Memory is not conversation history.**

长期 Memory 不能只是聊天记录的堆积。

---

> **02 · Retrieval is not understanding.**

找到相关文本，不代表系统理解了它对用户意味着什么。

---

> **03 · Model inference is not user fact.**

模型推测不能悄悄变成用户事实。

---

> **04 · Self-report is evidence, not absolute truth.**

用户自我评价很重要，但仍然可以与长期行为 Evidence 分开建模。

---

> **05 · People change. Memory should evolve.**

长期系统必须允许旧理解被支持、挑战和修正。

---

> **06 · Context matters.**

一个人在不同情境下表现不同，这些差异不应该被压成单一标签。

---

> **07 · Understanding should be explainable.**

如果 HUI 形成一个关于用户的判断，长期目标是能够回答：

> “为什么？”

---

# 27. Roadmap

- [x] CLI + SQLite
- [x] Web Chat + SSE
- [x] Genesis
- [x] Base Self v1
- [x] Base Self Calibration
- [x] Versioned Base Self
- [x] Self Belief / Observed Self separation
- [x] Evidence Priority design
- [x] Contextual Self design
- [ ] Observed Self long-term accumulation
- [ ] Self Evolution production loop
- [ ] Dense Embedding
- [ ] Vector Retrieval
- [ ] Evidence-aware Context Builder
- [ ] Memory Conflict Resolution
- [ ] Temporal Decay / Reconfirmation
- [ ] Evidence Provenance UI
- [ ] Tester Mode
- [ ] 5–10 user closed testing
- [ ] Long-term Evaluation

长期方向：

```text
Chatbot with Memory
        ↓
Long-term Personal Agent
        ↓
Evidence-driven Personal AI
```

---

# 28. Repository Scope

当前 GitHub Repository 主要作为 HUI 的公开技术作品集。

公开内容重点展示：

- Product Idea
- Memory Architecture
- Self Model Design
- Evidence Model
- RAG Pipeline
- Engineering Decisions
- Demo
- Roadmap

由于 HUI 涉及真实个人长期数据，公开 Repository 不应包含：

```text
Real User Memory
Personal Conversation
Private SQLite Database
API Key
.env
User Profile Data
Sensitive Logs
```

核心原则：

> **公开 Architecture，不公开 Personal Data。**

---

# 29. Project Positioning

HUI 最开始想回答的是：

> **“另一个更完整、更理性的自己”应该是什么样？**

但真正开始实现以后，问题逐渐变成：

```text
AI 应该记住什么？
什么不能直接记？
一次表达能代表长期人格吗？
用户和 AI 的判断冲突怎么办？
真实行为和 Self-report 冲突怎么办？
人的变化怎么表示？
不同 Context 下的自己怎么表示？
历史 Evidence 如何检索？
AI 如何解释自己的长期判断？
怎样避免 Memory 越积越错？
```

这些问题最终指向：

# **Long-term Agent Memory & Self Model**

因此 HUI 当前更准确的技术定位是：

> **面向长期 Personal AI 的 Memory / Context / Evidence / Self Evolution 工程实践。**

它研究的不是：

> 如何让 AI 永远记住更多东西。

而是：

> **如何让 AI 在时间中逐渐形成一个有证据、可解释、可修正、会演化的“对你的理解”。**

---

<div align="center">

**HUI · Long-term Memory · Self Model · Evidence Evolution · Personal AI**

</div>
