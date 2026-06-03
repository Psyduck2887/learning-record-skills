# Learning Record Skills

一组用于读写个人学习记录的 Agent Skills。

这个仓库包含两个 skill：

- `learning-record-read`：按主题读取学习记录，并加载到当前 Agent 上下文。
- `learning-record-write`：把已经解决的问题追加成一条轻量学习笔记。

这两个 skill 不绑定固定主题、固定目录结构、GitHub 账号或本机路径。真正的主题、别名、笔记文件和读写规则，都由使用者自己的 `learning_record` 仓库定义。

## 仓库结构

```text
skills/
  learning-record-read/
    SKILL.md
  learning-record-write/
    SKILL.md
examples/
  learning_record/
    README.md
    typescript/
      README.md
      notes.md
```

## 安装

把两个 skill 目录复制到你的 Agent runtime 使用的 skill 目录。

常见示例：

```sh
mkdir -p ~/.agents/skills
cp -R skills/learning-record-read ~/.agents/skills/
cp -R skills/learning-record-write ~/.agents/skills/
```

有些 runtime 使用 `~/.codex/skills`、项目内 `.agents/skills`，或其他自定义目录。如果你的 runtime 文档指定了不同位置，就把这两个目录复制到对应位置。

安装后，重新启动一个 Agent 会话，并让它列出或使用 `learning-record-read` 和 `learning-record-write`。skill 名称需要保持小写和连字符格式。

如果你的 runtime 不支持列出已安装 skill，可以用这个 smoke test：

```text
使用 learning-record-read 从示例 learning_record 仓库读取 TypeScript 学习记录。
```

## 配置

设置 `LEARNING_RECORD_REPO`，让 skill 知道你的学习记录仓库在哪里。

示例：

```sh
export LEARNING_RECORD_REPO=/path/to/learning_record
```

如果没有设置这个环境变量，skill 会要求 Agent 先询问用户本地 `learning_record` 仓库路径。

如果想长期生效，可以把这行 `export` 写入 `.zshrc`、`.bashrc` 等 shell 启动文件。注意：有些 Agent runtime 不一定继承交互式 shell 的环境变量，所以需要在启动 Agent 的同一个环境里确认变量是否可见。

如果 Agent 读不到 `LEARNING_RECORD_REPO`，也可以直接在 prompt 里告诉它 `learning_record` 仓库路径。两个 skill 都会在路径缺失时主动询问。

## learning_record 仓库格式

你的 `learning_record` 仓库需要有一个根目录 `README.md`，用于声明支持哪些主题和别名。每个主题目录也需要有自己的 `README.md`，用于声明读取哪些文件、写入哪个文件、笔记格式是什么。

主题规则里的路径默认相对于该主题目录，除非主题 `README.md` 明确说明其他规则。

可以参考 `examples/learning_record/`，它是一个最小可用模板。

根目录 `README.md` 模板：

```md
# Learning Record

## 主题列表

| 主题 | 别名 | 目录 |
|---|---|---|
| TypeScript | TS, typescript | `typescript/` |
```

主题目录 `README.md` 模板：

```md
# 主题名称

## 读取规则

读取这个主题时，加载：

1. `notes.md`

## 写入规则

目标文件：

`notes.md`

说明笔记格式、重复检查规则，以及可选的验证命令。
```

## 推荐流程

1. 创建你自己的 `learning_record` 仓库。
2. 在根目录 `README.md` 里写主题列表和别名。
3. 每个主题建一个目录。
4. 每个主题目录里写一个 `README.md`，声明读写规则。
5. 设置 `LEARNING_RECORD_REPO`。
6. 让 Agent 使用 `learning-record-read` 或 `learning-record-write`。

## 常见问题

- 找不到 skill：确认 runtime 的 skill 目录里存在 `learning-record-read/SKILL.md` 和 `learning-record-write/SKILL.md`。
- 找不到学习记录仓库：在启动 Agent 的环境里设置 `LEARNING_RECORD_REPO`，或直接在 prompt 里提供路径。
- 找不到主题：把主题和别名添加到 `learning_record` 根目录的 `README.md`。
- 写入规则不清楚：在主题 `README.md` 里明确目标笔记文件、笔记格式、重复检查规则和可选验证命令。
- 重复检查结果不稳定：如果你需要更确定的行为，在主题 `README.md` 里定义更严格的重复判断规则。

## 安全说明

- 发布学习记录前，先检查 Agent 生成的内容。
- 不要把密钥、凭证、token 或其他敏感信息写入学习记录。
- 共享模板时不要包含个人机器路径。
- Git commit 和 push 是可选操作。`learning-record-write` 只有在用户明确要求 Git 持久化时才会执行。
