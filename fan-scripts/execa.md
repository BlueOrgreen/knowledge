工具里，封装了一个 run 函数：

```ts
export const run = async (
  bin: string,
  args: string[],
  opts: any = {},
): Promise<any> => {
  return execa(bin, args, { stdio: 'inherit', ...opts })
}
```

- `bin`: 命令名，比如 'git' 或 'pnpm'
- `args`: 命令参数数组，如 ['status', '--porcelain']
- `opts`: `execa` 选项，比如 `cwd`, `stdio` 等
- `stdio`: `'inherit'`：将子进程的 `stdout/stderr/stdio` 直接绑定到父进程终端，方便看到输出

`stdio: 'inherit'` → 子进程会直接把输出“继承”到父进程，也就是直接打印到你当前终端。


改成 `stdio: 'pipe'` → 子进程的输出会被“管道化”，存储在返回对象的 `stdout`、`stderr` 属性里，而不是直接打印到终端