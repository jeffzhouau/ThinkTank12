# LoomLoom Creator Tutorial: From Idea to Income — Build Your First Hit SkillBot

> Using ThinkTank-12 as a complete case study: discover demand → design DAG → write TemplateSpec → test → publish → earn.

---

## Why LoomLoom Changes Everything

LoomLoom is an **AI skillbot marketplace**. You do not build backends, integrate model APIs, or handle billing. You do one thing: **define what your SkillBot solves, then describe it in JSON.**

ThinkTank-12 is the first open-source SkillBot on LoomLoom Market. It lets 12 AI incarnations of business legends (Musk, Jobs, Buffett, etc.) analyze your strategy simultaneously. This tutorial open-sources its complete source, DAG design, and publishing workflow.

| Traditional Way | LoomLoom Way |
|----------------|-------------|
| Build your own backend | Platform handles everything |
| Integrate model APIs yourself | 200+ models, just specify a modelKey |
| Set up billing from scratch | Pay-per-use, automatic revenue split |
| Do your own distribution | One listing → Codex, Claude Code, WorkBuddy users |
| Open-source code, anyone can copy | Black-box trade, users cannot see your prompts |

---

## The Creator's Role

On LoomLoom, you are not a "developer." You are an **AI experience designer**. Your core skills:

- **Spot demand**: Find scenarios users will pay for
- **Design DAGs**: Break complex tasks into parallel steps
- **Write prompts**: Give each step its soul
- **Price and operate**: Find the balance between price and volume

---

## The Creation Path: 0 to 1

### Step 0: Find Your "Aha" Scenario

Ask three questions:

1. **What pain is the user feeling?** (How do they solve it without this SkillBot?)
2. **Why can AI solve this pain?** (Multi-model, parallel, knowledge breadth — these are AI's unique advantages.)
3. **Why would the user pay?** (Time saved? Decision quality? New capability?)

**ThinkTank-12's insight**: Entrepreneurs making big decisions lack multi-perspective deep analysis. One person facing a strategic question easily falls into their own thinking habits. Hearing Musk's first principles, Buffett's moat analysis, and Munger's inversion simultaneously — decision quality improves dramatically.

### Step 1: Design Your DAG

![ThinkTank-12 DAG](skillbot-dag.svg)

DAG (Directed Acyclic Graph) is LoomLoom's core concept. Define which steps run in parallel, and which wait for upstream results.

**Three DAG principles:**

1. **Parallelize everything possible**: 12 council members analyze simultaneously. Wait time = slowest step, not sum of all 12.
2. **Convergence steps need clear output structure**: The weave step specifies structure (consensus, divergence, insights, recommendations, quotes, risks).
3. **Final step is the delivery layer**: HTML rendering turns the Markdown report into a polished, shareable page.

### Step 2: Write the TemplateSpec

A TemplateSpec is a JSON file that defines everything about your SkillBot.

**meta**: Name, description, tags — what users see on Market.

**inputSchema**: What users fill in. Fewer fields = higher conversion. ThinkTank-12 has only 5 fields, 2 optional.

**steps**: Your core business logic. Each step is an independent model call with an instruction defining the AI's role and thinking framework.

**upstreamBindings**: How data flows between steps. ThinkTank-12 uses `text_reference` to inject pre-reading materials into every council member's reference port.

### Step 3: Test and Iterate

```bash
loomloom template-spec check ./template.json
loomloom template-spec create ./template.json
loomloom template-spec precheck <template-id> --input-file test.json
loomloom template-spec run <template-id> --version-id <version-id> --input-file test.json
loomloom run get <run-id>
```

Run 3-5 times, observe each council member's output quality, tweak instructions, try different model combinations.

### Step 4: Publish to Market

```bash
loomloom listing publish <template-id> \
  --template-version-id <version-id> \
  --display-name "ThinkTank-12" \
  --description "12 world-class business minds advising on your strategy" \
  --task-fixed-fee "1"
```

### Step 5: Pricing Strategy

ThinkTank-12 is priced at ¥1 / run (~$0.14). This is based on:
- **Execution cost**: 12 council members + weave + HTML render ≈ ¥0.04 model cost
- **User psychology**: ¥1 for a strategy report — "too cheap to not try"
- **Acquisition positioning**: Low-price hit → users discover platform → find more SkillBots → ecosystem thrives

---

## 5 Laws of SkillBot Success

1. **Solve a clear pain point, not "interesting"**: Good SkillBots are useful, not just fun.
2. **Minimal input, stunning output**: 5 fields in, 12 analyses + polished HTML out.
3. **Design an "aha moment"**: The first time a user sees 12 different perspectives colliding on one page.
4. **Leverage LoomLoom's unique capabilities**: Multi-model parallel, DAG workflow, black-box protection, batch processing, text_reference input, multi-agent distribution.
5. **Open-source first, monetize later**: First SkillBot to build community. Low price to drive adoption.

---

## Design Patterns from ThinkTank-12

### Pattern 1: Multi-Model Parallel + Role Injection

Assign different models to different roles. Aggressive thinkers (Musk, Huang) use DeepSeek V4 Pro. Cautious thinkers (Buffett, Munger) use Gemini 3.5 Flash.

### Pattern 2: text_reference Pre-reading

Uploaded .md/.txt files are injected into each council member's reference port via upstreamBindings:

```json
{
  "upstreamBindings": [{
    "inputPort": "reference",
    "sourceType": "initial_input",
    "sourceInputKey": "briefing"
  }]
}
```

### Pattern 3: Convergence + Structured Output

The weave step's instruction explicitly specifies the output structure, ensuring consistent report quality.

### Pattern 4: HTML Delivery Layer

The final step renders a polished, multi-tab HTML page. Users get a finished product, not raw text. Lowers the sharing barrier, increases virality.

---

## FAQ

**Q: How many steps should my SkillBot have?**
A: Start with 3-5. ThinkTank-12 has 14 steps but the core logic is simple.

**Q: How do I choose models?**
A: Use `loomloom template-spec models text-generate` to see available models. Test different models during precheck.

**Q: Can I copy and modify ThinkTank-12?**
A: Yes. MIT license. Try a different domain (code review, investment analysis, legal compliance) with the same multi-perspective pattern.

---

## Next: Your First SkillBot

You now understand:
1. What LoomLoom changes — creators become AI experience designers
2. A repeatable creation path — discover demand → design DAG → write TemplateSpec → test → publish → price
3. 5 success laws — pain point, minimalism, aha moment, platform advantage, open-source first
4. 4 design patterns — multi-model parallel, text_reference, convergence output, HTML delivery

Open your editor, copy `template.json`, modify the instructions and inputSchema. Build your own.

**LoomLoom Market is still early. The best time to publish is now.**

Happy building!
