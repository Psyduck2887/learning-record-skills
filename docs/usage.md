# 使用说明

本文说明如何创建自己的 `learning_record` 仓库，并使用两个 skill 读取和写入学习记录。

## 创建学习记录仓库

可以直接复制模板：

```sh
cp -R templates/learning_record /path/to/my_learning_record
export LEARNING_RECORD_REPO=/path/to/my_learning_record
```

模板结构：

```text
learning_record/
  README.md
  typescript/
    README.md
    notes.md
```

## learning_record 仓库格式

根目录 `README.md` 用于声明支持哪些主题和别名：

```md
# Learning Record

## 主题列表

| 主题 | 别名 | 目录 |
|---|---|---|
| TypeScript | TS, typescript | `typescript/` |
```

每个主题目录也需要有自己的 `README.md`，用于声明读取哪些文件、写入哪个文件、笔记格式是什么：

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

主题规则里的路径默认相对于该主题目录，除非主题 `README.md` 明确说明其他规则。

## 读取记录

```text
使用 learning-record-read 读取 TypeScript 学习记录。
```

如果没有设置 `LEARNING_RECORD_REPO`，也可以直接提供路径：

```text
使用 learning-record-read，从 /path/to/my_learning_record 读取 TypeScript 学习记录。
```

## 写入记录

解决一个问题后，可以让 Agent 写入记录：

```text
使用 learning-record-write，把刚才解决的 TypeScript 问题记录到学习记录里。不要提交 Git。
```

默认不会 commit 或 push。只有用户明确要求 Git 持久化时，`learning-record-write` 才会执行 Git 操作。

## 常见问题

- 找不到 skill：确认 Agent 工具的 skill 目录里存在 `learning-record-read/SKILL.md` 和 `learning-record-write/SKILL.md`。
- 找不到学习记录仓库：在启动 Agent 的环境里设置 `LEARNING_RECORD_REPO`，或直接在 prompt 里提供路径。
- 找不到主题：把主题和别名添加到 `learning_record` 根目录的 `README.md`。
- 写入规则不清楚：在主题 `README.md` 里明确目标笔记文件、笔记格式、重复检查规则和可选验证命令。
- 重复检查结果不稳定：如果你需要更确定的行为，在主题 `README.md` 里定义更严格的重复判断规则。
