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
- A股分析 → stock market analysis

## Search Tips

1. Use specific keywords
2. Try alternative terms
3. Check popular sources (vercel-labs, ComposioHQ)
4. Always use English keywords

## When No Skills Found

Acknowledge the gap, offer direct help, and suggest creating custom skills with `npx skills init`.

---

**Original:** https://github.com/vercel-labs/skills
**Windows fix:** https://github.com/spsz831/find-skills-windows
