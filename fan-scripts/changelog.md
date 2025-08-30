
# CHANGELOG 自动化生成：集成 conventional-changelog，自动维护日志

`conventional-changelog` 可以根据 `Git` 提交记录 自动生成 `CHANGELOG`


## 核心封装函数

你项目中封装了一个 `updateChangelog`

```tsx
export const updateChangelog = async (
  pkgDirPath: string,
  pkgName: string,
  isMonorepo: boolean = true,
): Promise<void> => {
  const changelogBin = getSelfBinPath('conventional-changelog')

  const args = [
    '-p', 'conventionalcommits',  // preset：规范类型
    '-i', 'CHANGELOG.md',          // 输入文件
    '-s',                          // 修改文件而不是输出到 stdout
    ...(isMonorepo ? ['--commit-path', '.', '--lerna-package', pkgName] : []),
  ]

  await run(changelogBin, args, { cwd: pkgDirPath })
}

```