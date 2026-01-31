# Windows 电脑安装 find-skills 完全指南：让 AI Agent 拥有"技能商店"

## 前言

如果你在使用 Claude Code 或其他 AI Agent 工具，你可能听说过 **Skills** 这个概念。Skills 就像是给 AI 安装的"专业技能包"，让它能够更专业地处理特定领域的任务。

而 **find-skills** 就是这个生态系统中的"应用商店搜索功能"——它不是一个具体做事的技能，而是一份"说明书"，教 AI Agent 如何帮你搜索和安装其他技能。

但是，原版的 find-skills 在 Windows 上有严重的兼容性问题。本文将详细介绍如何在 Windows 电脑上正确安装和使用 find-skills。

---

## 什么是 find-skills？

### 核心概念

- **Skills**：给 AI Agent 增加专业能力的模块包
- **find-skills**：Skills 的"应用商店搜索功能"，帮你发现和安装其他 skills

### 它能做什么？

当你安装了 find-skills 后：

1. 你对 AI Agent 说："帮我搜索一个 React 性能优化的 skill"
2. AI Agent 会自动运行搜索命令
3. 展示搜索结果给你
4. 你确认后，AI Agent 帮你安装

全程自然语言交互，不需要手动输入命令。

### 为什么称之为"元 Skill"？

因为它不是帮你做具体事情的技能，而是帮你**找到其他技能**的技能。就像应用商店本身也是一个应用一样。

---

## Windows 兼容性问题

### 原版的两个致命问题

**问题 1：触发不稳定**
- AI 是语义理解的，同样的话有时触发有时不触发
- 解决方法：对话中明确带上"skill"这个词

**问题 2：Windows 上完全不能用**（最致命）
- Claude Code 在 Windows 上使用 Bash 环境运行 `npx skills find` 会返回空白
- 原版 find-skills 在 Windows 的 Claude Code 中基本不可用

### Windows 兼容版本的原理

让 Claude Code 使用 **PowerShell** 来运行 skills 命令，而不是默认的 Bash 环境。

**修复后的命令格式**：
```bash
powershell -Command "npx skills find '[query]'"
powershell -Command "npx skills add [package] -g -y"
powershell -Command "npx skills list -g"
```

---

## 安装步骤（Windows）

### 前置要求

你需要先安装 **Node.js**（它会自动包含 npm 和 npx）。

**检查是否已安装**：
```powershell
node -v
npm -v
```

如果显示版本号，说明已安装，可以跳到下一步。

**如果没安装**：
1. 访问 https://nodejs.org/
2. 下载 LTS 版本（推荐）
3. 安装时保持默认选项即可

### 安装 find-skills（Windows 兼容版本）

#### 方法一：手动安装（推荐）

**步骤 1：创建目录结构**

在 PowerShell 或命令提示符中运行：
```powershell
mkdir -p C:\Users\你的用户名\.agents\skills\find-skills
```

**步骤 2：下载 Windows 兼容版本的 SKILL.md**

访问以下地址，复制完整内容：
```
https://github.com/你的GitHub用户名/find-skills-windows/blob/main/SKILL.md
```

将内容保存到：
```
C:\Users\你的用户名\.agents\skills\find-skills\SKILL.md
```

**步骤 3：重启 Claude Code**

关闭并重新打开 Claude Code，让它读取新安装的 skill。

**步骤 4：验证安装**

对 Claude Code 说：
```
"帮我搜索一个 React 的 skill"
```

如果看到搜索结果，说明安装成功！

#### 方法二：通过 Git 克隆（适合开发者）

```powershell
# 克隆仓库
git clone https://github.com/你的GitHub用户名/find-skills-windows.git

# 复制到 skills 目录
cp -r find-skills-windows C:\Users\你的用户名\.agents\skills\find-skills

# 重启 Claude Code
```

---

## 使用方法

### 触发方式

以下说法更容易触发 find-skills：

