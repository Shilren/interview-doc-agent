# 📝 求职文档 Agent · Interview Doc Agent

> 一个把你的零散经历，沉淀成「面试就绪经历库」，再一键生成**简历**和**面试逐字稿**的 AI Skill。
> 借鉴 [Andrej Karpathy 的 LLM Wiki 思路](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)，可在 **Obsidian** 和 **飞书** 中使用。

---

## 💡 核心理念

求职准备最大的痛点不是「不会写」，而是：
- 经历散落在各种文档、聊天记录、脑子里，每次写简历/准备面试都要重新翻一遍
- 每次让 AI 生成，都要把一大堆原始资料重新喂一遍，**又贵又慢、还容易丢细节**
- 简历、逐字稿、不同岗位的定制版，各写各的，**数据对不齐**

这个 Agent 用 **Karpathy 的 LLM Wiki 模式**解决它：

> 不要每次都从原始资料里现查，而是**让 AI 增量地维护一个持久的知识库**——经历进来时整理一次，之后所有生成都基于这个精炼的库。

### 三层数据架构

```
原始素材 materials/ ──整理一次──▶ 完善经历 经历库/ ──生成──▶ output/
 （粘贴的原始 dump）            （面试就绪，单一可信源）    （简历 / 逐字稿）
                                      ▲
                          目标岗位 JD jd/ ──匹配定制──┘
```

| 层 | 作用 | 类比 Karpathy |
|---|---|---|
| `materials/` | 原始素材，粘进来就行 | Raw sources（原始文档） |
| `经历库/` | 整理成面试就绪的完善档案 | Wiki layer（LLM 维护的知识库） |
| `wiki/index.md` | 轻量检索表，生成时先看它定位 | Index（索引，避免每次全量检索）|
| `SKILL.md` | 指导 AI 行为的配置 | Schema（行为配置）|

**省 token 的关键**：生成时先读索引 → 只读相关的 1-2 篇经历 → 细节不足才回查原文。项目越多，省得越多。

---

## ✨ 亮点

- **🎯 面试方法论内置**：项目逐字稿强制走「背景思考 → 定义问题 → 手段&成果」三段式，复用「我判断发力重点在 X」「逻辑是…具体动作是…」等高质量句式
- **📊 数据零丢失**：整理经历时量化数据（CAC/留存/提升%）全部保留，生成时绝不编造，缺数据用 `___` 占位
- **♻️ 一次整理，处处复用**：简历、逐字稿、JD 定制版都从同一个经历库生成，数据永远对齐
- **🔌 双平台**：同一套 SKILL.md，既能在 Obsidian（Claudian 插件）用，也能接入飞书
- **💸 省钱省 token**：索引 + 压缩经历库，不必每次重喂全部原始资料
- **🆓 无需 API key**：由对话型 AI（Claudian / 飞书智能伙伴 / Claude Code）直接读写文件执行

---

## 🚀 快速开始

### 在 Obsidian 中使用 → 看 [docs/02-安装-obsidian.md](docs/02-安装-obsidian.md)
### 接入飞书使用 → 看 [docs/03-接入-飞书.md](docs/03-接入-飞书.md)
### 完整使用指南 → 看 [docs/04-使用指南.md](docs/04-使用指南.md)
### 设计理念详解 → 看 [docs/01-理念-karpathy-wiki.md](docs/01-理念-karpathy-wiki.md)

**30 秒上手：**
1. 把这个仓库放进你的知识库（Obsidian vault 或飞书云空间）
2. 把你的简历模板放进 `templates/简历/`，面试话术模板放进 `templates/逐字稿/`
3. 把你的项目经历（任何格式的原始记录）粘进 `materials/`
4. 对 AI 说：「整理进经历库」→ 再说「写一份简历」或「写小红书项目的逐字稿」
5. 产出出现在 `output/`

---

## 📂 目录结构

```
interview-doc-agent/
├── SKILL.md            # 核心：给 AI 读的执行说明
├── templates/          # 模板库（学写作风格）
│   ├── 简历/           #   简历模板（.tex 排版 / .md 改写）
│   └── 逐字稿/         #   面试话术模板 + 范文
├── 经历库/             # ✨ 完善经历（生成主来源）
│   └── 00-个人档案.md  #   基础信息 + 索引 + 人设关键词
├── materials/          # 原始素材（粘贴的 dump）
├── jd/                 # 目标岗位 JD（定制用）
├── output/             # 生成的文档
├── wiki/index.md       # 检索索引
└── docs/               # 保姆级教程
```

---

## 📜 License

MIT — 详见 [LICENSE](LICENSE)。模板部分参考了 [autoCVmkr / Puneet Gautam 的 MIT 简历模板](https://github.com/kryptoniteX/autocvmkr)。

## 🙏 致谢
- [Andrej Karpathy — LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) 的知识库维护思路
- [Claudian](https://github.com/YishenTu/claudian) — 把 Claude Code 嵌入 Obsidian 的插件
