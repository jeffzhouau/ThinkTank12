# LoomLoom Creator Tutorial: From Idea to Income — Build Your First Hit SkillBot

> Using ThinkTank-12 as a complete case study: discover demand → design DAG → write TemplateSpec → test and iterate → publish and price → promote and earn.

---

## Foreword: A New Continent for the Creator Economy

In 2026, something big is happening in the AI skillbot market.

In the past, to build an AI product, you had to set up your own backend, integrate model APIs, handle billing, and manage distribution. Now, [CogFoundry LoomLoom](https://github.com/Cogfoundry-ai/loomloom) / [Shengsuan Cloud](https://shengsuanyun.com/loomloom) handles all of that. You only need to do one thing: **figure out what problem your SkillBot solves, then describe it in JSON.**

ThinkTank-12 is the first open-source SkillBot on LoomLoom Market. It lets 12 AI incarnations of business legends (Musk, Bezos, Jobs, Buffett, and more) analyze your strategic questions simultaneously. **This tutorial open-sources its complete source code, design rationale, DAG architecture, and publishing workflow.**

More importantly, this tutorial will show you: **what kind of SkillBot succeeds on LoomLoom, and why.**

---

## Part 1: Re-understanding LoomLoom — What It Really Changes

### 1.1 Not "Just Another AI Tool Platform"

LoomLoom is fundamentally an **AI skillbot marketplace**. It changes three things:

| Traditional Way | LoomLoom Way |
|----------------|-------------|
| Developer integrates model APIs themselves | Platform aggregates 200+ models — you just specify a modelKey |
| Build your own billing system | Pay-per-use, automatic revenue split |
| Handle distribution yourself | One listing → Codex, Claude Code, WorkBuddy users can all use it |
| Open-source code, anyone can copy | Black-box trade, users cannot see your prompts and DAG design |

### 1.2 The Creator's Role Has Changed

On LoomLoom, creators are no longer "developers." They are **"AI experience designers."** Your core competency is not writing code, but:

- **Spotting demand**: Finding scenarios users are willing to pay for
- **Designing DAGs**: Breaking complex tasks into parallel steps
- **Writing prompts**: Giving each step its soul
- **Pricing and operating**: Finding the balance between price and volume

### 1.3 One TemplateSpec Is Your Entire Product

TemplateSpec is a JSON file that defines everything about your SkillBot:

| Section | Meaning | Why It Matters |
|---------|---------|---------------|
| `meta` | Name, description, tags | First impression users see on Market |
| `inputSchema` | What users need to fill in | Simpler input = higher conversion |
| `steps` | Workflow steps | Your core business logic |
| `paramBindings` | How user input is injected | Ensures each step "sees" the right data |
| `upstreamBindings` | How data flows between steps | The key to building complex DAGs |

---

## Part 2: The Creation Path — Building a SkillBot from 0 to 1

### Step 0: Find Your "Aha" Scenario

Before writing any JSON, ask yourself three questions:

1. **What pain is the user suffering?** (How do they solve it without this SkillBot?)
2. **Why can AI solve this pain?** (Multi-model, parallel execution, knowledge breadth — these are AI's unique advantages.)
3. **Why would the user pay?** (Time saved? Better decision quality? New capability unlocked?)

**ThinkTank-12's insight**: When entrepreneurs face major decisions, what they lack most is not information, but **multi-perspective deep analysis**. One person facing a strategic question easily falls into their own thinking habits. If they could simultaneously hear Musk's first principles, Buffett's moat analysis, and Munger's inversion — decision quality would improve dramatically.

**What might your "aha" scenario be?**

| Domain | Scenario | Multi-perspective Source |
|--------|----------|------------------------|
| Code Review | One codebase, multiple paradigm reviews | Functional, OOP, declarative, performance optimization |
| Investment Decisions | One asset, multiple school analyses | Value investing, growth investing, quantitative, macro hedge |
| Product Design | One proposal, multiple role reviews | Interaction designer, visual designer, frontend, user researcher |
| Content Creation | One topic, multiple style rewrites | Serious, humorous, emotional, minimalist |
| Legal Analysis | One business, multi-jurisdiction compliance | China, US, EU, Singapore |
| Education | One concept, multiple teaching methods | Socratic, case-based, analogy, Feynman technique |

**Core principle**: Find decision scenarios where "a single perspective cannot cover the full picture, but multiple parallel perspectives create a qualitative leap."

### Step 1: Design Your DAG — Turn "Ideas" into "Step Diagrams"

DAG (Directed Acyclic Graph) is LoomLoom's core concept. You don't write any code — you just define: **which steps run in parallel, and which steps wait for upstream results.**

Take ThinkTank-12 as an example:

```
Input Layer (5 fields)
  ├── Business Description
  ├── Strategic Question
  ├── Industry Context
  ├── Output Language
  └── Pre-reading (text_reference)

        ↓ 12 steps execute in parallel (no dependsOn = automatic parallel)

  ┌──────────────────────────────────────────┐
  │  stp_musk01   Musk       DeepSeek V4 Pro │
  │  stp_bezos02  Bezos      Gemini 3.5 Flash│
  │  stp_jobs03   Jobs       Gemini 3.5 Flash│
  │  stp_buffet04 Buffett    Gemini 3.5 Flash│
  │  stp_nadel05  Nadella    Gemini 3.5 Flash│
  │  stp_huang06  Huang      DeepSeek V4 Pro │
  │  stp_zhang07  Zhang YM   Gemini 3.5 Flash│
  │  stp_wangx08  Wang Xing  Gemini 3.5 Flash│
  │  stp_mayun09  Jack Ma    Gemini 3.5 Flash│
  │  stp_thiel0a  Peter Thiel Gemini 3.5 Flash│
  │  stp_munge0c  Munger     Gemini 3.5 Flash│
  │  stp_dalio0d  Dalio      Gemini 3.5 Flash│
  └──────────────────────────────────────────┘
        ↓ All complete → converge to weave

  ┌──────────────────────────────────────────┐
  │  stp_weave01  Strategy Report           │
  │  dependsOn: all 12 steps above          │
  │  upstreamBindings: receives each output  │
  │  Model: DeepSeek V4 Pro                 │
  └──────────────────────────────────────────┘
        ↓

  ┌──────────────────────────────────────────┐
  │  stp_htmlr01  HTML Report Render        │
  │  dependsOn: 12 members + weave          │
  │  Model: DeepSeek V4 Flash               │
  └──────────────────────────────────────────┘
```

**Three DAG design principles:**

1. **Parallelize everything possible**: 12 council members analyze simultaneously. User wait time = the slowest step, not the sum of all 12.
2. **Convergence steps need explicit output structure**: The weave step's instruction specifies the report structure (consensus, divergence, insights, recommendations, quotes, risks).
3. **The final step is the "delivery layer"**: The HTML render step turns the Markdown report into a polished web page. Users get a finished, shareable product.

### Step 2: Write the TemplateSpec — Turn the "Step Diagram" into JSON

#### 2.1 Define meta

```json
{
  "meta": {
    "name": "thinktank-12",
    "description": "12 world-class business minds: Musk, Bezos, Jobs, and 9 other legends analyze your strategy using their unique thinking frameworks.",
    "scenario": "Entrepreneurs input business description, strategic questions, industry context, and optionally upload pre-reading materials. 12 council members analyze in parallel, then converge into an HTML strategy report.",
    "inputSummary": "Describe your business, strategic questions, and industry context. 12 business legends advise you simultaneously.",
    "displayOutputType": "text",
    "primaryOutputType": "text",
    "tags": ["strategy", "mentor", "thinktank", "startup"]
  }
}
```

**Key points:**
- `description` is the Market display copy — make it clear at a glance what this SkillBot does
- `scenario` describes the use case, helping the platform with recommendations
- `tags` affect search and categorization — choose 3-5 precise tags

#### 2.2 Define inputSchema — What Users Can Configure

```json
{
  "inputSchema": {
    "fields": [
      {
        "key": "founder_business",
        "label": "Business Description",
        "valueType": "string",
        "description": "Describe your venture: product/service, target users, current stage",
        "required": true,
        "presentation": {
          "placeholder": "e.g., I am building an AI skillbot marketplace...",
          "hint": "The more detail the better — include business model, competitive advantages, team situation",
          "widget": "textarea"
        }
      },
      {
        "key": "strategic_question",
        "label": "Strategic Question",
        "valueType": "string",
        "description": "The strategic question you most need the 12 council members to analyze",
        "required": true,
        "presentation": {
          "placeholder": "e.g., Should I build the creator ecosystem first or go after enterprise clients?",
          "hint": "List 1-3 specific questions",
          "widget": "textarea"
        }
      },
      {
        "key": "industry_context",
        "label": "Industry Context",
        "valueType": "string",
        "description": "Additional industry background",
        "required": false,
        "presentation": {
          "placeholder": "e.g., The AI agent ecosystem is rapidly developing...",
          "hint": "Market size, competitive landscape, technology trends, etc.",
          "widget": "textarea"
        }
      },
      {
        "key": "output_language",
        "label": "Output Language",
        "valueType": "enum",
        "description": "Choose report output language",
        "required": true,
        "enumValues": ["Chinese", "English"],
        "defaultValue": "Chinese",
        "presentation": {
          "hint": "Choose Chinese or English output",
          "widget": "select"
        }
      },
      {
        "key": "briefing",
        "label": "Pre-reading Materials",
        "valueType": "text_reference",
        "acceptedMimeTypes": ["text/plain"],
        "required": false,
        "description": "Optional: upload a .md or .txt file as pre-reading. All 12 council members will read it before analysis.",
        "presentation": {
          "widget": "input",
          "placeholder": "Upload pre-reading file (optional)",
          "hint": "Upload .md or .txt files with project background, data, or context"
        }
      }
    ]
  }
}
```

**Design tips:**
- Fewer input fields = higher conversion. ThinkTank-12 has only 5 fields, 2 of which are optional.
- `text_reference` type is ThinkTank-12's key innovation — users upload pre-reading materials that council members read before analysis.
- Write `presentation.hint` and `placeholder` carefully — they directly affect the user's filling experience.

#### 2.3 Define steps — Your Core Business Logic

Each step is an independent model call. Take Musk as an example:

```json
{
  "stepId": "stp_musk01",
  "displayName": "Elon Musk",
  "executionUnit": "text-generate",
  "instruction": "You are simulating Elon Musk's thinking style. Core thinking: First Principles. Decision principle: Go back to physics fundamentals, question all assumptions, delete-simplify-optimize-accelerate. Style: Bold, direct, unafraid of risk. Classic stance: If things are not failing, you are not innovating enough. Analyze the entrepreneur's questions from first principles and give bold, uncompromising advice.\n\nProvide specific, actionable analysis tailored to the entrepreneur's business and strategic questions. Avoid generic advice. Reflect your unique thinking style and language.",
  "defaultModelRef": {
    "modelKey": "deepseek/deepseek-v4-pro"
  },
  "allowModelOverride": true,
  "upstreamBindings": [
    {
      "inputPort": "reference",
      "sourceType": "initial_input",
      "sourceInputKey": "briefing"
    }
  ]
}
```

**Key design decisions:**
- `instruction` is the "soul" of each step — it defines the AI's role, thinking framework, and language style.
- Different council members use different models: aggressive thinkers (Musk, Huang) use DeepSeek V4 Pro; cautious thinkers (Buffett, Munger) use Gemini 3.5 Flash.
- Pre-reading materials are injected into each council member's `reference` port via `upstreamBindings`.

#### 2.4 Define the Convergence Step — weave

```json
{
  "stepId": "stp_weave01",
  "displayName": "Strategy Report",
  "executionUnit": "text-generate",
  "dependsOn": [
    "stp_musk01", "stp_bezos02", "stp_jobs03", "stp_buffet04",
    "stp_nadel05", "stp_huang06", "stp_zhang07", "stp_wangx08",
    "stp_mayun09", "stp_thiel0a", "stp_munge0c", "stp_dalio0d"
  ],
  "upstreamBindings": [
    {
      "inputPort": "prompt",
      "sourceType": "step_output",
      "sourceStepId": "stp_musk01",
      "sourcePort": "output"
    }
    // ... 12 bindings total
  ]
}
```

**Key design:**
- `dependsOn` lists all upstream steps. The platform automatically waits for all to complete before executing.
- Each council member's full output is injected into the weave step's prompt via `upstreamBindings`.
- The weave step's instruction specifies the report structure: consensus, divergence, unique insights, action recommendations, classic quotes, risk warnings.

#### 2.5 Define the HTML Render Step

The final step is HTML rendering. The instruction is a detailed HTML design specification telling the model to generate a polished page with multiple tabs (Executive Summary, 12 Council Members, Position Spectrum, Quote Attribution, Full Report).

**Core design decision**: Put HTML rendering in LoomLoom cloud execution, not locally. Users receive a complete, browser-ready page — better experience and easier to screenshot and share.

### Step 3: Test and Iterate

```bash
# Validate JSON format locally
loomloom template-spec check ./template.json

# Create a private template
loomloom template-spec create ./template.json

# Prepare test data
echo '{"inputRows":[{"founder_business":"Test","strategic_question":"Test question","industry_context":"","output_language":"Chinese"}]}' > test.json

# Precheck cost
loomloom template-spec precheck <template-id> --input-file test.json

# Run
loomloom template-spec run <template-id> --version-id <version-id> --input-file test.json

# View results
loomloom run get <run-id>
```

**Iteration tips:**
- Run 3-5 times, observe each council member's output quality.
- Adjust instructions to make outputs more aligned with expectations.
- Try different model combinations to find the optimal balance of quality and cost.
- Create new versions: `loomloom template-spec create-version <template-id> ./template.json`

### Step 4: Publish to Market

```bash
loomloom listing publish <template-id> \
  --template-version-id <version-id> \
  --display-name "ThinkTank-12" \
  --description "12 world-class business minds advising on your strategy simultaneously, with a polished HTML report" \
  --task-fixed-fee "1"
```

### Step 5: Pricing Strategy

ThinkTank-12 is priced at ¥1/run. This pricing is based on:

- **Execution cost**: 12 council members + weave + HTML render ≈ ¥0.04 model cost
- **User psychology**: ¥1 for a strategy report — "too cheap not to try"
- **Acquisition positioning**: Low-price hit → users discover the platform → find more SkillBots → ecosystem thrives

---

## Part 3: 5 Laws of SkillBot Success

### Law 1: Solve a Clear Pain Point, Not "Interesting"

Good SkillBots are useful, not just fun. ThinkTank-12 solves the real need for "multi-perspective deep analysis during strategic decision-making."

**Ask yourself**: Before using your SkillBot, what pain is the user suffering?

### Law 2: Minimal Input, Stunning Output

Users fill in only 5 fields but receive 12 council members' deep analysis + a polished HTML report. **Leave complexity to the DAG, leave simplicity to the user.**

### Law 3: Design an "Aha Moment"

The moment users first see the results determines whether they will share. ThinkTank-12's "aha moment": seeing 12 different perspectives collide on one page, each feeling like it was written by a real person.

**Ask yourself**: When users see the results, what will their first reaction be? Will they screenshot and share?

### Law 4: Leverage LoomLoom's Unique Capabilities

Don't build a SkillBot that "could be done on any platform." LoomLoom's differentiators:

- **Multi-model parallel execution**: Call multiple different models in one SkillBot, using the best model for each step.
- **DAG workflow**: Complex multi-step dependencies with automatic parallel scheduling.
- **Black-box protection**: Users cannot see your core prompt design.
- **Batch processing**: Submit Excel/JSONL once, execute in batch.
- **text_reference input**: Users upload pre-reading materials for the SkillBot to work with.
- **Multi-agent distribution**: One listing → Codex, Claude Code, WorkBuddy users can all use it.

### Law 5: Open-Source First, Monetize Later

Your first SkillBot should not pursue high unit prices. ThinkTank-12 chose open-source + low price (¥1):

- **Open-source**: Let creators learn, copy, and improve — build a creator community.
- **Low price**: Let users try without pressure — drive word-of-mouth.
- **Ecosystem**: Individual SkillBot profits are limited, but a thriving creator ecosystem has unlimited value.

---

## Part 4: Advanced — Design Patterns from ThinkTank-12

### Pattern 1: Multi-Model Parallel + Role Injection

Each step uses a different model, with role definition injected through instruction. This ensures diversity of perspectives and differentiation of outputs.

```json
// Aggressive role → strong reasoning model
{ "stepId": "stp_musk01", "modelKey": "deepseek/deepseek-v4-pro" }

// Cautious role → balanced model
{ "stepId": "stp_buffet04", "modelKey": "google/gemini-3.5-flash" }
```

### Pattern 2: text_reference Pre-reading

This is the key upgrade from ThinkTank-13 to ThinkTank-12. Uploaded .md/.txt files are injected into each council member's `reference` port via `upstreamBindings`:

```json
{
  "upstreamBindings": [
    {
      "inputPort": "reference",
      "sourceType": "initial_input",
      "sourceInputKey": "briefing"
    }
  ]
}
```

### Pattern 3: Convergence + Structured Output

The convergence step's instruction explicitly specifies the output structure, ensuring consistent report quality:

```
Report structure:
1. Consensus (points all 12 members agree on)
2. Divergence & Collision (clash of different positions)
3. Unique Insights (one member's distinctive perspective)
4. Action Recommendations (prioritized)
5. Classic Quotes (each member's best lines)
6. Risk Warnings (potentially overlooked risks)
```

### Pattern 4: HTML Delivery Layer

The final step is HTML rendering. Users receive not raw text, but a polished, shareable web page. This lowers the sharing barrier and increases virality.

---

## Part 5: FAQ

**Q: How many steps should my SkillBot have?**
A: No limit. Start with 3-5 steps, validate, then expand. ThinkTank-12 has 14 steps (12 members + weave + HTML), but the core logic is simple.

**Q: How do I choose models?**
A: Use `loomloom template-spec models text-generate` to see available models. Test different models during precheck. Aggressive roles benefit from strong reasoning models; cautious roles work well with balanced models.

**Q: How do I prevent others from copying my SkillBot?**
A: LoomLoom's black-box mechanism ensures users cannot see your prompts and DAG design. But if you choose to open-source like this tutorial, that is your own choice — open-source builds community, which is also a strategy.

**Q: How much can a SkillBot earn?**
A: Depends on pricing and volume. ¥1 × 1,000 monthly runs = ¥1,000/month. ¥10 × 100 monthly runs = ¥1,000/month. The key is finding the balance between price and volume.

**Q: How do I get more people to discover my SkillBot?**
A: The HTML report itself is the best advertisement. Users will screenshot and share on social media, creating organic distribution. You can also add the SkillBot's QR code and usage instructions at the bottom of the report.

**Q: Can I modify ThinkTank-12 and publish my own version?**
A: Yes. MIT license allows copying, modification, and commercial use. Try a different domain (code review, investment decisions, legal analysis) with the same "multi-perspective parallel" pattern to build your own hit.

---

## Appendix: Complete Source Code

ThinkTank-12's full TemplateSpec and knowledge base are open-sourced:

- **GitHub**: [jeffzhouau/ThinkTank12](https://github.com/jeffzhouau/ThinkTank12)

Core files:
- `template.json` — Complete TemplateSpec, directly deployable
- `knowledge-base.md` — 12 council member thinking frameworks
- `attribution.md` — Attribution analysis
- `input.example.json` — Example input

---

## Next Step: Your First SkillBot

After reading this tutorial, you should now understand:

1. **What LoomLoom changes**: Creators shift from "developers" to "AI experience designers"
2. **A repeatable creation path**: Discover demand → Design DAG → Write TemplateSpec → Test → Publish → Price
3. **5 success laws**: Pain point, minimalism, aha moment, platform advantage, open-source first
4. **4 design patterns**: Multi-model parallel, text_reference, convergence output, HTML delivery

Now, open your editor, copy `template.json`, modify the instructions and inputSchema. Create your own SkillBot.

**LoomLoom Market is still in its early days. The best time to publish is now.**

Happy building!
