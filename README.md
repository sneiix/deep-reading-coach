# deep-reading-coach｜深度阅读教练

一个开源的 AI Skill：把任意英文文章变成**可学习、可自测、可复盘**的精读稿。

## 1. 解决的问题

读英文长文时，大多数人的动作只有两个：查生词、看翻译。结果是词都认识、文章仍然读不懂，做题也说不清为什么错。这个 Skill 把阅读拆成四件能练的事——**结构怎么看、句子怎么拆、语法点在哪、题目怎么定位**——并用固定字段输出，保证每次交付的深度一致，而不是随手写一段感想。

## 2. 主要功能

| 能力 | 说明 |
| --- | --- |
| 自定义阅读内容 | 精读用户粘贴的任意英文原文（100–900 词）；也可按主题与难度自建一篇原创短文（默认 B2、180–300 词、3–5 段） |
| 阅读学习指导 | 段落功能标签（引入／背景／论点／例证／让步／反驳／结论）、分层、立场与信号词、针对体裁的读法与 5 分钟训练 |
| 核心语法点提取 | 从句、非谓语、插入语、倒装、虚拟、比较、强调句等，每点给「结构式 + 逐字原句切片 + 作用 + 易错点」 |
| 阅读题目实战 | 按题型出题（主旨／细节／推断／词义／态度）、讲解自带题目、按错因复盘（定位错／偷换概念／程度过强／无中生有／过度推断） |

配额随文本长度自动调整（词数 → 长难句／语法点／词汇／题目数量），短文本不会硬凑，长文本不会注水。

## 3. 安装方法

Skill 是一个文件夹，把 `deep-reading-coach/` 整个复制到所用客户端的 skills 目录即可：

```
deep-reading-coach/
├── SKILL.md            # 触发描述 + 执行规则 + 输出模板
└── agents/
    └── openai.yaml     # 显示名、简介、默认提示词
```

- **豆包 / 工作模式**：放入
  `%LOCALAPPDATA%\Doubao\User Data\Default\.doubao\agent_mode\workspace\.user_skills\`
  即 `<workspace>/.user_skills/deep-reading-coach/`。
- **Claude Code / Codex 等支持 Skill 的客户端**：放入其 skills 根目录（如 `~/.claude/skills/`）。
- 校验：

```bash
python quick_validate.py deep-reading-coach
# Skill is valid!
```

无需安装依赖、无需运行脚本，全部能力由 SKILL.md 的规则与模板驱动。

## 4. 使用方法

直接把英文原文粘贴进来，加一句你的目的即可；不说明时默认走完整精读。

| 你可以这样说 | 交付内容 |
| --- | --- |
| 精读这篇 / 读懂这篇 / 分析这篇文章 | 概况、主旨、结构、长难句、语法点、词汇、立场、实战题、读法 |
| 提取语法点 / 这篇有什么语法 | 语法分布、逐点拆解、易错点、改写练习 |
| 出题考我 / 这几道题怎么做 / 我错了两道 | 出题自测、逐题定位排除、错因复盘 |
| 这句怎么分析 / 这段什么意思 | 单句七字段精析 |
| 怎么读这类文章 / 给我一套阅读方法 | 体裁读法、信号词、5 分钟训练、常见误区 |
| 给我一篇关于城市绿化的阅读 / 按雅思 6.5 难度写一篇 | 原创原文 + 生词 + 结构提示 + 重点语法 + 实战题 |

示例提问：

> 精读下面这篇文章，并出 4 道题考我：
> *（粘贴英文原文）*

## 5. 输入输出示例

**输入**（110 词，3 段，实际测试用例）：

> Schools that have replaced handwriting with keyboards often justify the change in terms of speed...
> Yet a growing body of research points the other way. Students who take notes by hand must summarise on the spot...
> None of this is an argument for banning laptops. It is an argument for knowing what a tool is doing to the mind that uses it.

**输出（节选，配额：110 词 → 长难句 2／语法点 3／词汇 6／题目 3）**：

```
【概况】110 词 / 3 段 / 议论文（教育评论）/ B2
【主旨】手写笔记的“慢”迫使思考，选工具要看它如何塑造思维。
【结构】
P2 论点：手写逼人提炼，键盘倾向照抄
   主题句：“Yet a growing body of research points the other way.”
【长难句】2 句
S1（P2 第 2 句，30 词）
原文：Students who take notes by hand must summarise on the spot, because no one can write down every word.
主干：Students must summarise
修饰：who take notes by hand ← Students；because no one can write down every word ← 原因状语从句
语法：定语从句 + 原因状语从句
直译：用手记笔记的学生必须当场概括，因为没有人能把每个词都写下来。
意译：手写笔记的人只能边听边概括，因为没人记得下每一个字。
【语法点】3 个
G1 不定式作宾语补足语｜结构式：force／allow／ask + 宾语 + to do
例：That constraint forces them to decide what matters（P2 第 3 句）
作用：交代“被迫”发生的动作。
【词汇】6 条
constraint /kənˈstreɪnt/ n. 限制 → 本句：That constraint 这一限制
【立场】有限保留｜信号词：Yet、by contrast、None of this is an argument for
【实战】3 题（题型：主旨 1／细节 1／推断 1）
Q3（推断）作者对“禁用笔记本”持什么态度？
A. 支持
B. 反对
C. 未表态
D. 主张立即推行
> 答案：B｜定位：P3 第 1 句 “None of this is an argument for banning laptops”｜排除：A、D 与原文相反；C 原文有明确表态｜错因：推断题—偷换立场
【读法】① 见 Yet 先判断：前一段是被推翻的常识。② 结论段出现 None of this is an argument for 时，读成“我不是要主张…”。
```

**输出（语法点单独提取，片段）**：

```
【语法分布】虚拟条件倒装、主语从句＋表语从句、插入语（as 从句）
G1 虚拟条件倒装｜结构式：Were + 主语 + 过去分词, 主句 would + do
例：Were the sums done honestly（第 4 句）
拆解：Were the sums done ＝ If the sums were done；主句 most transport planners would admit
作用：省略 if，语气更正式、语序更紧凑。
【易错点】把 as critics sometimes claim 当成定语从句修饰 The change，误译成“被批评者声称的变化”。
【练一练】用 Were 倒装改写：If the plan were published, residents would object.
参考答案：Were the plan published, residents would object.
```

**输出（自建原文，片段）**：

```
# Why Cities Need Trees More Than They Think（187 词 / B2）
On a hot afternoon the surface of asphalt can be fifteen degrees warmer than the air above a park...
【结构提示】
P2 论点一：树靠遮阴与释水降温
【重点语法】① 同位语（a process 解释前句动作）：a process that works like a small air conditioner
```

**输出（错因复盘，片段）**：

```
【错因归类】Q3 程度过强：把“有助于”读成“只能作用于数字”。
【回看】Q3 → P3 第 3 句 “turns a fact you can recite into an idea you can use”
【改法】凡选项出现 only／always／never，回原文找反例再排除。
```

## 6. 目录结构

```
.
├── LICENSE
├── README.md
└── deep-reading-coach/
    ├── SKILL.md
    └── agents/openai.yaml
```

许可证：MIT。

不包含脚本与额外依赖；`SKILL.md` 只保留规则与输出模板，两者一一对应，交付前有 9 项自检清单。
