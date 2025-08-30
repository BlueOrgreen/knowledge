```tsx
export const run = async (
  bin: string,
  args: string[],
  opts: any = {},
): Promise<any> => {
  return execa(bin, args, { stdio: 'inherit', ...opts })
}

```


在 Node.js（以及 `execa`）里，`stdio` 控制子进程的标准输入/输出（`stdin`、`stdout`、`stderr`）该怎么处理。

默认情况

你的 `run` 函数里写的是：

```bash
execa(bin, args, { stdio: 'inherit', ...opts })
```

`stdio: 'inherit'` → 子进程会直接把输出“继承”到父进程，也就是直接打印到你当前终端。

比如你 `run("git", ["status"])`，就会在终端里直接显示完整的 `git status` 输出。

但是这样在代码里 拿不到 `stdout`，因为输出已经直接写到屏幕了。

改成 `stdio: 'pipe'`

```bash
await run('git', ['status', '--porcelain'], { stdio: 'pipe' })
```

`stdio: 'pipe'` → 子进程的输出会被“管道化”，存储在返回对象的 `stdout`、`stderr` 属性里，而不是直接打印到终端。

这样你就可以在代码里拿到命令执行的结果：

```tsx
const result = await run('git', ['status', '--porcelain'], { stdio: 'pipe' })
console.log("Git 输出内容:", result.stdout)
```

如果工作区干净 → `result.stdout === ""`
如果有改动 → `result.stdout` 里会有修改的文件列表。

📌 总结区别

`stdio: 'inherit'` → 直接把子进程输出打印到终端（适合跑 `npm publish`、`pnpm install` 这种需要实时日志的命令）。

`stdio: 'pipe'` → 捕获子进程输出，放到返回结果里（适合 `git status --porcelain` 这种需要解析输出的命令）。