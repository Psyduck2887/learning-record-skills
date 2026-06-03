# TypeScript Notes

## Async Iteration Over Streams

When reading an async iterable stream, prefer `for await...of` so each chunk is handled in arrival order without manually managing iterator state.
