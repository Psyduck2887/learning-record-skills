# TypeScript 笔记

## 用 for await 读取异步流

读取 async iterable stream 时，优先使用 `for await...of`，这样可以按 chunk 到达顺序处理数据，不需要手动维护 iterator 状态。
