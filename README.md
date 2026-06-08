# 📝 求职文档 Agent · Interview Doc Agent

> 把零散经历沉淀成「经历库」，一键生成**简历**和**面试逐字稿**的 AI Skill。
> 
> 借鉴 [Karpathy 的 LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)，可在 Obsidian / 飞书 / 各类 coding AI 中使用。

---
###项目概述：[设计理念](docs/01-理念-karpathy-wiki.md) 
经历散落在各种文档里，每次写简历、准备面试都要重新翻一遍、重新喂给 AI，又贵又慢还容易丢细节，而且简历和面试逐字稿的数据经常对不齐。大多数人把 AI 当成「一次性改写工具」，但 AI 真正的杠杆其实在「可复用的知识沉淀」。

**怎么做的**：我借鉴了 Karpathy 的 LLM Wiki 思路，设计了一个三层架构——原始素材进来后，AI 把它整理成一个「经历库」，之后所有简历、逐字稿、不同岗位的定制版，都从这个经历库生成。生成时先查一个轻量索引定位、只读相关的经历，而不是把全部资料重喂一遍，这样既省 token 又保证数据对齐。我还把面试方法论写进了 AI 的指令里，强制它按「背景—问题—手段成果」的结构输出。

## 三步上手

### ① 装：下载一个文件

skill 本体就是 `SKILL.md` 一个文件，不用 clone 整个仓库。

### 用顺手的AI一键下载指令：

**Obsidian（Claudian 插件）**
```bash
curl -L https://raw.githubusercontent.com/Shilren/interview-doc-agent/main/SKILL.md \
  -o "<你的Vault>/.claudian/skills/生成求职文档.md"
```

**Claude Code**
```bash
mkdir -p ~/.claude/skills/interview-doc && \
curl -L https://raw.githubusercontent.com/Shilren/interview-doc-agent/main/SKILL.md \
  -o ~/.claude/skills/interview-doc/SKILL.md
```

**飞书**：把 `SKILL.md` 全文粘进「智能伙伴」指令框（详见 [docs/03-接入-飞书.md](docs/03-接入-飞书.md)）。

### ② 喂：放入经历

1. 对 AI 说「**帮我初始化**」→ 自动建好所有文件夹
2. 把项目经历（任何格式，复制粘贴）放进 `materials/`
3. 把简历模板放进 `templates/简历/`（可选，没有就用默认）

### ③ 用：开口要

| 你说 | 它做 |
|---|---|
| 「整理进经历库」 | 把 materials/ 的原始素材整理成完善档案 |
| 「写一份简历」 | 按模板 + 经历库生成简历 → `output/` |
| 「写小红书项目的逐字稿」 | 生成简单版+复杂版逐字稿 → `output/` |
| 「按 jd/ 里的 JD 定制简历」 | 匹配岗位生成定制版 |

---

## 支持哪些 AI

任何「能读写本地文件 + 能多轮对话」的 AI 都能用：

- **非程序员首选**：Obsidian + [Claudian](https://github.com/YishenTu/claudian)、飞书智能伙伴
- **Coding AI**：Claude Code、Cursor、Windsurf、Cline、GitHub Copilot、Aider、通义灵码等

---

## 它怎么做到省 token 又保质量

三层结构（借鉴 Karpathy LLM Wiki）：

```
materials/  ──整理一次──▶  经历库/  ──生成──▶  output/
原始素材                  完善档案(单一可信源)   简历/逐字稿
                             ▲
                       jd/ ──定制──┘
```

生成时先读 `wiki/index.md` 索引定位，**只读相关的 1-2 篇经历**，不必每次重喂全部资料 → 省 token；所有产出同源 → 数据永远对齐。

> **为什么不用 RAG？** 个人经历库整理后通常只有几千到一两万 token，远低于「上下文模式完胜 RAG」的 ~10 万 token 界限。这个量级下直接用上下文最可靠（检索零失败）、零维护（不需要向量库/嵌入/分块）。详见 [设计理念](docs/01-理念-karpathy-wiki.md)。

---

## 目录结构

```
├── SKILL.md      # 核心：给 AI 的执行说明（唯一必需文件）
├── templates/    # 模板（简历 / 逐字稿）
├── 经历库/        # 完善经历，生成主来源
├── materials/    # 原始素材
├── jd/           # 目标岗位 JD
├── output/       # 产出
├── wiki/index.md # 检索索引
└── docs/         # 详细教程
```

## 详细文档
[设计理念](docs/01-理念-karpathy-wiki.md) ｜ [Obsidian 安装](docs/02-安装-obsidian.md) ｜ [接入飞书](docs/03-接入-飞书.md) ｜ [使用指南](docs/04-使用指南.md)

## License & 致谢
MIT（[LICENSE](LICENSE)）。致谢 [Karpathy LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)、[Claudian](https://github.com/YishenTu/claudian)、[autoCVmkr 简历模板](https://github.com/kryptoniteX/autocvmkr)。