✅ **推荐说法**（带"skill"关键词）：
- "帮我搜索一个 React 的 skill"
- "find a skill for testing"
- "找个数据分析的 skill"
- "is there a skill that can help with deployment?"

⚠️ **不太稳定的说法**（可能触发，也可能不触发）：
- "帮我找个做数据分析的工具"
- "有没有什么能帮我做 PPT 的？"

**核心建议**：想稳定触发，对话中明确带上 **"skill"** 这个词。

### 使用流程

1. **你说**："帮我搜索一个 React 性能优化的 skill"
2. **AI Agent 理解**：你要做 React 性能优化
3. **AI Agent 翻译**：将中文需求翻译成英文关键词 "react performance"
4. **AI Agent 执行**：运行 `powershell -Command "npx skills find 'react performance'"`
5. **展示结果**：AI Agent 展示搜索结果给你
6. **确认安装**：你确认后，AI Agent 运行安装命令

全程自然语言交互，无需手动输入命令。

---

## 搜索技巧

### 中文关键词对照表

**搜索只支持英文关键词！** 但你可以用中文和 AI Agent 对话，它会自动翻译。

| 中文需求 | 英文关键词 | 推荐 Skill |
|---------|-----------|-----------|
| 数据分析 | data analysis | exploratory-data-analysis |
| 做 PPT | ppt, presentation | pptx |
| 写文章 | writing | writing-skills |
| 代码审查 | code review | code-reviewer |
| 部署上线 | deploy, deployment | vercel-deployment |
| 写测试 | testing | webapp-testing |
| 做视频 | video, remotion | remotion-best-practices |
| React 开发 | react | vercel-react-best-practices |
| Python 开发 | python | python-testing-patterns |
| 前端设计 | frontend, design | frontend-design |
| A 股分析 | stock market analysis | a-share-analysis |

### 搜索技巧

1. **使用具体关键词**
   - ✅ "react testing" 比 "testing" 效果好
   - ✅ "nextjs performance" 比 "performance" 效果好

2. **尝试同义词**
   - 如果 "deploy" 没找到，试试 "deployment"
   - 如果 "docs" 没找到，试试 "documentation"

3. **检查热门来源**
   - 很多优质 skills 来自 `vercel-labs/agent-skills`
   - 也可以关注 `ComposioHQ/awesome-claude-skills`

4. **组合关键词**
   - "react performance optimization"
   - "python data analysis"
   - "nextjs deployment vercel"

---

## 常用命令

### 在 AI Agent 中使用（推荐）

直接用自然语言和 AI Agent 对话：

```
"帮我搜索一个 React 的 skill"
"find a skill for testing"
"找个数据分析的 skill"
```

AI Agent 会自动执行相应的命令。

### 手动运行（在 PowerShell 中）

如果你想手动运行命令：

```powershell
# 搜索 skill
npx skills find "react"

# 查看已安装的全局 skills
npx skills list -g

# 查看当前项目的 skills
npx skills list

# 安装某个 skill（全局）
npx skills add <owner/repo@skill> -g -y

# 安装某个 skill（项目级别）
npx skills add <owner/repo@skill> -y

# 检查更新
npx skills check

# 更新所有 skills
npx skills update

# 卸载 skill
npx skills remove <skill名称> -g
```

### 参数说明

- `-g`：全局安装（用户级别），在任何项目中都可用
- `-y`：跳过确认提示，自动安装
- 不加 `-g`：项目级别安装，只在当前项目中可用

---

## 常见 Skill 分类

### Web 开发
- **react**：React 开发最佳实践
- **nextjs**：Next.js 开发指南
- **typescript**：TypeScript 使用技巧
- **css**：CSS 样式技巧
- **tailwind**：Tailwind CSS 使用

### 测试
- **testing**：通用测试指南
- **jest**：Jest 测试框架
- **playwright**：Playwright 浏览器测试
- **e2e**：端到端测试

