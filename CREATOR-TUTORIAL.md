# LoomLoom 创作者教程：从灵感到收入——构建你的第一个爆款 SkillBot

> 以「顶级智囊团 ThinkTank-12」为完整案例，拆解一条可复制的创作路径：发现需求 → 设计 DAG → 编写 TemplateSpec → 测试迭代 → 上架定价 → 推广赚钱。

---

## 前言：一个创作者经济的新大陆

2026 年，AI 技能体市场正在发生一件大事。

过去，你想做一个 AI 产品，需要自己搭后端、对接模型 API、处理计费、做分发。现在，[胜算云 LoomLoom](https://shengsuanyun.com/loomloom) 把这些全包了。你只需要做一件事：**想清楚你的 SkillBot 能解决什么问题，然后用 JSON 描述它。**

「顶级智囊团」是 LoomLoom Market 上第一个开源的 SkillBot。它让 12 位商业巨擘（马斯克、乔布斯、巴菲特等）的 AI 分身同时为你的战略问题出谋划策。**这篇文章，将它的完整源码、设计思路、DAG 架构、上架流程全部开源。**

更重要的是，这篇文章会告诉你：**在 LoomLoom 平台上，什么样的 SkillBot 能成功，以及为什么。**

---

## 第一部分：重新理解 LoomLoom——它到底改变了什么

### 1.1 不是"又一个 AI 工具平台"

LoomLoom 的本质是一个 **AI 技能体交易市场**。它改变了三件事：

| 传统方式 | LoomLoom 方式 |
|---------|-------------|
| 开发者自己对接模型 API | 平台聚合 200+ 模型，你只需指定 modelKey |
| 自己搭建计费系统 | 平台按次收费，自动分账 |
| 自己做分发和推广 | 一次上架，Codex、Claude Code、Workbuddy 用户都能用 |
| 代码开源，谁都能抄 | 黑盒交易，使用者看不到你的提示词和 DAG 设计 |

### 1.2 创作者的角色变化

在 LoomLoom 上，创作者不再是"开发者"，而是 **"AI 体验设计师"**。你的核心能力不是写代码，而是：

- **洞察需求**：找到用户愿意付费的场景
- **设计 DAG**：把复杂任务拆解成并行步骤
- **编写提示词**：给每个步骤注入灵魂
- **定价运营**：找到价格和销量的平衡点

### 1.3 一个 TemplateSpec 就是你的全部产品

TemplateSpec 是一个 JSON 文件，它定义了你的 SkillBot 的一切：

| 部分 | 含义 | 为什么重要 |
|------|------|----------|
| `meta` | 名称、描述、标签 | 用户在 Market 看到的第一印象 |
| `inputSchema` | 用户需要填什么 | 输入越简单，转化率越高 |
| `steps` | 工作流步骤 | 你的核心业务逻辑 |
| `paramBindings` | 用户输入如何注入 | 让每个步骤"看到"正确的数据 |
| `upstreamBindings` | 步骤间如何传递数据 | 构建复杂 DAG 的关键 |

---

## 第二部分：创作路径——从 0 到 1 构建一个 SkillBot

### 第 0 步：找到你的"啊哈场景"

在开始写任何 JSON 之前，先问自己三个问题：

1. **用户正在承受什么痛苦？**（没有这个 SkillBot 之前，他在怎么做？）
2. **为什么这个痛苦 AI 能解决？**（多模型、并行、知识广度——这些是 AI 的独特优势）
3. **为什么用户愿意付费？**（省时间？决策质量提升？获得新能力？）

**顶级智囊团的洞察**：创业者在做重大决策时，最缺的不是信息，而是**多视角的深度分析**。一个人面对战略问题，很容易陷入自己的思维惯性。如果能同时听到马斯克的第一性原理、巴菲特的护城河分析、芒格的逆向思维——决策质量会大幅提升。

**你的"啊哈场景"可能是什么？**

| 领域 | 场景 | 多视角来源 |
|------|------|----------|
| 代码审查 | 一份代码，多种编程范式角度审查 | 函数式、面向对象、声明式、性能优化 |
| 投资决策 | 一个标的，多个投资流派分析 | 价值投资、成长投资、量化、宏观对冲 |
| 产品设计 | 一个方案，多个角色评审 | 交互设计师、视觉设计师、前端、用户研究员 |
| 内容创作 | 一个主题，多种风格重写 | 严肃、幽默、煽情、极简 |
| 法律分析 | 一个业务，多个法域合规审查 | 中国、美国、欧盟、新加坡 |
| 教育辅导 | 一个知识点，多种教学方法 | 苏格拉底式、案例教学、类比法、费曼技巧 |

**核心原则**：找到那些"单一视角无法覆盖全貌，但多视角并行就能产生质变"的决策场景。

### 第 1 步：设计你的 DAG——把"想法"变成"步骤图"

DAG（有向无环图）是 LoomLoom 的核心概念。你不需要写任何代码，只需要定义：**哪些步骤并行执行，哪些步骤等待上游结果。**

以顶级智囊团为例：

```
输入层（5 个字段）
  ├── 业务描述
  ├── 核心战略问题
  ├── 行业背景
  ├── 输出语言
  └── 会前资料（text_reference）

        ↓ 12 个步骤并行执行（无 dependsOn = 自动并行）

  ┌──────────────────────────────────────────┐
  │  stp_musk01  马斯克    DeepSeek V4 Pro  │
  │  stp_bezos02  贝索斯    Gemini 3.5 Flash │
  │  stp_jobs03   乔布斯    Gemini 3.5 Flash │
  │  stp_buffet04 巴菲特    Gemini 3.5 Flash │
  │  stp_nadel05  纳德拉    Gemini 3.5 Flash │
  │  stp_huang06  黄仁勋    DeepSeek V4 Pro  │
  │  stp_zhang07  张一鸣    Gemini 3.5 Flash │
  │  stp_wangx08  王兴      Gemini 3.5 Flash │
  │  stp_mayun09  马云      Gemini 3.5 Flash │
  │  stp_thiel0a  彼得·蒂尔  Gemini 3.5 Flash │
  │  stp_munge0c  查理·芒格  Gemini 3.5 Flash │
  │  stp_dalio0d  雷·达里奥  Gemini 3.5 Flash │
  └──────────────────────────────────────────┘
        ↓ 全部完成后，汇聚到 weave

  ┌──────────────────────────────────────────┐
  │  stp_weave01  战略汇总报告              │
  │  dependsOn: 上面 12 个步骤              │
  │  upstreamBindings: 接收每个智囊的 output │
  │  模型: DeepSeek V4 Pro                  │
  └──────────────────────────────────────────┘
        ↓

  ┌──────────────────────────────────────────┐
  │  stp_htmlr01  HTML 报告渲染             │
  │  dependsOn: 12 个智囊 + weave           │
  │  模型: DeepSeek V4 Flash                │
  └──────────────────────────────────────────┘
```

**设计 DAG 的三个原则**：

1. **能并行的绝不串行**：12 个智囊同时分析，用户等待时间 = 最慢的那个步骤，而不是 12 个步骤之和
2. **汇聚步骤要有明确的输出结构**：weave 步骤的 instruction 里指定了报告结构（共识、分歧、洞察、建议、警句、风险）
3. **最后一步是"交付层"**：HTML 渲染步骤把 Markdown 报告变成精美网页，用户拿到的是可分享的成品

### 第 2 步：编写 TemplateSpec——把"步骤图"变成 JSON

#### 2.1 定义 meta

```json
{
  "meta": {
    "name": "thinktank-12",
    "description": "12 位世界顶级商业智囊：让马斯克、贝索斯、乔布斯等 12 位商业巨擘用其独特的思维框架为你的创业战略问题进行分析和建议。",
    "scenario": "创业者输入业务描述、战略问题、行业背景，可选上传会前资料，12 位智囊并行分析后汇总成 HTML 战略报告。",
    "inputSummary": "输入你的业务描述、核心战略问题、行业背景，12 位商业巨擘同步为你出谋划策。",
    "displayOutputType": "text",
    "primaryOutputType": "text",
    "tags": ["strategy", "mentor", "thinktank", "startup"]
  }
}
```

**要点**：
- `description` 是 Market 上的展示文案，要让人一眼看懂这个 SkillBot 能做什么
- `scenario` 描述使用场景，帮助平台推荐
- `tags` 影响搜索和分类，选 3-5 个精准标签

#### 2.2 定义 inputSchema——用户能配置什么

```json
{
  "inputSchema": {
    "fields": [
      {
        "key": "founder_business",
        "label": "创业业务描述",
        "valueType": "string",
        "description": "请描述你的创业项目，包括产品/服务、目标用户、当前阶段",
        "required": true,
        "presentation": {
          "placeholder": "例：我正在做一个 AI 技能体交易平台...",
          "hint": "越详细越好，包括商业模式、竞争优势、团队情况",
          "widget": "textarea"
        }
      },
      {
        "key": "strategic_question",
        "label": "核心战略问题",
        "valueType": "string",
        "description": "你最需要 12 位智囊帮你分析的战略问题",
        "required": true,
        "presentation": {
          "placeholder": "例：我应该先做创作者生态还是先做企业客户？",
          "hint": "可以列出 1-3 个具体问题",
          "widget": "textarea"
        }
      },
      {
        "key": "industry_context",
        "label": "行业背景",
        "valueType": "string",
        "description": "补充行业背景信息",
        "required": false,
        "presentation": {
          "placeholder": "例：AI Agent 生态正在快速发展...",
          "hint": "市场规模、竞争格局、技术趋势等",
          "widget": "textarea"
        }
      },
      {
        "key": "output_language",
        "label": "输出语言",
        "valueType": "enum",
        "description": "选择报告输出语言",
        "required": true,
        "enumValues": ["Chinese", "English"],
        "defaultValue": "Chinese",
        "presentation": {
          "hint": "选择中文或英文输出",
          "widget": "select"
        }
      },
      {
        "key": "briefing",
        "label": "会前资料",
        "valueType": "text_reference",
        "acceptedMimeTypes": ["text/plain"],
        "required": false,
        "description": "可选：上传一份 .md 或 .txt 文件作为会前资料，12 位智囊将在分析前阅读",
        "presentation": {
          "widget": "input",
          "placeholder": "上传会前资料文件（可选）",
          "hint": "上传 .md 或 .txt 文件，包含项目背景、数据或上下文"
        }
      }
    ]
  }
}
```

**设计要点**：
- 输入字段越少，用户转化率越高。ThinkTank-12 只有 5 个字段，其中 2 个是可选的
- `text_reference` 类型是 ThinkTank-12 的关键创新——用户可以上传会前资料，智囊在分析前阅读
- 每个字段的 `presentation.hint` 和 `placeholder` 要认真写，这直接影响用户填写体验

#### 2.3 定义 steps——你的核心业务逻辑

每个 step 是一个独立的模型调用。以马斯克为例：

```json
{
  "stepId": "stp_musk01",
  "displayName": "马斯克",
  "executionUnit": "text-generate",
  "instruction": "你正在模拟埃隆·马斯克的思维方式。核心思维：第一性原理。决策原则：回到物理本质，质疑一切假设，删除-简化-优化-加速。风格：大胆、直接、不惧风险。经典立场：如果事情没有失败的可能，说明你不够创新。请从第一性原理出发，分析创业者的问题，给出大胆、不妥协的建议。\n\n请根据创业者的具体业务和战略问题进行针对性分析。给出具体、可操作的建议，而非泛泛而谈。体现你独特的思维方式和语言风格。",
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

**关键设计**：
- `instruction` 是每个 step 的"灵魂"——它定义了 AI 的角色、思维框架、语言风格
- 不同智囊用不同模型：激进型（马斯克、黄仁勋）用 DeepSeek V4 Pro，稳健型（巴菲特、芒格）用 Gemini 3.5 Flash
- 会前资料通过 `upstreamBindings` 注入到 `reference` 端口，让每个智囊在分析前阅读

#### 2.4 定义汇聚步骤——weave

```json
{
  "stepId": "stp_weave01",
  "displayName": "战略汇总报告",
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
    // ... 共 12 个绑定
  ]
}
```

**关键设计**：
- `dependsOn` 列出所有上游步骤，平台自动等待全部完成后才执行
- 每个智囊的完整输出通过 `upstreamBindings` 注入到 weave 的 prompt
- weave 的 instruction 中指定了报告结构：共识、分歧、洞察、建议、警句、风险

#### 2.5 定义 HTML 渲染步骤

最后一步是 HTML 渲染。instruction 是一份详细的 HTML 设计规范，告诉模型生成一个包含多个 Tab（执行摘要、12 位智囊、立场光谱、警句归属、完整报告）的精美页面。

**核心设计决策**：把 HTML 渲染放在 LoomLoom 云端执行，而不是在本地。用户拿到的是一个完整的、可直接在浏览器打开的页面，体验更好，也更容易截图分享。

### 第 3 步：测试和迭代

```bash
# 本地校验 JSON 格式
loomloom template-spec check ./template.json

