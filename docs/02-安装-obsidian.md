# 保姆级教程：在 Obsidian 中使用

本教程教你把这个 Agent 装进 Obsidian，用侧边栏对话就能生成简历和逐字稿。全程不需要写代码。

---

## 它的原理（先理解，30 秒）

- Obsidian 本质是一堆 Markdown 文件夹，天然适合当知识库
- [Claudian 插件](https://github.com/YishenTu/claudian) 把 AI（Claude Code）嵌进 Obsidian 侧边栏，能直接读写你 vault 里的文件
- 我们把这个 Agent 文件夹放进 vault，把 `SKILL.md` 注册成 Claudian 的 skill，对话时 AI 就会按 SKILL.md 的流程帮你生成

---

## 步骤一：准备 Obsidian 和 Claudian 插件

1. 安装 [Obsidian](https://obsidian.md)（如已装跳过）
2. 打开 Obsidian → 左下角 **设置（齿轮）** → **社区插件** → **浏览**
3. 搜索 `Claudian`（作者 YishenTu）→ **安装** → **启用**
4. Claudian 依赖本机的 Claude Code CLI。若未装，按 Claudian 插件说明页指引安装并登录。

> 💡 Claudian 是「套壳」——它调用你本机已登录的 Claude，不是独立账号，所以无需单独的 API key。

## 步骤二：把 Agent 放进你的 vault

把整个 `interview-doc-agent` 文件夹放进你的 Obsidian vault。两种方式任选：

**方式 A（命令行，推荐）**
```bash
git clone https://github.com/<你的用户名>/interview-doc-agent.git \
  "/path/to/你的Vault/interview-doc-agent"
```

**方式 B（手动）**
下载本仓库 ZIP → 解压 → 把 `interview-doc-agent` 文件夹拖进 vault 文件夹。

完成后，Obsidian 左侧文件树应能看到 `interview-doc-agent/` 及其子文件夹。

## 步骤三：把 SKILL.md 注册给 Claudian

Claudian 从 `<vault>/.claudian/skills/` 读取 skill。我们建一个**软链接**指向仓库里的 SKILL.md，这样仓库自包含、Claudian 也能识别：

```bash
cd "/path/to/你的Vault"
mkdir -p .claudian/skills
ln -s "../../interview-doc-agent/SKILL.md" ".claudian/skills/生成求职文档.md"
```

> 不会用命令行？也可以直接把 `SKILL.md` 复制一份到 `<vault>/.claudian/skills/生成求职文档.md`（缺点：以后改了要手动同步两边）。

重启 Obsidian，在 Claudian 侧边栏输入 `/` 应能看到 `生成求职文档` 这个 skill。

## 步骤四：放入你的模板和经历

1. **简历模板** → 放进 `interview-doc-agent/templates/简历/`
   - 有 LaTeX 模板放 `.tex`，或直接放 Markdown 简历
2. **面试话术模板** → 仓库已自带 `templates/逐字稿/产品面试话术模版.示例.md`，可直接用或替换成你的
3. **项目经历** → 把你的项目记录（任何格式，复制粘贴即可）放进 `materials/`

## 步骤五：开始用

在 Claudian 侧边栏对话：

**整理经历进经历库：**
> 我往 materials/ 放了新项目，帮我整理进经历库

**写简历：**
> 按 templates/简历 的风格，生成一份突出搜索经验的简历

**写逐字稿：**
> 写小红书项目的面试逐字稿，要简单版和复杂版

生成结果会出现在 `output/`，Obsidian 左侧直接打开。

---

## 常见问题

**Q：Claudian 里看不到 skill？**
A：确认 `.claudian/skills/` 下有 `生成求职文档.md`（或软链接），重启 Obsidian。

**Q：必须用 Claudian 吗？**
A：不必。任何能读写 vault 文件的 AI（如 Cursor 打开 vault、Claude Code）都能用——它们读 `SKILL.md` 即可按流程执行。

**Q：我的隐私数据会上传吗？**
A：不会。Agent 只在你本地 vault 里读写文件。只有你主动 git push 才会上传，且 `.gitignore` 已预留忽略个人数据的配置。
