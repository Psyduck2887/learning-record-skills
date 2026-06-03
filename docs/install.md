# 安装说明

本文说明如何安装 `learning-record-read` 和 `learning-record-write`。

## 复制 skill

把两个 skill 目录复制到你的 Agent 工具读取 skill 的位置。

常见示例：

```sh
mkdir -p ~/.agents/skills
cp -R skills/learning-record-read ~/.agents/skills/
cp -R skills/learning-record-write ~/.agents/skills/
```

有些 Agent 工具使用 `~/.codex/skills`、项目内 `.agents/skills`，或其他自定义目录。如果你的工具文档指定了不同位置，就把这两个目录复制到对应位置。

## 验证安装

安装后，重新启动一个 Agent 会话，并让它列出或使用 `learning-record-read` 和 `learning-record-write`。skill 名称需要保持小写和连字符格式。

如果你的 Agent 工具不支持列出已安装 skill，可以用下面的验证提示词。把 `/path/to/this/repo` 换成当前仓库所在路径：

```text
使用 learning-record-read，从 /path/to/this/repo/templates/learning_record 读取 TypeScript 学习记录。
```

## 配置学习记录仓库

设置 `LEARNING_RECORD_REPO`，让 skill 知道你的学习记录仓库在哪里。

示例：

```sh
export LEARNING_RECORD_REPO=/path/to/learning_record
```

如果没有设置这个环境变量，skill 会要求 Agent 先询问用户本地 `learning_record` 仓库路径。

如果想长期生效，可以把这行 `export` 写入 `.zshrc`、`.bashrc` 等 shell 启动文件。注意：有些 Agent 工具不一定继承交互式 shell 的环境变量，所以需要在启动 Agent 的同一个环境里确认变量是否可见。

如果 Agent 读不到 `LEARNING_RECORD_REPO`，也可以直接在 prompt 里告诉它 `learning_record` 仓库路径。两个 skill 都会在路径缺失时主动询问。