### DevOps
- **deploy**：部署指南
- **docker**：Docker 容器化
- **kubernetes**：K8s 编排
- **ci-cd**：持续集成/部署

### 文档
- **docs**：文档编写
- **readme**：README 编写
- **changelog**：变更日志
- **api-docs**：API 文档

### 代码质量
- **review**：代码审查
- **lint**：代码检查
- **refactor**：重构指南
- **best-practices**：最佳实践

### 设计
- **ui**：UI 设计
- **ux**：用户体验
- **design-system**：设计系统
- **accessibility**：无障碍设计

---

## 常见问题

### Q1：我说"帮我找个工具"，AI 没有调用 find-skills？

**原因**：AI 是语义理解的，"找工具"这种说法有时候会触发，有时候不会。

**解决方法**：想稳定触发，建议话里带上 **"skill"** 这个词。

✅ "帮我搜索一个数据分析的 **skill**" → 更容易触发 find-skills

### Q2：Windows 上 Claude Code 搜索没有输出？

**原因**：原版 find-skills 使用 Bash 环境，在 Windows 上不兼容。

**解决方法**：使用本文介绍的 Windows 兼容版本，或者手动在 PowerShell 里运行：
```powershell
npx skills find "data analysis"
```

### Q3：怎么验证安装成功？

**方法 1**：对 AI Agent 说"帮我搜索一个 React 的 skill"，看是否有搜索结果。

**方法 2**：检查文件是否存在：
```powershell
ls C:\Users\你的用户名\.agents\skills\find-skills\SKILL.md
```

### Q4：Skill 和 MCP 有什么区别？

- **Skill**：知识和指南，教 AI **怎么做事**（比如 React 最佳实践）
- **MCP**：工具和能力，让 AI **能够做新的事**（比如读取文件、调用 API）

简单说：
- Skill 是"知道怎么做"（知识层面）
- MCP 是"能够做"（能力层面）

### Q5：怎么卸载或更新 skill？

```powershell
# 卸载
npx skills remove [skill名称] -g

# 更新所有 skills
npx skills update

# 检查更新
npx skills check
```

### Q6：全局安装和项目安装有什么区别？

**全局安装**（`-g`）：
- 安装在 `C:\Users\你的用户名\.agents\skills\`
- 在任何项目中都可用
- 适合通用的 skills（如 find-skills、code-reviewer）

**项目安装**（不加 `-g`）：
- 安装在当前项目的 `.agents/skills/` 目录
- 只在当前项目中可用
- 适合项目特定的 skills

### Q7：如何查看某个 skill 的详细信息？

访问 https://skills.sh/ 并搜索 skill 名称，或者直接访问：
```
https://skills.sh/<owner>/<repo>/<skill-name>
```

例如：
```
https://skills.sh/vercel-labs/skills/find-skills
```

---

## 使用建议

### 1. 优先安装通用 Skills

推荐全局安装以下 skills：

```powershell
# find-skills（必装）
npx skills add vercel-labs/skills@find-skills -g -y

# 代码审查
npx skills add vercel-labs/agent-skills@code-reviewer -g -y

# React 最佳实践（如果你做前端）
npx skills add vercel-labs/agent-skills@vercel-react-best-practices -g -y

# 测试指南
npx skills add vercel-labs/agent-skills@webapp-testing -g -y
```

### 2. 项目特定的 Skills 用项目安装

如果某个 skill 只在特定项目中使用，用项目级别安装：

```powershell
# 在项目目录下运行（不加 -g）
npx skills add <owner/repo@skill> -y
```

### 3. 定期更新 Skills

Skills 会不断更新和改进，建议定期检查更新：

```powershell
# 检查更新
npx skills check

