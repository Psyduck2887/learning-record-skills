# Learning Record Skills

一组用于读写个人学习记录的 Agent Skills。

这个仓库把内容分成三层：

- `skills/`：skill 本体，只放 Agent 安装和执行时需要读取的 `SKILL.md`。
- `templates/`：可复制的 `learning_record` 仓库模板。
- `docs/`：面向人的安装、使用和设计说明。

## 新用户建议

如果你第一次使用这类 skill，建议先让 Codex 读取这个仓库，并根据你的本地环境总结安装和配置步骤。可以直接使用下面这段 prompt：

```text
请阅读这个仓库的 README.md、docs/、skills/learning-record-read/SKILL.md、skills/learning-record-write/SKILL.md 和 templates/learning_record/，然后用中文告诉我：这个仓库是做什么的、我应该把 skill 安装到哪里、如何配置 LEARNING_RECORD_REPO，以及如何创建自己的 learning_record 仓库。
```

## 包含的 skills

- `learning-record-read`：按主题读取学习记录，并加载到当前 Agent 上下文。
- `learning-record-write`：把已经解决的问题追加成一条轻量学习笔记。

这两个 skill 不绑定固定主题、具体笔记文件、GitHub 账号或本机路径；但你的 `learning_record` 仓库需要用 `README.md` 声明主题、别名和读写规则。

## 快速开始

安装两个 skill：

```sh
mkdir -p ~/.agents/skills
cp -R skills/learning-record-read ~/.agents/skills/
cp -R skills/learning-record-write ~/.agents/skills/
```

复制示例模板作为自己的学习记录仓库：

```sh
cp -R templates/learning_record /path/to/my_learning_record
export LEARNING_RECORD_REPO=/path/to/my_learning_record
```

让 Agent 读取示例主题：

```text
使用 learning-record-read 读取 TypeScript 学习记录。
```

写入一条已解决的问题：

```text
使用 learning-record-write，把刚才解决的 TypeScript 问题记录到学习记录里。不要提交 Git。
```

## 仓库结构

```text
skills/
  learning-record-read/
    SKILL.md
  learning-record-write/
    SKILL.md
templates/
  learning_record/
    README.md
    typescript/
      README.md
      notes.md
docs/
  install.md
  usage.md
  design.md
```

## 文档

- [安装说明](docs/install.md)
- [使用说明](docs/usage.md)
- [设计说明](docs/design.md)

## License

MIT
