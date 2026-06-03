# TypeScript 笔记

## 用 for await 读取异步流

读取异步可迭代流（async iterable stream）时，优先使用 `for await...of`，这样可以按数据块（chunk）到达顺序处理数据，不需要手动维护 iterator 状态。
