# Huluhuluu Blog Style

一个面向 `Codex` 的本地写作 skill，用来约束 AI 生成更接近 **huluhuluu 个人博客**既有风格的文章。

这套 skill 是从当前博客中已经发布的非 `draft` 文章里抽出来的一套稳定写法，目标是让新文章在语气、结构、细节粒度和格式上自然融入现有仓库。

## 1. 风格特点

这套 skill 重点保留的是当前博客里已经比较稳定的写作习惯：

- 中文为主，保留必要英文术语
- 风格偏工程记录，不写空泛铺垫
- 强调“真实问题 -> 可执行方案 -> 够用解释”
- 大量使用表格、命令块、步骤拆分
- 常用 `## 1.`、`### 1.1` 这类层级
- 命令、路径、类名、配置项统一用行内代码或代码块表示
- 遇到未完成内容会明确标记 `TODO` / `WIP`

更完整的风格归纳见：

- [SKILL.md](./SKILL.md)
- [references/style-profile.md](./references/style-profile.md)

## 2. 目录结构

```text
huluhuluu-blog-style/
├── README.md
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    └── style-profile.md
```

其中：

- `SKILL.md`：技能主体，定义适用任务、写作规则、结构模板和示例
- `references/style-profile.md`：从当前非 `draft` 博客中提炼的稳定风格画像
- `agents/openai.yaml`：提供 skill 的展示名称、简介和默认提示

## 3. 安装配置

### 3.1 Codex 安装

#### 3.1.1 克隆仓库

先把仓库克隆到本地工作目录：

```bash
# clone repo
git clone https://github.com/huluhuluu/huluhuluu-blog-skill.git

# enter repo
cd huluhuluu-blog-skill
```

#### 3.1.2 Windows PowerShell

把 `huluhuluu-blog-style/` 放到 `Codex` 的 skills 目录：

```powershell
# create codex skill dir
New-Item -ItemType Directory -Force -Path "$HOME\\.codex\\skills" | Out-Null

# copy skill into codex skills
Copy-Item -Recurse -Force ".\\huluhuluu-blog-style" "$HOME\\.codex\\skills\\huluhuluu-blog-style"
```

#### 3.1.3 Linux / macOS

```bash
# create codex skill dir
mkdir -p ~/.codex/skills

# copy skill into codex skills
cp -r ./huluhuluu-blog-style ~/.codex/skills/
```

使用软链接可以让 skill 后续和仓库内容保持同步，做法如下：

```bash
# create codex skill dir
mkdir -p ~/.codex/skills

# replace copied directory with symlink
ln -sfn "$(pwd)/huluhuluu-blog-style" ~/.codex/skills/huluhuluu-blog-style
```

#### 3.1.4 验证

`/skills` 不是 PowerShell 命令，不能在 `codex` 外部直接执行。

直接用显式调用验证：

1. 启动 `codex`
2. 在 `codex` 交互界面里输入：

```text
Use $huluhuluu-blog-style to draft a new post about tmux.
```

也可以在 PowerShell 里直接执行：

```powershell
codex exec 'Use $huluhuluu-blog-style to draft a new post about tmux.'
```

这里使用单引号，避免 PowerShell 把 `$huluhuluu-blog-style` 当成变量展开。

### 3.2 cc-switch 导入

`cc-switch` 导入基于 3.1 已经完成的本地仓库和 `Codex` skills 目录。先克隆仓库，再安装到 `~/.codex/skills`，再执行下面命令。

#### 3.2.1 扫描未管理 skill

```bash
# scan unmanaged skills from codex
cc-switch skills scan-unmanaged --app codex
```

扫描结果里会出现 `huluhuluu-blog-style`。

#### 3.2.2 导入到 cc-switch

```bash
# import skill into cc-switch ssot
cc-switch skills import-from-apps huluhuluu-blog-style
```

#### 3.2.3 为 Codex 启用

```bash
# enable skill for codex
cc-switch skills enable huluhuluu-blog-style --app codex
```

#### 3.2.4 查看状态

```bash
# verify skill status
cc-switch skills list
```

启用完成后，`Codex` 一列会显示启用状态。

## 4. 推荐用法

### 4.1 新文章

```text
Use $huluhuluu-blog-style to write a tools note about xxx.
```

### 4.2 重写草稿

```text
Use $huluhuluu-blog-style to rewrite this draft so it matches the existing blog tone and structure.
```

### 4.3 系列首页

```text
Use $huluhuluu-blog-style to create an index page for this tutorial series with overview tables and TODO status.
```

## 5. 注意

- 这个 skill 只约束写作风格，不替代事实核查。
- 如果文章涉及最新工具版本、产品行为、论文结论或命令兼容性，仍然需要单独核实。
- 这套风格更偏“工程记录 + 技术笔记”，不适合直接拿去写营销稿或平台教程文案。
