# ThinkTank-12 · Open Source

> 12 world-class business minds advising on your strategy — simultaneously. The first open-source SkillBot on LoomLoom, and the best reference for creators learning to build AI skillbots.

[English](README.md) | [中文](README.zh-CN.md)

---

## What Is This

ThinkTank-12 is a **SkillBot** running on [CogFoundry LoomLoom](https://github.com/Cogfoundry-labs/loomloom) / [Shengsuan Cloud](https://shengsuanyun.com/loomloom). You describe your business, strategic question, and industry context — optionally upload pre-reading materials — and 12 AI incarnations of legendary business leaders analyze in parallel, converging into a polished HTML strategy report.

It is also the **teaching case** for the LoomLoom creator ecosystem — the full TemplateSpec JSON, knowledge base, and DAG design are open-sourced. Anyone can copy, modify, and commercialize.

> Want to build your own SkillBot? Read the **[Creator Tutorial](CREATOR-TUTORIAL.md)** for a step-by-step guide from idea to revenue.

---

## The 12 Council Members

| | Member | Thinking Framework | Specialty |
|---|--------|---------|---------|
| Elon Musk | First Principles | Tech strategy, disruptive innovation |
| Jeff Bezos | Long-term thinking + Customer obsession | Business models, long-term strategy |
| Steve Jobs | Minimalism + Product intuition | Product design, brand building |
| Warren Buffett | Value investing + Economic moat | Capital allocation, risk management |
| Satya Nadella | Growth mindset + Empathy | Organizational transformation, platform ecosystems |
| Jensen Huang | Accelerated computing + Platform strategy | Tech strategy, AI infrastructure |
| Zhang Yiming | Algorithm-driven + Delayed gratification | Product strategy, globalization |
| Wang Xing | Deep thinking + Infinite game | Competitive strategy, platform economics |
| Jack Ma | Vision-driven + Ecosystem thinking | Business model innovation, market expansion |
| Peter Thiel | Zero to One + Monopoly theory | Disruptive innovation, competitive strategy |
| Charlie Munger | Mental models + Inversion | Decision frameworks, risk identification |
| Ray Dalio | Principle-driven + Radical transparency | Systematic decision-making, organizational principles |

---

## Input Fields: Fully Configurable

| Field | Type | Description |
|------|------|------|
| Business Description | string | Product/service, target users, current stage |
| Strategic Question | string | 1-3 specific questions (the meeting agenda) |
| Industry Context | string | Market size, competitive landscape, tech trends |
| Output Language | enum | Chinese / English |
| Pre-reading | text_reference | Upload .md/.txt background materials for council review |

---

## SkillBot DAG

![ThinkTank-12 DAG](skillbot-dag.svg)

```
Input (5 fields)
  ├── Business Description (founder_business)
  ├── Strategic Question (strategic_question)
  ├── Industry Context (industry_context)
  ├── Output Language (output_language)
  └── Pre-reading (briefing) → injected into each member via upstreamBindings

        ↓ 12 parallel council members (different models, independent analysis)

  ┌─────────────────────────────────────┐
  │  stp_weave01 → Strategy Report     │
  │  dependsOn: all 12 members         │
  │  Model: DeepSeek V4 Pro            │
  └─────────────────────────────────────┘
        ↓

  ┌─────────────────────────────────────┐
  │  stp_htmlr01 → HTML Render         │
  │  dependsOn: 12 members + weave     │
  │  Model: DeepSeek V4 Flash          │
  └─────────────────────────────────────┘
```

---

## LoomLoom Architecture

![LoomLoom Architecture](architecture.svg)

ThinkTank-12 runs on the LoomLoom platform. The architecture above shows the full lifecycle:

- **Creator Workspace**: Four parallel inputs — Skills, Agents, Prompts, Source Code — compiled into IR (TemplateSpec JSON)
- **Build Pipeline**: IR → SkillBot Package → Deploy to CogFoundry / Shengsuan Cloud
- **Platform**: SkillBot Service (registry & versioning) → LoomLoom Hub / Market (listing & pricing)
- **Execution System**: Durable Workflow Execution, Model Execution, and Model Inference core modules, plus Extensible Step Execution (Search / HTTP / Python / MCP)
- **Consumption**: Web App, AI Agents (Codex / Claude Code / Workbuddy), IM/X Chat Plugin
- **Value Flow**: Users pay per use → platform share → creators earn

---

## Files

```
thinktank-12-open-source/
├── README.md                  # This file (English)
├── README.zh-CN.md            # Chinese version
├── CREATOR-TUTORIAL.md        # Creator tutorial (English)
├── CREATOR-TUTORIAL.zh-CN.md  # Creator tutorial (Chinese)
├── template.json              # Full TemplateSpec JSON (deployable)
├── knowledge-base.md          # 12 council member thinking frameworks
├── attribution.md             # Attribution analysis
├── architecture.svg           # LoomLoom platform architecture diagram
├── skillbot-dag.svg           # ThinkTank-12 DAG flow diagram
├── dag-flow.html              # Mermaid DAG visualization
├── input.example.json         # Example input
└── LICENSE                    # MIT
```

---

## Quick Start

```bash
# 1. Install LoomLoom CLI, register on CogFoundry/Shengsuan Cloud for an API key
# 2. Validate locally
loomloom template-spec check ./template.json

# 3. Create as your private template
loomloom template-spec create ./template.json

# 4. Create a new version
loomloom template-spec create-version <template-id> ./template.json

# 5. Publish to Market
loomloom listing publish <template-id> \
  --template-version-id <version-id> \
  --display-name "ThinkTank-12" \
  --description "12 world-class business minds advising on your strategy simultaneously" \
  --task-fixed-fee "1"
```

---

## License

MIT License — Copy, modify, and commercialize freely. If you build something interesting based on this template, we would love to hear about it.

---

## About LoomLoom

[CogFoundry LoomLoom](https://github.com/Cogfoundry-ai/loomloom) / [Shengsuan Cloud](https://shengsuanyun.com/loomloom) is an AI skillbot marketplace aggregating 200+ LLMs and 80+ media generation models. Creators define DAG workflows in JSON, upload them as black-box SkillBots, and sell them on the Market. Users purchase and run SkillBots through CLI in AI Agents like Codex, Claude Code, and WorkBuddy.

- CogFoundry: [Cogfoundry-ai/loomloom](https://github.com/Cogfoundry-ai/loomloom)
- Shengsuan Cloud: https://shengsuanyun.com/loomloom