# 更新所有 skills
npx skills update
```

### 4. 浏览 Skills 生态

访问 https://skills.sh/ 浏览所有可用的 skills，发现更多有用的工具。

### 5. 创建自己的 Skills

如果你有经常重复的工作流程，可以创建自己的 skill：

```powershell
npx skills init my-custom-skill
```

---

## 总结

find-skills 是一个非常实用的"元 Skill"，它让 AI Agent 能够自主搜索和安装其他技能。

**核心要点**：

1. **Windows 兼容性问题**：原版在 Windows 上不可用，需要使用兼容版本
2. **安装简单**：创建目录 → 下载 SKILL.md → 重启 Claude Code
3. **触发技巧**：对话中带上"skill"关键词更容易触发
4. **搜索技巧**：使用具体的英文关键词，尝试同义词
5. **全局安装**：在任何项目中都可用

**参考资源**：

- find-skills 官方：https://skills.sh/vercel-labs/skills/find-skills
- Windows 兼容版本：https://github.com/你的GitHub用户名/find-skills-windows
- Skills CLI 文档：https://skills.sh/docs
- Skills 生态浏览：https://skills.sh/

---

## 附录：完整的 Windows 兼容版 SKILL.md

如果你想手动创建 SKILL.md 文件，以下是完整内容：

```markdown
# Find Skills (Windows Compatible Version)

This skill helps discover and install skills from the open agent skills ecosystem. It's a Windows-compatible fork that fixes empty output issues in Claude Code on Windows.

## Critical Windows Compatibility

On Windows, you **must use PowerShell** to run skills commands. The default Bash/Git Bash environment doesn't work with `npx skills` and returns empty output.

**Required Windows format:**
```bash
powershell -Command "npx skills find '[query]'"
powershell -Command "npx skills add [package] -g -y"
powershell -Command "npx skills list -g"
```

## When to Use

Use when users:
- Ask "how do I do X" for common tasks
- Request "find a skill for X"
- Ask about specialized capabilities
- Want to extend agent functionality
- Search for tools, templates, or workflows

## Skills CLI Overview

The Skills CLI (`npx skills`) is the package manager for the open agent skills ecosystem.

**Key commands (Windows):**
- Find: `powershell -Command "npx skills find '[query]'"`
- Install: `powershell -Command "npx skills add [package] -g -y"`
- List: `powershell -Command "npx skills list -g"`
- Check updates: `powershell -Command "npx skills check"`
- Update: `powershell -Command "npx skills update"`

Browse at: https://skills.sh/

## Usage Workflow

**Step 1:** Identify the domain and specific task

**Step 2:** Search using relevant queries (Windows format required)

**Step 3:** Present options with skill name, install command, and skills.sh link

**Step 4:** Offer to install if user agrees

## Common Categories

- Web Development: react, nextjs, typescript, css, tailwind
- Testing: testing, jest, playwright, e2e
- DevOps: deploy, docker, kubernetes, ci-cd
- Documentation: docs, readme, changelog, api-docs
- Code Quality: review, lint, refactor, best-practices
- Design: ui, ux, design-system, accessibility

## Chinese to English Keywords

**Search only supports English!**

- 数据分析 → data analysis
- 做PPT → ppt, presentation
- 写文章 → writing
- 代码审查 → code review
- 部署上线 → deploy, deployment
- 写测试 → testing
- 做视频 → video, remotion
- React开发 → react
- Python开发 → python
- 前端设计 → frontend, design

## Search Tips

1. Use specific keywords
2. Try alternative terms
3. Check popular sources (vercel-labs, ComposioHQ)
4. Always use English keywords

## When No Skills Found

Acknowledge the gap, offer direct help, and suggest creating custom skills with `npx skills init`.

---

**Original:** https://github.com/vercel-labs/skills
**Windows fix:** https://github.com/你的GitHub用户名/find-skills-windows
```

将以上内容保存为 `SKILL.md`，放在 `C:\Users\你的用户名\.agents\skills\find-skills\` 目录下即可。

---

**作者**：[你的名字]
**日期**：2026-01-31
**版本**：1.0

如有问题或建议，欢迎在 GitHub 上提 Issue 或 PR！