# 创建私有模板
loomloom template-spec create ./template.json

# 准备测试数据
echo '{"inputRows":[{"founder_business":"测试","strategic_question":"测试问题","industry_context":"","output_language":"Chinese"}]}' > test.json

# 预检成本
loomloom template-spec precheck <template-id> --input-file test.json

# 正式运行
loomloom template-spec run <template-id> --version-id <version-id> --input-file test.json

# 查看结果
loomloom run get <run-id>
```

**迭代建议**：
- 先跑 3-5 次，观察每个智囊的输出质量
- 调整 instruction 让输出更符合预期
- 尝试不同模型组合，找到质量和成本的最优平衡
- 创建新版本：`loomloom template-spec create-version <template-id> ./template.json`

### 第 4 步：上架到 Market

```bash
loomloom listing publish <template-id> \
  --template-version-id <version-id> \
  --display-name "顶级智囊团" \
  --description "12 位世界顶级商业智囊同时为你的战略问题出谋划策，输出精美 HTML 报告" \
  --task-fixed-fee "1"
```

### 第 5 步：定价策略

顶级智囊团定价 ¥1/次。这个定价基于：

- **执行成本**：12 个智囊 + 汇总 + HTML 渲染 ≈ ¥0.04 模型调用成本
- **用户心理价位**：一份战略报告，¥1 让用户觉得"太便宜了，试试无妨"
- **引流定位**：低价爆款 → 用户接触平台 → 发现更多 SkillBot → 生态繁荣

---

## 第三部分：让 SkillBot 成功的 5 条创作法则

### 法则 1：解决一个明确的痛点，而不是"有趣"

好的 SkillBot 不是"有趣"，而是"有用"。顶级智囊团解决的是"战略决策时缺乏多视角深度分析"这个刚需。

**问自己**：用户用你的 SkillBot 之前，他正在承受什么痛苦？

### 法则 2：输入极简，输出惊艳

用户只需要填 5 个字段，但拿到的是 12 位智囊的深度分析 + 精美 HTML 报告。**把复杂留给 DAG，把简单留给用户。**

### 法则 3：设计一个"啊哈时刻"

用户第一次看到结果时的那个瞬间，决定了会不会传播。顶级智囊团的"啊哈时刻"是：看到 12 个不同视角的观点在同一个页面里碰撞，而且每个都像真人写的。

**问自己**：用户看到结果时，第一反应会是什么？他会截图分享吗？

### 法则 4：利用 LoomLoom 的独特能力

不要做"换个平台也能做"的 SkillBot。LoomLoom 的差异化优势：

- **多模型并行**：一个 SkillBot 里同时调用多个不同模型，每个步骤用最合适的模型
- **DAG 工作流**：复杂的多步骤依赖关系，自动并行调度
- **黑盒保护**：使用者看不到你的核心提示词设计
- **批量处理**：Excel/JSONL 一次提交，批量执行
- **text_reference 输入**：用户可以上传会前资料，让 SkillBot 基于具体材料工作
- **多 Agent 分发**：一次上架，Codex、Claude Code、Workbuddy 用户都能用

### 法则 5：先开源引流，再商业化赚钱

第一个 SkillBot 不要追求高单价。ThinkTank-12 选择了开源 + 低价（¥1）的策略：

- **开源**：让创作者学习、复制、改进，形成创作者社区
- **低价**：让用户无压力尝试，形成口碑传播
- **生态**：单个 SkillBot 的利润有限，但一个繁荣的创作者生态的价值是无限的

---

## 第四部分：进阶——从 ThinkTank-12 学到的设计模式

### 模式 1：多模型并行 + 角色注入

每个步骤使用不同的模型，同时通过 instruction 注入角色设定。这保证了视角的多样性和输出的差异化。

```json
// 激进型角色 → 强推理模型
{ "stepId": "stp_musk01", "modelKey": "deepseek/deepseek-v4-pro" }

