---
name: learning-record-read
description: 当用户要求读取某个主题的学习记录、历史笔记或踩坑记录时使用；从用户配置的 learning_record 仓库加载对应主题内容。
---

# Learning Record Read

只负责读取学习记录，不总结、不分析、不写入。

## 路径解析

1. 优先使用 `LEARNING_RECORD_REPO`。
2. 如果没有设置 `LEARNING_RECORD_REPO`，询问用户本地 `learning_record` 仓库路径。
3. 不要假设默认本机路径、GitHub 账号或仓库位置。

## 执行流程

1. 如果用户没有指定主题，询问要读取哪个主题。
2. 读取 `learning_record` 根目录 `README.md`。
3. 根据根目录 `README.md` 的主题列表和别名，找到主题目录。
4. 读取主题目录下的 `README.md`。
5. 严格按照主题 `README.md` 的读取规则加载文件。
6. 加载完成后，只输出简短确认语。

## 规则

- 主题名称、别名、笔记文件和读取顺序都由用户自己的 `learning_record` 仓库定义。
- 不要在 skill 内硬编码具体主题。
- 如果根目录 `README.md` 没有定义用户请求的主题，说明该仓库当前没有这个主题，不要猜测其他路径。
- 如果主题 `README.md` 定义了精确确认语，使用该确认语；否则输出：

```text
已读取请求的学习记录。
```
