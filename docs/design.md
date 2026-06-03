# 设计说明

这个仓库刻意区分 skill 本体、用户模板和说明文档。

## 分层

- `skills/` 只放 Agent 执行时需要读取的内容。
- `templates/` 放用户可以复制的 `learning_record` 仓库模板。
- `docs/` 放面向人的说明文档。

这样做的目的，是避免把“给 Agent 执行的规则”和“给用户阅读的教程”混在一起。

## skill 本体

每个 skill 是一个独立目录，入口文件是 `SKILL.md`：

```text
skills/
  learning-record-read/
    SKILL.md
  learning-record-write/
    SKILL.md
```

`SKILL.md` 只描述 Agent 被调用时应该怎么做，不承担仓库首页、教程或模板说明的职责。

## 用户模板

`templates/learning_record/` 是一个可复制模板，不是 skill 安装内容。用户可以复制它，再按自己的主题扩展：

```text
templates/
  learning_record/
    README.md
    typescript/
      README.md
      notes.md
```

真正的主题、别名、笔记文件和读写规则，都由用户自己的 `learning_record` 仓库定义。

## 安全边界

- skill 不假设固定本机路径、GitHub 账号或仓库位置。
- skill 不硬编码具体主题。
- `learning-record-read` 只读文件，不写入。
- `learning-record-write` 只有在用户明确要求时才执行 Git commit 或 push。
- 学习记录发布前，用户仍然需要自行检查是否包含密钥、凭证、token 或其他敏感信息。
