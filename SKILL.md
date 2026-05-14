---
name: huluhuluu-blog-style
description: Write Chinese-first technical blog posts in huluhuluu's personal blog style. Use when drafting or rewriting Hugo blog content under this repo, especially for tool notes, environment setup guides, tutorial series index pages, paper reading notes, source code analysis, and engineering record posts that should match the existing `content/post` writing style.
---

# Huluhuluu Blog Style

Use this skill when writing a new blog post, rewriting an existing draft, or generating a series index page that should read like it naturally belongs in this repository.

Read [references/style-profile.md](references/style-profile.md) first if the requested article type is unclear or if you need a quick reminder of the stable style traits.

## Core goals

- Write in Chinese, keep necessary English technical terms.
- Preserve an engineering-record tone: practical, direct, reproducible.
- Optimize for "real problem -> executable solution -> enough explanation".
- Match the repository's existing structure and formatting habits instead of generic tutorial prose.

## Default writing rules

- Start from the concrete problem or task, not abstract industry background.
- Prefer short paragraphs plus clear section headings.
- Use `## 1.` and `### 1.1` style headings when the content is procedural or layered.
- Write commands, paths, env vars, config keys, class names, function names, model names, and file names in inline code.
- Use fenced code blocks for commands or config snippets that the reader may copy directly.
- Add one or two lines of explanation around commands when the intent is not obvious.
- Mention platform and environment details when they matter: Windows, Ubuntu, Android, device model, SoC, toolchain, shell, package manager, or runtime.
- Surface caveats explicitly when there are path differences, API quirks, permissions, or version-sensitive behavior.
- Do not pad the article with motivational talk, marketing language, or generic claims.

## Format conventions

### Front matter

Follow the repository's common front matter shape:

```yaml
---
title: "文章标题"
date: 2026-01-01T12:00:00+08:00
lastmod: 2026-01-01T12:00:00+08:00
draft: true
description: "一句话描述文章解决什么问题"
slug: "article-slug"
tags: ["tag1", "tag2"]
categories: ["category"]

comments: true
math: true
---
```

Use `build.list: never` for series index pages when they are intended as landing pages instead of normal list entries.

### Heading style

- Procedural content: `## 1. xxx` -> `### 1.1 xxx`
- Series index pages: overview first, then section-by-section tables
- Notes or cheat sheets: group by topic, commands, or workflow stage

### Table style

Use tables when summarizing:

- `文章 | 说明 | 状态`
- `阶段 | 内容 | 文章数`
- `命令 | 说明`
- `类型 | 内容 | 文章数`

Status labels should stay simple and recognizable:

- `✅ 完成`
- `🚧 TODO`
- `🚧 进行中`
- `📝 TODO`
- `✅ 持续更新`

### Command block style

- Put runnable commands in fenced blocks with the right language tag: `bash`, `powershell`, `pwsh`, `toml`, `yaml`.
- Keep placeholder values obvious, such as `<ip>` or `Qwen/Qwen3-8B`.
- If a command is dangerous or environment-specific, explain it right above or below the block.

## Structure templates

### Tool note / config memo

Use this pattern for shell tools, CLI tools, IDE setup, agent tools, package managers, and environment config:

1. Briefly state what the tool is and why it is useful.
2. `## 1. 安装`
3. `## 2. 配置`
4. `## 3. 使用`
5. `## 4. 常见命令` or `## 4. 其它补充`
6. Add references or links only if they help the reader continue.

### Engineering tutorial / setup record

Use this pattern for platform setup, cross-compilation, remote debugging, deployment, or end-to-end workflows:

1. Explain the concrete scenario and environment.
2. Add prerequisite knowledge only when it helps the reader follow later steps.
3. Split the workflow into numbered sections.
4. Keep the commands copyable.
5. Explain the validation signal after major steps.
6. Mention pitfalls, version constraints, or path differences.

### Series index page

Use this pattern for repository landing pages or topic overview pages:

1. One paragraph stating the series scope.
2. Optional line marking current status such as `TODO` or `已完成`.
3. Add a total overview table.
4. Split the series into sections.
5. For each section, use a table with `文章 | 说明 | 状态`.
6. Add related links if the repository or upstream project matters.

### Paper reading note

Use this pattern for paper summaries:

1. State the line of research and what problem the paper tries to solve.
2. Explain the key mechanism or design choice.
3. Use figures, structures, or comparisons when needed.
4. Focus on the technical path, not citation filler.
5. End with your own judgment only when it is concrete and defensible.

### Source code analysis

Use this pattern for framework internals or model code reading:

1. Anchor the article to a specific model, module, file, or code path.
2. Start from the role of the module in the full system.
3. Walk through key classes, functions, or execution flow.
4. Explain why the implementation is organized that way.
5. Use filenames, class names, and APIs in inline code.
6. Add diagrams or TODO comments when the article is still incomplete.

## Do

- Write as if you are leaving a reliable technical note for your future self.
- Keep explanations grounded in actual commands, files, runtime behavior, or code paths.
- Reuse terms consistently across the whole article.
- Prefer repository-local terminology when the repo already established one.
- Keep examples close to the current article topic instead of switching domains.
- Mark unfinished parts honestly with `TODO` or `WIP`.

## Don't

- Do not write as a generic content platform tutorial.
- Do not add persuasive filler, slogans, or “best practice” platitudes without evidence.
- Do not replace technical nouns with over-simplified wording when the precise term matters.
- Do not produce huge theory-first introductions before the practical path starts.
- Do not make every article look academically formal; this blog is closer to structured engineering notes.
- Do not overuse bold text or decorative formatting.

## Example snippets

### Example 1: practical opening

```markdown
# ttyd 使用备忘

临时使用手机连接服务器上的 Codex，会碰到两个问题：

- 远程桌面在手机上比例差不顺手
- 纯 SSH 连接使用 `tmux` 退出的前置键位等操作不顺手

可以使用下面方案：

`tmux + ttyd + Tailscale`
```

### Example 2: tool section

```markdown
## 1. 安装

~~~bash
sudo apt install -y tmux
tmux -V
~~~

如果只是临时使用，装完先确认版本号正常输出，再继续后面的配置。
```

### Example 3: series table

```markdown
## 2. 核心概念

| 文章 | 说明 | 状态 |
|------|------|------|
| [Backend 介绍](/p/introduce-backend/) | CPU/OpenCL/Vulkan 等后端的作用和选择 | ✅ 完成 |
| [工厂模式介绍](/p/introduce-factory/) | MNN 中工厂模式的设计与应用 | 📝 TODO |
```

### Example 4: source-code framing

```markdown
本文以 `Qwen3` 模型代码为例，梳理 HuggingFace `Transformers` 中一个 `CausalLM` 模型从 `config` 到完整模型的构建流程。代码基于 `transformers/models/qwen3/modeling_qwen3.py`。
```

## Workflow

When using this skill:

1. Identify the article type first: tool note, setup guide, series page, paper note, source code note, or summary.
2. Pick the matching structure template from this skill.
3. Draft the front matter and heading skeleton before filling in details.
4. Ensure commands, paths, and code identifiers are formatted in inline code or code blocks.
5. Add only the background needed to understand the concrete workflow.
6. Before finalizing, scan for generic filler and delete it.
