# 📝 求职文档 Agent · Interview Doc Agent

> 把零散经历沉淀成「经历库」，一键生成**简历**和**面试逐字稿**的 AI Skill。
> 借鉴 [Karpathy 的 LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)，可在 Obsidian / 飞书 / 各类 coding AI 中使用。

---

## 三步上手

### ① 装：下载一个文件

skill 本体就是 `SKILL.md` 一个文件，不用 clone 整个仓库。

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
