### 当前文件所在目录

```ts
const __dirname = path.dirname(fileURLToPath(import.meta.url))
```

- `fileURLToPath(import.meta.url)` 用于 `ESM` 获取文件路径