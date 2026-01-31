# Find Skills - Windows Compatible Version

> Windows 兼容版本的 find-skills，修复了原版在 Windows 上无法使用的问题。

## 问题背景

原版 [find-skills](https://github.com/vercel-labs/skills) 在 Windows 的 Claude Code 中使用时，由于 Bash 环境兼容性问题，`npx skills find` 命令会返回空白输出，导致功能完全不可用。

## 解决方案

本项目通过修改 `SKILL.md`，让 Claude Code 在 Windows 上使用 **PowerShell** 来运行 skills 命令，而不是默认的 Bash 环境。

**修复后的命令格式**：
```bash
powershell -Command "npx skills find '[query]'"
powershell -Command "npx skills add [package] -g -y"
powershell -Command "npx skills list -g"
```

## 快速安装

### 前置要求

- 已安装 Node.js（包含 npm 和 npx）
- 使用 Claude Code 或其他支持 Skills 的 AI Agent

### 安装步骤

**方法一：标准安装流程（推荐）**

这是最完整、最标准的安装方式，结合了原版的包结构和 Windows 兼容性修复。

1. 安装原版 find-skills：
```powershell
npx skills add vercel-labs/skills@find-skills -g -y
```

2. 下载 [SKILL.md](./SKILL.md) 文件，**覆盖保存**到：
```
C:\Users\你的用户名\.agents\skills\find-skills\SKILL.md
```

3. 重启 Claude Code

4. 验证安装：
```
对 Claude Code 说："帮我搜索一个 React 的 skill"
```

如果看到搜索结果（类似下面的输出），说明安装成功：
```
Install with npx skills add <owner/repo@skill>

vercel-labs/agent-skills@vercel-react-best-practices
└ https://skills.sh/vercel-labs/agent-skills/vercel-react-best-practices
```

**为什么要这样做？**
- 步骤 1 安装原版，创建完整的包结构
- 步骤 2 替换 SKILL.md，修复 Windows 兼容性问题（原版用 Bash，Windows 兼容版用 PowerShell）

**方法二：纯手动安装（简化版）**

如果步骤 1 的 `npx skills add` 命令无法正常工作，可以使用这个简化方法：

1. 创建目录：
```powershell
mkdir C:\Users\你的用户名\.agents\skills\find-skills
```

2. 下载 [SKILL.md](./SKILL.md) 文件，保存到：
```
C:\Users\你的用户名\.agents\skills\find-skills\SKILL.md
```

3. 重启 Claude Code

4. 验证安装：
```
对 Claude Code 说："帮我搜索一个 React 的 skill"
```

**注意**：这个方法虽然简单，但缺少完整的包结构，`npx skills list -g` 可能无法识别。不过对 Claude Code 来说完全可用。

**方法三：通过 Git 克隆（适合开发者）**

```powershell
# 克隆仓库
git clone https://github.com/spsz831/find-skills-windows.git

# 复制到 skills 目录
cp -r find-skills-windows C:\Users\你的用户名\.agents\skills\find-skills

# 重启 Claude Code
```

## 使用方法

### 触发建议

对话中明确带上 **"skill"** 关键词，更容易触发：

✅ **推荐说法**：
- "帮我搜索一个 React 的 skill"
- "find a skill for testing"
- "找个数据分析的 skill"

### 中文关键词对照

| 中文需求 | 英文关键词 |
|---------|-----------|
| 数据分析 | data analysis |
| 做 PPT | ppt, presentation |
| 写文章 | writing |
| 代码审查 | code review |
| 部署上线 | deploy, deployment |
| 写测试 | testing |
| React 开发 | react |
| Python 开发 | python |

### 常用命令

```powershell
# 搜索 skill
npx skills find "react"

# 查看已安装的 skills
npx skills list -g

# 安装 skill
npx skills add <owner/repo@skill> -g -y

# 更新 skills
npx skills update

# 卸载 skill
npx skills remove <skill名称> -g
```

## 与原版的区别

| 项目 | 原版 | Windows 兼容版 |
|-----|------|---------------|
| 命令格式 | `npx skills find` | `powershell -Command "npx skills find"` |
| Windows 兼容性 | ❌ 不可用 | ✅ 完全可用 |
| 其他平台 | ✅ 可用 | ✅ 可用 |

## 常见问题

### Q：为什么原版在 Windows 上不能用？

Claude Code 在 Windows 上使用 Git Bash 环境运行命令，但 `npx skills` 在 Bash 环境中会返回空白输出。通过使用 PowerShell 运行命令可以解决这个问题。

### Q：这个版本在 Mac/Linux 上能用吗？

可以。PowerShell 命令在 Mac/Linux 上也能正常工作（如果安装了 PowerShell）。但在这些平台上，原版已经可以正常使用，不需要这个修复版本。

### Q：如何验证安装成功？

对 Claude Code 说："帮我搜索一个 React 的 skill"，如果看到搜索结果，说明安装成功。

### Q：Skill 和 MCP 有什么区别？

- **Skill**：知识和指南，教 AI 怎么做事（比如 React 最佳实践）
- **MCP**：工具和能力，让 AI 能做新的事（比如读取文件、调用 API）

## 参考资源

- 原版项目：https://github.com/vercel-labs/skills
- Skills 生态：https://skills.sh/
- 官方文档：https://skills.sh/docs
- 详细安装指南：[查看完整教程](./docs/installation-guide.md)

## 贡献

欢迎提交 Issue 和 Pull Request！

如果你发现任何问题或有改进建议，请：
1. 提交 Issue 描述问题
2. Fork 项目并创建新分支
3. 提交 Pull Request

## 许可证

MIT License

## 致谢

- 感谢 [Vercel Labs](https://github.com/vercel-labs) 创建了 Skills 生态系统
- 感谢 [@KimYx0207](https://github.com/KimYx0207) 的 Windows 兼容性探索

---

**作者**：[@spsz831](https://github.com/spsz831)
**日期**：2026-01-31
**版本**：1.0.0