// 稳健型角色 → 平衡模型
{ "stepId": "stp_buffet04", "modelKey": "google/gemini-3.5-flash" }
```

### 模式 2：text_reference 会前资料

这是 ThinkTank-12 相比 ThinkTank-13 的关键升级。用户上传的 .md/.txt 文件通过 `upstreamBindings` 注入到每个智囊的 `reference` 端口：

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

### 模式 3：汇聚 + 结构化输出

汇聚步骤的 instruction 明确指定了输出结构，确保报告质量一致：

```
报告结构：
1. 共识区域（12 位智囊都认同的观点）
2. 分歧与碰撞（不同立场的激烈交锋）
3. 独特洞察（某个智囊的独到见解）
4. 行动建议（按优先级排序）
5. 经典警句（每位智囊的精彩原话）
6. 风险警示（可能被忽略的风险）
```

### 模式 4：HTML 交付层

最后一步是 HTML 渲染。用户拿到的不是原始文本，而是一个精美的、可分享的网页。这降低了分享门槛，提升了传播力。

---

## 第五部分：常见问题

**Q: 我的 SkillBot 需要多少步骤？**
A: 没有限制。建议从 3-5 个步骤开始，验证效果后再扩展。ThinkTank-12 有 14 个步骤（12 个智囊 + weave + HTML），但核心逻辑很简单。

**Q: 如何选择模型？**
A: 用 `loomloom template-spec models text-generate` 查看可用模型。建议在 precheck 阶段测试不同模型，比较输出质量和成本。激进型角色用推理能力强的模型，稳健型角色用平衡型模型。

**Q: 如何防止别人抄袭我的 SkillBot？**
A: LoomLoom 的黑盒机制确保使用者看不到你的提示词和 DAG 设计。但如果你像本文一样选择开源，那就是你自己的选择——开源可以建立创作者社区，也是一种策略。

**Q: 一个 SkillBot 能赚多少钱？**
A: 取决于定价和销量。定价 ¥1 × 月销 1000 次 = ¥1000/月。定价 ¥10 × 月销 100 次 = ¥1000/月。关键是找到定价和销量的平衡点。

**Q: 如何让更多人知道我的 SkillBot？**
A: HTML 报告本身就是最好的广告。用户会截图分享到社交媒体，形成自然传播。也可以在报告底部加入 SkillBot 的二维码和使用说明。

**Q: 我可以基于 ThinkTank-12 修改后上架吗？**
A: 可以。MIT 许可证允许复制、修改、商用。建议你换一个领域（比如代码审查、投资决策、法律分析），用同样的"多视角并行"模式，打造你自己的爆款。

---

## 附录：完整源码

顶级智囊团 ThinkTank-12 的完整 TemplateSpec 和知识库已开源：

- **GitHub**: [Cogfoundry-ai/loomloom](https://github.com/Cogfoundry-ai/loomloom)
- **开源目录**: 见本仓库 `thinktank-12-open-source/`

核心文件：
- `template.json` — 完整的 TemplateSpec，可直接部署
- `knowledge-base.md` — 12 位智囊的思维框架知识库
- `attribution.md` — 智囊发言归属分析
- `input.example.json` — 示例输入

---

## 下一步：你的第一个 SkillBot

读完这篇文章，你应该已经理解了：

1. **LoomLoom 改变了什么**：创作者从"开发者"变成"AI 体验设计师"
2. **一条可复制的创作路径**：发现需求 → 设计 DAG → 写 TemplateSpec → 测试 → 上架 → 定价
3. **5 条成功法则**：痛点、极简、啊哈时刻、平台优势、开源引流
4. **4 个设计模式**：多模型并行、text_reference、汇聚输出、HTML 交付

现在，打开你的编辑器，复制 `template.json`，修改 instruction 和 inputSchema，创建你自己的 SkillBot。

**LoomLoom 的 Market 还在早期，最好的上架时间是现在。**

Happy building!
