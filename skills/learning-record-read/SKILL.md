---
name: learning-record-read
description: 从用户配置的 learning_record 仓库中读取指定主题的学习记录，并加载到当前 Agent 上下文。
---

# Learning Record Read

用于把指定主题的历史学习记录读取到当前 Agent 上下文。这个 skill 只负责读取文件，不负责总结、分析、编辑或写入。

## 仓库路径

优先使用 `LEARNING_RECORD_REPO` 指向的仓库路径。

如果没有设置 `LEARNING_RECORD_REPO`，先询问用户本地 `learning_record` 仓库路径，再继续执行。

不要假设默认本机路径、GitHub 账号或仓库位置。

## 工作流程

1. 如果用户没有指定主题，先询问要读取哪个主题。
2. 从 `LEARNING_RECORD_REPO` 或用户提供的路径中确定学习记录仓库位置。
3. 读取仓库根目录 `README.md`。
4. 根据根目录 `README.md`，把用户请求的主题或别名映射到主题目录。
5. 读取主题目录下的 `README.md`。
6. 严格按照主题 `README.md` 的规则，决定需要加载哪些笔记文件。
7. 加载完成后，只输出简短确认语。

## 主题规则

主题名称、别名、笔记文件名和读取顺序都由用户自己的 `learning_record` 仓库定义。不要在这个 skill 里硬编码具体主题。

如果根目录 `README.md` 没有定义用户请求的主题，说明该仓库当前没有这个主题。不要猜测其他路径。

## 输出规则

成功读取主题后，输出简短确认语，例如：

```text
已读取请求的学习记录。
```

如果主题 `README.md` 定义了精确确认语，优先使用主题 `README.md` 里的确认语。
