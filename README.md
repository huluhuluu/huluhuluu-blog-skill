# Huluhuluu Blog Style

这个目录是一个面向 Codex 的本地 skill，用来约束 AI 生成更接近当前博客既有风格的文章。

核心文件：

- `SKILL.md`：技能主体，定义适用场景、写作规则、结构模板和示例
- `references/style-profile.md`：从当前非 draft 博客中提炼出的稳定风格画像
- `agents/openai.yaml`：给支持 skill UI 的工具提供展示名称和默认提示

它的目标是让 AI 生成更接近当前博客已有文章风格的内容，尤其适用于：

- 工具配置 / 命令备忘
- 环境搭建 / 工程记录
- 系列首页
- 论文阅读笔记
- 源码解析

## 安装到 Codex

Codex 会自动从本地 skills 目录发现 skill。最直接的做法是把这个 skill 复制到 `~/.codex/skills`。

### Windows PowerShell

```powershell
$dst = "$HOME\\.codex\\skills\\huluhuluu-blog-style"
New-Item -ItemType Directory -Force -Path "$HOME\\.codex\\skills" | Out-Null
Copy-Item -Recurse -Force ".\\huluhuluu-blog-style" $dst
```

### Linux / macOS

```bash
mkdir -p ~/.codex/skills
cp -r ./huluhuluu-blog-style ~/.codex/skills/
```

如果你希望 skill 内容始终跟当前仓库同步，也可以用符号链接代替复制。

### 在 Codex 中使用

启动 `codex` 后，可以直接显式调用：

```text
Use $huluhuluu-blog-style to draft a new post about ...
```

如果界面支持 `/skills`，也可以在那里查看是否已经被发现。

## 导入到 cc-switch 并应用到 Codex

如果你已经用 `cc-switch` 管理 Codex skill，可以按下面步骤导入。

### 1. 先把 skill 放到 Codex 可扫描的位置

推荐先完成上一节，把 skill 放到 `~/.codex/skills`。

### 2. 扫描未管理 skill

```bash
cc-switch skills scan-unmanaged --app codex
```

如果扫描正常，应该能看到类似 `huluhuluu-blog-style` 的条目。

### 3. 导入到 cc-switch

```bash
cc-switch skills import-from-apps huluhuluu-blog-style
```

### 4. 为 Codex 启用

```bash
cc-switch skills enable huluhuluu-blog-style --app codex
```

### 5. 查看状态

```bash
cc-switch skills list
```

如果启用成功，`Codex` 一列应该会显示启用状态。

## 推荐用法

### 新文章

```text
Use $huluhuluu-blog-style to write a tools note about xxx.
```

### 重写草稿

```text
Use $huluhuluu-blog-style to rewrite this draft so it matches the existing blog tone and structure.
```

### 系列首页

```text
Use $huluhuluu-blog-style to create an index page for this tutorial series with overview tables and TODO status.
```

## 注意

- 这个 skill 只约束写作风格，不替代事实核查。
- 如果文章涉及最新工具版本、产品行为、论文结论或命令兼容性，仍然需要单独核实。
- 这个 skill 更偏“工程记录风格”，不是通用营销文案或平台教程风格。
